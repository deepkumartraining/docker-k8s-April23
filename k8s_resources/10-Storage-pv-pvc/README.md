# Kubernetes Volumes
**Kubernetes typically treats individual pods as ephemeral, disposable resources. Applications have different approaches available to them for using and persisting data. A volume represents a way to store, retrieve, and persist data across pods and through the application lifecycle.**
- **A Pod can specify a set of shared storage Volumes. All containers in the Pod can access the shared volumes, allowing those containers to share data. Volumes also allow persistent data in a Pod to survive in case one of the containers within needs to be restarted.**

- Note:
  - The Pod remains on that Node until the process is terminated, the pod object is deleted, the Pod is evicted for lack of resources, application, or the Node fails.

## Core concepts that provide storage for our applications in Kubernetes on different platforms:
  - Volumes
  - Persistent Volumes
  - StorageClass (Dynamic)
  - Persistent Volume Claim

## PersistentVolume and PersistentVolumeClaim
- A PV will be provisioned by administrator to store the data Persistence through **Static or Dynamic** approach, which means data will be available even after POD deletion. We can also provision the PV dynamically using Storage Classes.
- A PersistentVolumeClaim (PVC) is a request for storage by a user.
- It is similar to a pod. Pods consume node resources and PVCs consume PV resources.
- Pods can request specific levels of resources (CPU and Memory). Claims can request specific size and access modes (e.g., can be mounted once read/write or many times read-only).
- Dynamic provisioning uses a **StorageClass** to identify what type of storage needs to be created.
- As updated earlier, PVs can be provisioned in two ways:
  - Static and Dynamic
    - Static PV are provisioned by cluster administrator, which can be managed by kubernetes api-server
    - Dynamic PV are created when none of the PV exists created by administrator, it will provision the dynamic PV in the background.

[pv-pvc](../src/images/pv-pvc.png)

### Volume Policies
- We have three types of reclaim policies:
  - Retain, Delete and Recycle
    - The Retain reclaim policy (manual reclamation) allows for manual reclamation of the resource. When the PersistentVolumeClaim is deleted, the PersistentVolume still exists and the volume is considered “released”. But it is not yet available for another claim because the previous claimant’s data remains on the volume. An administrator can manually reclaim the volume with the following steps.
      1) Delete the PersistentVolume. The associated storage asset in external infrastructure still exists after the PV is deleted.
      2)Manually clean up the data on the associated storage asset accordingly.
      3)Manually delete the associated storage asset, or if you want to reuse the same storage asset, create a new PersistentVolume with the storage asset definition.

  - For Delete policy, For volume plugins that support the Delete reclaim policy, deletion removes both the PersistentVolume object from Kubernetes, as well as the associated storage asset in the external infrastructure, such as an AWS EBS, GCE PD, Azure Disk, or Cinder volume.

  - For recycle, If supported by the underlying volume plugin, the Recycle reclaim policy performs a basic scrub (rm -rf /the volume/*) on the volume and makes it available again for a new claim.

- Resizing the in-use PersistentVolumeClaim:

- In this case, you don’t need to delete and recreate a Pod or deployment that is using an existing PVC. Any in-use PVC automatically becomes available to its Pod as soon as its file system has been expanded. This feature has no effect on PVCs that are not in use by a Pod or deployment. You must create a Pod that uses the PVC before the expansion can complete.

- Note:
  - Currently, only NFS and HostPath support recycling. AWS EBS, GCE PD, Azure Disk, and Cinder volumes support deletion.

### Access Modes
- The access modes are:
  - ReadWriteOnce – the volume can be mounted as read-write by a single node
  - ReadOnlyMany – the volume can be mounted read-only by many nodes
  - ReadWriteMany – the volume can be mounted as read-write by many nodes

### Volume status
- Available – a free resource that is not yet bound to a claim
- Bound – the volume is bound to a claim
- Released – the claim has been deleted, but the resource is not yet reclaimed by the cluster
- Failed – the volume has failed its automatic reclamation

- A VolumeSnapshotContent is a snapshot taken from a volume in the cluster that has been provisioned by an administrator. It is a resource in the cluster just like a PersistentVolume is a cluster resource.

- A VolumeSnapshot is a request for snapshot of a volume by a user. It is similar to a PersistentVolumeClaim.

- VolumeSnapshotClass allows you to specify different attributes belonging to a VolumeSnapshot. These attributes may differ among snapshots taken from the same volume on the storage system and therefore cannot be expressed by using the same StorageClass of a PersistentVolumeClaim.

- Files or directories created with HostPath on the host are only writable by root. Which means, you either need to run your container process as root or modify the file permissions on the host to be writable by non-root user, which may lead to security issues

- You should NOT use hostPath volume type for StatefulSets

#### References:
- [Storage](https://kubernetes.io/docs/concepts/storage/)
- [Volumes](https://kubernetes.io/docs/concepts/storage/volumes/)
- [Persistant Volume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)
- [Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/)
- https://docs.openshift.com/container-platform/3.5/install_config/storage_examples/ceph_rbd_dynamic_example.html
- https://docs.openshift.com/container-platform/4.4/storage/persistent_storage/persistent-storage-local.html

## Commands executed during session
Date - 17th May 2023
```
cd storage/
cat pv-01.yaml 
vim pv-01.yaml 
kubectl create -f pv-01.yaml 
kubectl get pv
kubectl get pvc
kubectl delete pvc nfs-test-pvc
kubectl delete pv nfs-test-pv
kubectl get pv
kubectl get pvc
kubectl get pvc
kubectl delete pvc nfs-test-pvc
kubectl delete pvc nfs-test-pvc --force
kubectl get pvc
vim pv-01.yaml 
kubectl create -f pv-01.yaml 
kubectl get pv
vim pvc-01.yaml 
kubectl get pv
kubectl create -f pvc-01.yaml
kubectl get pvc
kubectl get pv
clear
cat pod-nfs.yaml 
vim pod-nfs.yaml 
clear
kubectl creat -f pod-nfs.yaml 
kubectl create -f pod-nfs.yaml 
kubectl get po
kubectl get po -o yaml
clear
kubectl get po
kubectl get deployment
kubectl delete deployment nginx-deployment-dy
kubectl delete deployment nginx-deployment
kubectl get po
kubectl delete po hello-nginx-nfs-pod
clear
kubectl get po
kubectl create -f pod-nfs.yaml 
kubectl get po
kubectl describe po hello-nginx-nfs-pod
kubectl get po
kubectl exec -it d hello-nginx-nfs-pod /bin/bash
kubectl exec -it hello-nginx-nfs-pod /bin/bash
clear
vim pod-nfs.yaml 
vim pvc-01.yaml 
vim pv-01.yaml 
vim pvc-01.yaml 
kubectl get pvc
kubectl get pv
vim pv-01.yaml
kubectl get storageclass
vim pv-01.yaml 
vim pvc-01.yaml 
clear
ll
vim deployment-01.yaml 
kubectl create -f deployment-01.yaml 
kubectl get deployments
kubectl get rs
kubectl get po
vim deployment-01.yaml 
clear
kubectl get pv
kubectl get pvc
kubectl get storageclass
ll
cd dynamic/
ll
clear
cat storage-class.yaml 
ll
cat dynamic-prov.yaml 
cat nginx-dy.yaml 
clear
kubectl get deployment
clear
kubectl get po
kubectl delete deployment nginx-deployment
kubectl delete deployment pod hello-nginx-nfs-pod
kubectl delete pod hello-nginx-nfs-pod
clear
kubectl get pv
kubectl get pvc
kubectl delete pvc claim-dy nfs-pvc
clear
kubectl get pvc
kubectl get pv
kubectl delete pv nfs-pv
clear
kubectl get pv
kubectl get pvc
kubectl get storageclass
kubectl delete storageclass
kubectl delete storageclass fast
clear
kubectl get po
clear
cd storage/
clear
ll
cat deployment-01.yaml 
ll
clear
ll
rm civo_pvc.yaml 
clear
ll
cd dynamic/
clear
ll
rm *
ll
clear
vim pvc-dp-01.yaml
kubectl apply -f pvc-dp-01.yaml 
kubectl get pvc
clear
kubectl get pvc
vim pod-dp-01.yaml
kubectl create -f pod-dp-01.yaml 
kubectl get po
kubectl get pvc
kubectl get po
kubectl describe po pod-demo
kubectl describe pvc pvc-demo
kubectl get storageclass
kubectl describe pvc pvc-demo
clear
ll
vim storageclass-pd.yaml
kubectl describe pvc pvc-demo
vim pvc-dp-01.yaml 
vim storageclass-pd.yaml 
kubectl apply -f storageclass-pd.yaml 
kubectl get sc
clear
kubectl get sc
kubectl get pvc
kubectl delete pvc pvc-demo
kubectl create -f pvc-dp-01.yaml 
kubectl get pods
kubectl delete po pod-demo
kubectl create -f pod-dp-01.yaml 
clear
kubectl get pvc
kubectl get pods
kubectl get pvc
kubectl get pods
kubectl describe pvc pvc-demo
kubectl get po
kubectl describe po pod-demo
clear
kubectl get po
kubeclt logs pod-demo
kubectl logs pod-demo
kubectl get pvc
kubectl logs pod-demo
kubectl describe po pod-demo
kubeclt get nodes -o wide
kubectl get nodes -o wide
kubectl describe po pod-demo
kubectl get pvc
clear
kubectl get pvc -A
kubectl get pvc
kubectl describe pvc pvc-demo
clear
ll
vim pod-dp-01.yaml 
kubectl get pvc
clear
ll
kubectl delete pvc pvc-demo
clear
kubectl delete po pod-demo
kubectl get sc
clear
ll
vim storageclass-dp-02.yaml 
kubectl apply -f storage-class.yaml
kubectl apply -f storageclass-dp-02.yaml 
kubectl get sc
vim pvc-dp-02.yaml
kubectl create -f pvc-dp-02.yaml 
vim pvc-dp-02.yaml 
cat pvc-dp-02.yaml 
kubectl create -f pvc-dp-02.yaml
vim pvc-dp-02.yaml 
kubectl create -f pvc-dp-02.yaml
kubectl get pvc
clear
kubectl get pvc
kubectl get pv
kubectl get pvc
gcloud -v
clear
gcloud compute disks create gke-pv  --zone=us-central1-a --size=50GB
kubectl get pvc
kubectl describe pvc webapps-storage
kubectl get pvc
clear
ll
vim sc-03.yaml
kubectl create -f sc-03.yaml 
kubectl get sc
vim pvc-03.yaml
cat pvc-dp-02.yaml 
kubectl create -f pvc-03.yaml 
kubectl get pvc
clear
ll
vim pod-03.yaml
kubectl create -f pod-03.yaml
kubectl get pv, pvcs
kubectl get pv, pvc
kubectl get pvc
kubectl get pods
clear
kubectl exec -it web -- bash
kubectl delete po web
kubectl delete pvc claimtest
kubectl get pvc
kubectl delete pvc claim-test
clear
cat sc-03.yaml 
kubectl get sc
kubectl get pvc
ll
vim pvc-03.yaml 
kubectl get pvc
kubectl apply -f pvc-03.yaml 
kubectl get pvc
ll
kubectl create -f pod-03.yaml 
kubectl get pvc
kubectl get pods
kubectl describe pods web
clear
gcloud compute disks create gke-pv  --zone=us-central1-a --size=50GB
clear
vim pv-04.yaml
kubectl create -f pv-04.yaml 
vim pvc-04.yaml
kubectl create -f pvc-04.yaml 
kubectl get pv
kubectl get pvc
vim pod-04.yaml
kubectl create -f pod-04.yaml 
kubectl get pods
kubectl describe pod nginx-app-pod
kubectl get sc
kubectl get sc standard -o yaml
kubectl get pv
kubectl get pvc
kubectl get pod
clear
ll
cd storage/
ll
cd dynamic/
clear
kubectl get pv
kubectl get pvc
kubectl delete pv app-storage-claim claim-test webapps-storage
kubectl delete pvapp-storage
kubectl delete pv app-storage
kubectl get pv
clear
history | awk '{print substr($0, index($0, $2))}'
```