# Aula 7 — CI/CD e deploy em cloud

**Duração:** ~40 min · **Módulo 24 — Etapa 7**

## Objetivo
Automatizar build, testes e deploy, colocando o sistema em produção na nuvem.

## Passo a passo
1. **CI** (GitHub Actions) em todo PR: instalar dependências com cache → lint → testes → build → scan de vulnerabilidades.
2. **Imagem Docker** multi-stage, usuário não root, versionada pelo SHA do commit; publique no registry.
3. **Infraestrutura como código** (Terraform) ou PaaS gerenciado (Render, Fly.io, Cloud Run, ECS).
4. **Segredos** no cofre/secrets do provedor; nunca no repositório.
5. **CD**: merge na `main` → deploy em *staging* → smoke test → promoção para produção.
6. **Migrations** executadas no deploy; estratégia de **rollback**.
7. **Domínio e HTTPS** (TLS), banco gerenciado com backup.

### Pipeline mínimo
```yaml
name: ci
on: [pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with: { python-version: '3.12', cache: pip }
      - run: pip install -r requirements.txt
      - run: ruff check . && pytest --cov --cov-fail-under=80
```

### Checklist de deploy
```text
[ ] Testes e CI verdes na main
[ ] Variáveis e segredos configurados no ambiente
[ ] Backup do banco e plano de rollback definidos
[ ] Migrations testadas em staging
[ ] Health check e smoke test após o deploy
[ ] HTTPS ativo e logs acessíveis
```

## Entregáveis
- `.github/workflows/ci.yml` e `deploy.yml`
- Sistema acessível por URL pública com HTTPS
- `docs/deploy.md` com o runbook e o rollback

## Critérios de aceite
- [ ] PR com testes falhando não pode ser mesclado (branch protection)
- [ ] Merge na main implanta sem passos manuais
- [ ] Rollback testado ao menos uma vez
