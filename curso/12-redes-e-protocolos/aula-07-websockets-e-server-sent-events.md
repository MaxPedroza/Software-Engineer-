# Aula 7 — WebSockets e Server-Sent Events

**Duração:** ~25 min · **Módulo 12**

## Objetivo
Escolher entre polling, SSE e WebSockets para comunicação em tempo real.

## Teoria
HTTP tradicional: o cliente pergunta, o servidor responde. Para tempo real:
- **Polling**: o cliente consulta a cada N segundos. Simples, mas desperdiça requisições.
- **SSE** (Server-Sent Events): uma resposta HTTP aberta (`text/event-stream`) pela qual o servidor envia eventos. **Unidirecional**, reconecta sozinho (`EventSource`), passa bem por proxies.
- **WebSocket**: conexão **bidirecional** persistente, iniciada por um `Upgrade` de HTTP (resposta `101 Switching Protocols`). Mensagens de texto/binário; ideal para chat, jogos e colaboração.

| | SSE | WebSocket |
|--|-----|-----------|
| Direção | Servidor → cliente | Bidirecional |
| Protocolo | HTTP | WS (`ws://`, `wss://`) |
| Reconexão | Automática | Manual |

Cuidado: conexões longas consomem recursos; escalar exige sticky sessions ou um *pub/sub* (ex.: Redis) entre instâncias. Use sempre `wss://`.

## Exemplo (FastAPI)
```python
from fastapi import FastAPI, WebSocket
from fastapi.responses import StreamingResponse
import asyncio

app = FastAPI()

@app.websocket("/ws")
async def ws(socket: WebSocket):
    await socket.accept()
    while True:
        msg = await socket.receive_text()
        await socket.send_text(f"eco: {msg}")

@app.get("/eventos")
async def eventos():
    async def gerar():
        for i in range(5):
            yield f"data: tick {i}\n\n"
            await asyncio.sleep(1)
    return StreamingResponse(gerar(), media_type="text/event-stream")
```
```bash
curl -N localhost:8000/eventos
```

## Exercício
1. Rode `curl -N` no endpoint SSE e observe os eventos chegando.
2. Teste o WebSocket com `websocat ws://localhost:8000/ws`.
3. Que opção usaria para (a) notificações de deploy; (b) chat? Justifique.

## Checklist
- [ ] Diferencio polling, SSE e WebSocket
- [ ] Sei o que é o `Upgrade` e o status 101
- [ ] Conheço os desafios de escalar conexões longas
