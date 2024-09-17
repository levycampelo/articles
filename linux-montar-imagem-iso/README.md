## Montar uma imagem ISO e ajustar repositório YUM

Neste artigo, vou demonstrar como montar uma ISO e ajustar o repo YUM.
Nesse ambiente, usamos a seguinte versão:

> **Sistema Operacional:** Red Hat Enterprise Linux 8.8

## Introdução:
Em um dos ambientes que operamos, um dos servidores não possui acesso externo e precisamos instalar um pacote que depende de algumas bibliotecas. Para isso,utilizamos a imagem ISO como fonte local para a instalação dos pacotes via YUM, eliminando a necessidade de acessar a internet.

## Comandos:

cd /opt
ls -la
mkdir RHEL
mount -o loop,ro /opt/rhel-8.8-x86_64-dvd.iso /opt/RHEL
vi /etc/yum.repos.d/rhel8.repo

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
