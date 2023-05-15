# K8S Job

### A Job creates one or more Pods and will continue to retry execution of the Pods until a specified number of them successfully terminate. As pods successfully complete, the Job tracks the successful completions. When a specified number of successful completions is reached, the task (ie, Job) is complete. Deleting a Job will clean up the Pods it created. Suspending a Job will delete its active Pods until the Job is resumed again.

### Here is an example Job config. It computes π to 2000 places and prints it out. It takes around 10s to complete.

```
kubectl apply -f controlers-job.yaml 
kubectl get pod -w
kubectl logs <POD name>
kubectl delete -f controlers-job.yaml
```

### Example of key generator one shot 
```
kubectl apply -f job-oneshot.yaml
```

### Example of key generator parallel 
```
kubectl apply -f job-parallel.yaml
```

```
kubectl delete pods --all
```

### Work with queue
#### A common use case for jobs is to process work from a work queue. In this scenario, some task creates a number of work items and publishes them to a work queue. A worker job can be run to process each work item until the work queue is empty.
```
cd queue
kubectl apply -f dp-queue.yaml
QUEUE_POD=$(kubectl get pods -l app=work-queue,component=queue -o jsonpath='{.items[0].metadata.name}')
kubectl port-forward $QUEUE_POD 8080:8080
kubectl apply -f svc-queue.yaml
./load-queue.sh
kubectl apply -f job-consumers.yaml
```
