# Aula 8 — Documentação técnica e RFCs

**Duração:** ~25 min · **Módulo 21**

## Objetivo
Documentar decisões e propor mudanças relevantes com RFCs e ADRs.

## Teoria
### Tipos de documentação (Diátaxis)
- **Tutoriais** (aprender), **guias práticos** (how-to), **referência** (API) e **explicação** (conceitos/arquitetura).
- Mantenha perto do código (README, docs/ no repositório), revisada em PR; "docs as code".
- Diagramas simples (C4, Mermaid) valem mais que muito texto.

### RFC (Request for Comments)
Documento que propõe uma mudança significativa **antes** de implementar, abrindo para revisão da equipe. Evita retrabalho, registra o raciocínio e alinha pessoas.

### ADR (Architecture Decision Record)
Registro curto e imutável de **uma** decisão: contexto, decisão, consequências.

## Template: RFC
```markdown
# RFC-005: Notificações por e-mail
- Autor: @ana · Status: Rascunho | Em revisão | Aprovada | Rejeitada · Data: 2025-03-10
## Contexto e problema
Usuários perdem prazos; queremos lembretes.
## Objetivos / Não objetivos
Enviar lembretes 24h antes. Não inclui SMS.
## Proposta
Job diário (cron) → fila → serviço de e-mail. Diagrama: ...
## Alternativas consideradas
Push web (custo alto de adoção); polling no cliente.
## Impactos: segurança, privacidade (LGPD), custo, migração
## Plano de rollout e métricas de sucesso
## Questões em aberto
```

## Template: ADR
```markdown
# ADR-012: Usar PostgreSQL
Status: Aceita · Contexto: precisamos de transações e JSON.
Decisão: PostgreSQL 16 gerenciado.
Consequências: + maturidade; − custo operacional maior que SQLite.
```

## Exercício
1. Escreva o RFC da nova funcionalidade do seu projeto (projeto contínuo).
2. Registre 2 ADRs de decisões já tomadas (linguagem, banco, etc.).

## Checklist
- [ ] Sei quando uma RFC é necessária
- [ ] RFC com alternativas e impactos
- [ ] Decisões registradas em ADRs
