# Kustomize


### Kustomize cross-cutting-fields
```
cd cross-cutting-fields
kubectl kustomize ./
```
### Review output
---
### Kustomize secret generator
```
cd msql-wordpress
kubectl kustomize ./
```
### Review output
### Let's deploy 
```
kubectl apply -k .
```
### delete all by
```
kubectl delete -k . 
```