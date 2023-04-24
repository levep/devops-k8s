# ConfigMap

### Let's create configmap with kubectl:
```
kubectl create configmap my-config --from-file=simple-config.txt --from-literal=extra-param=extra-value --from-literal=another-param=another-value
```

### Let's explore it
```
kubectl get configmaps my-config -o yaml

kubectl port-forward kuard-config 8080
```