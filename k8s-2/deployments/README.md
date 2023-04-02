# K8S Deployments
## Creating Deployment
```  
  kubectl apply -f first-deployment.yaml
```
### Get details of your Deployment
```
  kubectl describe deployments
```
---
## Updating Deployment
```
  kubectl set image deployment.v1.apps/nginx-deployment nginx=nginx:1.16.1
```
### or use the following command
```
  kubectl set image deployment/nginx-deployment nginx=nginx:1.16.1
```

### To see the rollout status, run
```
  kubectl rollout status deployment/nginx-deployment
```

### Get details of your Deployment
```
  kubectl describe deployments
```
---
### Checking Rollout History of a Deployment
```
  kubectl rollout history deployment/nginx-deployment
```

### To see the details of each revision, run
```
  kubectl rollout history deployment/nginx-deployment --revision=2
  kubectl rollout history deployment/nginx-deployment --revision=1
```
### Rolling Back to a Previous Revision
```
  kubectl rollout undo deployment/nginx-deployment
```

### Alternatively, you can rollback to a specific revision by specifying it with --to-revision

```
  kubectl rollout undo deployment/nginx-deployment --to-revision=2
```
---
### Scaling a Deployment
```
  kubectl scale deployment/nginx-deployment --replicas=10
```

### Proportional scaling
- For example, you are running a Deployment with 10 replicas, maxSurge=3, and maxUnavailable=2.


```
  kubectl set image deployment/nginx-deployment nginx=nginx:sometag
  kubectl get rs
  kubectl get pods
  kubectl get deploy
  kubectl rollout undo deployment/nginx-deployment
```
---
### Pausing and Resuming a rollout of a Deployment
- RollingUpdate Deployments support running multiple versions of an application at the same time. When you or an autoscaler scales a RollingUpdate Deployment that is in the middle of a rollout (either in progress or paused), the Deployment controller balances the additional replicas in the existing active ReplicaSets (ReplicaSets with Pods) in order to mitigate risk. This is called proportional scaling.
```
  kubectl rollout pause deployment/nginx-deployment
  kubectl set image deployment/nginx-deployment nginx=nginx:1.16.1
```

#### Notice that no new rollout started
```
  kubectl rollout history deployment/nginx-deployment
```
#### You can make as many updates as you wish, for example, update the resources that will be used

```
  kubectl set resources deployment/nginx-deployment -c=nginx --limits=cpu=200m,memory=512Mi
```

#### Eventually, resume the Deployment rollout and observe a new ReplicaSet coming up with all the new updates
```
  kubectl rollout resume deployment/nginx-deployment
```

#### Watch the status of the rollout until it's done
```
  kubectl get rs -w
```
---
#### Clean resources
```
  kubectl delete -f first-deployment.yaml
```