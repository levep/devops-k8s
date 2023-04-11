### Let's create deployment
```
    kubectl create deployment nginx --image=nginx
    kubectl get deploy nginx
    kubectl get pod
```

### let's create 3 services review and compare them
```
    kubectl apply -f nginx-svc.yaml
    kubectl apply -f nginx-svc-nodeport.yaml
    kubectl apply -f nginx-svc-loadbalancer.yaml
```
---
```
kubectl get svc
```