## Infraestrutura como código (IaC)

Neste artigo, vou demonstrar como instalar o terraform no WSL.
Nesse ambiente, usamos a seguinte versão:

> **Sistema Operacinal:** Windows 11 Pro

## Introdução:
IaC é capacidade de gerenciar e (ou) provisionar recursos por meio de código, ao invés de executar processos manuais usando console. As ferramentas de IaC permitem às organizações automatizar e padronizar as configurações de servidores, rede e outros componentes de infraestrutura em cloud ou ambiente on-premises, garantindo consistência, escalabilidade e resiliência. Essa tarefa normalmente é exercida pelo time de DevOps ou SRE, promovendo a eficiência e reduzindoerros operacionais humanos na infraestrutura.

- Terraform:
O Terraform é uma ferramenta desenvolvida pela HashiCorp que permite provisionar infraestrutura como código. O arquivo de configuração é escrito no formato YAML e a ferramenta suporta multi-cloud, ou seja, opera em provedores como AWS, Azure ou Google Cloud. Os profissionais de DevOps agilizam suas rotinas ao criar, alterar e versionar a infraestrutura. 

- OpenTofu:
O OpenTofu é um fork de código aberto do popular Terraform desenvolvido pela HashiCorp. Esta ferramenta foca no uso e a possibilidade de modificação sob licença Apache 2.0. O OpenTofu é uma alternativa para aqueles que preferem ferramenta sem restrições de licença.

## Instalação do Terraform:
### Atualizar os pacotes
```bash
$ apt-get update && sudo apt-get upgrade -y
```
### Instalar dependencias
```bash
$ apt-get install -y gnupg software-properties-common curl
```
### Adicionar o repo
```bash
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
```
### Atualizar os pacotes para incluir o terraform
```bash
$ apt-get update
```
### Instalar o terraform
```bash
$ apt-get install terraform
```
### Validar instalação e versão:
```bash
root@DESKTOP-B6RBPK9:/home/levycampelo# terraform -v
Terraform v1.9.5
on linux_amd64
```
