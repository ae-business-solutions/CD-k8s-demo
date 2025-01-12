# K8s Demos

## Demo

This demo will show how to use argocd to manage manifests in a kubernetes cluster

### Setup

1. Start the minikube cluster `minikube start --addons=ingress`
2. Deploy argocd `kubectl apply -f cluster/argocd/argocd.yaml -n argocd`
3. Get argocd password `kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath={.data.password} | base64 -d`
4. Port forward argo to login from website `kubectl port-forward svc/argocd-server -n argocd 8080:443`
5. Login with password from before
6. Apply secrets from local files `kubectl apply -f cluster/cert-manager/cloudflare-token.unc.yaml` and `kubectl apply -f cluster/tunnel/cloudflare-tunnel-token.unc.yaml`
7. Edit local windows hostfile at `C:\Windows\System32\drivers\etc` for local DNS

### ArgoCD setup

1. Apply the default apps for cert-manager and demo app `kubectl apply -f config/`
2. Explore dashboard

### Cert manager

1. Look at issuers `kubectl get issuer`
2. Look at certificate secrets `kubectl get secrets`
3. Look at website deployed locally `curl --insecure --resolve "demo-work.buddylgreen.com:443:$( minikube ip )" -vvi https://demo-work.buddylgreen.com`
4. Switch issuer from stage to prod via code change and argocd sync

### Cloudflared Tunnel

1. Should have been already deployed with config apps
2. Edit local DNS to turn off resolving
3. Goto [Cloudflare Dashboard](https://dash.cloudflare.com) to edit cloudflare DNS records
4. Might need to goto zero trust to check on tunnel

> [!NOTE]  
> Cloudflared issues its own certificate and cert-manager is not needed


## Debugging
```
kubectl run ubuntu --image=ubuntu:latest --command sleep 604800
kubectl exec -it pods/ubuntu -- sh
apt update && apt install curl dnsutils

kubectl rollout restart deployment/nginx
```

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
