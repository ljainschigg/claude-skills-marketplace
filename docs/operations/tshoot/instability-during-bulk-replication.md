# Instability during bulk replication

When you initiate a large number of replication rules simultaneously,
for example, more than 200, the surge in concurrent operations can overwhelm
backing services. This can lead to:

- **Database overload and failover** 

    PostgreSQL can become unresponsive or trigger leader
    elections due to a high connection churn. In severe cases, logs indicate
    unexpected failovers or leader elections:

    ```bash
    INFO: received failover request with leader=msr-postgres-0 \
    candidate=msr-postgres-1
    WARNING: received failover request with leader specified - performing \
    switchover instead
    ```

- **Optimistic locking failures and retry timeouts** 

     When database rows undergo concurrent modification by too many threads,
     MSR 4 components can fail to update project quotas or job statuses,
     resulting in retry timeouts in core or jobservice logs:

    ```bash
    [ERROR] reserve resources {"storage":...} for project 63 failed, \
    error: retry timeout: the object has been modified; please apply your \
    changes to the latest version and try again
    ```

- **Service instability and Pod restarts**

    Services such as core, PostgreSQL, or Redis can exceed
    resource limits and crash, causing cascading restarts of critical Pods.

- **Replication Jobs Stuck** 

    Replication jobs indefinitely remain in a **Pending** or **In Progress** state.

## Resolution options

To resolve the issue, you can:

- Perform the migration in batches (recommended)
- Tune the infrastructure for high levels of concurrency

### Option 1: Batch replication (recommended)

The most reliable way to avoid overloading the system is to stagger the
execution of replication rules.

- Forego the **Run All** option in the MSR web UI.

- Do not simultaneously start all replication rules through the API.

- Trigger replication rules in small groups, between 10 and 30 rules at a
  time, and wait for each batch to complete before starting the next one.

- If you are using
  [Migration Tool](../../migration/tool-migration/index.md), use the manual
  trigger workflow to control execution order to reduce the risk of
  replication errors.

### Option 2: Infrastructure tuning

If your workload requires that you run high-concurrency replication jobs,
you must scale MSR 4 components and significantly tune the backing services to
handle the load.

!!! example "Disclaimer"

    The configuration values provided below are indicative
    examples only, and are derived from a specific test environment with 
    3 worker nodes, 4 vCPUs, 16 GB of RAM.

    Every environment is unique. The optimal settings for your deployment 
    will greatly depend on your hardware, storage IOPS, network latency, and
    concurrency requirements. Do not apply these settings without prior evaluation.

    Before applying any changes, complete the following steps:

    1. Analyze your current resource usage to identify bottlenecks.
    2. Review the official documentation for
       [PostgreSQL](https://www.postgresql.org/docs/current/runtime-config-resource.html)
       and
       [Redis](https://redis.io/docs/latest/operate/oss_and_stack/management/optimization/)
       to understand the impact of each parameter.
    3. Test all configuration changes in a staging environment.

1. Tune your MSR 4 components.

    - Increase the number of replicas for core, jobservice, and other 
      components to improve concurrency handling. 
    - Configure resource requests and limits to
      prevent resource overuse and reduce the risk of service instability.

    Example `values.yaml`:

    ```yaml
    core:
      replicas: 3
      resources:
        requests:
          cpu: "1"
          memory: "2Gi"
        limits:
          cpu: "2"
          memory: "4Gi"
     
    jobservice:
      replicas: 3
      resources:
        requests:
          cpu: "1"
          memory: "2Gi"
        limits:
          cpu: "2"
          memory: "4Gi"
    ```

2. Tune PostgreSQL resources.

    Increase allocated resources and tune PostgreSQL parameters such
    as `max_connections` and `shared_buffers` to support a higher load.

    Example `postgresql` configuration:

    ```yaml
    apiVersion: "acid.zalan.do/v1"
    kind: postgresql
    metadata:
      name: msr-postgres
    spec:
      numberOfInstances: 3
      resources:
        requests:
          cpu: "1"
          memory: "2Gi"
        limits:
          cpu: "3"
          memory: "4Gi"
      postgresql:
        version: "17"
        parameters:
          # Memory tuning for high load
          shared_buffers: "4GB"
          work_mem: "16MB"
          maintenance_work_mem: "1GB"
          effective_cache_size: "8GB"
          # Connection tuning
          max_connections: "500"
          max_wal_senders: "10"
      patroni:
        failsafe_mode: true
        synchronous_mode: true
    ```

    Example `values.yaml`:

    ```yaml
    database:
      external:
        # Limit the number of idle/open connections to prevent flooding Postgres
        maxIdleConns: 100
        maxOpenConns: 800
        # Default is 1024; lower this if Postgres is hitting max_connections
    ```

    **Key parameters to review:**

    | Parameter           | Description                                                   |
    |---------------------|---------------------------------------------------------------|
    | `max_connections`     | Maximum number of concurrent connections. Must increase when core scales up.                                               |
    | `shared_buffers`      | Amount of memory dedicated to caching data.                  |
    | `work_mem`            | Memory allowed for internal sort operations and hash tables before writing to disk.                                      |

    Refer to the [Postgres Operator official documentation](https://opensource.zalando.com/postgres-operator/)
    for a complete list of configurable parameters and tuning guidance.
    

3. Tune Redis resources.

    Redis is critical for the job queue. Under high load, insufficient memory or
    CPU can cause job status updates to time out.

    Example of Redis installation with custom configuration options.

    ```bash
    helm install msr-redis redis-replication \
        --repo https://ot-container-kit.github.io/helm-charts \
        --set redisReplication.clusterSize=3 \
        --set redisReplication.redisSecret.secretName=msr-redis-secret \
        --set redisReplication.redisSecret.secretKey=REDIS_PASSWORD \
        --set redisReplication.image=quay.io/opstree/redis \
        --set redisReplication.tag=v8.2.2 \
        --set redisReplication.resources.requests.cpu="1" \
        --set redisReplication.resources.requests.memory="2Gi" \
        --set redisReplication.resources.limits.cpu="2" \
        --set redisReplication.resources.limits.memory="4Gi" \
        --set redisReplication.redisConfig.maxclients="20000" \
        --set redisReplication.redisConfig.maxmemory="7gb" \
        --set redisReplication.redisConfig.maxmemory-policy="allkeys-lru" \
        --set redisReplication.redisConfig.timeout="0" \
        --set redisReplication.redisConfig.tcp-keepalive="300" \
        --set redisReplication.redisConfig.tcp-backlog="511" \
        --set redisReplication.redisConfig.databases="16" \
        --set redisReplication.redisConfig.save="" \
        --set redisReplication.redisConfig.appendonly="yes" \
        --set redisReplication.redisConfig.appendfsync="everysec" \
        --set redisReplication.redisConfig.stop-writes-on-bgsave-error="no" \
        --set redisReplication.redisConfig.lua-time-limit="10000"
    ```

    **Key parameters to review:**

    | Parameter  | Description                                                                            |
    |------------|----------------------------------------------------------------------------------------|
    | `maxmemory`  | Maximum amount of memory Redis can use to store data before evicting keys.   |
    | `maxclients` | Maximum number of concurrent client connections Redis will accept.|

    Refer to the [Redis Operator official documentation](https://redis-operator.opstree.dev/)
    for a complete list of configurable parameters and tuning guidance

