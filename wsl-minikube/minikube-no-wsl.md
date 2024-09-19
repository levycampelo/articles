---
title: "Minikube no WSL"
date: 2024-08-04T09:20:05-03:00
draft: true
authors:
  - levy
tags:
  - k8s 
---
Eu vou começar os estudos no Kubernetes e o melhor cenário é testando na prática. Com isso vamos instalar o minikube no nosso WSL do Windows para poder ter o single-node do K8S para os nossos testes.

Vamos iniciar, já pensando que você todos já possuim o WSL instalado com o Ubuntu, caso não tenha eu vou fazer um outro posts com a instalação.

### 1º Iniciar o WSL e ajustar o systemd:
```
vi /etc/wsl.conf
[boot]
systemd=true
```

### 2º Reiniciar o WSL:
```
wsl --shutdown
wsl
```

### 3º Vamos atualizar o ambiente:
```
apt update && sudo apt upgrade -y
```

### 4º Instalar alguns pacotes essenciais e docker:
```
    apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
### 5º Adicionar repositorio:
```
add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```
### 6º Agora vamos rodar um update e instalar o docker:
```
apt-get update -y
apt-get install -y docker-ce
```
### 7º Adicionar o novo usuario do docker:
```
usermod -aG docker $USER && newgrp docker
```
### Nessa etapa vamos iniciar a instalação do Minikube:

1º Download do Minikube:
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```
2º Torna um executavel: 
```
chmod +x ./minikube
```
3º Mover para path de executaveis:
```
mv ./minikube /usr/local/bin/
```

4º Ajustar o driver do app do container:
```
minikube config set driver docker
```

### Instalar o Kubectl:
1º Download do Kubectl
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```
2º Torna um executavel:
```
chmod +x ./kubectl
```
3º Mover para path de executaveis:
```
mv ./kubectl /usr/local/bin/
```

### Iniciar o minikube:
```
minikube start
```
Caso ocorra algum erro de permissões do seu SO, tente executar o minikube com --force:
```
minikube start --force
```
