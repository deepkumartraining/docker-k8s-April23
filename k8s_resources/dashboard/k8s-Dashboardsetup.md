# Kubernetes Dashboarding setup


kubectl apply -f /root/dashboard.yaml
kubectl -n kubernetes-dashboard wait --for=condition=ready pod --all


need to change
args:
- --namespace=kubernetes-dashboard
- --enable-skip-login
- --disable-settings-authorizer
- --enable-insecure-login
- --insecure-bind-address=0.0.0.0

# Service needs to created for dashboard
---
kind: Service
apiVersion: v1
metadata:
  labels:
    k8s-app: kubernetes-dashboard
  name: kubernetes-dashboard
  namespace: kubernetes-dashboard
spec:
  ports:
    - port: 9090
      targetPort: 9090
  selector:
    k8s-app: kubernetes-dashboard
---


kubectl -n kubernetes-dashboard create sa admin-user
kubectl create clusterrolebinding admin-user --clusterrole cluster-admin --serviceaccount kubernetes-dashboard:admin-user
kubectl -n kubernetes-dashboard create token admin-user

# Copy Token for dashboard setup


kubectl -n kubernetes-dashboard port-forward service/kubernetes-dashboard 9090:9090 --address 0.0.0.0

https://6b724fa6-c7b3-44a1-9150-2d5c9ce7d1f2-10-244-4-119-9090.papa.r.killercoda.com/

https://killercoda.com/scenario/traffic/eeba9b55-41df-4742-80ad-b19f518c0411
