# Aula 7 — Fluxos de trabalho (trunk-based, GitFlow)

**Duração:** ~20 min · **Módulo 7**

## Objetivo
Conhecer estratégias de ramificação e escolher a adequada para a equipe.

## Teoria
- **Trunk-based development**: todos integram frequentemente (ao menos diariamente) em `main`, com branches curtas (horas a poucos dias). Combina com **feature flags**, testes automatizados e CI/CD. Favorece entregas contínuas.
- **GitFlow**: branches permanentes `main` (produção) e `develop` (integração), mais `feature/*`, `release/*` e `hotfix/*`. Adequado a releases versionados e planejados (apps móveis, software instalado), porém mais pesado e com merges grandes.
- **GitHub Flow**: simples — `main` sempre implantável; branch por mudança → PR → revisão → merge → deploy.
- Escolha conforme: frequência de releases, maturidade de testes, tamanho do time e necessidade de manter várias versões.
- Convenção de nomes: `feature/`, `fix/`, `hotfix/`, `release/`. Versionamento: **SemVer** (`MAJOR.MINOR.PATCH`) com **tags**.

| Fluxo | Branches de vida longa | Ideal para |
|---|---|---|
| Trunk-based | só `main` | CI/CD, times maduros |
| GitHub Flow | só `main` | web/SaaS |
| GitFlow | `main` + `develop` | releases planejados |

## Exemplo
```bash
# GitHub Flow / trunk-based
git switch -c feature/busca-tarefas
git commit -am "Adiciona busca por prefixo"
git push -u origin feature/busca-tarefas   # PR curto e merge no mesmo dia

# GitFlow: hotfix
git switch main
git switch -c hotfix/1.0.1
git commit -am "Corrige cálculo de prazo"
git switch main && git merge --no-ff hotfix/1.0.1
git tag -a v1.0.1 -m "Hotfix 1.0.1"
git switch develop && git merge --no-ff hotfix/1.0.1
git push origin main develop --tags
```

## Exercício
1. Desenhe o grafo de branches de um release no GitFlow.
2. Escolha um fluxo para (a) um site com deploy diário e (b) um app móvel com release mensal; justifique.
3. Crie uma tag `v0.1.0` no seu projeto e envie ao GitHub.

## Checklist
- [ ] Diferencio trunk-based, GitHub Flow e GitFlow
- [ ] Justifico a escolha de um fluxo
- [ ] Uso tags e SemVer
