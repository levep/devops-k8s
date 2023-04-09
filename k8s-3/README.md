# Helm

```
 $ helm repo add stable https://kubernetes-charts.storage.googleapis.com/

$ helm search repo stable

$ cd /tmp; helm fetch stable/tomcat

$ tar xfvz tomcat-0.4.1.tgz; cd tomcat
```

```
$ helm install my-release stable/tomcat

$  kubectl get svc --namespace default my-release-tomcat
```