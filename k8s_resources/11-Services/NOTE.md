# Headless service with selectors.
With a headless service that defines selectors, the endpoints controller creates endpoint records in the API, modifying the DNS configuration to return A records (addresses) that point to the pods that back the service.

# Headless service without selectors.
Headless services don’t define selectors, so the endpoints controller does not create endpoint records. However, the DNS system configures one of the following:
For service type ExternalName, CNAME records
For the other service types, a record for any endpoints that share names with the service

Kube-proxy implements a form of virtual IP for services for all types other than ExternalName. To achieve this, you can set three possible modes:

Proxy-mode: userspace. In this mode, kube-proxy keeps an eye on the Kubernetes master, watching for services and endpoints objects that get added or removed. For each service, the mode opens a random port on your local node. Any connections to this “proxy port” are proxied to a service’s backend pods and reported in the endpoints.

Proxy-mode: iptables. When this mode is on, kube-proxy continues to watch the Kubernetes master for added or removed services and endpoint objects.
For each service, unlike in userspace, this mode installs iptables rules in order to capture traffic to the service’s clusterIP (virtual) and port, and then redirects that traffic to a service backend set.
For each endpoints object, the mode installs iptables rules to select a random (by default) backend pod.

Proxy-mode: ipvs. In this mode, kube-proxy watches the services and endpoints and calls netlink interface in order to create appropriate ipvs rules. Then, to ensure ipvs status is consistent with its expectations, the mode periodically syncs ipvs rules with services and endpoints. When a service is accessed, traffic gets redirected to a backend pod.

Testing of headless service:

Inside busybox pod:
kubectl run --generator=run-pod/v1 --rm utils -it --image trainingxxx/utils bash
for i in $(seq 1 10) ; do curl headless-service; done
curl -v headless-service

```
root@controlplane:~# kubectl create -f services/nodeport.yaml 
The Service "my-nginx" is invalid: spec.ports[0].nodePort: Invalid value: 24000: provided port is not in the valid range. The range of valid ports is 30000-32767
root@controlplane:~# 
```