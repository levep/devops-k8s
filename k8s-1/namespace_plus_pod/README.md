Create Namespace + runnig pod + set context + delete namespace, intro to kubectl commandline
================================================

    $ kubectl create -f namespaces-dev.json

    $ kubectl get namespace

    $ kubectl run kuard  --image=gcr.io/kuar-demo/kuard-amd64:1 -n development

    $ kubectl get pods -n development

kubectl conventions: https://kubernetes.io/docs/reference/kubectl/conventions/
-------------------

    $  kubectl config set-context --current --namespace=development

    $ kubectl get pods kuard -o yaml

    $ kubectl get pods kuard -o json

    $ kubectl edit pods kuard

kubectl context and configuration: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#config
---------------------------------

    $ kubectl config set-context --current --namespace=default

    $ kubectl delete namespace development
