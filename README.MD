# Projeto Fullstack Kubernetes (K8s) - IFPB

Este projeto consiste em uma aplicação fullstack (Frontend React, Backend Flask e Banco de Dados PostgreSQL) conteinerizada e orquestrada via Kubernetes. A arquitetura foi desenhada para garantir alta disponibilidade, persistência de dados e roteamento inteligente de tráfego.

## 🏗️ Arquitetura do Cluster

A aplicação está dividida em dois namespaces principais para isolamento de recursos:

* **Namespace `app`**: Contém o Frontend (Vite/React) e o Backend (Flask API).
* **Namespace `database`**: Contém o Banco de Dados PostgreSQL gerenciado por um StatefulSet.

## 🚀 Tecnologias Utilizadas

* **Frontend**: React + Vite
* **Backend**: Python (Flask) + SQLAlchemy + Psycopg2
* **Banco de Dados**: PostgreSQL 15-alpine
* **Infraestrutura**: Kubernetes (Namespaces, Deployments, StatefulSets, Services, PVC, Secrets, Ingress)

## 🔧 Como Rodar o Projeto

### Pré-requisitos

* Cluster Kubernetes (Kind, Minikube ou Docker Desktop)
* Ingress Nginx Controller instalado no cluster

### 1. Clonar o repositório

```bash
git clone https://github.com/0xEg0x/lucas-k8s-deploy.git
cd lucas-k8s-deploy.git
```

### 2. Aplicar as configurações no Kubernetes

Siga a ordem de execução para garantir que as dependências (namespaces e segredos) subam primeiro:

```bash
# Criar Namespaces
kubectl apply -f namespace.yaml

# Configurar Banco de Dados (Namespace: database)
kubectl apply -f database/

# Configurar Backend (Namespace: app)
kubectl apply -f backend/

# Configurar Frontend (Namespace: app)
kubectl apply -f frontend/deployment.yaml

# Configurar Roteamento (Ingress)
kubectl apply -f ingress/ingress.yaml
```

### 3. Acessar a Aplicação

Se estiver usando Kind, utilize o port-forward para o Ingress Controller:

```bash
kubectl port-forward -n ingress-nginx service/ingress-nginx-controller 8080:80
```

Acesse no navegador: `http://localhost:8080`

## 📊 Recursos Implementados (Checklist de Avaliação)

* [x] **Persistência**: Uso de `PersistentVolumeClaim` para o banco de dados
* [x] **Escalabilidade**: Deployments com 2 réplicas para Frontend e Backend
* [x] **Segurança**: Uso de `Secrets` para credenciais sensíveis de banco
* [x] **Roteamento**: Ingress configurado com caminhos `/api` (backend) e `/` (frontend)
* [x] **Saúde**: Rota de `/health` no backend para monitoramento

---

## 📞 Contato

**Lucas** - [@0xEg0x](https://github.com/0xEg0x)

**Link do Projeto:** [https://github.com/0xEg0x/lucas-k8s-deploy.git](https://github.com/0xEg0x/lucas-k8s-deploy.git)

---

<div align="center">

**⭐ Se este projeto foi útil, considere dar uma estrela!**

Made with ❤️ and ☕ by Lucas

</div>
