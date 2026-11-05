# Aula 10 — Revisão e quiz do módulo

**Duração:** ~25 min · **Módulo 18**

## Resumo
- DevOps = cultura + automação + medição (métricas DORA).
- **Docker**: imagens em camadas, multi-stage, usuário não-root.
- **Compose**: serviços, redes por nome, volumes e healthchecks.
- **CI** (GitHub Actions): lint + testes em PRs, matrix, cache, branch protegida.
- **CD**: build único, tag por SHA, environments com aprovação, rollback.
- Deploy: rolling, blue/green, canary; migrações expand/contract.
- **Feature flags** separam deploy de release; segredos fora do Git.
- **Kubernetes**: Pod, Deployment, Service, probes, modelo declarativo.
- **Terraform**: plan/apply, state remoto, infraestrutura versionada.

## Quiz
1. Cite as 4 métricas DORA.
2. Por que copiar `requirements.txt` antes do código no Dockerfile?
3. Como a API acessa o banco em uma rede do Compose?
4. Qual evento do GitHub Actions roda em pull requests?
5. Por que construir a imagem uma só vez e promovê-la entre ambientes?
6. Qual estratégia oferece rollback instantâneo, ao custo de dobrar recursos?
7. Qual a diferença entre liveness e readiness probe?
8. Qual a diferença entre entrega contínua e implantação contínua?
9. Para que serve o `terraform plan`?
10. Por que remover feature flags antigas?

## Gabarito resumido
1. Frequência de deploy, lead time, taxa de falha, tempo de restauração.
2. Aproveitar o cache de camadas: dependências mudam menos.
3. Pelo nome do serviço (ex.: `db:5432`).
4. `pull_request`.
5. Garante que o que foi testado é o que vai à produção.
6. Blue/green.
7. Liveness reinicia o container; readiness controla se recebe tráfego.
8. Na entrega o deploy final é manual/aprovado; na implantação é automático.
9. Mostra as mudanças previstas antes de aplicá-las.
10. Evitam dívida técnica e caminhos de código mortos.

## Entregável do módulo
**Pipeline CI/CD completo versionado** no repositório: `Dockerfile`, `compose.yaml`, `.github/workflows/ci.yml` (lint + testes) e `cd.yml` (build da imagem com tag por SHA, deploy em staging e produção com aprovação), manifestos Kubernetes e/ou Terraform, com um README explicando como reverter um deploy.

## Checklist final
- [ ] Imagem Docker enxuta e segura
- [ ] CI bloqueia merges com testes falhando
- [ ] CD publica e implanta automaticamente
- [ ] Rollback documentado e testado
