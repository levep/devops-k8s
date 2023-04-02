# Labels

```
kubectl run alpaca-prod --image=gcr.io/kuar-demo/kuard-amd64:1 --replicas=2 --labels="ver=1,app=alpaca,env=prod"
kubectl run alpaca-test --image=gcr.io/kuar-demo/kuard-amd64:2 --replicas=1 --labels="ver=2,app=alpaca,env=test"

kubectl run bandicoot-prod --image=gcr.io/kuar-demo/kuard-amd64:2 --replicas=2 --labels="ver=2,app=bandicoot,env=prod"
kubectl run bandicoot-staging --image=gcr.io/kuar-demo/kuard-amd64:2 --replicas=1 --labels="ver=2,app=bandicoot,env=staging"

kubectl get deployments --show-labels
kubectl label deployments alpaca-test "canary=true"
kubectl get deployments -L canary
kubectl label deployments alpaca-test "canary-"  # Remove label
kubectl get pods --show-labels
kubectl get pods --selector="ver=2"
kubectl get pods --selector="app=bandicoot,ver=2"
kubectl get pods --selector="app in (alpaca,bandicoot)"
kubectl get deployments --selector="canary"
```