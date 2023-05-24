# ExternalIP - Pending State - Fix
This document will cover issue for fixing of externalIP - Pending in case of load Balancer svc type setup in KubeAdm way, this is required for exposing of services to outside

## Issue Reference:

```
#$ kubectl describe svc frontend
...
Events:
  Type     Reason                  Age   From                Message
  ----     ------                  ----  ----                -------
  Normal   EnsuringLoadBalancer    9s    service-controller  Ensuring load balancer
  Warning  SyncLoadBalancerFailed  1s    service-controller  Error syncing load balancer: failed to ensure load balancer: no node tags supplied and also failed to parse the given lists of hosts for tags. Abort creating firewall rule
```

# Steps:

# First: 

Tag your nodes with hostname in Network tags, for example in our POC setup we have two nodes with hostname - controlplane & computeplane1. Edit your VM and update by refering below image for reference

![NetworkTag-ControlNode](/k8s_resources/src/images/NetworkTag-ControlPlane.JPG)
![NetworkTag-ComputePlane](/k8s_resources/src/images/NetworkTag-ComputePlane.JPG)

# Second: 
Provide right IAM permission to default compute service account, refer below image for reference

![IAM-Acces](/k8s_resources/src/images/IAM-Access.JPG)

# Third: 
Create/update firewall rule to allow access of service from outside/internet

![Firewall-Rules](/k8s_resources/src/images/Firewall-Rules-Allow-HttpAccess.JPG)

# Fourth: 
Update kube-controller-manager and kube-api-server on controller node with cloud provider in target manifest file, in our case it is --cloudprovider=gce. Refer image for reference

```
Manifest location
...
root@controlplane:/etc/kubernetes/manifests# pwd
/etc/kubernetes/manifests
root@controlplane:/etc/kubernetes/manifests# ll
total 24
drwxr-xr-x 2 root root 4096 May 24 02:24 ./
drwxr-xr-x 4 root root 4096 May  7 13:51 ../
-rw------- 1 root root 2144 May  7 13:51 etcd.yaml
-rw------- 1 root root 3830 May 20 15:58 kube-apiserver.yaml
-rw------- 1 root root 3343 May 20 15:51 kube-controller-manager.yaml
-rw------- 1 root root 1385 May  7 13:51 kube-scheduler.yaml
root@controlplane:/etc/kubernetes/manifests# 
```

![ControllerManager-ManifestFile-Update](/k8s_resources/src/images/cloudProvider-kubecontrollermanager.JPG)
![ApiServer-ManifestFile-Update](/k8s_resources/src/images/cloudprovider-kubeapiserver.JPG)
