# DaemonSet
### Let's start by review and deploy our yaml:

```
kubectl apply -f fluentd.yaml

kubectl describe daemonset fluentd -n kube-system

kubectl get pods -n kube-system -o wide
```

Limiting DaemonSets to Specific Nodes
    The most common use case for DaemonSets is to run a Pod across every node in a
    Kubernetes cluster. However, there are some cases where you want to deploy a Pod
    to only a subset of nodes. For example, maybe you have a workload that requires a
    GPU or access to fast storage only available on a subset of nodes in your cluster. In
    cases like these node labels can be used to tag specific nodes that meet workload
    requirements.

    The first step in limiting DaemonSets to specific nodes is to add the desired set of
    labels to a subset of nodes. This can be achieved using the kubectl label
    command.
    The following command adds the ssd=true label to a single node:
```
    kubectl get nodes 
    kubectl label nodes lke104613-156419-6446b28c62c5 ssd=true

    kubectl apply -f nginx-fast-storage.yaml

    kubectl get pods -o wide
```
### Clean all 