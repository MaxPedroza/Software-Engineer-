# Aula 2 — Arquitetura e ADRs

**Duração:** ~30 min · **Módulo 24 — Etapa 2**

## Objetivo
Desenhar a arquitetura do sistema e registrar as decisões importantes em ADRs.

## Passo a passo
1. **Escolha o estilo**: comece por um monólito modular, salvo motivo forte para microsserviços.
2. **Diagrama C4**: nível 1 (contexto) e nível 2 (contêineres): cliente, API, banco, cache, fila, serviços externos.
3. **Tecnologias**: linguagem, framework, banco, hospedagem; justifique cada uma frente aos requisitos não funcionais.
4. **Estrutura do repositório** e convenções (branches, commits, lint).
5. **Escreva 3+ ADRs** para decisões difíceis de reverter (banco, autenticação, estilo de arquitetura, deploy).

### Template de ADR (`docs/adr/0001-banco-de-dados.md`)
```markdown
# ADR 0001 — Usar PostgreSQL como banco principal
Status: Aceita · Data: 2026-01-10
## Contexto
Dados relacionais, transações e consultas com joins; time conhece SQL.
## Decisão
Usaremos PostgreSQL 16 gerenciado.
## Alternativas consideradas
MongoDB (modelo relacional é mais adequado aos dados), SQLite (pouca concorrência de escrita).
## Consequências
+ ACID, ecossistema maduro. − Escala vertical primeiro; exige migrations.
```

## Entregáveis
- `docs/architecture.md` com diagramas C4 (Mermaid ou imagem)
- Pasta `docs/adr/` com pelo menos 3 ADRs
- Esqueleto do repositório rodando (`docker compose up` sobe API vazia e banco)

## Critérios de aceite
- [ ] Diagramas mostram todos os componentes e fluxos principais
- [ ] Cada ADR tem contexto, decisão, alternativas e consequências
- [ ] A arquitetura atende aos requisitos não funcionais da etapa 1
- [ ] Esqueleto sobe com um único comando
