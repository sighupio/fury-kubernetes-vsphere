# vSphere Container Storage Interface Driver

This katalog deploys the [vSphere container storage interface driver](https://github.com/kubernetes-sigs/vsphere-csi-driver) on a VMware Kubernetes cluster backed by vCenter.

## Requirements

Follow all the [prerequisites from `vsphere-cm` modules](../vsphere-cm/).

## Image repository and tag

- `registry.sighup.io/fury/csi-vsphere/driver:v3.3.1`
- `registry.sighup.io/fury/csi-vsphere/syncer:v3.3.1`
- `registry.sighup.io/fury/sig-storage/csi-attacher:v4.5.1`
- `registry.sighup.io/fury/sig-storage/csi-node-driver-registrar:v2.10.0`
- `registry.sighup.io/fury/sig-storage/csi-provisioner:v4.0.1`
- `registry.sighup.io/fury/sig-storage/csi-resizer:v1.10.1`
- `registry.sighup.io/fury/sig-storage/csi-snapshotter:v7.0.2`
- `registry.sighup.io/fury/sig-storage/livenessprobe:v2.12.0`

## Setting credentials

Credential are set via secret, patch it via Kustomize:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: vsphere-config-secret
  namespace: vmware-system-csi
stringData:
  csi-vsphere.conf: |
    [Global]
    cluster-id = "demo-cluster-id"
    [VirtualCenter "1.1.1.1"]
    insecure-flag = "true"
    user = "Administrator@vsphere.local"
    password = "password"
    port = "443"
    datacenters = "datacenter"

type: Opaque
```

⚠️ `cluster-id` represents the unique cluster identifier. Each Kubernetes cluster should have its own unique cluster-id set in the `csi-vsphere.conf` file.

## Install

After setting all prerequisites and the password, you can apply all manifests to the cluster.

## Check that everything is working after installation

Run these commands, the output should be similar:

```bash
$ kubectl get CSINode
NAME        CREATED AT
k8s-node1   2019-06-01T00:50:26Z
k8s-node2   2019-06-01T00:50:38Z
k8s-node3   2019-06-01T00:50:26Z
k8s-node4   2019-06-01T00:50:25Z
```

## Define a storage class

Now you will need to set a Storage Policy in VCenter to define which datastore will be used by volumes:

![create storage policy](screen/createstoragepolicy.png)

Follow the wizard to select the storage. Storage is selected using vSAN or using tags on Datastores. After the procedure, you will have a storage policy that shows some disks under `Storage Compatibility`.

Create your `storageClass`:

```yaml
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
  name: vsphere
  annotations:
    storageclass.kubernetes.io/is-default-class: "true"
provisioner: csi.vsphere.vmware.com
parameters:
  storagepolicyname: "your-awesome-storage-policy-in-vcenter"
  fstype: ext4
```
