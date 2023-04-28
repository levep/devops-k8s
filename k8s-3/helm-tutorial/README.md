# Helm

## Helm Basic

### Initialize a Helm Chart Repository
```
helm repo add bitnami https://charts.bitnami.com/bitnami

helm search repo bitnami
```

### Install an Example Chart
```
helm repo update              # Make sure we get the latest list of charts

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
### Review README.md, default and optional values.
---
---

## Helm Chart creation - step by step

### Let's create/explore simple chart
### review directory stracture, Chart.yaml and templates files
```
cd hello-world
```

### Let's explore output yamls 
```
helm install hello-world .  --debug  --dry-run
```

### templating image
### review directory stracture, Chart.yaml and templates files
```
cd hello-world2
helm install hello-world .  --debug  --dry-run
```

### templating tags
### review directory stracture, Chart.yaml and templates files
```
cd hello-world3
helm install hello-world .  --debug  --dry-run
```

### tpl functions
### review directory stracture, Chart.yaml and templates files
```
cd hello-world4
helm install hello-world .  --debug  --dry-run
```
---
### Let's create Helm Chart with helm utility 
### review directory stracture, Chart.yaml and templates files
```
helm create my-chart 
cd my-chart
helm install my-chart .  --debug  --dry-run
```
