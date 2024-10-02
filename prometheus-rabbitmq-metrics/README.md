## Monitorar as metricas do RabbitMQ com prometheus

Neste artigo, vou demonstrar como montar uma ISO e ajustar o repo YUM.<br>
Nesse ambiente, usamos a seguinte versão:

> **Sistema Operacional:** Oracle Linux 8 <br>
> **RabbitMQ:** 3.12.2 <br>
> **Prometheus:** 2.46.0

## Introdução:
Em um dos novos ambientes que estamos deployando, temos uma infraestrutura operando com três servidores RabbitMQ para tratar toda a mensageria até chegar em nosso cluster de ACS. Devido a isso, temos a necessidade de monitorar as filas com mais facilidade. Por isso, adotamos o plugin do Prometheus no RabbitMQ.

### Habilitar o plugin RabbitMQ Prometheus: 
```bash
# rabbitmq-plugins enable rabbitmq_prometheus
```

### Visualizar as metrics localmente:
```bash
http://192.168.250.12:15692/metrics
```

### Adicionar ao prometheus os RabbitMQ:
```bash
- job_name: 'rabbitmq-metrics'
    # metrics plugin
    metrics_path: /metrics
    scrape_interval: 5s
    static_configs:
      - targets: ["192.168.250.12:15692","192.168.250.113:15692","192.168.250.115:15692"]
```
![rabbitmq](/prometheus-rabbitmq-metrics/images/rabbitmq.png)
