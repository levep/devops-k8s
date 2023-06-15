# Istio


### Let's start by installing istio and applicatiogetting-started/

```
curl -L https://istio.io/downloadIstio | sh -
cd istio-1.17.2/
export PATH=$PWD/bin:$PATH
istioctl install --set profile=demo -y
kubectl label namespace default istio-injection=enabled
```
### Explore Istio installation in istio-system namespace
### port-forward grafana explore dashboards
```
kubectl port-forward svc/grafana 3000:3000 -n istio-system 
```
### port-forward kiali
```
kubectl port-forward -n istio-system svc/kiali 9090:20001
```

### deploying demo application https://istio.io/latest/docs/examples/bookinfo/



### check istio envoy proxy, describe one of the pod
### explore observability in kiali (port-forwarded previously) 