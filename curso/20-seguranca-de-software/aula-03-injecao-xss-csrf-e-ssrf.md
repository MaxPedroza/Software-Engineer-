# Aula 3 — Injeção, XSS, CSRF e SSRF na prática

**Duração:** ~25 min · **Módulo 20**

## Objetivo
Reconhecer e corrigir quatro classes comuns de vulnerabilidades web.

## Teoria
- **SQL Injection**: entrada do usuário vira parte do comando SQL. Correção: *queries parametrizadas*.
- **XSS**: script malicioso executa no navegador da vítima. Correção: escapar saída por contexto, CSP, evitar `innerHTML`.
- **CSRF**: site malicioso faz o navegador do usuário enviar requisição autenticada. Correção: tokens anti-CSRF, cookies `SameSite`.
- **SSRF**: o servidor é induzido a requisitar URLs internas (ex.: metadados de nuvem). Correção: allowlist de hosts, bloquear IPs privados.

## SQL Injection
```python
# Inseguro
cur.execute(f"SELECT * FROM users WHERE email = '{email}'")
# email = "' OR '1'='1" retorna todos os usuários

# Seguro
cur.execute("SELECT * FROM users WHERE email = %s", (email,))
```

## XSS
```js
// Inseguro
el.innerHTML = comentario;
// Seguro: trata como texto
el.textContent = comentario;
```

## CSRF e cookies
```python
response.set_cookie("sessao", token, httponly=True, secure=True, samesite="Lax")
```

## SSRF
```python
import ipaddress, socket
from urllib.parse import urlparse

PERMITIDOS = {"api.parceiro.com"}

def url_segura(url: str) -> bool:
    host = urlparse(url).hostname
    if host not in PERMITIDOS:
        return False
    ip = ipaddress.ip_address(socket.gethostbyname(host))
    return not (ip.is_private or ip.is_loopback or ip.is_link_local)
```

## Exercício
1. Reescreva uma consulta do seu projeto que concatena strings para usar parâmetros.
2. Insira `<script>alert(1)</script>` em um campo de texto. Ele é escapado na tela?
3. Verifique as flags dos seus cookies de sessão.

## Checklist
- [ ] Uso queries parametrizadas
- [ ] Escapo saída e uso `textContent`
- [ ] Configuro cookies com HttpOnly/Secure/SameSite
- [ ] Valido URLs para evitar SSRF
