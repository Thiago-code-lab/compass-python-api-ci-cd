<div align="center">

![Banner](https://github.com/user-attachments/assets/bc251934-6e76-47f8-99ef-af6788691611)

# 🚀 Pipeline CI/CD com GitHub Actions, ArgoCD e Kubernetes

[![GitHub Actions](https://img.shields.io/badge/CI-GitHub%20Actions-2088FF?logo=githubactions&logoColor=white)](https://github.com/features/actions)
[![ArgoCD](https://img.shields.io/badge/CD-ArgoCD-EF7B4D?logo=argo&logoColor=white)](https://argo-cd.readthedocs.io/)
[![Kubernetes](https://img.shields.io/badge/K8s-1.28+-326CE5?logo=kubernetes&logoColor=white)](https://kubernetes.io/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104+-009688?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![Docker](https://img.shields.io/badge/Docker-Hub-2496ED?logo=docker&logoColor=white)](https://hub.docker.com/)

**Implementação completa de pipeline CI/CD automatizado utilizando GitOps para uma aplicação FastAPI**

[Sobre](#-sobre-o-projeto) • [Arquitetura](#-arquitetura) • [Tecnologias](#-tecnologias) • [Demonstração](#-demonstração) • [Como Usar](#-como-usar)

</div>

---

## 📋 Sobre o Projeto

Este projeto foi desenvolvido como parte do **Programa de Bolsas - DevSecOps da Compass UOL** e demonstra a implementação completa de um pipeline CI/CD moderno, automatizando todo o ciclo de vida de uma aplicação desde o desenvolvimento até o deploy em produção.

### 🎯 Objetivos

- ✅ Automatizar o processo de **build**, **teste** e **deploy** de aplicações
- ✅ Implementar práticas de **GitOps** com ArgoCD
- ✅ Utilizar **GitHub Actions** para integração contínua
- ✅ Gerenciar deployments em **Kubernetes** de forma declarativa
- ✅ Separar responsabilidades entre código da aplicação e manifests de infraestrutura

### 🌟 Diferenciais

- **Totalmente Automatizado**: Um simples `git push` dispara todo o pipeline
- **GitOps**: O repositório Git é a única fonte de verdade
- **Rastreabilidade**: Cada deploy é versionado e rastreável
- **Rollback Simplificado**: Reverter para versões anteriores é trivial

---

## 🏗️ Arquitetura

### Fluxo do Pipeline

```mermaid
graph TD
    subgraph "👨‍💻 Desenvolvedor"
        A[Desenvolvedor] -->|1. git push| B(📦 Repositório da Aplicação<br/>compass-python-api-ci-cd)
    end

    subgraph "🔄 CI: GitHub Actions"
        B -->|2. Trigger Workflow| C(🤖 GitHub Actions)
        C -->|3. Build & Test| D(🐳 Docker Build)
        D -->|4. Push Image| E(📚 Docker Hub<br/>compass-python-api:SHA)
        C -->|5. Update Manifest| F(📦 Repositório de Manifestos<br/>compass-kubernetes-deployments)
    end

    subgraph "🚀 CD: GitOps com ArgoCD"
        F -->|6. Detecta Mudança| G(🚢 ArgoCD)
        G -->|7. Sync & Deploy| H(☸️ Cluster Kubernetes<br/>Rancher Desktop)
        H -->|8. Pull Image| E
    end

    style B fill:#22272E,stroke:#58A6FF,stroke-width:2px,color:#fff
    style F fill:#22272E,stroke:#58A6FF,stroke-width:2px,color:#fff
    style C fill:#2088FF,stroke:#fff,stroke-width:2px,color:#fff
    style G fill:#EF7B4D,stroke:#fff,stroke-width:2px,color:#fff
    style H fill:#326CE5,stroke:#fff,stroke-width:2px,color:#fff
    style E fill:#2496ED,stroke:#fff,stroke-width:2px,color:#fff
```

### Componentes Principais

| Componente | Função | Responsabilidade |
|------------|--------|------------------|
| **GitHub Actions** | CI Pipeline | Build, test e push da imagem Docker |
| **Docker Hub** | Registry | Armazenamento de imagens containerizadas |
| **ArgoCD** | CD Engine | Sincronização GitOps e deploy no K8s |
| **Kubernetes** | Orchestrator | Execução e gerenciamento dos containers |
| **Git Repositories** | Source of Truth | Versionamento de código e manifestos |

---

## 🛠️ Tecnologias Utilizadas

<table>
<tr>
<td align="center" width="33%">

### Integração Contínua
**GitHub Actions**
- Workflows automatizados
- Matrix builds
- Secret management
- Triggers configuráveis

</td>
<td align="center" width="33%">

### Containerização
**Docker & Docker Hub**
- Multi-stage builds
- Image optimization
- Tag versionamento (SHA)
- Registry público/privado

</td>
<td align="center" width="33%">

### Orquestração
**Kubernetes**
- Deployments
- Services (ClusterIP)
- Health checks
- Resource limits

</td>
</tr>
<tr>
<td align="center" width="33%">

### GitOps
**ArgoCD**
- Continuous Delivery
- Auto-sync
- Rollback automático
- UI declarativa

</td>
<td align="center" width="33%">

### Aplicação
**FastAPI**
- API REST moderna
- Auto-documentação
- Alta performance
- Type hints (Python)

</td>
<td align="center" width="33%">

### Desenvolvimento Local
**Rancher Desktop**
- Kubernetes local
- Docker runtime
- K3s distribution
- Easy setup

</td>
</tr>
</table>

---

## 📁 Estrutura dos Repositórios

Este projeto segue a prática de **separação de responsabilidades** com dois repositórios distintos:

### 1️⃣ Repositório da Aplicação
**`compass-python-api-ci-cd`** - Código fonte e CI

```
compass-python-api-ci-cd/
├── .github/
│   └── workflows/
│       └── main.yml          # 🎯 Pipeline CI/CD
├── .gitignore
├── Dockerfile                # 🐳 Containerização
├── main.py                   # 🚀 Aplicação FastAPI
├── requirements.txt          # 📦 Dependências Python
└── README.md
```

**Responsabilidades:**
- Código da aplicação
- Testes unitários
- Build da imagem Docker
- Atualização automática dos manifestos

### 2️⃣ Repositório de Manifestos
**`compass-kubernetes-deployments`** - Infraestrutura como Código (IaC)

```
compass-kubernetes-deployments/
├── deployment.yaml           # 🎯 Definição dos Pods
├── service.yaml              # 🌐 Exposição da aplicação
└── README.md
```

**Responsabilidades:**
- Manifestos Kubernetes
- Configuração de recursos
- Fonte de verdade para o ArgoCD
- Versionamento da infraestrutura

---

## 🚦 Pré-requisitos

Antes de começar, certifique-se de ter as seguintes ferramentas instaladas:

### Essenciais

- [x] **Git** (v2.30+) - [Instalar](https://git-scm.com/downloads)
- [x] **Python** (v3.9+) - [Instalar](https://www.python.org/downloads/)
- [x] **Docker** - [Instalar](https://docs.docker.com/get-docker/)
- [x] **kubectl** - [Instalar](https://kubernetes.io/docs/tasks/tools/)
- [x] **Rancher Desktop** - [Instalar](https://rancherdesktop.io/)

### Contas Necessárias

- [x] **GitHub Account** - Com 2 repositórios públicos
- [x] **Docker Hub Account** - Com Personal Access Token configurado
<img width="1904" height="942" alt="Image" src="https://github.com/user-attachments/assets/b8a4af4c-f6d4-4892-9c5c-36ca9d217442" />
<img width="1876" height="958" alt="Image" src="https://github.com/user-attachments/assets/76472fe1-267d-47ad-a981-670f9792053a" />
<img width="1906" height="944" alt="Image" src="https://github.com/user-attachments/assets/1a41041e-b5ec-4a14-abdd-82bd29508d46" />

### Instalação do ArgoCD

```bash
# Criar namespace
kubectl create namespace argocd

# Instalar ArgoCD
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Aguardar todos os pods ficarem prontos
kubectl wait --for=condition=Ready pods --all -n argocd --timeout=300s
```

---

## 🚀 Como Usar

### 📥 Passo 1: Clone os Repositórios

```bash
# Clone o repositório da aplicação
git clone https://github.com/seu-usuario/compass-python-api-ci-cd.git
cd compass-python-api-ci-cd

# Clone o repositório de manifestos
git clone https://github.com/seu-usuario/compass-kubernetes-deployments.git
```

### 🔐 Passo 2: Configure os Secrets no GitHub

Acesse: **Repositório → Settings → Secrets and variables → Actions**

Adicione os seguintes secrets:

| Secret | Descrição | Como Obter |
|--------|-----------|------------|
| `DOCKER_USERNAME` | Seu usuário do Docker Hub | Seu username do Docker Hub |
| `DOCKER_PASSWORD` | Token de acesso do Docker Hub | Account Settings → Security → New Access Token |
| `SSH_PRIVATE_KEY` | Chave SSH para atualizar manifestos | `ssh-keygen -t ed25519 -C "github-actions"` |
<img width="1901" height="936" alt="Image" src="https://github.com/user-attachments/assets/635b7b20-56d7-4e3b-8e02-f9347d45fc8f" />
<img width="1906" height="930" alt="Image" src="https://github.com/user-attachments/assets/efa7f376-ee57-4454-9409-f3a15c7fb356" />
<img width="1160" height="314" alt="Image" src="https://github.com/user-attachments/assets/337dd45b-3ed4-44b1-966c-5e620ef29c66" />
<img width="1585" height="764" alt="Image" src="https://github.com/user-attachments/assets/067fbc1b-334e-424c-83ad-49404b415208" />


### ⚙️ Passo 3: Configure o Workflow

O arquivo `.github/workflows/main.yml` já está pronto! Ele faz:

1. ✅ Login no Docker Hub
2. ✅ Build da imagem com tag SHA do commit
3. ✅ Push da imagem para o Docker Hub
4. ✅ Checkout do repositório de manifestos
5. ✅ Atualização do `deployment.yaml` com a nova tag
6. ✅ Commit e push automático das mudanças

### 🎯 Passo 4: Configure o ArgoCD

```bash
# Acesse a UI do ArgoCD
kubectl port-forward svc/argocd-server -n argocd 8081:443

# Obtenha a senha inicial (usuário: admin)
kubectl -n argocd get secret argocd-initial-admin-secret \
  -o jsonpath="{.data.password}" | base64 -d; echo
```

Acesse: `https://localhost:8081`

**Crie uma nova aplicação:**

- **Application Name:** `hello-app`
- **Project:** `default`
- **Sync Policy:** `Automatic`
- **Repository URL:** `https://github.com/seu-usuario/compass-kubernetes-deployments`
- **Path:** `.`
- **Cluster:** `https://kubernetes.default.svc`
- **Namespace:** `default`

### 🧪 Passo 5: Teste o Pipeline

```bash
# Edite a aplicação
echo 'return {"message": "Hello GitOps!"}' > main.py

# Commit e push
git add .
git commit -m "Update message to GitOps"
git push origin main

# Acompanhe o workflow
# GitHub → Actions → Veja o workflow executando

# Verifique o ArgoCD sincronizando
# ArgoCD UI → hello-app → Veja o status

# Acesse a aplicação
kubectl port-forward svc/hello-app-service 8080:80
curl http://localhost:8080
```

---

## 📊 Demonstração (Entregáveis)

### ✅ Evidência 1: Workflow GitHub Actions (Sucesso)

O `git push` no `main.py` acionou o workflow, que executou com sucesso todas as etapas.

<!-- COLE AQUI A IMAGEM DA TELA DE "ACTIONS" NO GITHUB MOSTRANDO O ✅ VERDE -->
<img width="938" height="784" alt="Image" src="https://github.com/user-attachments/assets/bea06f63-a19f-458b-8afe-e0c05199e49e" />
<img width="1390" height="849" alt="Image" src="https://github.com/user-attachments/assets/2cb2410f-3f6d-4226-a86c-60f02621ad5c" />

**Etapas executadas:**
- ✅ Checkout do código
- ✅ Login no Docker Hub
- ✅ Build da imagem Docker
- ✅ Push para Docker Hub com tag SHA
- ✅ Atualização do manifest no repositório de deployments

---

### ✅ Evidência 2: Imagem no Docker Hub

A imagem `compass-python-api` foi enviada ao Docker Hub com a tag correspondente ao SHA do commit.

<!-- COLE AQUI A IMAGEM DA SUA PÁGINA DO DOCKER HUB MOSTRANDO A NOVA TAG -->
<img width="1876" height="797" alt="Image" src="https://github.com/user-attachments/assets/ab61bffa-cc21-4e0b-aee6-46e02918f046" />

**Detalhes da imagem:**
- **Repository:** `seu-usuario/compass-python-api`
- **Tag:** `d6c7d3b` (SHA do commit)
- **Size:** ~50MB (otimizada)
- **Última atualização:** Timestamp do push

---

### ✅ Evidência 3: Commit Automático nos Manifestos

O GitHub Actions realizou um commit automático no repositório `compass-kubernetes-deployments`, atualizando a tag da imagem no `deployment.yaml`.

<!-- COLE AQUI A IMAGEM DO HISTÓRICO DE COMMITS DO compass-kubernetes-deployments -->
<img width="1037" height="482" alt="Image" src="https://github.com/user-attachments/assets/ad57b77d-09c2-400b-b0ab-ac5b2dad89ab" />

**Commit realizado por:** `github-actions[bot]`
**Mensagem:** `Update image tag to d6c7d3b`

---

### ✅ Evidência 4: Sincronização no ArgoCD

O ArgoCD detectou automaticamente a mudança no repositório de manifestos e sincronizou o cluster.

<!-- COLE AQUI A IMAGEM DA INTERFACE DO ARGOCD MOSTRANDO O APP -->
<img width="1142" height="541" alt="Image" src="https://github.com/user-attachments/assets/658f6468-693e-4255-9e5c-dcd00d2af74c" />
<img width="968" height="354" alt="Image" src="https://github.com/user-attachments/assets/e481d249-1e7a-48f7-89a8-e52e9fbd6dc9" />
<img width="1134" height="461" alt="Image" src="https://github.com/user-attachments/assets/880c5d8d-e166-4a7d-a70b-270ed0a62ad1" />
<img width="938" height="641" alt="Image" src="https://github.com/user-attachments/assets/7cff695a-e7af-4c81-b676-f8260896d328" />
<img width="927" height="606" alt="Image" src="https://github.com/user-attachments/assets/80cab352-17f0-4233-bb52-ea40d3b75fd4" />
<img width="915" height="771" alt="Image" src="https://github.com/user-attachments/assets/a2150cc3-15a9-4d05-a3a7-9ad02a0f65af" />
<img width="1354" height="860" alt="Image" src="https://github.com/user-attachments/assets/5a5bc511-0102-432a-a0fd-5e2d4a07b02e" />
<img width="1795" height="993" alt="Image" src="https://github.com/user-attachments/assets/ea50e19f-74e9-4969-b580-04f0f0266869" />


**Status da aplicação:**
- 🟢 **Health:** Healthy
- 🔄 **Sync:** Synced
- 📊 **Resources:** 1 Deployment, 1 Service, 1 Pod

---

### ✅ Evidência 5: Pods em Execução no Kubernetes

O comando `kubectl get pods` mostra o novo pod da aplicação em estado `Running`.

<!-- COLE AQUI A IMAGEM DO TERMINAL COM kubectl get pods -->
<img width="870" height="471" alt="Image" src="https://github.com/user-attachments/assets/609d63d4-2ad1-406c-89dd-87393fd8b829" />

```bash
NAME                         READY   STATUS    RESTARTS   AGE
hello-app-xxxxxxxxx-xxxxx    1/1     Running   0          68m
```

---

### ✅ Evidência 6: Aplicação Funcionando (Teste Final)

Após executar `kubectl port-forward svc/hello-app-service 8080:80`, a aplicação responde corretamente no navegador.

<!-- COLE AQUI A IMAGEM DO NAVEGADOR EM localhost:8080 -->
<img width="876" height="421" alt="Image" src="https://github.com/user-attachments/assets/e70eceb6-63fc-4375-b77d-5ac0443c2427" />
<img width="1006" height="675" alt="Image" src="https://github.com/user-attachments/assets/93364a7d-21c4-40ea-b829-7fc7bf3b72f3" />
**Response:**
```json
{
  "message": "Hello GitOps! Acionando o pipeline corrigido!"
}
```

---

## 🔧 Comandos Úteis

### Kubernetes

```bash
# Verificar status do cluster
kubectl cluster-info
kubectl get nodes

# Gerenciar recursos
kubectl get all -n default
kubectl get pods -w  # watch mode
kubectl describe pod <pod-name>
kubectl logs <pod-name> -f  # follow logs

# Acessar a aplicação
kubectl port-forward svc/hello-app-service 8080:80

# Debug
kubectl exec -it <pod-name> -- /bin/sh
kubectl get events --sort-by=.metadata.creationTimestamp
```

### ArgoCD

```bash
# Acessar UI
kubectl port-forward svc/argocd-server -n argocd 8081:443

# CLI do ArgoCD
argocd app list
argocd app get hello-app
argocd app sync hello-app
argocd app history hello-app

# Obter senha
kubectl -n argocd get secret argocd-initial-admin-secret \
  -o jsonpath="{.data.password}" | base64 -d
```

### Docker

```bash
# Build local
docker build -t compass-python-api:local .

# Run local
docker run -p 8080:80 compass-python-api:local

# Verificar imagens
docker images | grep compass-python-api

# Limpar imagens antigas
docker image prune -a
```

---

## 🐛 Troubleshooting

### Problema: Falha no Login do Docker Hub

**Erro:** `Error: unauthorized: incorrect username or password`

**Causa:** Token do Docker Hub expirado ou incorreto

**Solução:**
1. Acesse Docker Hub → Account Settings → Security
2. Gere um novo **Personal Access Token** (permissões: Read, Write, Delete)
3. Atualize o secret `DOCKER_PASSWORD` no GitHub
4. Execute novamente o workflow

---

### Problema: Falha no Push Git

**Erro:** `! [rejected] main -> main (non-fast-forward)`

**Causa:** Repositório local desatualizado em relação ao remoto

**Solução:**
```bash
# Atualizar repositório local
git pull origin main --rebase

# Tentar push novamente
git push origin main
```

---

### Problema: ArgoCD não sincroniza

**Erro:** Status "OutOfSync" permanece

**Causa:** Configuração incorreta do repositório ou permissões

**Solução:**
1. Verifique a URL do repositório no ArgoCD
2. Confirme que o repositório é público ou adicione credenciais
3. Force uma sincronização manual:
```bash
argocd app sync hello-app --force
```

---

### Problema: Pod não inicia

**Erro:** `ImagePullBackOff` ou `CrashLoopBackOff`

**Solução:**
```bash
# Verificar logs detalhados
kubectl describe pod <pod-name>
kubectl logs <pod-name> --previous

# Verificar se a imagem existe no Docker Hub
# Verificar se o deployment.yaml tem a tag correta
kubectl get deployment hello-app -o yaml | grep image:
```

---

## 📚 Recursos Adicionais

### Documentação Oficial

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [ArgoCD Documentation](https://argo-cd.readthedocs.io/)
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [Docker Documentation](https://docs.docker.com/)

### Artigos e Tutoriais

- [GitOps Best Practices](https://www.gitops.tech/)
- [CI/CD Pipeline Design Patterns](https://martinfowler.com/articles/continuousIntegration.html)
- [Kubernetes Production Best Practices](https://kubernetes.io/docs/setup/best-practices/)

---

## 🤝 Contribuindo

Contribuições são bem-vindas! Sinta-se à vontade para:

1. 🍴 Fazer um fork do projeto
2. 🔀 Criar uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. ✅ Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. 📤 Push para a branch (`git push origin feature/AmazingFeature`)
5. 🎉 Abrir um Pull Request

---

## 👨‍💻 Autor

**Thiago Cardoso Davi**

- 📧 Email: analyticsdev.thiago@gmail.com
- 💼 LinkedIn: www.linkedin.com/in/analyticsthiagocardoso
- 🐙 GitHub: https://github.com/Thiago-code-lab

> Desenvolvido como parte do **Programa de Bolsas DevSecOps - Compass UOL** 🧭

---

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

---

## ⭐ Agradecimentos

- **Compass UOL** pelo programa de bolsas e oportunidade de aprendizado
- Comunidade **Cloud Native** pelas ferramentas open-source incríveis
- Todos os contribuidores que ajudaram a melhorar este projeto

---

<div align="center">

**Se este projeto foi útil para você, considere dar uma ⭐!**

Feito com ❤️ e ☕ por [Thiago Cardoso Davi](https://github.com/seu-usuario)

</div>
