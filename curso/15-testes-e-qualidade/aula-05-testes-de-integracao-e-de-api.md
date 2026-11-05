# Aula 5 — Testes de integração e de API

**Duração:** ~25 min · **Módulo 15**

## Objetivo
Testar a API junto com o banco de dados usando FastAPI TestClient e pytest.

## Teoria
- **Teste de integração** verifica que componentes funcionam **juntos** (rota + serviço + banco), sem mocks internos.
- Cada teste deve ser **isolado**: banco limpo por teste (SQLite em memória, transação com rollback ou contêiner via Testcontainers).
- **Testes de API** validam contrato HTTP: status, corpo JSON, cabeçalhos, validação e autenticação.
- Use `dependency_overrides` do FastAPI para trocar o banco real pelo de teste.
- Cubra também caminhos de erro: 404, 422 (validação), 401/403.
- São mais lentos que unitários: rode em CI separado se necessário (`pytest -m integracao`).

## Exemplo
```python
# app.py
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel

app = FastAPI()
_db: dict[int, dict] = {}

class NovaTarefa(BaseModel):
    titulo: str

@app.post("/tarefas", status_code=201)
def criar(t: NovaTarefa):
    id_ = len(_db) + 1
    _db[id_] = {"id": id_, "titulo": t.titulo}
    return _db[id_]

@app.get("/tarefas/{id_}")
def obter(id_: int):
    if id_ not in _db:
        raise HTTPException(404, "não encontrada")
    return _db[id_]
```
```python
# test_api.py  (pip install httpx pytest)
import pytest
from fastapi.testclient import TestClient
import app as modulo

@pytest.fixture
def client():
    modulo._db.clear()                 # estado limpo por teste
    return TestClient(modulo.app)

def test_criar_e_obter(client):
    r = client.post("/tarefas", json={"titulo": "estudar"})
    assert r.status_code == 201
    id_ = r.json()["id"]

    r2 = client.get(f"/tarefas/{id_}")
    assert r2.status_code == 200
    assert r2.json()["titulo"] == "estudar"

def test_obter_inexistente_retorna_404(client):
    assert client.get("/tarefas/99").status_code == 404

def test_criar_sem_titulo_retorna_422(client):
    assert client.post("/tarefas", json={}).status_code == 422
```

## Exercício
1. Adicione `DELETE /tarefas/{id}` e teste sucesso e 404.
2. Troque o dicionário por SQLite em memória e use um override de dependência no teste.
3. Teste que uma rota protegida retorna 401 sem token.

## Checklist
- [ ] Testo rota + banco juntos
- [ ] Isolo o estado entre testes
- [ ] Cubro erros 404, 422 e 401
