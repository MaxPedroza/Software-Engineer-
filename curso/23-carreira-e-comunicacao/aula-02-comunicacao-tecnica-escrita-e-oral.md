# Aula 2 — Comunicação técnica escrita e oral

**Duração:** ~20 min · **Módulo 23**

## Objetivo
Comunicar ideias técnicas com clareza para públicos técnicos e não técnicos.

## Teoria
- **Conheça o público**: o que ele já sabe? O que precisa decidir?
- **Pirâmide invertida**: conclusão/pedido primeiro, detalhes depois.
- **Escrita**: frases curtas, voz ativa, listas, termos consistentes, links para contexto.
- **Oral**: estrutura *contexto → problema → proposta → próximos passos*; pare para perguntas.
- **Assíncrono primeiro**: mensagens autossuficientes evitam reuniões.
- Documentos úteis: RFC/design doc, ADR, postmortem, README, descrição de PR.

### Template de mensagem (Slack/e-mail)
```text
Assunto: [Decisão] Migrar fila de jobs para SQS até 30/11

Resumo: propomos migrar para SQS para reduzir falhas de jobs (hoje 3%/semana).
Impacto: 2 dias de trabalho; sem downtime.
Preciso de: aprovação até sexta.
Detalhes: <link para o design doc>
```

### Template de descrição de PR
```text
O quê: adiciona paginação em /tarefas
Por quê: listagem estourava timeout com +10k itens
Como testar: GET /tarefas?page=2&size=20
Riscos: clientes antigos sem parâmetros recebem page=1
```

## Exercício
1. Reescreva este texto ruim em até 5 linhas: "Oi, tava vendo aqui o sistema e acho que talvez a gente podia ver o banco porque às vezes fica lento...".
2. Explique "cache" em 30 segundos para uma pessoa de negócios, sem jargão.

## Checklist
- [ ] Começo pela conclusão
- [ ] Adapto a linguagem ao público
- [ ] Escrevo PRs e mensagens autossuficientes
