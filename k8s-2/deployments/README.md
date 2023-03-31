kubectl  get deployments kuard \
-o jsonpath --template {.spec.selector.matchLabels}

kubectl  get replicasets --selector=run=kuard

kubectl  scale deployments kuard --replicas=2

kubectl  get replicasets --selector=run=kuard

kubectl  scale replicasets kuard-1128242161 --replicas=1 (Deployment managed ReplicaSet !!!)

kubectl  get replicasets --selector=run=kuard

----
kubectl  get deployments kuard --export -o yaml >  first-deployment.yaml

kubectl  replace -f  first-deployment.yaml --save-config
You also need to run kubectl replace --save-config. This adds an annotation so
that, when applying changes in the future, kubectl will know what the last applied
configuration was for smarter merging of configs. If you always use kubectl apply,
this step is only required after the first time you create a deployment using kubectl
create -f
---
kubectl  describe deployments kuard

Two of the most important pieces of information in the output are
OldReplicaSets and NewReplicaSet. These fields point to the
ReplicaSet objects this deployment is currently managing. If a deployment
is in the middle of a rollout, both fields will be set to a value. If a rollout is
complete, OldReplicaSets will be set to <none>.
---
kubectl  rollout history deployment kuard
kubectl  rollout status  deployment kuard
===
Updating Deployment
	change in YAML to 3 and apply

kubectl  apply -f  first-deployment.yaml
----
Updating a Container Image
	gcr.io/kuar-demo/kuard-amd64:green
	imagePullPolicy: Always

We are also going to put an annotation in the template for the deployment
to record some information about the update:
...
spec:
...
template:
  metadata:
    annotations:
      kubernetes.io/change-cause: "Update to green kuard"
…
kubectl  apply -f  first-deployment.yaml
kubectl  rollout status deployments kuard
kubectl  get replicasets -o wide

 kubectl  rollout history deployment kuard --revision=3
 kubectl  rollout undo deployments kuard --to-revision=2

---

Recreate Strategy
The Recreate strategy is the simpler of the two rollout strategies. It
simply updates the ReplicaSet it manages to use the new image and
terminates all of the Pods associated with the deployment. The ReplicaSet
notices that it no longer has any replicas, and re-creates all Pods using the
new image. Once the Pods are re-created, they are running the new
version.
While this strategy is fast and simple, it has one major drawback—it is
potentially catastrophic, and will almost certainly result in some site
downtime. Because of this, the Recreate strategy should only be used for
test deployments where a service is not user-facing and a small amount of
downtime is acceptable.

RollingUpdate Strategy
The RollingUpdate strategy is the generally preferable strategy for any
user-facing service. While it is slower than Recreate, it is also
significantly more sophisticated and robust. Using RollingUpdate, you
can roll out a new version of your service while it is still receiving user
traffic, without any downtime.
As you might infer from the name, the RollingUpdate strategy works by
updating a few Pods at a time, moving incrementally until all of the Pods
are running the new version of your software.
RollingUpdate is a fairly generic strategy; it can be used to update a
variety of applications in a variety of settings. Consequently, the rolling
update itself is quite configurable; you can tune its behavior to suit your
particular needs. There are two parameters you can use to tune the rolling
update behavior: maxUnavailable and maxSurge.
The maxUnavailable parameter sets the maximum number of Pods that
can be unavailable during a rolling update. It can either be set to an
absolute number (e.g., 3, meaning a maximum of three Pods can be
unavailable) or to a percentage (e.g., 20%, meaning a maximum of 20% of
the desired number of replicas can be unavailable).

