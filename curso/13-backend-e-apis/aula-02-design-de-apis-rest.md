# Aula 2 — Design de APIs REST

**Duração:** ~25 min · **Módulo 13**

## Objetivo
Projetar endpoints REST consistentes, usando corretamente recursos, métodos e status.

## Teoria
REST modela a API em torno de **recursos** (substantivos, no plural), identificados por URLs; os **métodos HTTP** expressam a ação.

| Método | Rota | Ação | Sucesso |
|--------|------|------|---------|
| GET | `/tarefas` | Listar | 200 |
| POST | `/tarefas` | Criar | 201 + `Location` |
| GET | `/tarefas/{id}` | Obter | 200 / 404 |
| PUT | `/tarefas/{id}` | Substituir | 200 |
| PATCH | `/tarefas/{id}` | Atualizar parcial | 200 |
| DELETE | `/tarefas/{id}` | Remover | 204 |

- **Seguros**: GET. **Idempotentes**: GET, PUT, DELETE.
- Evite verbos na URL (`/criarTarefa`); aninhe com moderação (`/projetos/1/tarefas`).
- Status: 400 requisição inválida, 401 não autenticado, 403 sem permissão, 404 não encontrado, 409 conflito, 422 validação, 500 erro interno.
- JSON com nomes consistentes; sem estado entre requisições.

## Exemplo
```python
from fastapi import FastAPI, HTTPException, Response, status
from pydantic import BaseModel

app = FastAPI()
db: dict[int, dict] = {}

class TarefaIn(BaseModel):
    titulo: str
    feita: bool = False

@app.post("/tarefas", status_code=status.HTTP_201_CREATED)
def criar(t: TarefaIn, response: Response):
    id = len(db) + 1
    db[id] = {"id": id, **t.model_dump()}
    response.headers["Location"] = f"/tarefas/{id}"
    return db[id]

@app.get("/tarefas/{id}")
def obter(id: int):
    if id not in db:
        raise HTTPException(404, "Tarefa não encontrada")
    return db[id]

@app.delete("/tarefas/{id}", status_code=204)
def remover(id: int):
    db.pop(id, None)
```
```bash
curl -i -X POST localhost:8000/tarefas -H 'Content-Type: application/json' -d '{"titulo":"Ler"}'
```

## Exercício
1. Implemente PUT e PATCH para `/tarefas/{id}`.
2. Corrija o design: `GET /getTarefas`, `POST /tarefas/delete/3`.

## Checklist
- [ ] Modelo recursos e rotas no plural
- [ ] Uso métodos e status corretos
- [ ] Sei o que é idempotência
