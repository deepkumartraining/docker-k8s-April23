# ReplicationController and ReplicaSet
- A ReplicationController ensures that a specified number of pod replicas
are running at any one time.
- For example:
  - If there are too many pods, the ReplicationController terminates the extra pods. If there are too few, the ReplicationController starts more pods. Unlike manually created pods, the pods maintained by a ReplicationController are automatically replaced if they fail, are deleted, or are terminated.
- To fetch all the pods of RC:
```
pods=$(kubectl get pods --selector=app=nginx --output=jsonpath={.items..metadata.name})
echo $pods
```
- How to scale your RC?
```
kubectl scale --replicas=3 rc/nginx

RS:
Difference of rc and rs in yaml file
...
spec:
   replicas: 3
   selector:
     matchExpressions:
      - {key: app, operator: In, values: [soaktestrs, soaktestrs, soaktest]}
      - {key: teir, operator: NotIn, values: [production]}
  template:
     metadata:
...
```
## Difference between ReplicationController and ReplicaSet
- ReplicationController:
  - ReplicationController has scalein and scaleout strategy, where replicaset has the same.
  - It has Equality based selectors.
  - It is based on filtering by label keys and values. Matching objects must satisfy all of the specified label constraints.
  ```
  env = prod
  app != database
  ```
- ReplicaSet:
  - It works same as ReplicationController except selectors.
  - It has Set based selectors.
  - It helps to allow filtering keys according to a set of values.
  ```
  env in (production, staging)
  app notin (frontend, backend)
  qa
## Commands executed
```
mkdir rc-rs
cd rc-rs/
clear
vim rc-basic.yaml
clear
kubectl create -f rc-basic.yaml 
vim rc-basic.yaml
kubectl create -f rc-basic.yaml 
clear
kubect get replicationcontroller
kubectl get replicationcontroller
kubectl describe rc myapp-nginx-rc
kubectl get replicationcontroller
kubectl get pods
history
clear
ll
vim rs-basic.yaml
kubectl create -f rs-basic.yaml 
vim rs-basic.yaml
kubectl create -f rs-basic.yaml 
vim rs-basic.yaml
kubectl create -f rs-basic.yaml 
kubectl get replicaset
kubectl describe replicaset myapp-nginx-rs
clear
kubectl describe replicaset myapp-nginx-rs
kubectl get pods
kubect get replicaset
kubectl get replicaset
clear
kubectl get replicaset -o wide
kubectl get services
curl -I 10.96.0.1
kubectl get rc -o wide
clear
kubectl get rc
kubectl get rs
kubectl scale --replicas=6 -f rc-basic.yaml 
kubectl scale --replicas=6 -f rs-basic.yaml 
kubectl get rc
kubectl get rs
vim rc-basic.yaml 
kubectl scale --replicas=5 rc myapp-nginx-rc
kubectl scale --replicas=5 rc myapp-nginx-rs
kubectl scale --replicas=5 rs myapp-nginx-rs
clear
kubectl get rc
kubectl get rs
clear
history | awk '{print substr($0, index($0, $2))}'
```
  ```