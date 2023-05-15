# Daemonset
- A DaemonSet ensures that all (or some) Nodes run a copy of a Pod. As nodes are added to the cluster, Pods are added to them. As nodes are removed from the cluster, those Pods are garbage collected.
- Deleting a DaemonSet will clean up the Pods it created.
- Update image of all containers of daemonset abc to 'nginx:1.9.1'
```
#kubectl set image daemonset abc *=nginx:1.9.1

We can set the labels for different objects as mentioned below:

Examples:
  # Update pod 'foo' with the label 'unhealthy' and the value 'true'.
  kubectl label pods foo unhealthy=true

  # Update pod 'foo' with the label 'status' and the value 'unhealthy', overwriting any existing value.
  kubectl label --overwrite pods foo status=unhealthy

  # Update all pods in the namespace
  kubectl label pods --all status=unhealthy

  # Update a pod identified by the type and name in "pod.json"
  kubectl label -f pod.json status=unhealthy

  # Update pod 'foo' only if the resource is unchanged from version 1.
  kubectl label pods foo status=unhealthy --resource-version=1

  # Update pod 'foo' by removing a label named 'bar' if it exists.
  # Does not require the --overwrite flag.
  kubectl label pods foo bar-

From 1.6 we can do rolling updates.
# kubectl set image ds/frontend webserver=httpd
```
## Command Executed for Daemonset
```
kubectl get nodes
kubectl get daemonset
kubectl get daemonset --all
kubectl get daemonset --all-namespaces
kubectl get ds kube-proxy -n kube-system
kubectl create deployment elasticsearch -n kube-system --image=k8s.gcr.io/fluentd-elasticsearch:1.20 --dry-run=client -o yaml
mkdir daemonset
cd daemonset/
kubectl create deployment elasticsearch -n kube-system --image=k8s.gcr.io/fluentd-elasticsearch:1.20 --dry-run=client -o yaml > fluentd.yaml
vim fluentd.yaml 
kubectl create -f fluentd.yaml
vim fluentd.yaml 
kubectl create -f fluentd.yaml
kubectl get ds
kubectl get ds -n kube-system
kubectl get ds -n kube-system
kubectl delete ds elasticsearch -n kube-system
kubectl get ds -n kube-system
vim fluentd-advanced.yaml
kubectl create -f fluentd-advanced.yaml 
kubectl get ds -n kube-system
kubectl describe ds/fluentd-elasticsearch -n kube-system
kubectl get pods -n kube-system
kubectl get ds -n kube-system
kubectl logs ds fluentd-elasticsearch
kubectl logs fluentd-elasticsearch-2wgmw
kubectl describe pods fluentd-elasticsearch-2wgmw
kubectl logs fluentd-elasticsearch-2wgmw
kubectl get ds -n kube-system
kubectl get pods -n kube-system
kubectl get ds -n kube-system
kubectl describe ds fluentd-elasticsearch -n kube-system
kubectl get ds -n kube-system
kubectl describe ds fluentd-elasticsearch -n kube-system
kubectl get rs -n kube-system
kubectl get pods -n kube-system
kubectl delete pods fluentd-elasticsearch-2wgmw
kubectl delete pods fluentd-elasticsearch-2wgmw -n kube-system
kubectl get pods -n kube-system
kubectl logs fluentd-elasticsearch-f4jss -n kube-system
vim fluentd-advanced.yaml 
kubectl apply -f fluentd-advanced.yaml 
kubect get ds -n kube-system
kubectl get ds -n kube-system
kubectl get pods -n kube-system
kubectl delete pods fluentd-elasticsearch-f4jss -n kube-system
kubectl delete pods fluentd-elasticsearch-vlqgl -n kube-system
kubectl get pods -n kube-system
kubectl get ds -n kube-system
kubectl delete ds fluentd-elasticsearch -n kube-system
kubectl get ds -n kube-system
vim fluentd-02.yaml
kubectl apply -f fluentd-02.yaml 
vim fluentd-02.yaml
kubectl apply -f fluentd-02.yaml 
kubectl get ds -n kube-system
kubectl get pods -n kube-system
kubectl get ds -n kube-system
clear
kubectl create clusterrolebinding fluentd --clusterrole=cluster-admin --user=system:serviceaccount:kube-system:default
vim fluentd-02.yaml
kubectl apply -f fluentd-02.yaml 
kubectl get ds -n kube-system
kubectl get pods -n kube-system
vim fluentd.yaml 
history | awk '{print substr($0, index($0, $2))}'
kubectl get ds -n kube-system
kubectl rollout history ds fluentd-elasticsearch -n kube-system
cd daemonset/
vim fluentd-02.yaml 
kubectl apply -f fluentd-02.yaml --record
vim fluentd-02.yaml 
kubectl apply -f fluentd-02.yaml --record
clear
kubectl rollout history ds fluentd-elasticsearch -n kube-system
kubectl rollout undo ds fluentd-elasticsearch -n kube-system
kubectl rollout history ds fluentd-elasticsearch -n kube-system
kubectl rollout undo ds fluentd-elasticsearch -n kube-system
kubectl rollout history ds fluentd-elasticsearch -n kube-system
```