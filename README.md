# K8s Demos

## ArgoCD Install

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
or
kubectl apply -n argocd -f cluster/argocd/argocd.yaml
```

## Demo

This demo will show how to use argocd to manage manifests in a kubernetes cluster

### Setup

1. Start local cluster `minikube start`
2. Enable ingress controller for minikube `minikube addons enable ingress`
3. Set default argocd namespace `kubectl config set-context --current --namespace=argocd`
4. Expose argocd service `kubectl port-forward svc/argocd-server -n argocd 8080:443`
5. Get the initial password `kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath={.data.password} | base64 -d`
6. Login at [localhost:8080](localhost:8080)

### Run

## Repo structure

There are a few different folders in this repo, below is an explainer on all of them

### cluster

This folder is used to contain all of the manifest files I want argocd to manage.

### config

This folder will contain configuration files and files not ment for argocd to manage

## Referneces

[ArgoCD Docs](https://argo-cd.readthedocs.io/en/stable/getting_started/)
[Nginx Ingress Controller](https://kubernetes.github.io/ingress-nginx/deploy/)
[Minikube ingress](https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/)
