# Aula 10 — Revisão e quiz do módulo

**Duração:** ~20 min · **Módulo 15**

## Resumo
- **Pirâmide**: muitos unitários, alguns de integração, poucos E2E; testes AAA e F.I.R.S.T.
- **Unitários** com pytest: fixtures, parametrização, bordas e erros.
- **Test doubles**: dummy, stub, fake, mock, spy; **DI** facilita o isolamento.
- **TDD**: Red → Green → Refactor.
- **Integração/API**: TestClient, estado isolado, 404/422/401.
- **E2E** com Playwright: locators por papel, sem `sleep`, jornadas críticas.
- **Cobertura** (≥ 80%), **mutation testing** e **property-based testing** (Hypothesis).
- **Contrato** (Pact/OpenAPI) e **carga** (k6, p95); **qualidade estática**: Ruff, mypy, pre-commit, CI e code review.

## Quiz
1. Por que a pirâmide tem poucos testes E2E no topo?
2. O que significa AAA?
3. Qual a diferença entre stub e mock?
4. O que é injeção de dependência e como ajuda nos testes?
5. Descreva o ciclo do TDD.
6. Por que 100% de cobertura não garante ausência de bugs?
7. O que indica um mutante sobrevivente?
8. O que é um teste de propriedade?
9. Por que usar p95/p99 em testes de carga em vez da média?
10. Qual o papel do pre-commit e do CI em relação ao linter?

## Gabarito resumido
1. São lentos, caros e frágeis; unitários dão feedback mais rápido.
2. Arrange, Act, Assert: preparar, executar, verificar.
3. Stub devolve respostas fixas; mock verifica interações (chamadas).
4. Receber dependências de fora; permite substituí-las por doubles.
5. Red (teste falha), Green (código mínimo), Refactor (melhorar com testes verdes).
6. Linhas executadas não implicam verificações corretas (ex.: teste sem `assert`).
7. Os testes não detectam uma alteração do código: teste fraco ou ausente.
8. Afirma uma propriedade válida para qualquer entrada, com dados gerados automaticamente.
9. A média esconde as caudas lentas que afetam usuários reais.
10. Pre-commit dá feedback local; o CI é a barreira obrigatória no PR.

## Entregável do módulo
Suíte de testes do projeto de tarefas com unitários e de integração no backend, testes no frontend, ao menos 2 E2E com Playwright, relatório de cobertura ≥ 80% (`--cov-fail-under=80`) e pipeline de CI executando lint, tipos e testes.

## Checklist final
- [ ] Pirâmide de testes aplicada ao projeto
- [ ] Cobertura mínima de 80% com relatório
- [ ] E2E das jornadas críticas
- [ ] Lint, formatação e tipos no CI
- [ ] Sei revisar um pull request
