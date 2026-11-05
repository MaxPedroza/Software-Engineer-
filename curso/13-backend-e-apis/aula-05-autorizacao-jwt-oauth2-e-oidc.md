# Aula 5 — Autorização, JWT, OAuth2 e OIDC

**Duração:** ~30 min · **Módulo 13**

## Objetivo
Proteger rotas com JWT e entender os fluxos OAuth2 e OIDC.

## Teoria
- **Autorização**: decidir o que o usuário autenticado pode fazer (RBAC por papéis; ou por dono do recurso). Retorne 403 quando autenticado, mas sem permissão.
- **JWT**: token assinado com três partes `header.payload.signature` (Base64URL). O payload tem *claims* (`sub`, `exp`, `iat`, `scope`). É **assinado, não criptografado** — não ponha segredos nele. Use expiração curta + *refresh token*, e valide assinatura e `exp`.
- **OAuth2**: protocolo de **delegação de acesso**: um app obtém um *access token* para acessar recursos em nome do usuário, sem ver sua senha. Fluxo recomendado para apps: *Authorization Code* com **PKCE**.
- **OIDC** (OpenID Connect): camada de **identidade** sobre o OAuth2; adiciona o *ID token* (JWT) e o endpoint `userinfo` — é o "Entrar com Google".

## Exemplo
```python
# pip install pyjwt
import jwt, time
from fastapi import FastAPI, Depends, HTTPException
from fastapi.security import HTTPBearer, HTTPAuthorizationCredentials

SEGREDO = "troque-por-variavel-de-ambiente"
app = FastAPI()
bearer = HTTPBearer()

def criar_token(user_id: int) -> str:
    return jwt.encode({"sub": str(user_id), "exp": int(time.time()) + 900},
                      SEGREDO, algorithm="HS256")

def usuario_atual(c: HTTPAuthorizationCredentials = Depends(bearer)) -> int:
    try:
        return int(jwt.decode(c.credentials, SEGREDO, algorithms=["HS256"])["sub"])
    except jwt.PyJWTError:
        raise HTTPException(401, "Token inválido ou expirado")

tarefas = {1: {"dono": 1, "titulo": "A"}, 2: {"dono": 2, "titulo": "B"}}

@app.get("/tarefas/{id}")
def obter(id: int, uid: int = Depends(usuario_atual)):
    t = tarefas.get(id)
    if not t: raise HTTPException(404)
    if t["dono"] != uid: raise HTTPException(403, "Sem permissão")
    return t
```
```bash
curl -H "Authorization: Bearer $TOKEN" localhost:8000/tarefas/1
```

## Exercício
1. Decodifique um JWT em jwt.io (ou `base64 -d`) e liste as claims.
2. Teste o acesso à tarefa de outro usuário (deve dar 403) e com token expirado (401).
3. Diferencie OAuth2 de OIDC em duas frases.

## Checklist
- [ ] Diferencio autenticação e autorização
- [ ] Gero e valido JWT com expiração
- [ ] Explico OAuth2 (PKCE) e OIDC
