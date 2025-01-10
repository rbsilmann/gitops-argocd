# Laboratório ArgoCD 🚀

Este guia ajudará você a configurar um ambiente ArgoCD em um cluster Kubernetes usando Minikube.

---

## ✅ Pré-requisitos

Certifique-se de ter as seguintes ferramentas instaladas em sua máquina:

- [**kubectl**](https://kubernetes.io/pt-br/docs/tasks/tools/) - CLI para interagir com clusters Kubernetes.
- [**minikube**](https://minikube.sigs.k8s.io/docs/start/) - Ferramenta para executar clusters Kubernetes localmente.

---

## 🛠️ Passos para Configuração

### 1️⃣ Inicie o Minikube:
```bash
minikube start
```

### 2️⃣ Habilite e configure o addon MetalLB:
```bash
minikube addons enable metallb
minikube addons configure metallb
```

### 3️⃣ Instale o ArgoCD:
1. Crie o namespace para o ArgoCD:
   ```bash
   kubectl create namespace argocd
   ```

2. Aplique o manifesto de instalação:
   ```bash
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
   ```

3. Verifique os recursos criados:
   ```bash
   kubectl -n argocd get all
   ```

### 4️⃣ Configure o LoadBalancer:
Altere o tipo do serviço `argocd-server` para `LoadBalancer`:
```bash
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

### 5️⃣ Obtenha a senha do administrador:
Recupere a senha inicial do administrador do ArgoCD:
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```

---

## 🎯 Conclusão

Após completar os passos acima, seu ambiente ArgoCD estará configurado e pronto para uso! 🎉

Para acessar o dashboard do ArgoCD, utilize o IP externo do LoadBalancer.