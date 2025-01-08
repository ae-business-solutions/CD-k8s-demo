# K8s Demos

## ArgoCD Install

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

## Demo

1. Start local cluster `minikube start`
2. Set default argocd namespace `kubectl config set-context --current --namespace=argocd`
3. Expose argocd service `kubectl port-forward svc/argocd-server -n argocd 8080:443`
4. Get the initial password `kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath={.data.password} | base64 -d`
5. Login at [localhost:8080](localhost:8080)

## Repo structure

There are a few different folders in this repo, below is an explainer on all of them

### cluster

This folder is used to contain all of the manifest files I want argocd to manage.

### config

This folder will contain configuration files and files not ment for argocd to manage

## Referneces

[ArgoCD Docs](https://argo-cd.readthedocs.io/en/stable/getting_started/)
