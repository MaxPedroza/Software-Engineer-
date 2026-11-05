# Aula 5 — Entrega e implantação contínuas (CD)

**Duração:** ~25 min · **Módulo 18**

## Objetivo
Construir e publicar uma imagem Docker e implantá-la automaticamente após o CI.

## Teoria
- **Artefato único**: construa a imagem **uma vez**, tagueie com o SHA do commit e promova a mesma imagem por ambientes (staging → produção).
- **Registry**: GHCR, Docker Hub, ECR.
- **Environments** do GitHub: segredos por ambiente e **aprovação manual** para produção.
- **GitOps**: o estado desejado fica no Git e um agente (Argo CD, Flux) sincroniza o cluster.
- Tenha **rollback** fácil (reimplantar a tag anterior) e *smoke tests* pós-deploy.
- Prefira **OIDC** a chaves de longa duração para autenticar na nuvem.

## Exemplo: `.github/workflows/cd.yml`
```yaml
name: CD
on:
  push:
    branches: [main]

permissions:
  contents: read
  packages: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: docker/login-action@v3
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}
      - uses: docker/build-push-action@v6
        with:
          push: true
          tags: ghcr.io/${{ github.repository }}:${{ github.sha }}

  deploy-staging:
    needs: build
    runs-on: ubuntu-latest
    environment: staging
    steps:
      - run: echo "kubectl set image deploy/api api=ghcr.io/${{ github.repository }}:${{ github.sha }}"
      - run: curl --fail https://staging.exemplo.com/health

  deploy-prod:
    needs: deploy-staging
    runs-on: ubuntu-latest
    environment: production   # exige aprovação configurada
    steps:
      - run: echo "deploy da mesma imagem em produção"
```

## Exercício
1. Faça o pipeline publicar a imagem no GHCR com a tag do SHA.
2. Configure o environment `production` com revisor obrigatório e simule um rollback.

## Checklist
- [ ] Construo o artefato uma só vez
- [ ] Uso environments, segredos e aprovação
- [ ] Sei fazer rollback e smoke test
