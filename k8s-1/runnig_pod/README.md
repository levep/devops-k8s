# K8S POD
## Basic features
### In terminal please type:
```
    kubectl create -f kuard-pod.yaml

    kubectl port-forward  --address 0.0.0.0 kuard  8080:8080
```
### In browser go to localhost:8080, take a moment to explore our application. Once you finish Ctrl+C to terminate port-forward

### In terminal please type:
```
    kubectl exec kuard -- date

    kubectl exec -it kuard -- ash

    kubectl delete pod kuard
```
## Pod with health check

```
    kubectl create -f kuard-pod-health.yaml
    kubectl port-forward  --address 0.0.0.0 kuard  8080:8080
```
### In our application go to Liveness Probe section.
### Fail for next N calls, choose 2.
### What happend?
### Fail for next N calls, choose 3.
### What happend?
### For more information please explore documentation:
```
https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/
```

```
    kubectl delete pod kuard
```
## Resource Management

With scheduling systems like Kubernetes managing resource packing, you can drive
your utilization to greater than 50%.
Kubernetes allows users to specify two different resource metrics. Resource requests
specify the minimum amount of a resource required to run the application. Resource
limits specify the maximum amount of a resource that an application can consume. When you establish limits on a container, the kernel is configured to ensure that consumption cannot exceed these limits. A container with a CPU limit of 0.5 cores will only ever get 0.5 cores, even if the CPU is otherwise idle. A container with a memory limit of 256 MB will not be allowed additional memory (e.g., malloc will fail) if its memory usage exceeds 256 MB.

```
    kubectl apply -f kuard-pod-resreq.yaml
    kubectl describe pod kuard
    kubectl port-forward  --address 0.0.0.0 kuard  8080:8080
```
### Navigate to our application, Memory: Allocate 500MiB
### What happend?
```
    kubectl delete pod kuard
    kubectl apply -f kuard-pod-reslim.yaml
    kubectl describe pod kuard
    kubectl port-forward  --address 0.0.0.0 kuard  8080:8080
```
### Navigate to our application, Memory: Allocate 500MiB
### What happend?

```
    kubectl delete pod kuard
```

 ## Persisting Data with Volumes
```
    kubectl apply -f kuard-pod-vol.yaml
    kubectl describe pod kuard
    kubectl delete pod kuard
```


### Few and recommended patterns :
- Communication/synchronization
    Two containers used a shared volume to serve a site while keeping it synchronized to a remote Git location.
    To achive this. the Pod uses an emptyDir volume.
- Cashe :
    application may use a volume that is valuable for performance, but not required
    for correct operation of the application. 
    emptyDir works well for the cache use case as well.
- Persistent data :
    Sometimes you will use a volume for truly persistent data—data that is independent
    of the lifespan of a particular Pod, and should move between nodes in the cluster if a
    node fails or a Pod moves to a different machine for some reason. To achieve this,
    Kubernetes supports a wide variety of remote network storage volumes, including
    widely supported protocols like NFS or iSCSI as well as cloud provider network
    storage like Amazon’s Elastic Block Store, Azure’s Files and Disk Storage, as well
    as Google’s Persistent Disk.
- Mounting the host filesystem :
    Other applications don’t actually need a persistent volume, but they do need some
    access to the underlying host filesystem. For example, they may need access to the
    /dev filesystem in order to perform raw block-level access to a device on the system.
    For these cases, Kubernetes supports the hostDir volume, which can mount
    arbitrary locations on the worker node into the container.

## POD full
```
    kubectl apply -f kuard-pod-full.yaml
    kubectl describe pod kuard
```
### Navigate to our application discover all features that we talk about

```
    kubectl delete pod kuard
```

## POD with multiple containers

```
    kubectl apply -f pod-multicontainers.yaml
    kubectl port-forward  --address 0.0.0.0 mc1  8080:80
```
### Navigate to localhost:8080
### Where is print comming from?
```
    kubectl describe pod mc1
    kubectl delete pod mc1
```
