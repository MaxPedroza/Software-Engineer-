# Aula 5 — Gestão de senhas, segredos e chaves

**Duração:** ~20 min · **Módulo 20**

## Objetivo
Armazenar senhas corretamente e manter segredos fora do código.

## Teoria
### Senhas
- Nunca guarde senha em texto puro nem com hash rápido (SHA-256 puro, MD5).
- Use funções **lentas e com sal**: **Argon2id** (preferido), **bcrypt** ou **scrypt**.
- O *salt* é único por senha e evita rainbow tables; *pepper* é um segredo extra fora do banco.
- Compare em tempo constante e limite tentativas de login.

### Segredos
- Nunca commite chaves, tokens ou senhas. Use variáveis de ambiente ou **cofres** (Vault, AWS Secrets Manager, Azure Key Vault).
- Rotacione periodicamente e revogue imediatamente após vazamento (remover do Git não basta: o histórico persiste).
- Use `.gitignore` para `.env` e *secret scanning* (gitleaks, GitHub secret scanning).
- Chaves distintas por ambiente; escopo mínimo.

## Exemplo
```python
from argon2 import PasswordHasher
from argon2.exceptions import VerifyMismatchError
import os

ph = PasswordHasher()
hash_salvo = ph.hash("minha-senha-forte")  # salt embutido

def login_ok(senha: str) -> bool:
    try:
        return ph.verify(hash_salvo, senha)
    except VerifyMismatchError:
        return False

# Segredo vem do ambiente, nunca do código
DB_URL = os.environ["DATABASE_URL"]  # KeyError se ausente: falha cedo
```

## Exercício
1. Instale `argon2-cffi`, gere dois hashes da mesma senha e explique por que diferem.
2. Rode `gitleaks detect` (ou busque `password`/`token` com grep) no seu repositório e liste achados.
3. Mova um segredo hardcoded para variável de ambiente.

## Checklist
- [ ] Uso Argon2id/bcrypt para senhas
- [ ] Nenhum segredo no repositório
- [ ] Tenho plano de rotação e revogação
