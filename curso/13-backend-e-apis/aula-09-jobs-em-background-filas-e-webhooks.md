# Aula 9 — Jobs em background, filas e webhooks

**Duração:** ~25 min · **Módulo 13**

## Objetivo
Mover trabalho lento para segundo plano e integrar sistemas com webhooks seguros.

## Teoria
- Requisições devem responder rápido. Tarefas lentas (e-mails, relatórios, processamento de imagens) vão para **jobs em background**.
- **Fila de mensagens** (Redis, RabbitMQ, SQS, Kafka): o produtor (API) enfileira; **workers** consomem de forma assíncrona. Ganhos: desacoplamento, absorção de picos, retentativas.
- Boas práticas: jobs **idempotentes** (podem rodar duas vezes — entrega *at-least-once*), *retries* com *backoff* exponencial, **dead-letter queue** para falhas definitivas, *timeouts*.
- **Webhook**: o servidor chama uma URL do cliente quando ocorre um evento (HTTP POST). Segurança: assinatura **HMAC** no cabeçalho, verificação com comparação em tempo constante, proteção contra replay (timestamp), responder 2xx rápido e processar em fila.
- Tarefas simples: `BackgroundTasks` do FastAPI. Tarefas robustas: Celery, RQ, Arq.

## Exemplo
```python
import hmac, hashlib
from fastapi import FastAPI, BackgroundTasks, Request, Header, HTTPException

app = FastAPI()
SEGREDO = b"segredo-do-webhook"

def enviar_email(dest: str):
    print(f"enviando e-mail para {dest}")

@app.post("/tarefas", status_code=202)
def criar(bg: BackgroundTasks):
    bg.add_task(enviar_email, "ana@x.com")
    return {"status": "aceita"}

@app.post("/webhooks/pagamento")
async def webhook(req: Request, x_assinatura: str = Header()):
    corpo = await req.body()
    esperado = hmac.new(SEGREDO, corpo, hashlib.sha256).hexdigest()
    if not hmac.compare_digest(esperado, x_assinatura):
        raise HTTPException(401, "Assinatura inválida")
    return {"ok": True}
```
```bash
CORPO='{"evento":"pago"}'
SIG=$(printf '%s' "$CORPO" | openssl dgst -sha256 -hmac 'segredo-do-webhook' | awk '{print $2}')
curl -X POST localhost:8000/webhooks/pagamento -H "X-Assinatura: $SIG" -d "$CORPO"
```
Com Redis + RQ: `queue.enqueue(enviar_email, "ana@x.com")` e `rq worker`.

## Exercício
1. Envie o webhook com assinatura correta e depois alterada.
2. Faça a criação de tarefa disparar um job de notificação e simule uma falha com retentativa.
3. Por que o job precisa ser idempotente?

## Checklist
- [ ] Sei quando usar fila/worker
- [ ] Aplico retries e DLQ
- [ ] Verifico assinaturas HMAC em webhooks
