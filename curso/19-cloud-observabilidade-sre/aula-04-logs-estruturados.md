# Aula 4 — Logs estruturados

**Duração:** ~20 min · **Módulo 19**

## Objetivo
Produzir logs em JSON, correlacionáveis e seguros, prontos para busca e análise.

## Teoria
- **Log estruturado**: cada evento é um objeto (JSON) com campos consultáveis, em vez de texto livre.
- Campos essenciais: `timestamp` (UTC, ISO 8601), `level`, `service`, `message`, `trace_id`/`request_id`, e contexto (`user_id`, `route`, `status`, `duration_ms`).
- **Níveis**: DEBUG, INFO, WARNING, ERROR, CRITICAL. Em produção, INFO ou acima.
- **Correlation ID**: propagado entre serviços (header `X-Request-ID`) para seguir uma requisição.
- **Nunca logue** senhas, tokens, cartões ou dados pessoais sensíveis (LGPD); mascare.
- Logue em **stdout** (12-factor); um agente (Fluent Bit, Promtail) coleta e envia para Loki, Elasticsearch ou CloudWatch.
- Logs são caros em volume: use amostragem e retenção por nível.

## Exemplo em Python
```python
import json, logging, sys, time, uuid

class JsonFormatter(logging.Formatter):
    def format(self, r):
        d = {
            "timestamp": time.strftime("%Y-%m-%dT%H:%M:%SZ", time.gmtime(r.created)),
            "level": r.levelname,
            "service": "api",
            "message": r.getMessage(),
            **getattr(r, "ctx", {}),
        }
        if r.exc_info:
            d["exception"] = self.formatException(r.exc_info)
        return json.dumps(d, ensure_ascii=False)

h = logging.StreamHandler(sys.stdout)
h.setFormatter(JsonFormatter())
log = logging.getLogger("api")
log.addHandler(h)
log.setLevel(logging.INFO)

req_id = str(uuid.uuid4())
log.info("pedido criado", extra={"ctx": {"request_id": req_id, "pedido_id": 123, "duration_ms": 42}})
```
Saída:
```json
{"timestamp": "2026-03-01T12:00:00Z", "level": "INFO", "service": "api", "message": "pedido criado", "request_id": "...", "pedido_id": 123, "duration_ms": 42}
```
Consulta com `jq`: `docker logs api | jq 'select(.level=="ERROR")'`

## Exercício
1. Converta os logs do projeto para JSON e adicione `request_id` via middleware.
2. Escreva uma consulta que liste as 10 requisições mais lentas a partir de `duration_ms`.

## Checklist
- [ ] Logo em JSON com campos úteis
- [ ] Uso correlation ID
- [ ] Não registro dados sensíveis
