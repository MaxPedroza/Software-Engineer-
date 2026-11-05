# Aula 6 — Paginação, filtros, versionamento e idempotência

**Duração:** ~25 min · **Módulo 13**

## Objetivo
Tornar a API escalável e segura contra repetições, mudanças e grandes volumes.

## Teoria
- **Paginação**: nunca retorne coleções inteiras.
  - *Offset/limit* (`?limit=20&offset=40`): simples, mas lento em offsets grandes e instável com inserções.
  - *Cursor* (`?after=<id>`): estável e eficiente (`WHERE id > :cursor ORDER BY id LIMIT n`).
- **Filtros e ordenação**: `?status=aberta&ordem=-criada_em`; valide campos permitidos.
- **Versionamento**: permite mudanças incompatíveis sem quebrar clientes: no caminho (`/v1/tarefas`) ou cabeçalho. Evolua de forma compatível (adicionar campos) e anuncie descontinuações.
- **Idempotência**: repetir a requisição tem o mesmo efeito que enviá-la uma vez. GET/PUT/DELETE já são; para **POST** use o cabeçalho `Idempotency-Key`, guardando a resposta da primeira execução (essencial em pagamentos e retentativas de rede).

## Exemplo
```python
from fastapi import FastAPI, Header, Query, APIRouter

app = FastAPI()
v1 = APIRouter(prefix="/v1")
TAREFAS = [{"id": i, "titulo": f"T{i}", "status": "aberta" if i % 2 else "feita"}
           for i in range(1, 101)]
chaves: dict[str, dict] = {}

@v1.get("/tarefas")
def listar(limit: int = Query(20, ge=1, le=100), after: int = 0, status: str | None = None):
    itens = [t for t in TAREFAS if t["id"] > after and (not status or t["status"] == status)]
    pagina = itens[:limit]
    prox = pagina[-1]["id"] if len(itens) > limit else None
    return {"itens": pagina, "proximo_cursor": prox}

@v1.post("/tarefas", status_code=201)
def criar(titulo: str, idempotency_key: str = Header()):
    if idempotency_key in chaves:
        return chaves[idempotency_key]
    nova = {"id": len(TAREFAS) + 1, "titulo": titulo, "status": "aberta"}
    TAREFAS.append(nova); chaves[idempotency_key] = nova
    return nova

app.include_router(v1)
```
```bash
curl 'localhost:8000/v1/tarefas?limit=5&after=10&status=aberta'
curl -X POST 'localhost:8000/v1/tarefas?titulo=X' -H 'Idempotency-Key: abc-1'  # repita: mesma resposta
```

## Exercício
1. Percorra todas as páginas seguindo `proximo_cursor`.
2. Envie o POST duas vezes com a mesma chave: quantas tarefas foram criadas?
3. Por que offset é ruim em tabelas de milhões de linhas?

## Checklist
- [ ] Implemento paginação por cursor
- [ ] Versiono a API
- [ ] Garanto idempotência em POST
