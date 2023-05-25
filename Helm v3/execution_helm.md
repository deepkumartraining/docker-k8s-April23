### We will browse some execution with helm

Installation cover in this folder only

# Installation of Helm Charts
helm repo add bitnami https://charts.bitnami.com/bitnami
helm search repo bitnami
helm repo update 
# Install mysql charts
helm install bitnami/mysql --generate-name
helm install my-custom-name bitnami/mysql
helm show chart bitnami/mysql
helm status mysql-1652869723 <Name would be different>
kubectl get all