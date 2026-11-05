# Aula 9 — Estudos de caso (encurtador de URL, feed, chat, e-commerce)

**Duração:** ~30 min · **Módulo 17**

## Objetivo
Aplicar o método de design: requisitos → estimativas → API → dados → arquitetura → gargalos.

## Teoria
### 1. Encurtador de URL
- API: `POST /urls {url}` → `{codigo}`; `GET /{codigo}` → 301/302.
- Código base62 de 7 caracteres (62⁷ ≈ 3,5 trilhões). Gerar via contador distribuído/faixas de IDs, não por hash truncado (colisões).
- Leitura >> escrita: **cache** de códigos populares + banco chave-valor.

### 2. Feed de notícias
- **Fan-out on write**: ao postar, insere no feed de cada seguidor (leitura rápida; caro para celebridades).
- **Fan-out on read**: monta o feed na leitura (escrita barata, leitura lenta).
- Híbrido: push para usuários comuns, pull para contas com milhões de seguidores.

### 3. Chat
- Conexões persistentes (WebSocket), gateways que mantêm mapa usuário→servidor.
- Mensagens ordenadas por conversa (partição por `conversa_id`), ack de entrega/leitura, fila para usuários offline, push notification.

### 4. E-commerce
- Catálogo (leitura, cache/busca), carrinho (Redis), pedido (consistência forte).
- **Saga** para pedido→pagamento→estoque com compensações; **outbox** para publicar eventos de forma confiável; **idempotency key** no pagamento.
- Evitar overselling com reserva de estoque atômica.

## Exemplo: geração de código base62
```python
ALFABETO = "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ"

def base62(n: int) -> str:
    if n == 0:
        return ALFABETO[0]
    s = ""
    while n:
        n, r = divmod(n, 62)
        s = ALFABETO[r] + s
    return s

print(base62(125))        # "21"
print(base62(3_521_614_606_207))  # 62**7 - 1 -> "ZZZZZZZ"
```

## Exercício
1. Desenhe (Mermaid ou ASCII) o diagrama do encurtador com cache, banco e gerador de IDs.
2. Para o e-commerce, descreva a saga de um pedido e a compensação se o pagamento falhar.

## Checklist
- [ ] Sigo um roteiro de design
- [ ] Comparo fan-out on write/read
- [ ] Sei usar saga, outbox e idempotency key
