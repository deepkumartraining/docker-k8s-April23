## K8S-Cluster Prep Up - Kubeadm way
------------------------------------------------------------------------------------------
## Pre-Requisite VMs

	Control Plane & Compute Plane
	Configuration - Type: E2 Standard 2 - 2 vcpu and 8 GB RAM, Allow default svc account and all IPs

## Need to execute on both the nodes - ControlPlane and ComputePlane
------------------------------------------------------------------------------------------
## Docker Installation for container runtime

apt update
apt dist-upgrade -y
apt-get install apt-transport-https ca-certificates curl gnupg lsb-release -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
apt-get update
apt-cache policy docker-ce

--5:19.03.15~3-0~ubuntu-focal --- This docker daemon version is compatiable with Kubernetes 1.21.X version

apt install -y docker-ce=5:19.03.15~3-0~ubuntu-focal docker-ce-cli=5:19.03.15~3-0~ubuntu-focal containerd.io
docker --version
systemctl status docker

-------------------------------------------------------------------------------------------
## Kubernetes related installation on Both Nodes - Control Plan and Compute Plane
--------------------------------------------------------------------------------------------

## Install kubernetes packages on both the nodes, before that we have to enable network module for iptables and bridges as mentioned below

cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
br_netfilter
EOF

cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF

echo 1 > /proc/sys/net/ipv4/ip_forward

sudo sysctl --system

## Lets create a repo for kubernetes and install kubernetes v1.21.4 version for now, since v1.22.x has issues in "kubeadm init bootstrap" command.

apt-get install -y apt-transport-https ca-certificates curl
curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
apt update
apt install -y kubeadm=1.21.4-00 kubelet=1.21.4-00 kubectl=1.21.4-00
apt-mark hold kubelet kubeadm kubectl

## Need to execute on Control plane node only
---------------------------------------------------------------------------------------------
We are going to bootstrap control plane first in the cluster.
These node now will be control plane node for the entire cluster.
We will use "--pod-network-cidr" with subnet that doesn't conflict with my base network.
Since instances/VMs are using "10.128.0.0/16" series, I can gohead and use "192.168.0.0/16" which calico will use by default.
We are using calico network for kubernetes as CNI(Container Network Interface)

--Bootstrap the control plane node using "kubeadm init" command as mentioned below:

My Control Plan internal IP - 10.xx.x.x/32 -- Change your internal IP accordingly
ip -a

kubeadm init --apiserver-advertise-address=<internalIP of VM> --pod-network-cidr=192.168.0.0/16

## Possible failure
```
-----------------------------------------------------------------------------------------------------------------------
kubeadm init --apiserver-advertise-address=10.xx.x.x --pod-network-cidr=192.168.0.0/16
I0507 13:47:59.076704   17121 version.go:254] remote version is much newer: v1.27.1; falling back to: stable-1.21
[init] Using Kubernetes version: v1.21.14
[preflight] Running pre-flight checks
        [WARNING IsDockerSystemdCheck]: detected "cgroupfs" as the Docker cgroup driver. The recommended driver is "systemd". Please follow the guide at https://kubernetes.io/docs/setup/cri/
error execution phase preflight: [preflight] Some fatal errors occurred:
        [ERROR FileContent--proc-sys-net-ipv4-ip_forward]: /proc/sys/net/ipv4/ip_forward contents are not set to 1
[preflight] If you know what you are doing, you can make a check non-fatal with `--ignore-preflight-errors=...`
To see the stack trace of this error execute with --v=5 or higher
------------------------------------------------------------------------------------------------------------------------
```
## Perform IP forwarding for fix by enabling

echo 1 > /proc/sys/net/ipv4/ip_forward

Execute above code again
kubeadm init <>

## Similar to below output would be coming post complete installation, token and IP specific details are system dependent
```
------------------------------------------------------------------------------------------------------------------------
Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

Alternatively, if you are the root user, you can run:

  export KUBECONFIG=/etc/kubernetes/admin.conf

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 10.128.0.4:6443 --token <runtime token> \
        --discovery-token-ca-cert-hash sha256:<runtime token>

-----------------------------------------------------------------------------------------------------------------------
```
## Note:
  apiserver-advertise-address needs update with the Internal IP address of the control plane node.
  After successful completion of the command, execute below command as shown in the result as well.
  Copy the result at last which has details mentioned below to add compute plane node to the cluster.

-----------------------------------------------------------------------------------------------------------------------
## Commands for keeping kubernetes config at controller node
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

## Execute YAML files for calico CNI configuration to get installed on the cluster for networking.

kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.25.1/manifests/tigera-operator.yaml
kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.25.1/manifests/custom-resources.yaml

## Note: This is generated as per system specifications and important to join the worker node to the master.

-----------------------------------------------------------------------------------------------------------------------
## Execute this command on computenode for joining of cluster

kubeadm join 10.xxx.xx.xx:6443 --token <runtime token> \
        --discovery-token-ca-cert-hash sha256:<runtime token>
		

## Possible failure:
-----------------------------------------------------------------------------------------------------------------------
```
kubeadm init --apiserver-advertise-address=10.xx.xx.xx --pod-network-cidr=192.168.0.0/16
I0507 13:47:59.076704   17121 version.go:254] remote version is much newer: v1.27.1; falling back to: stable-1.21
[init] Using Kubernetes version: v1.21.14
[preflight] Running pre-flight checks
        [WARNING IsDockerSystemdCheck]: detected "cgroupfs" as the Docker cgroup driver. The recommended driver is "systemd". Please follow the guide at https://kubernetes.io/docs/setup/cri/
error execution phase preflight: [preflight] Some fatal errors occurred:
        [ERROR FileContent--proc-sys-net-ipv4-ip_forward]: /proc/sys/net/ipv4/ip_forward contents are not set to 1
[preflight] If you know what you are doing, you can make a check non-fatal with `--ignore-preflight-errors=...`
To see the stack trace of this error execute with --v=5 or higher
```
------------------------------------------------------------------------------------------------------------------------

## Perform IP forwarding for fix by enabling

echo 1 > /proc/sys/net/ipv4/ip_forward

Execute above code again
kubeadm join <>

## Post success message, proceed with validation
------------------------------------------------------------------------------------------------------------------------
## validation commands

kubectl get nodes
kubectl get pods --all-namespaces


------------------------------------------------------------------------------------------------------------------------
## EXTRA commands for labelling of nodes
------------------------------------------------------------------------------------------------------------------------
## labeling of Nodes - Compute node

kubectl label node <node name> node-role.kubernetes.io/<role name>=<key - (any name)>

kubectl label node computeplanenode1 node-role.kubernetes.io/compute-plane=worker1

kubectl label --overwrite nodes computeplanenode1 kubernetes.io/role

node-role.kubernetes.io/role=compute-plane

Examples - Commands executed

kubectl get nodes
kubectl label node computeplanenode1 node-role.kubernetes.io/role=compute-plane, worker
kubectl label node computeplanenode1 node-role.kubernetes.io/role=compute-plane
kubectl get nodes
kubectl label node computeplanenode1 node-role.kubernetes.io/compute-plane=worker
kubectl get nodes
kubectl label node computeplanenode1 node-role.kubernetes.io/worker=worker1
kubectl get nodes
kubectl label --overwrite nodes computeplanenode1 kubernetes.io/role=worker1
kubectl get nodes
kubectl label --list nodes computeplanenode1
kubectl label --overwrite nodes computeplanenode1 kubernetes.io/role

------------------------------------------------------------------------------------------------------------------------



