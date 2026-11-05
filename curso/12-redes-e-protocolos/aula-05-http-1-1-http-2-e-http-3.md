# Aula 5 — HTTP/1.1, HTTP/2 e HTTP/3

**Duração:** ~25 min · **Módulo 12**

## Objetivo
Entender a estrutura do HTTP e a evolução entre suas versões.

## Teoria
HTTP é um protocolo de requisição/resposta, sem estado. Uma requisição tem **método** (GET, POST, PUT, PATCH, DELETE), **caminho**, **cabeçalhos** e **corpo**; a resposta tem **código de status** (2xx sucesso, 3xx redirecionamento, 4xx erro do cliente, 5xx erro do servidor), cabeçalhos e corpo.

| Versão | Transporte | Principais características |
|--------|-----------|----------------------------|
| 1.1 | TCP | Texto, conexões persistentes (keep-alive); *head-of-line blocking*: uma resposta por vez por conexão (browsers abrem ~6 conexões) |
| 2 | TCP + TLS | Binário, **multiplexação** de streams numa conexão, compressão de cabeçalhos (HPACK); ainda sofre bloqueio no nível TCP |
| 3 | **QUIC sobre UDP** | Streams independentes (sem HOL no transporte), TLS 1.3 embutido, handshake mais rápido, migração de conexão |

Cache: `Cache-Control`, `ETag` e `If-None-Match` (resposta `304 Not Modified`).

## Exemplo
```bash
curl -v https://example.com            # requisição/resposta completas
curl -I https://example.com            # só cabeçalhos
curl --http1.1 -sI https://example.com | head -1
curl --http2 -sI https://example.com | head -1   # HTTP/2 200
curl --http3 -sI https://cloudflare.com | head -1  # requer curl com suporte
curl -X POST localhost:8000/tarefas -H 'Content-Type: application/json' \
     -d '{"titulo":"nova"}'
```
Requisição crua HTTP/1.1:
```
GET /tarefas HTTP/1.1
Host: api.local
Accept: application/json
```

## Exercício
1. Compare a versão do protocolo usada por 3 sites com `curl -sI -w '%{http_version}\n' -o /dev/null URL`.
2. Faça duas requisições com `ETag` e obtenha um `304`.
3. Por que HTTP/2 reduz a necessidade de várias conexões?

## Checklist
- [ ] Conheço métodos e classes de status
- [ ] Explico multiplexação e head-of-line blocking
- [ ] Sei que HTTP/3 usa QUIC/UDP
