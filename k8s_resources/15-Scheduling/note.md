# kube-scheduler selects a node for the pod in a 2-step operation:

Filtering
Scoring

The filtering step finds the set of Nodes where it's feasible to schedule the Pod. For example, the PodFitsResources filter checks whether a candidate Node has enough available resource to meet a Pod's specific resource requests. After this step, the node list contains any suitable Nodes; often, there will be more than one. If the list is empty, that Pod isn't (yet) schedulable.

In the scoring step, the scheduler ranks the remaining nodes to choose the most suitable Pod placement. The scheduler assigns a score to each Node that survived filtering, basing this score on the active scoring rules.

policies:
https://kubernetes.io/docs/reference/scheduling/policies/

https://kubernetes.io/docs/concepts/scheduling-eviction/scheduler-perf-tuning/

https://kubernetes.io/docs/concepts/workloads/pods/pod-topology-spread-constraints/