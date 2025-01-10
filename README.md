# Laboratório ArgoCD

#### Pré-requisitos:
- [kubectl](https://kubernetes.io/pt-br/docs/tasks/tools/)
- [minikube](https://minikube.sigs.k8s.io/docs/start/)

```bash
minikube start
```

```bash
minikube addons enable metallb
```

```bash
minikube addons configure metallb
```

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

```bash
kubectl -n argocd get all
```

```bash
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```

