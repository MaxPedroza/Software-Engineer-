# Aula 6 — Autenticação forte (MFA, passkeys)

**Duração:** ~20 min · **Módulo 20**

## Objetivo
Entender fatores de autenticação, MFA, TOTP e passkeys (WebAuthn).

## Teoria
- **Autenticação** = quem é você; **autorização** = o que pode fazer.
- Fatores: algo que **sabe** (senha), que **tem** (celular, chave física), que **é** (biometria).
- **MFA** combina 2+ fatores diferentes. SMS é o mais fraco (SIM swap); prefira TOTP, push com número ou chaves FIDO2.
- **TOTP**: código de 6 dígitos derivado de segredo compartilhado + tempo (janela de 30 s).
- **Passkeys / WebAuthn**: par de chaves por site; a chave privada nunca sai do dispositivo. Resistem a **phishing**, pois a credencial é atrelada ao domínio.
- Sessões: cookies `HttpOnly`, expiração, renovação do ID após login, logout invalida no servidor.
- **JWT**: valide assinatura, `exp`, `aud` e `iss`; nunca aceite `alg: none`.
- Defesas: rate limit, bloqueio progressivo, mensagem de erro genérica, verificação contra senhas vazadas.

## Exemplo: TOTP
```python
import pyotp

segredo = pyotp.random_base32()          # guardado cifrado no servidor
totp = pyotp.TOTP(segredo)
print(totp.provisioning_uri("ana@exemplo.com", issuer_name="MeuApp"))  # QR code

codigo = input("Código: ")
print("ok" if totp.verify(codigo, valid_window=1) else "inválido")
```

## Exercício
1. Ative MFA com app autenticador em uma conta sua e gere códigos de recuperação.
2. Implemente o exemplo e teste um código expirado.
3. Explique por que uma passkey resiste a phishing e uma senha+TOTP nem sempre.

## Checklist
- [ ] Diferencio autenticação e autorização
- [ ] Sei por que SMS é fraco
- [ ] Entendo o princípio de passkeys
