# StatefulSet


```
cd devops-k8s/k8s-2/StatefulSet/
kubectl apply -f web.yaml
kubectl get service nginx
kubectl get statefulset
kubectl get pod
```

### For a StatefulSet with N replicas, when Pods are being deployed, they are created sequentially, in order from {0..N-1}. Examine the output of the kubectl get command in the first terminal. Eventually, the output will look like the example below.

Pods in a StatefulSet have a unique ordinal index and a stable network identity.
```
for i in 0 1; do kubectl exec web-$i -- sh -c 'hostname'; done
```

```
kubectl run -i --tty --image busybox:1.28 dns-test --restart=Never --rm  nslookup web-0.nginx
kubectl run -i --tty --image busybox:1.28 dns-test --restart=Never --rm  nslookup web-1.nginx
```
```
kubectl get pvc
kubectl scale sts web --replicas=5
```
--- 
kubectl delete sts web
kubectl delete sts web --cascade=false

# Headless service
When you create a headless service by setting clusterIP None, no load-balancing is done and no cluster IP is allocated for this service. Only DNS is automatically configured. When you run a DNS query for headless service, you will get the list of the Pods IPs and usually client dns chooses the first DNS record.

```
kubectl create deployment nginx --image=stenote/nginx-hostname
kubectl scale --replicas=3 deployment nginx
```
### Expose a headless service by setting --cluster-ip=None
```
$ kubectl expose deployment nginx --name nginxheadless --cluster-ip=None
```

### Expose a standart service (ClusterIP type)
```
$ kubectl expose deployment nginx --name nginxclusterip --port=80  --target-port=80
```
To test our case we need to run DNS queries and curl command. arunvelsriram/utils contains all the tool that we need.
```
kubectl run -i --tty --rm --image busybox:1.28 bash
nslookup nginxheadless
nslookup nginxclusterip
```
---
### Optional Casandra deploy
```
cd devops-k8s/k8s-2/StatefulSet/casandra
kubectl apply -f .

```
---
### Optional MySQL deploy
```
cd devops-k8s/k8s-2/StatefulSet/mysql
```
#### review yamls
```
kubectl apply -f .
```

### Clean all statefulsets and volumes