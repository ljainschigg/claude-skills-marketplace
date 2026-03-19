# Install MSR

To start, install a test instance of Mirantis Secure Registry (MSR) on
a Kubernetes cluster. For production environments, do not follow these test
instructions. Instead, follow the [high-availability (HA) installation guide](../../installation/installation-with-high-availability/index.md) 
to deploy a fully supported, production-ready MSR instance.

## Prepare the environment

- Identify the IP address of your worker node and
  set the `$MSR_IP` environment variable to this value:

    ```bash
    export MSR_IP=<node-ip-address>
    ```

- The Helm installation requires an external URL. If the cluster
  has a single worker node, use the node IP address as the
  external URL value. This configuration uses the NodePort
  service type to expose the application.

- Use the default PostgreSQL and Redis components included in the Helm chart,
  omitting the high-availability configuration for these components. Also, you can
  skip custom certificate configuration for testing purposes.

## Install the MSR instance

1. Run the following command to install MSR:

    ```bash
    helm install my-msr4 oci://registry.mirantis.com/harbor/helm/msr \
    --version 4.13.2 \
    --set externalURL=https://${MSR_IP?}:34443 \
    --set expose.type=nodePort \
    --set expose.nodePort.ports.http.nodePort=34080 \
    --set expose.nodePort.ports.https.nodePort=34443
    ```

2. Verify the installation status:

    ```bash
    kubectl get pods --watch
    ```

3. Wait until all pods report a `Running` status.

## Retrieve the redirect URI

Retrieve the redirect URI from the OIDC configuration, which you will need to
[set up Entra ID](set-up-entra-id.md).

1. Navigate to `https://${MSR_IP?}:34443`.
2. Log in as an administrator (default password `Harbor12345`).
3. Navigate to **Administration** → **Configuration** → **Authentication**.
4. Change the **Auth Mode** to **OIDC**.
5. Scroll to the bottom of the page and locate the redirect URI note,
   which should list a value like `https://12.345.678.90:34443/c/oidc/callback`.
   Save this value for the OIDC application registration.
