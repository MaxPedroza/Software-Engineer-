# Aula 2 — OWASP Top 10

**Duração:** ~20 min · **Módulo 20**

## Objetivo
Conhecer as categorias de risco mais críticas em aplicações web e como mitigá-las.

## Teoria
O **OWASP Top 10** é uma lista periódica dos riscos mais críticos. Categorias da edição 2021 (verifique a versão vigente em owasp.org):

| # | Categoria | Mitigação típica |
|---|-----------|------------------|
| A01 | Broken Access Control | Checar autorização no servidor, negar por padrão |
| A02 | Cryptographic Failures | TLS, algoritmos modernos, não guardar dados sensíveis à toa |
| A03 | Injection | Queries parametrizadas, escape de saída |
| A04 | Insecure Design | Threat modeling, requisitos de segurança |
| A05 | Security Misconfiguration | Hardening, remover defaults, headers de segurança |
| A06 | Vulnerable Components | Atualizar dependências, SCA |
| A07 | Identification & Auth Failures | MFA, política de senhas, limite de tentativas |
| A08 | Software & Data Integrity Failures | Assinar artefatos, pipeline protegido |
| A09 | Logging & Monitoring Failures | Logs de eventos de segurança, alertas |
| A10 | SSRF | Allowlist de destinos, bloquear IPs internos |

### Exemplo: Broken Access Control (IDOR)
```python
# Inseguro: qualquer usuário logado lê qualquer pedido
@app.get("/pedidos/{id}")
def ver(id: int, user=Depends(usuario_atual)):
    return db.pedido(id)

# Seguro: verifica a propriedade do recurso
@app.get("/pedidos/{id}")
def ver(id: int, user=Depends(usuario_atual)):
    pedido = db.pedido(id)
    if pedido is None or pedido.usuario_id != user.id:
        raise HTTPException(404)
    return pedido
```

## Exercício
1. Escolha 3 categorias e aponte onde poderiam ocorrer no seu projeto.
2. Teste o seu sistema: um usuário consegue acessar o recurso de outro mudando o ID na URL?

## Checklist
- [ ] Nomeio as principais categorias do Top 10
- [ ] Sei o que é IDOR e como evitar
- [ ] Mapeei riscos no meu projeto
