## Trocar o certificado do cluster OpenShift

Neste artigo, vou demonstrar como trocar o certificado do cluster Openshift.
Nesse ambiente, usamos as seguintes versões:

**Cluster Openshift:** v4.12.49

## Introdução:

No Cluster de OpenShift, o certificado é um arquivo que contém informações criptográficas que usamos para estabelecer e garantir a comunicação segura entre os componentes do cluster e com os clientes externos.

No comando abaixo, vamos criar uma nova secret no openshift contendo o novo certificado gerado, que inclui o certificado e a chave privada.

```bash 
oc create secret tls custom-certs-default-2024 --cert=/openshift/certs/2024/STAR.apps.meudominio.com.br.crt --key=/openshift/certs/2024/apps.meudominio.com.br.key -n openshift-ingress```

Neste comando, vamos configurar o controlador de Ingress para utilizar o novo segredo criado anteriormente.
```bash
oc patch ingresscontroller.operator default --type=merge -p '{"spec":{"defaultCertificate": {"name": "custom-certs-default-2024"}}}' -n openshift-ingress-operator```

Após a alteração do controlador de Ingress, todos os pods no namespace openshift-ingress serão reiniciados.
```bash
oc get pods -n openshift-ingress```

Caso isso não ocorra, os pods podem ser excluídos manualmente.
```bash 
oc delete pods --all -n openshift-ingress```

Criar um ConfigMap (um objeto que armazena pares chave-valor) que aponta para o novo certificado (.crt).
```bash
oc create configmap custom-ca-2024 --from-file=ca-bundle.crt=/openshift/certs/2024/STAR.apps.meudominio.com.br.crt -n openshift-config```

Esse comando atualiza a configuração do certificado no OpenShift, adicionando o certificado novo.
```
bash
oc patch proxy/cluster --type=merge --patch='{"spec":{"trustedCA":{"name":"custom-ca-2024"}}}'```
