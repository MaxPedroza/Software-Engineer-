# Aula 5 — Métricas e dashboards (Prometheus/Grafana)

**Duração:** ~25 min · **Módulo 19**

## Objetivo
Instrumentar uma aplicação, coletar métricas com Prometheus e consultá-las com PromQL.

## Teoria
- **Métricas**: números agregados no tempo — baratas e ideais para alertas.
- Tipos: **Counter** (só cresce; use `rate()`), **Gauge** (sobe/desce), **Histogram** (distribuição, para latência e percentis).
- Prometheus faz **pull** (*scrape*) do endpoint `/metrics`. **Labels** adicionam dimensões — evite alta cardinalidade (ex.: `user_id`).
- Métodos: **RED** (Rate, Errors, Duration) para serviços; **USE** (Utilization, Saturation, Errors) para recursos; **Golden Signals** (latência, tráfego, erros, saturação).
- **Grafana** cria dashboards sobre o Prometheus; **Alertmanager** roteia alertas.

## Exemplo
App Python:
```python
from prometheus_client import Counter, Histogram, start_http_server
import random, time

REQS = Counter("http_requests_total", "Requisições", ["metodo", "status"])
LAT = Histogram("http_request_duration_seconds", "Latência", buckets=[.05, .1, .25, .5, 1])

start_http_server(8000)
while True:
    with LAT.time():
        time.sleep(random.random() / 5)
    REQS.labels("GET", random.choice(["200"] * 9 + ["500"])).inc()
```
`prometheus.yml`:
```yaml
global:
  scrape_interval: 15s
rule_files: [alertas.yml]
scrape_configs:
  - job_name: api
    static_configs:
      - targets: ["host.docker.internal:8000"]
```
PromQL:
```promql
sum(rate(http_requests_total[5m]))                                  # tráfego
sum(rate(http_requests_total{status=~"5.."}[5m])) / sum(rate(http_requests_total[5m]))  # erros
histogram_quantile(0.99, sum by (le) (rate(http_request_duration_seconds_bucket[5m])))  # p99
```
Alerta (`alertas.yml`):
```yaml
groups:
  - name: api
    rules:
      - alert: TaxaDeErrosAlta
        expr: sum(rate(http_requests_total{status=~"5.."}[5m])) / sum(rate(http_requests_total[5m])) > 0.05
        for: 10m
        labels: { severity: page }
        annotations: { summary: "Mais de 5% de erros 5xx" }
```

## Exercício
1. Suba Prometheus e Grafana via Compose, e monte um painel RED com as 3 consultas acima.
2. Por que usar `user_id` como label é perigoso?

## Checklist
- [ ] Conheço Counter, Gauge e Histogram
- [ ] Escrevo consultas PromQL com `rate`
- [ ] Crio um alerta e um painel RED
