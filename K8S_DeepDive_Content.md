## Kubernetes Course Content in Detail
```
kubernetes Deep Dive:
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

2) Deployment of kubernets cluster using microk8s(ubuntu),minikube,kubeadm
	Two nodes (1 for controller and 1 for compute nodes)

3) POD object creation using single container and multi-container
	Understanding common networking and common storage in POD (shared namespaces)
	Sample application deployment using nginx for single container in POD
	Multi-container deployment, one for web application and second for data pull
	POD creation with initContainer advantages for pre-request
	static POD deployment
	Deploying application from Private repository
	resource allocation like CPU and MEMORY
	Sidecar containers

4) ReplicationController object (RC)
	When tuse replication controller?
	Disadvantages of deploying application with single POD
	Understanding template and selector parameters

5) Replica Set object (RS)
	Difference between Replication Controller and Replica Set
	Advantages of adding match Labels
	when to use replica Set?

6) Deployment object (deploy)
	Advantages of Deployment over POD, RC and RS
	Sample application deployment like Jenkins, nginx and capture the advantages over other
	objects
	Scaleout and Scale in for Deployment
	Deployment Strategies like Rolling Update and Recreate difference
	Rollout, Rollback and Rollout History of deployment

7) Daemon set object (DS)
	DaemonSet usecases over deployment object
	Advantages of using monitoring tools tdeploy through DaemonSet object
	Deployment Strategies like Rolling Update and On Delete difference
	Rollout, Rollback and Rollout History of DaemonSet

8) StatefulSet object (sts)
	Difference between stateful and stateless applications
	StatefulSet application deployment advantages
	Scaleout and Scalein for Deployment
	Deployment Stratagies like RollingUpdate and OnDelete difference
	Rollout, Rollback and Rollout History of StatefulSet

9) volumes:
	Empheimeral and persistent storage differences
	Different types of volume plugins like emptyDir, hostPath, NFS etc.,
	Do's and Dont's of using volumes for application deployment

10) PersistentVolume, PersistantVolumeClaim and StorageClass (PV and PVC)
	Advanatages of using PV over volume plugins for data dependent applications
	Static and Dynamic PV creation
	PVC assignment in POD, Deployment, Daemonset, StatefulSet objects
	StargaeClass creation for Dynamic provision
	NFS, Ceph RBD storage as examples

11) Services (svc)
	Exposing application running on different object through service
	Understanding difference between ClusterIP, NodePort, Load Balancing, ExternalIP and ExternalName
	When to use these different types of services?

12) secrets and configmap (secret, cm)
	How to pass sensitive data through secret like certs, password, token etc.,
	How to pass paintext data through configMap like configuration files, scripts etc.,
	Using secret in POD object through env and volumes
	using configMap in POD object through env and volumes

13) Ingress (ing)
	Access application deployed with the cluster through IngressController
	Deploying Nginx IngressController
	Ingress rules creation secured and non-secure communication

14) Horizontal POD AutoScalling (HPA):
	HPA deployent ttest autscalling
	Deployment of metric server tachieve HPA

15) Scheduling and probes
	Different types of scheduling like nodename, nodeSelector, podAffinity, podAntiAffinity,
	nodeAffinity
	Advantages of using liveness, readiness and startup probes tverify application availability

16) Jobs and CronJobs
	How to achieve autbackup and restore using CronJobs for application like etcd key-value pair storage for kubernetes cluster
	Jobs responsibility

17) calico networking
	flannel network understanding
	migrate from flannel to calico
	How to  use flannel for POD networking and Calicfor network security
	calicoctl operations
	network policy and global network policy

18) authetication and authorization
	authetication:
		user, group and serviceaccount (token), certs
		kubeconfig entries and access multiple cluster through kubernetes config file
	autherization:
		Role Back Access Control (RBAC), ABAC, Node, Webhook
		Role, RoleBinding, ClusterRole, ClusterRoleBinding

19) Dashboard
	deployment of kubernetes dashboard and creating kubernetes object through dashboard
	How tauthenticate tdashboard through token and kubeconfig

20) Task:
	a. wordpress and database application deployment
	b. Jenkins deployment with data persistent after upgrading/downgrade
	c. Backup and restore of etcd service data using cronjob
	d. kubernetes upgrade from one version tanother (1.20.1 t1.20.2)
	e. maintaince task using taint and toleration
	f. Automate application deployment with the help of GitOps and ArgoCD
	g. Understanding CRD and CR for operators

Extra: Docker and Kubernetes Security:
	Docker Image vulnerability scanning using Trivy tool as part of DevSecOps
	Kubernetes Cluster scanning using kubescan etc.,
	Servie Mash
```