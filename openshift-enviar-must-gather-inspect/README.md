## RedHat Support Tool

Neste artigo, vou demonstrar como instalar o redhat-support-tool no bastion.
Nesse ambiente, usamos a seguinte versão:

> **Sistema Operacional:** Red Hat Enterprise Linux 7.7 

## Introdução:

Com o suporte do time da Red Hat, é comum solicitar o must-gather (uma ferramenta que coleta dados de diagnóstico) ou o inspect (uma ferramenta que coleta informações detalhadas sobre os recursos e o estado de um namespace) de um namespace específico. Normalmente, um must-gather completo é bem grande, o que dificulta o upload no portal para atualizar o chamado. No entanto, se você tiver uma máquina RHEL licenciada, é possível enviar os arquivos diretamente do seu bastion, facilitando a criação e atualização de chamados.

- Verificar subscription:
```bash
$ subscription-manager repos --list | grep "rhel-*-optional-rpms"
```

- Caso o repo não esteja habilitado, você pode ativa-lo:
```bash
$ subscription-manager repos --enable rhel-*-optional-rpms
```

- Instalar o pacote:
```bash
$ yum install redhat-support-tool
```

- Exemplo para enviar must-gather:
```bash
$ redhat-support-tool addattachment -c <numero-chamado> <nome-do-arquivo>


