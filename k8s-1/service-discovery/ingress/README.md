# Ingress
```
    kubectl create -f hello-one.yaml
    kubectl create -f hello-two.yaml
```
---
### Install the NGINX Ingress Controller

```
    helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
    helm repo update
    helm install ingress-nginx ingress-nginx/ingress-nginx
```

```
    kubectl --namespace default get services -o wide -w ingress-nginx-controller
```

```
    kubectl create -f my-new-ingress.yaml
```

### Create a Subdomain DNS Entries for your Example Applications:
### edit /etc/host and add two records:
```
<LB IP> blog.devopscourse.co
<LB IP> shop.devopscourse.co
```
### In browser navigate to blog.devopscourse.co and shop.devopscourse.co

### Let's clean
```
helm uninstall ingress-nginx
```

### in ingress directory:
```
kubectl delete -f .
```
