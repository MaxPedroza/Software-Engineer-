# Aula 8 — Gestão de incidentes, on-call e post-mortems

**Duração:** ~25 min · **Módulo 19**

## Objetivo
Responder a incidentes de forma organizada e aprender com eles sem culpar pessoas.

## Teoria
- **Incidente**: evento que degrada o serviço além do aceitável. Prioridade por severidade (SEV1 crítico → SEV4 menor).
- **Papéis**: **Incident Commander** (coordena e decide), **Comunicações** (status page, stakeholders), **Operações/responsáveis técnicos** (investigam), **Escriba** (linha do tempo).
- **Fluxo**: detectar → triar → **mitigar primeiro** (rollback, desligar flag, escalar) → resolver → post-mortem. Causa raiz vem depois da mitigação.
- **On-call**: rodízio sustentável, runbooks para cada alerta, escalonamento, hand-off. Alertas devem ser **acionáveis**; barulho causa fadiga.
- Métricas: MTTD (detecção), MTTA (reconhecimento), **MTTR** (resolução).
- **Post-mortem sem culpa (blameless)**: foca em sistemas e processos; produz ações com dono e prazo. Técnicas: 5 porquês, fatores contribuintes.

## Exemplo: modelo de post-mortem
```markdown
# Post-mortem: API de pedidos indisponível (SEV1)
**Data:** 2026-03-01 · **Duração:** 47 min · **Autores:** equipe pedidos

## Resumo
Pico de erros 5xx após deploy 2.4.0 por migração que travou a tabela `pedidos`.

## Impacto
~12% das requisições falharam; 3.200 pedidos afetados. Budget mensal consumido: 109%.

## Linha do tempo (UTC)
- 14:02 Deploy 2.4.0
- 14:09 Alerta TaxaDeErrosAlta dispara (MTTD 7 min)
- 14:15 IC designado; suspeita do deploy
- 14:31 Rollback concluído
- 14:49 Erros normalizados

## Causa raiz e fatores contribuintes
Migração com lock longo; sem teste de carga em staging; rollback manual demorado.

## O que deu certo / errado
...

## Ações
| Ação | Dono | Prazo |
|------|------|-------|
| Migrações online (expand/contract) | Ana | 15/03 |
| Rollback automático por canary | Bruno | 30/03 |
```

## Exercício
1. Simule um incidente (derrube o banco do Compose), cumpra os papéis em equipe ou sozinho, registrando a linha do tempo.
2. Escreva o post-mortem blameless usando o modelo e 5 porquês.

## Checklist
- [ ] Conheço papéis e fluxo de incidente
- [ ] Priorizo mitigar antes de investigar
- [ ] Escrevo post-mortem blameless com ações
