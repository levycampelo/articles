## Montar uma imagem ISO e ajustar repositório YUM

Neste artigo, vou demonstrar como montar uma ISO e ajustar o repo YUM.<br>
Nesse ambiente, usamos a seguinte versão:

> **Sistema Operacional:** Red Hat Enterprise Linux 8.8<br>
> **Imagem:** rhel-8.8-x86_64.iso

## Introdução:
Em um dos ambientes que operamos, um dos servidores não possui acesso externo e precisamos instalar um pacote que depende de algumas bibliotecas. Para isso,utilizamos a imagem ISO como fonte local para a instalação dos pacotes via YUM, eliminando a necessidade de acessar a internet.

## Comandos:
```bash
$ scp levy@192.168.250.60:/tmp/rhel-8.8-x86_64.iso .
```
```bash
$ mv rhel-8.8-x86_64.iso /opt
$ cd /opt
$ mkdir RHEL
$ mount -o loop,ro /opt/rhel-8.8-x86_64-dvd.iso /opt/RHEL
```
```bash
$ vi /etc/yum.repos.d/rhel8.repo
```
```bash
$ vi /etc/yum.repos.d/rhel8.repo
[dvd-BaseOS]
name=DVD for RHEL - BaseOS
baseurl=file:///opt/RHEL/BaseOS
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

[dvd-AppStream]
name=DVD for RHEL - AppStream
baseurl=file:///opt/RHEL/AppStream
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
```
