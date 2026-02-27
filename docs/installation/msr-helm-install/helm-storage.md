# Create PVC across Kubernetes workers

MSR requires volumes which can be provided by Persistent Volume Claim (PVC)
or local node storage (hostPath).

!!! note

    MSR 4 can use any StorageClass and PVC that you configure on your
    Kubernetes cluster. The following example sets up `cephfs` or NFS your
    default StorageClass. For more information, see
    [Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/)
    in the official Kubernetes documentation.

## Configure cephfs

The following example shows how to configure persistent storage for Kubernetes
using ``cephfs``. You can adapt these steps for your environment.

1. Create a ``StorageClass``, the specifics of which depend on the storage
   backend you are using. The following example illustrates how to create a
   StorageClass class with a CephFS backend and Ceph CSI:

    ```yaml
    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
      name: cephfs
      annotations:
       storageclass.kubernetes.io/is-default-class: "true"
    provisioner: cephfs.csi.ceph.com
    parameters:
      clusterID: <cluster-id>
    ```

2. Run `kubectl apply` to apply the StorageClass configuration to the
   cluster, in the appropriate namespace.

3. Create the PVC:

    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: shared-pvc
    spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 10Gi
      storageClassName: cephfs
    ```

    !!! note

        The `.spec.storageClassName` references the name of the
        `StorageClass` you created above.

4. Run `kubectl apply` to apply PVC to the cluster, in the appropriate
   namespace.

## Configure NFS

The following example shows how to configure persistent storage for Kubernetes
using NFS. You can adapt these steps for your environment.

1. Add the Helm repository for the NFS subdirectory external provisioner.

    ```bash
    helm repo add nfs-provisioner https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner/
    helm repo update
    ```

2. Install the NFS client provisioner. Replace the placeholders with values
   for your environment.

    ```bash
    helm install nfs-client-provisioner nfs-provisioner/nfs-subdir-external-provisioner \
      --set nfs.server=<NFS-SERVER-IP> \
      --set nfs.path=</DIRECTORY/YOU/WANT/TO/USE> \
      --set storageClass.name=nfs-storage \
      --set storageClass.defaultClass=true
    ```

## Configure hostPath

The following example shows how to configure hostPath.
You can adapt these steps for your environment.

1. Create a Persistent Volume Claim (PVC) to claim storage from the node's
   local storage:

    ```yaml
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: hostpath-pvc
    spec:
      accessModes:
      - ReadWriteOnce
      resources:
        requests:
          storage: 10Gi
      volumeName: hostpath-pv
    ```

2. Create a Persistent Volume indicating the local directory:

    ```yaml
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: hostpath-pv
    spec:
      capacity:
        storage: 10Gi
      accessModes:
      - ReadWriteOnce
      hostPath:
        path: /mnt/data
      persistentVolumeReclaimPolicy: Retain
    ```
