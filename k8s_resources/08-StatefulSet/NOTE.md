#A stateful application saves data about each client session that occurs and
#holds on to that data until the next time the client issues a request. The
#data which is saved is known as the state of the app, hence the term
#stateful. How is that data stored? Either locally or on a remote host until
#the time at which the user logs out.

#A stateless application, by contrast, is an application program that
#doesn’t save client data generated in one session for use in the next with
#the same client. HTTP, for instance, is inherently stateless. This means
#that when a state is desired for a web app, stateful features need to be
#built in with dynamic pages. The pages can store sessions via web address
#variables and server and client-side stored data, such as via cookies.

StatefulSets are valuable for applications that require one or more of the following.

Stable, persistent storage.
Ordered, graceful deployment and scaling.
Ordered, graceful deletion and termination.
Unique naming convention for stateful application
Unique network identity
Unique stable storage and ordered provisioning/termination
Updates will be done from last and followed by next in an ordered way

webserver --> 3 (replicas)

webserver-0, webserver-1, webserver-2


Preserving the data is called Statefulset application and if we are not bothered about the application data its a Stateless application


Cluster Domain	Service (ns/name)	StatefulSet (ns/name)	StatefulSet Domain	               Pod DNS	Pod Hostname
cluster.local	default/nginx	    default/web	            nginx.default.svc.cluster.local	   web-{0..N-1}.nginx.default.svc.cluster.local	web-{0..N-1}

cluster.local	foo/nginx	        foo/web	                nginx.foo.svc.cluster.local	web-{0..N-1}.nginx.foo.svc.cluster.local	web-{0..N-1}

kube.local	    foo/nginx	        foo/web	                nginx.foo.svc.kube.local	web-{0..N-1}.nginx.foo.svc.kube.local	


Deployment and Scaling Guarantee
1)For a StatefulSet with N replicas, when Pods are being deployed, they are created sequentially, in order from {0..N-1}.
2)When Pods are being deleted, they are terminated in reverse order, from {N-1..0}.
3)Before a scaling operation is applied to a Pod, all of its predecessors must be Running and Ready.
4)Before a Pod is terminated, all of its successors must be completely shutdown.


note:
1) Headless service is typically used with StatefulSets where the name of the pods are fixed. This is useful in situations 
like when you're settling up a MySQL cluster where you need to know the name of the master. StatefulSets appends an ordinal
number to the name of the pod and it will always assign the same ordinal number of the pod is restarted or migrated by the
scheduler.

In the case of a regular Deployment, ReplicaSet appends a hash to the pod's name making addressing specific pods difficult. The hash sort of anonomize the pods.

So if your application is stateless then you will just use with a 'regular' service because you don't care which pod you get. They're all the same.

Pod Management Policy
For some distributed systems, the StatefulSet ordering guarantees are unnecessary and/or undesirable. These systems require only uniqueness and identity. To address this, in Kubernetes 1.7, we introduced .spec.podManagementPolicy to the StatefulSet API Object.

OrderedReady Pod Management 
OrderedReady pod management is the default for StatefulSets. It tells the StatefulSet controller to respect the ordering guarantees demonstrated above.

Parallel Pod Management
Parallel pod management tells the StatefulSet controller to launch or terminate all Pods in parallel, and not to wait for Pods to become Running and Ready or completely terminated prior to launching or terminating another Pod.

https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/