# Prerequisites

To deploy MSR on a Single-Host using Helm, ensure that your environment meets
the following requirements.

## Host environment

- **Kubernetes 1.10+ Cluster**
   MSR runs on an existing MKE or other Kubernetes cluster.

- **Kubernetes storage backend with ReadWriteOnce (RWO) support**
   A storage backend that provides volumes to MSR 4 components (for example,
   CephFS, AWS EFS, Azure Files).
   The hostPath is also supported for testing or development purposes, it
   is not recommended for production environments due to limitations in
   scalability, data persistence, and portability.

## Management workstation

Use a laptop or virtual machine running Linux, Windows, or macOS, configured to
manage Kubernetes and install MSR and its dependencies:

- **Helm 2.8.0+** - Required for installing MSR components, and other
  dependencies.

- **kubectl** - Install a kubectl version that matches your Kubernetes cluster.

## Kubernetes client access

Obtain and install a Kubernetes `client bundle` or
`kubeconfig` with embedded certificates on your management workstation to
allow kubectl and Helm to manage your cluster.
This depends on your Kubernetes distribution and configuration.

For MKE 3.8 host cluster, refer to
[Download the client bundle](https://docs.mirantis.com/mke/3.8/ops/access-cluster/client-bundle/download-client-bundle.html) for more information.
