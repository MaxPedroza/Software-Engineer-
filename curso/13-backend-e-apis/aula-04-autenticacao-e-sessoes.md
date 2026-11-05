# Aula 4 — Autenticação e sessões

**Duração:** ~25 min · **Módulo 13**

## Objetivo
Implementar login seguro com hash de senha e entender sessões e cookies.

## Teoria
- **Autenticação**: provar *quem é* o usuário. (Autorização — o que ele pode — é a próxima aula.)
- **Senhas**: nunca guarde em texto puro nem com hash rápido (MD5/SHA-256). Use algoritmos lentos com *salt*: **argon2**, **bcrypt**, scrypt.
- **Sessão com cookie**: após o login, o servidor cria uma sessão (ID aleatório guardado no Redis/banco) e envia um cookie. Cookies devem ter `HttpOnly` (sem acesso por JS), `Secure` (só HTTPS) e `SameSite` (mitiga CSRF).
- **Token** (stateless): o cliente envia `Authorization: Bearer <token>` (próxima aula).
- Boas práticas: mensagem genérica em falha ("credenciais inválidas"), limite de tentativas (*rate limiting*), HTTPS, MFA.

## Exemplo
```python
# pip install passlib[argon2]
from passlib.hash import argon2
from fastapi import FastAPI, HTTPException, Response
from pydantic import BaseModel
import secrets

app = FastAPI()
usuarios = {"ana@x.com": argon2.hash("senha-forte-123")}
sessoes: dict[str, str] = {}

class Login(BaseModel):
    email: str
    senha: str

@app.post("/login")
def login(d: Login, resp: Response):
    h = usuarios.get(d.email)
    if not h or not argon2.verify(d.senha, h):
        raise HTTPException(401, "Credenciais inválidas")
    sid = secrets.token_urlsafe(32)
    sessoes[sid] = d.email
    resp.set_cookie("sid", sid, httponly=True, secure=True,
                    samesite="lax", max_age=3600)
    return {"ok": True}
```
```bash
curl -i -c cookies.txt -X POST https://localhost/login \
  -H 'Content-Type: application/json' -d '{"email":"ana@x.com","senha":"senha-forte-123"}'
```

## Exercício
1. Implemente `/me`, que lê o cookie `sid` e devolve o e-mail (401 se inválido).
2. Implemente `/logout`, removendo a sessão.
3. Por que `HttpOnly` reduz o impacto de XSS?

## Checklist
- [ ] Faço hash de senha com argon2/bcrypt
- [ ] Entendo sessões e atributos de cookie
- [ ] Retorno erros de login genéricos
