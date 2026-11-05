# Aula 9 — Linters, formatadores, análise estática e revisão de código

**Duração:** ~20 min · **Módulo 15**

## Objetivo
Automatizar verificações de qualidade e conduzir boas revisões de código.

## Teoria
- **Formatador** (Black, Prettier, `ruff format`): padroniza estilo automaticamente, encerrando discussões sobre espaços.
- **Linter** (Ruff, Flake8, ESLint): detecta erros e más práticas (variável não usada, import faltando).
- **Análise estática de tipos**: `mypy`/`pyright` (Python), `tsc` (TypeScript) pegam erros de tipo sem executar.
- **SAST/segurança**: Bandit, CodeQL, `npm audit`, Dependabot.
- **pre-commit**: roda as verificações antes de cada commit; o **CI** repete como barreira final (PR só entra se passar).
- **Revisão de código** (pull request):
  - PRs pequenos e focados, com descrição do porquê.
  - Revisor avalia corretude, legibilidade, testes, segurança; comenta o código, não a pessoa.
  - Distinga bloqueios de sugestões (prefixo `nit:`).
  - Automatize o que a máquina verifica; humanos revisam design.

## Exemplo
```toml
# pyproject.toml
[tool.ruff]
line-length = 100
[tool.ruff.lint]
select = ["E", "F", "I", "B", "UP"]
[tool.mypy]
strict = true
```
```yaml
# .pre-commit-config.yaml
repos:
  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.6.9
    hooks:
      - id: ruff
        args: [--fix]
      - id: ruff-format
```
```yaml
# .github/workflows/qualidade.yml
name: qualidade
on: [pull_request]
jobs:
  checks:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with: { python-version: "3.12" }
      - run: pip install ruff mypy pytest pytest-cov
      - run: ruff check . && ruff format --check .
      - run: mypy src
      - run: pytest --cov=src --cov-fail-under=80
```

## Exercício
1. Configure Ruff e mypy no projeto e corrija os avisos.
2. Instale o `pre-commit` (`pre-commit install`) e tente commitar código mal formatado.
3. Revise um PR de um colega usando uma lista de 5 critérios.

## Checklist
- [ ] Configuro formatador, linter e verificador de tipos
- [ ] Automatizo as verificações no CI
- [ ] Reviso código de forma construtiva
