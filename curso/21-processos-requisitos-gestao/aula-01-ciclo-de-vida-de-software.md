# Aula 1 — Ciclo de vida de software (cascata, iterativo, ágil)

**Duração:** ~20 min · **Módulo 21**

## Objetivo
Comparar modelos de ciclo de vida e escolher o adequado ao contexto.

## Teoria
Fases comuns: requisitos → design → implementação → testes → implantação → manutenção.

| Modelo | Como funciona | Vantagens | Riscos |
|--------|---------------|-----------|--------|
| **Cascata** | Fases sequenciais, cada uma só começa quando a anterior termina | Previsível, bem documentado | Feedback tardio, mudanças caras |
| **Iterativo/incremental** | Entregas em ciclos, refinando o produto | Riscos reduzidos cedo | Exige arquitetura que suporte evolução |
| **Espiral** | Iterações guiadas por análise de risco | Bom para projetos de alto risco | Complexo de gerir |
| **Ágil** | Ciclos curtos, colaboração, adaptação contínua | Feedback rápido, valor frequente | Requer disciplina e envolvimento do cliente |

### Manifesto Ágil (2001) — valores
Indivíduos e interações > processos e ferramentas; software funcionando > documentação abrangente; colaboração com o cliente > negociação de contratos; responder a mudanças > seguir um plano.

### Quando usar
- Requisitos estáveis e regulados (ex.: software embarcado crítico): cascata ou híbrido.
- Requisitos incertos, produto em descoberta: ágil.
- **DevOps** complementa o ágil: entrega e operação contínuas (módulo de CI/CD).

## Exercício
1. Escolha 3 projetos (ex.: app de startup, sistema bancário regulado, software de foguete) e indique o modelo mais adequado, justificando.
2. Em uma tabela, compare o custo de mudar um requisito no início e no fim para cascata e ágil.

## Checklist
- [ ] Descrevo cascata, iterativo e ágil
- [ ] Cito os 4 valores do Manifesto Ágil
- [ ] Escolho modelo conforme o contexto
