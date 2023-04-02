# Labels
### Let's deploy our workloads
```
    kubectl apply -f .
```
### Discover our deployments
```
    kubectl get deployments --show-labels
```
---
### Let's see how we use labels and label selector
```
    kubectl label deployments alpaca-test "canary=true"
    kubectl get deployments -L canary
    kubectl get deployments --show-labels
```
### Removing labels
```
    kubectl label deployments alpaca-test "canary-"  # Remove label
    kubectl get pods --show-labels
```
---
### Using label selector
```
    kubectl get pods --selector="ver=2"
    kubectl get pods --selector="app=bandicoot,ver=2"
    kubectl get pods --selector="app in (alpaca,bandicoot)"
    kubectl get deployments --selector="canary"
```