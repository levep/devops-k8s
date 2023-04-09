# Prometheus
```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```
```
helm install my-monitoring prometheus-community/kube-prometheus-stack

```

### Explore values.yaml
```
helm pull prometheus-community/kube-prometheus-stack
tar xvf kube-prometheus-stack-45.9.1.tgz
cd kube-prometheus-stack
```
### Take time to review values.yaml


### Let's expose grafana via NodePort, change ClusterIP to NodePort:
```
kubectl edit svc my-monitoring-grafana
```

### Uninstall prometheus:
```
helm uninstall my-monitoring
kubectl delete crd alertmanagerconfigs.monitoring.coreos.com
kubectl delete crd alertmanagers.monitoring.coreos.com
kubectl delete crd podmonitors.monitoring.coreos.com
kubectl delete crd probes.monitoring.coreos.com
kubectl delete crd prometheuses.monitoring.coreos.com
kubectl delete crd prometheusrules.monitoring.coreos.com
kubectl delete crd servicemonitors.monitoring.coreos.com
kubectl delete crd thanosrulers.monitoring.coreos.com
```



```
https://artifacthub.io/packages/helm/prometheus-community/kube-prometheus-stack

https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack
```