# Aula 6 — Tracing distribuído (OpenTelemetry)

**Duração:** ~25 min · **Módulo 19**

## Objetivo
Rastrear uma requisição através de vários serviços usando OpenTelemetry.

## Teoria
- **Trace**: caminho completo de uma requisição. **Span**: uma operação dentro do trace (com início, duração, atributos, status, relação pai/filho).
- **Propagação de contexto**: o `trace_id` viaja entre serviços no header W3C `traceparent` (`00-<trace_id>-<span_id>-<flags>`).
- **OpenTelemetry (OTel)**: padrão aberto e neutro para traces, métricas e logs — API/SDK, instrumentação automática e **Collector**, que recebe (OTLP), processa e exporta para Jaeger, Tempo, Datadog etc.
- Os três pilares se complementam: métricas dizem *que* há problema, traces dizem *onde*, logs dizem *por quê* (logue o `trace_id`).
- **Amostragem** (head/tail) controla custo.

## Exemplo em Python
```python
from opentelemetry import trace
from opentelemetry.sdk.resources import Resource
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor
from opentelemetry.exporter.otlp.proto.http.trace_exporter import OTLPSpanExporter

provider = TracerProvider(resource=Resource.create({"service.name": "pedidos"}))
provider.add_span_processor(BatchSpanProcessor(
    OTLPSpanExporter(endpoint="http://localhost:4318/v1/traces")))
trace.set_tracer_provider(provider)
tracer = trace.get_tracer(__name__)

def criar_pedido(pedido_id):
    with tracer.start_as_current_span("criar_pedido") as span:
        span.set_attribute("pedido.id", pedido_id)
        with tracer.start_as_current_span("consultar_estoque"):
            ...
        with tracer.start_as_current_span("cobrar_pagamento"):
            ...
```
Jaeger local:
```bash
docker run -d --name jaeger -p 16686:16686 -p 4318:4318 jaegertracing/all-in-one:1.57
```
Abra http://localhost:16686 para ver a cascata de spans.

## Exercício
1. Instrumente 2 serviços (API → worker) propagando `traceparent` e veja o trace único no Jaeger.
2. Identifique no trace qual span domina a latência e proponha uma otimização.

## Checklist
- [ ] Diferencio trace e span
- [ ] Entendo propagação de contexto
- [ ] Correlaciono logs, métricas e traces
