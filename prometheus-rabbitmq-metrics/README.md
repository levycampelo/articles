## Monitorar as metricas do RabbitMQ com prometheus

Neste artigo, vou demonstrar como monitorar um cluster RabbitMQ via Prometheus utilizando o plugin nativo.<br>
Nesse ambiente, usamos a seguinte versão:

> **Sistema Operacional:** Oracle Linux 8 <br>
> **RabbitMQ:** 3.12.2 <br>
> **Prometheus:** 2.46.0

## Introdução:
Em um dos novos ambientes que estamos implantando, temos uma infraestrutura operando com três servidores RabbitMQ para gerenciar toda a mensageria até chegar ao nosso cluster de ACS. Devido a isso, temos a necessidade de monitorar as filas com mais facilidade. Por isso, adotamos o plugin do Prometheus no RabbitMQ.

### Habilitar o plugin RabbitMQ Prometheus: 
```bash
# rabbitmq-plugins enable rabbitmq_prometheus
```

### Ajustar as metrics no arquivo rabbitmq.config:
```bash
[
  {rabbit, [
    {vm_memory_high_watermark_relative, 0.7},
    {disk_free_limit, "20GB"}
  ]},
  {rabbitmq_prometheus, [
    {return_per_object_metrics, true},
    {return_detailed_metrics, true}
  ]}
].
```

### Reiniciar o serviço:
```bash
systemctl restart rabbitmq-server
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
![rabbitmq](/prometheus-rabbitmq-metrics/images/rabbitmq-01.jpeg)
![rabbitmq2](/prometheus-rabbitmq-metrics/images/rabbitmq-02.jpeg)
