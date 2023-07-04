# Helm

## Helm Basic

### Initialize a Helm Chart Repository
```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update              # Make sure we get the latest list of charts
helm search repo bitnami
```


### We can see default values by typing
```
helm show values bitnami/mysql 
```
### We can rewrite values via command line helm install --set param=value
### or to pass file helm install --values app1.yaml
```
helm install bitnami/mysql --generate-name
```

### Learn About Releases
```
helm list
helm status mysql-1682664088 
```

### Uninstall a Release
```
helm uninstall mysql-1682664088
```

### Download chart
```
helm pull bitnami/mysql --untar
cd mysql
```
### Set root password and deploy chart, see: https://helm.sh/docs/helm/helm_install/

### Review README.md, default and optional values.
---
---

## In this tutorial we will create simple helm chart - hello-world.
```
cd hello-world
```
### review directory stracture, Chart.yaml and files in templates directory 
### execute:

```
helm install hello-world .  --debug  --dry-run
```
### explore output yamls 
---

### Let's start by templating image
```
cd hello-world2
```
### review values.yaml, and deployment.yaml (image value on line 17 comming from values.yaml, repository:tag)
```
helm install hello-world .  --debug  --dry-run
```
---
### Next, let's templating tags.
```
cd hello-world3
```
### review deployment.yaml, and execute
```
helm install -g .  --debug  --dry-run
```
### explore output yamls, pay attention to labels where the values come from?
---
### finaly let's make our deployment more robust and generic by adding tpl functions

```
cd hello-world4
```
### review _helpers.tpl and deployment.yaml
```
helm install -g .  --debug  --dry-run
```
### explore output yamls
---
---
### Finally let's create template Helm Chart with helm utility 

```
helm create my-chart 
cd my-chart
helm install my-chart .  --debug  --dry-run
```
### Take time to review directory stracture, Chart.yaml, values.yaml and  files in templates directory