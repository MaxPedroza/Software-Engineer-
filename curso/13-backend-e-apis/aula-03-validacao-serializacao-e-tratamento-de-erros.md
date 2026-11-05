# Aula 3 — Validação, serialização e tratamento de erros

**Duração:** ~25 min · **Módulo 13**

## Objetivo
Validar entradas, serializar saídas com segurança e padronizar respostas de erro.

## Teoria
- **Validação**: toda entrada externa é hostil até prova em contrário. Valide tipo, tamanho, formato e regras de negócio na borda da API.
- **Serialização**: converter objetos internos em JSON. Use modelos de **saída** separados dos de entrada e do banco, para nunca vazar campos sensíveis (`senha_hash`).
- **Erros padronizados**: o mesmo formato sempre, com status correto. O padrão **RFC 9457** (*Problem Details*) define `type`, `title`, `status`, `detail`.
- Nunca exponha *stack traces* ao cliente; registre-os em log.
- Pydantic valida automaticamente e retorna `422` em caso de falha.

## Exemplo (FastAPI + Pydantic)
```python
from fastapi import FastAPI, Request
from fastapi.responses import JSONResponse
from pydantic import BaseModel, Field, EmailStr  # pip install email-validator

app = FastAPI()

class UsuarioIn(BaseModel):
    email: EmailStr
    senha: str = Field(min_length=8)

class UsuarioOut(BaseModel):
    id: int
    email: EmailStr

class RegraDeNegocio(Exception):
    def __init__(self, detalhe: str):
        self.detalhe = detalhe

@app.exception_handler(RegraDeNegocio)
async def tratar(req: Request, exc: RegraDeNegocio):
    return JSONResponse(
        status_code=409,
        media_type="application/problem+json",
        content={"title": "Conflito", "status": 409, "detail": exc.detalhe},
    )

@app.post("/usuarios", response_model=UsuarioOut, status_code=201)
def criar(u: UsuarioIn):
    if u.email == "ja@existe.com":
        raise RegraDeNegocio("E-mail já cadastrado")
    return {"id": 1, "email": u.email, "senha": u.senha}  # 'senha' é filtrada
```
```bash
curl -s -X POST localhost:8000/usuarios -H 'Content-Type: application/json' \
  -d '{"email":"x","senha":"123"}'   # 422
```

## Exercício
1. Envie dados inválidos e leia o corpo do `422`.
2. Confirme que `senha` nunca aparece na resposta.
3. Adicione um handler genérico de `Exception` que retorna 500 sem detalhes internos.

## Checklist
- [ ] Valido entradas na borda
- [ ] Separo modelos de entrada e saída
- [ ] Padronizo erros sem vazar detalhes
