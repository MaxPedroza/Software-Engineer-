# Aula 7 — Documentação com OpenAPI/Swagger

**Duração:** ~20 min · **Módulo 13**

## Objetivo
Documentar e testar a API usando a especificação OpenAPI gerada pelo FastAPI.

## Teoria
- **OpenAPI** é a especificação (JSON/YAML) que descreve endpoints, parâmetros, corpos, respostas e esquemas de segurança. **Swagger UI** e **ReDoc** são interfaces que a exibem.
- Benefícios: documentação sempre atual, **contrato** entre times, geração de clientes/SDKs, testes de contrato e mocks.
- O FastAPI gera o OpenAPI a partir dos tipos Python: `/openapi.json`, `/docs` (Swagger UI) e `/redoc`.
- Enriqueça com `summary`, `description`, `tags`, `responses` e exemplos. Documente também os erros (401, 403, 404, 422).

## Exemplo
```python
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel, Field

app = FastAPI(
    title="API de Tarefas",
    version="1.0.0",
    description="Gerencia tarefas de usuários autenticados.",
)

class Tarefa(BaseModel):
    id: int
    titulo: str = Field(examples=["Estudar OpenAPI"])
    feita: bool = False

@app.get(
    "/tarefas/{id}",
    response_model=Tarefa,
    tags=["tarefas"],
    summary="Obtém uma tarefa",
    responses={404: {"description": "Tarefa não encontrada"}},
)
def obter(id: int):
    raise HTTPException(404, "Tarefa não encontrada")
```
```bash
uvicorn main:app --reload
curl -s localhost:8000/openapi.json | python -m json.tool | head -30
# Navegador: http://localhost:8000/docs
# Gerar cliente: npx @openapitools/openapi-generator-cli generate -i openapi.json -g python -o cliente
```

## Exercício
1. Abra `/docs`, execute uma requisição pelo "Try it out".
2. Adicione `tags`, `summary` e respostas de erro a todas as rotas.
3. Exporte `openapi.json` e importe no Postman/Insomnia para criar a coleção de requisições.

## Checklist
- [ ] Gero e navego `/docs` e `/openapi.json`
- [ ] Documento erros e exemplos
- [ ] Exporto o contrato para uma coleção
