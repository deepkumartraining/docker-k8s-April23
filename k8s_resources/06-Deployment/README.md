## Deployment provides declarative updates for Pods and ReplicaSets
- The following are typical use cases for Deployments:
  - Create a Deployment to rollout a ReplicaSet. The ReplicaSet creates Pods in the background. Check the status of the rollout to see if it succeeds or not.
  - Declare the new state of the Pods by updating the PodTemplateSpec of the Deployment. A new ReplicaSet is created and the Deployment manages moving the Pods from the old ReplicaSet to the new one at a controlled rate. Each new ReplicaSet updates the revision of the Deployment.
  - Rollback to an earlier Deployment revision if the current state of the Deployment is not stable. Each rollback updates the revision of the Deployment.
  - Scale up the Deployment to facilitate more load.
  - Pause the rollout of a Deployment to apply multiple fixes to its PodTemplateSpec and then resume it to start a new rollout.
  - Use the status of the Deployment as an indicator that a rollout has stuck.
  - Clean up older ReplicaSets that you don't need anymore.

- we can use deployment for application upgrade/Rollout and Rollback/downgrade the changes if the desired function crashes. we can also scale the number of replicas for the deployment as well.
```
#kubectl scale deployment/nginx-deployment --replicas=5
```

- For example:
if we want to change the image for a deployment like from 1.7.9 to 1.9.1 which is upgrade of your applications

Set a deployment's nginx container image to 'nginx:1.9.1', and its busybox container image to 'busybox'.
#kubectl set image deployment/nginx busybox=busybox nginx=nginx:1.9.l

## Print result (in yaml format) of updating nginx container image from local file, without hitting the server
kubectl set image -f path/to/file.yaml nginx=nginx:1.9.1 --local -o yaml

Let’s update the nginx Pods to use the nginx:1.9.1 image instead of the nginx:1.7.9 image.
#kubectl --record deployment.apps/nginx-deployment set image deployment.v1.apps/nginx-deployment nginx=nginx:1.9.1

or

kubectl set image deployment/nginx-deployment nginx=nginx:1.9.1 --record

Tp update anotation with the changes caused:
#kubectl annotate deployment.v1.apps/nginx-deployment kubernetes.io/change-cause="image updated to 1.9.1"

How to update resources for a deployment:
```
#kubectl set resources deployment.v1.apps/nginx-deployment -c=nginx --limits=cpu=200m,memory=512Mi

root@kubernetesmaster:~# kubectl rollout
Manage the rollout of a resource.

Valid resource types include:

  *  deployments
  *  daemonsets
  *  statefulsets

Examples:
  ### Rollback to the previous deployment
  kubectl rollout undo deployment/abc

  ### Check the rollout status of a daemonset
  kubectl rollout status daemonset/foo

Available Commands:
  history     View rollout history
  pause       Mark the provided resource as paused
  restart     Restart a resource
  resume      Resume a paused resource
  status      Show the status of the rollout
  undo        Undo a previous rollout

Usage:
  kubectl rollout SUBCOMMAND [options]

Use "kubectl <command> --help" for more information about a given command.
Use "kubectl options" for a list of global command-line options (applies to all commands).
root@kubernetesmaster:~#
```
- The RollingUpdateStrategy shows that we have a limit of 1 maxUnavailable — meaning that when we’re updating the Deployment, we can have up to 1 missing pod before it’s replaced, and 1 maxSurge, meaning we can have one extra pod as we scale the new pods back up.

```

## Deployment Set Commands execution reference

kubectl get nodes
kubectl get deployments
cd deployments/
vim deployment-01.yaml 
vim deployment-01.yaml 
kubectl apply -f deployment-01.yaml 
kubectl get deployments
kubectl get replicaset
kubectl describe deployments nginx-deployment
vim deployment-01.yaml 
cp deployment-01.yaml deployment-01-bkp.yaml
vim deployment-01.yaml
clear
kubectl apply -f deployment-01.yaml 
kubectl get deployment
kubectl get replicaset
kubectl describe deployments nginx-deployment
clear
kubectl rollout undo deployment nginx-deployment
kubectl get replicaset
kubectl rollout status deployment/nginx-deployment
kubectl rollout history deployment/nginx-deployment
kubectl rollout undo deployment nginx-deployment --to-revision=3
kubectl rollout undo deployment nginx-deployment --to-revision=2
kubectl get replicaset
vim deployment-01.yaml 
kubectl apply -f deployment-01.yaml 
kubectl get deployments
vim deployment-02.yaml
kubectl get deployments
kubectl create deployment-02.yaml 
kubectl create -f deployment-02.yaml 
kubectl get deployments
vim deployment-02.yaml 
kubectl apply -f deployment-02.yaml 
vim deployment-02.yaml 
kubectl create --save-config -f deployment-02.yaml 
kubectl apply --save-config -f deployment-02.yaml 
kubectl apply -f deployment-02.yaml 
kubectl get deployments
kubectl describe deployment nginx-deployment-02
kubctl get rs deployment/nginx-deployment-02
kubectl get rs deployment/nginx-deployment-02
kubectl get rs
kubectl rollout history deployments/nginx-deployment-02
vim deployment-02.yaml 
kubectl apply -f deployment-02.yaml --record
kubectl rollout history deployments/nginx-deployment-02
kubectl get deploymentset
kubectl get deployment
kubectl get rs
kubectl rollout history deployments/nginx-deployment-02
history | awk '{print substr($0, index($0, $2))}'```
kubectl edit deployment nginx-deployment
kubectl rollout status deployment/nginx-deployment
```