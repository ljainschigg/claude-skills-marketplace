# Prerequisites

To deploy MSR with High Availability (HA), ensure that your environment meets
the following requirements.

## Host environment

- **Kubernetes 1.10+ Cluster**  
  HA MSR runs on an existing MKE or other Kubernetes cluster, preferably with
  a highly available control plane (at least three controllers),
  a minimum of three worker nodes, and highly available ingress.

- **Kubernetes storage backend with ReadWriteMany (RWX) support**  
  A storage backend that allows a Persistent Volume Claim to be shared across
  all worker nodes in the host cluster (for example, CephFS, AWS EFS,
  Azure Files).

- **Highly-Available PostgreSQL 9.6+**  
  A relational database for metadata storage.

- **Highly-Available Redis**  
  An in-memory cache and message/job queue.

## Management workstation

Use a laptop or virtual machine running Linux, Windows, or macOS, configured to
manage Kubernetes and install MSR and its dependencies:

- **Helm 2.8.0+** – Required for installing databases (PostgreSQL, Redis), MSR
  components, and other dependencies.

- **kubectl** – Install a kubectl version that matches your Kubernetes cluster.

## Kubernetes client access

Obtain and install a Kubernetes `client bundle` or
`kubeconfig` with embedded certificates on your management workstation to
allow kubectl and Helm to manage your cluster.  
This depends on your Kubernetes distribution and configuration.

For MKE 3.8 host cluster, refer to  
[Download the client bundle](https://docs.mirantis.com/mke/3.8/ops/access-cluster/client-bundle/download-client-bundle.html) for more information.
