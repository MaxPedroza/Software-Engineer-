# Aula 10 — Revisão e quiz do módulo

**Duração:** ~25 min · **Módulo 19**

## Resumo
- IaaS/PaaS/SaaS: quanto mais alto o nível, menor sua responsabilidade; dados e acessos são sempre seus.
- Blocos essenciais: computação, VPC (sub-redes privadas), storage e **IAM com menor privilégio**.
- **Serverless**: escala a zero, cold start, funções stateless e idempotentes.
- **Observabilidade**: logs estruturados (com `trace_id`), métricas (RED/Golden Signals) e traces (OTel).
- **SLO** e **error budget** guiam o equilíbrio entre velocidade e confiabilidade; alertas por burn rate.
- Incidentes: mitigar primeiro, papéis claros, post-mortem blameless com ações.
- **FinOps**: tags, right-sizing, reservas/spot, planejamento de capacidade.

## Quiz
1. Em um PaaS, o que continua sendo responsabilidade do cliente?
2. Por que o banco de dados deve ficar em sub-rede privada?
3. O que é cold start?
4. Cite 4 campos úteis em um log estruturado.
5. Qual função do PromQL se aplica a um Counter e por quê?
6. O que é o header `traceparent`?
7. Qual o error budget mensal de um SLO de 99,9%?
8. Qual a diferença entre SLO e SLA?
9. Qual a prioridade no início de um incidente: achar a causa raiz ou mitigar?
10. Cite duas formas de reduzir custo de cloud.

## Gabarito resumido
1. Código, dados, configuração, identidades e acessos.
2. Para não ficar exposto à internet; só a aplicação o acessa.
3. Latência extra na primeira invocação, ao iniciar o ambiente da função.
4. `timestamp`, `level`, `service`, `message`, `trace_id`, `request_id`.
5. `rate()`, pois Counter só cresce e interessa a taxa por segundo.
6. Header W3C que propaga o contexto do trace entre serviços.
7. ≈ 43,2 minutos.
8. SLO é meta interna; SLA é contrato com consequências, geralmente mais frouxo.
9. Mitigar (rollback, desligar flag); a causa raiz vem depois.
10. Right-sizing, reservas/spot, desligar ambientes ociosos, ciclo de vida de storage.

## Entregável do módulo
**Dashboard operacional** (Grafana com painéis RED, saturação e SLO/error budget) e **post-mortem blameless** de um incidente simulado, com linha do tempo, causa raiz e ações. No projeto contínuo, publique o sistema na nuvem com monitoramento, alertas e SLOs.

## Checklist final
- [ ] Sei o modelo de responsabilidade compartilhada
- [ ] Sistema emite logs, métricas e traces
- [ ] SLOs e alertas por burn rate definidos
- [ ] Dashboard e post-mortem entregues
