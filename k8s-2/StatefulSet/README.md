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
kubectl delete sts web 

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
###  MySQL deploy
```
cd devops-k8s/k8s-2/StatefulSet/mysql
```
#### review yamls
```
kubectl apply -f .
```
### Sending client traffic
```
kubectl run mysql-client --image=mysql:5.7 -i --rm --restart=Never --\
  mysql -h mysql-0.mysql <<EOF
CREATE DATABASE test;
CREATE TABLE test.messages (message VARCHAR(250));
INSERT INTO test.messages VALUES ('hello');
EOF
```
### Use the hostname mysql-read to send test queries to any server that reports being Ready:
```
kubectl run mysql-client --image=mysql:5.7 -i -t --rm --restart=Never --\
  mysql -h mysql-read -e "SELECT * FROM test.messages"
```

### To demonstrate that the mysql-read Service distributes connections across servers, you can run SELECT @@server_id in a loop:
```
kubectl run mysql-client-loop --image=mysql:5.7 -i -t --rm --restart=Never --\
  bash -ic "while sleep 1; do mysql -h mysql-read -e 'SELECT @@server_id,NOW()'; done"
```

### When you use MySQL replication, you can scale your read query capacity by adding replicas. For a StatefulSet, you can achieve this with a single command:
```
kubectl scale statefulset mysql  --replicas=5
```
### Watch the new Pods come up by running:
```
kubectl get pods -l app=mysql --watch
```

### Once they're up, you should see server IDs 103 and 104 start appearing in the SELECT @@server_id loop output.
### You can also verify that these new servers have the data you added before they existed:
```
kubectl run mysql-client --image=mysql:5.7 -i -t --rm --restart=Never --\
  mysql -h mysql-3.mysql -e "SELECT * FROM test.messages"
```

### Scaling back down is also seamless:
```
kubectl scale statefulset mysql --replicas=3
```
### Clean all statefulsets and volumes
### Although scaling up creates new PersistentVolumeClaims automatically, scaling down does not automatically delete these PVCs.
### Delete all PVC, PV and volumes 
---
### Deploying Casandra
```
cd casandra
kubectl apply -f casandra-svc.yaml
kubectl get svc cassandra
```
#### Using a StatefulSet to create a Cassandra ring
```
kubectl apply -f casandra-sts.yaml
kubectl get pods -w
```
#### Validating the Cassandra StatefulSet
```
kubectl get statefulset cassandra
```
#### Run the Cassandra nodetool inside the first Pod, to display the status of the ring.
```
kubectl exec -it cassandra-0 -- nodetool status
```
#### Modifying the Cassandra StatefulSet. Change the number of replicas to 4 
```
kubectl edit statefulset cassandra
```
### Get the Cassandra StatefulSet to verify your change:
```
kubectl get statefulset cassandra
```
---
### Running ZooKeeper as StatefullSet. (Pod disruption budgets)
#### please follow tutorial on: https://kubernetes.io/docs/tutorials/stateful-application/zookeeper/

