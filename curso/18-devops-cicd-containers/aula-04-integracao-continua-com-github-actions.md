# Aula 4 — Integração contínua com GitHub Actions

**Duração:** ~25 min · **Módulo 18**

## Objetivo
Criar um workflow de CI que roda lint e testes a cada push e pull request.

## Teoria
- **Workflow**: YAML em `.github/workflows/`. Contém **eventos** (`on`), **jobs** (rodam em paralelo por padrão) e **steps**.
- **Runner**: máquina que executa o job (`ubuntu-latest`).
- **Actions**: passos reutilizáveis (`actions/checkout`, `actions/setup-python`). Fixe versões.
- **matrix**: roda o job em várias versões.
- **cache** acelera dependências; **artifacts** guardam resultados.
- **secrets** guardam credenciais (`${{ secrets.NOME }}`); use `permissions` mínimas.
- Proteja a branch `main`: exija CI verde antes do merge.

## Exemplo: `.github/workflows/ci.yml`
```yaml
name: CI
on:
  push:
    branches: [main]
  pull_request:

permissions:
  contents: read

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python: ["3.11", "3.12"]
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: ${{ matrix.python }}
          cache: pip
      - run: pip install -r requirements.txt
      - run: ruff check .
      - run: pytest --cov=app --cov-fail-under=80
      - uses: actions/upload-artifact@v4
        if: always()
        with:
          name: cobertura-${{ matrix.python }}
          path: .coverage
```

## Exercício
1. Adicione o workflow ao projeto, abra um PR com um teste quebrado e veja o CI falhar; corrija.
2. Configure proteção de branch exigindo o job `test`.

## Checklist
- [ ] Sei a estrutura de um workflow
- [ ] Uso matrix, cache e artifacts
- [ ] Bloqueio merge sem CI verde
