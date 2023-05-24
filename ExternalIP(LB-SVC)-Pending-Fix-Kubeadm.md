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

# Third: 
Create/update firewall rule to allow access of service from outside/internet

# Fourth: 
Update kube-controller-manager and kube-api-server with cloud provider in target manifest file, in our case it is --cloudprovider=gce. Refer image for reference

