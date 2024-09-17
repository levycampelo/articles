## Aumentar recursos do cluster OpenShift

Neste artigo, vou demonstrar como aumentar recursos de CPU e\ou memória dos nodes do cluster Openshift.
Nesse ambiente, usamos a seguinte versão:

> **Cluster Openshift:** v4.12.49

## Introdução:

No Cluster de OpenShift, um redimensionamento de memória ou CPU em um node do cluster OpenShift pode ser necessário em várias situações, dependendo da carga de trabalho e das necessidades do cluster.

- Verificar a utilização dos recursos:
```bash
oc adm top node
```

- Após identificar o node que precisa do resize, validar o node:
```bash
oc get nodes 
```

- Agora, vamos remover o primeiro nó, no qual iremos alterar os recursos:
```bash
oc adm drain <nome-node> --delete-emptydir-data --ignore-daemonsets
```
* Se o cluster não conseguir realizar o drain no node, adicione `--force` ao final do comando.

> **Observação:** O comando de drain pode varias de acordo com a versão do OCP.

- Observe no comando abaixo quando o status do nó mudar para `SchedulingDisabled`:
```bash
oc get nodes
...
NAME                STATUS                   ROLES  AGE  VERSION 
xpto-w6xpo-master-1 Ready,SchedulingDisabled master 260d v1.24.6+deccab3
...
```

- Resize dos recursos:

No meu caso esse cluster de OpenShift está em uma infraestrutura de VMware com vCenter, executei o seguinte procedimento:

[1]: Identifiquei o node e desligamos o servidor. (power-off).

[2]: Adicionei o recurso de CPU de 4vCPU para 8vCPU.

[3]: Adicionei o recurso de memória de 16GiB para 32GiB.

[4]: Ligamos o servidor. (power-on).

