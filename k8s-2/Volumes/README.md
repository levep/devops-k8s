# Volumes

### get and describe Storage Class
```
kubectl get sc
kubectl describe sc linode-block-storage
```
### Check CSI driver daemonSet
```
kubectl get daemonset.apps/csi-linode-node -n kube-system
```