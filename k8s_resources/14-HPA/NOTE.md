#kubectl autoscale deployment.v1.apps/nginx-deployment --min=10 --max=15 --cpu-percent=80

Metrics server needs to setup prior to HPA as that will help to gather metrics for pods

https://github.com/kubernetes-sigs/metrics-server

kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.3.6/components.yaml

Release: https://github.com/kubernetes-sigs/metrics-server/releases




# Note: 
Depending on your cluster configuration, you may also need to change flags passed to the Metrics Server container. Most useful flags:
In our poc environment we are not using TLS certificate so you may get problem related to metrics calculation
Check metrics server is working fine or not
Check Deployment, replica set and Pods for more details via logs, describe
Based on finding, it may require to update the metrics server configuration file
Download file locally via wget or curl command 
wget https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.3.6/components.yaml

Update component.yaml with below details:

 containers:
      - name: metrics-server
        image: k8s.gcr.io/metrics-server-amd64:v0.3.6
        imagePullPolicy: IfNotPresent
        args:
          - --cert-dir=/tmp
          - --secure-port=4443
          - --kubelet-insecure-tls #This needs to update
          - --kubelet-preferred-address-types=InternalIP # This needs to update

Save component.yaml and perform metric server deployment
kubectl apply -f component.yaml

Validate after a minutes
Kubectl top nodes
kubectl top pods

Expected result: it should provide output



# Additional configuration that may require to update based on setup

--kubelet-preferred-address-types - The priority of node address types used when determining an address for connecting to a particular node (default [Hostname,InternalDNS,InternalIP,ExternalDNS,ExternalIP])
--kubelet-insecure-tls - Do not verify the CA of serving certificates presented by Kubelets. For testing purposes only.
--requestheader-client-ca-file - Specify a root certificate bundle for verifying client certificates on incoming requests before trusting usernames in headers specified by --requestheader-username-headers.
WARNING: Do not depend on prior authorization for incoming requests.


# Now resume back with your HPA based testing mentioned in deployment-python-hpa.yaml

Testing load on HPA:

kubectl autoscale deployment php-apache --cpu-percent=50 --min=1 --max=10
kubectl run -it --rm load-generator --image=busybox /bin/sh
while true; do wget -q -O- http://php-apache; done