## Monitorar as metricas do RabbitMQ com prometheus

Neste artigo, vou demonstrar como montar uma ISO e ajustar o repo YUM.<br>
Nesse ambiente, usamos a seguinte versão:

> **Sistema Operacional:** Oracle Linux 8 <br>
> **RabbitMQ:** 3.12.2 <br>
> **Prometheus:** 2.46.0

## Introdução:
Em um dos ambientes que operamos, um dos servidores não possui acesso externo(internet) e precisamos instalar um pacote que depende de algumas bibliotecas. Para isso, utilizamos a imagem ISO como fonte local para a instalação dos pacotes via YUM, eliminando a necessidade de acessar a internet.

### Habilite o plugin RabbitMQ Prometheus: 
```bash
# rabbitmq-plugins enable rabbitmq_prometheus
```

### Visualizar metrics:
```bash
http://192.168.250.12:15692/metrics
```

### Adicionar ao prometheus:
```bash
- job_name: 'rabbitmq-metrics'
    # metrics plugin
    metrics_path: /metrics
    scrape_interval: 5s
    static_configs:
      - targets: ["192.168.250.12:15692","192.168.250.113:15692","192.168.250.115:15692"]
```
![rabbitmq](/prometheus-rabbitmq-metrics/images/rabbitmq.png)
