# Kubernetes architecture items in details
************************************************************************************************
```
1) kubernetes components and responsibility
	controller nodes:
	 kube-apiserver
	 kube-control-manager/cloud-control-manager
	 kube-schduler
	 calico,flannel(deprecated from 1.18),wavenet etc.,
	 coreDNS
	 etcd key-value pair storage
	 kubelet
	 kube-proxy
	 Docker Engine/containerd/cri-etc.,
	compute nodes:
	 kubelet
	 kube-proxy
	Docker Engine/containerd/cri-etc.,

```