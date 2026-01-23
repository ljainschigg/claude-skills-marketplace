# CPU throttling

By default, the Go runtime sets `GOMAXPROCS`, which controls how many operating
system threads can concurrently execute Go code. The value is based on the
number of logical CPUs that are available on the physical node and does not account
for CPU limits that are defined for a container or Pod.

Whenever you configure CPU limits for MSR 4 containers or Pods, the Go scheduler
is able to assume more CPU capacity than the container is permitted to use. As a
result, the application might create more runnable threads than the assigned CPU
quota can sustain. Thereafter, when these threads compete for CPU time, the 
container can repeatedly reach the Linux Completely Fair Scheduler (CFS) 
quota and become throttled.

For more information, refer to
[Go's official blog post on Container-aware GOMAXPROCS](https://go.dev/blog/container-aware-gomaxprocs).

## Symptoms

CPU throttling can cause the following negative behaviors:

- Increased latency in API responses or UI interactions.
- Containers or Pods become slower or unresponsive despite low memory usage.
- CPU usage consistently reaches or slightly exceeds the configured limit.

For example, if the registry Pod is configured with a CPU limit of
1 core (1000m), resource metrics may show the Pod repeatedly reaching that
limit:

```bash
$ kubectl top pods

NAME                                      CPU(cores)   MEMORY(bytes)
msr4-harbor-core-5f5859c7cb-dn8p8         300m         135Mi
msr4-harbor-database-0                    7m           180Mi
msr4-harbor-jobservice-7dbcfc66f5-59fvp   2m           21Mi
msr4-harbor-nginx-67c568fdd4-sg9tb        1m           33Mi
msr4-harbor-portal-5469889b75-wkmmr       1m           12Mi
msr4-harbor-redis-0                       4m           23Mi
msr4-harbor-registry-7558fbf44f-gprhf     1002m        141Mi  <-- Reaching limit
msr4-harbor-trivy-0                       1m           12Mi
```

## Workaround

Configure `GOMAXPROCS` to align with the container's CPU limit
instead of the total CPU count of the host.
This ensures that the Go scheduler does not oversubscribe CPU resources.

Set the `GOMAXPROCS` environment variable dynamically based on the
`limits.cpu` value allocated to the Pod.

The following examples both apply to a 1 CPU (1000m) limit.

=== "Kubernetes"

    Configure the value in the MSR 4 `values.yaml` file or by using the Helm CLI: 
   

    ```yaml
    extraEnvVars:
      - name: GOMAXPROCS
        valueFrom:
          resourceFieldRef:
            resource: limits.cpu
            divisor: "1"
    ```
  
=== "Docker Compose deployment"

    Configure the value in the `harbor.yml` file:

    ```yaml
    version: '3.8'
    services:
      registry:
        deploy:
          resources:
            limits:
              cpus: '1.0'
        environment:
          - GOMAXPROCS=1
    ```
