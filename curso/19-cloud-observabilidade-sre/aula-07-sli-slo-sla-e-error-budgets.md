# Aula 7 — SLI, SLO, SLA e error budgets

**Duração:** ~25 min · **Módulo 19**

## Objetivo
Definir metas de confiabilidade mensuráveis e usar o error budget para decisões.

## Teoria
- **SLI** (indicador): medida do nível de serviço, em geral razão de eventos bons/total. Ex.: % de requisições com status < 500 e latência < 300 ms.
- **SLO** (objetivo): meta para o SLI em uma janela. Ex.: 99,9% em 30 dias.
- **SLA** (acordo): contrato com consequências (créditos) — mais frouxo que o SLO.
- **Error budget** = 100% − SLO. Com 99,9%: 0,1% ≈ **43,2 min/mês** de indisponibilidade.
- Budget sobrando → pode lançar mais rápido; esgotado → congela features e foca em confiabilidade.
- 100% é a meta errada: custa caro e impede evolução.
- **Alertas por burn rate**: alerte quando o budget é consumido rápido demais (ex.: 14,4× em 1 h).

| SLO | Indisponibilidade/mês |
|-----|----------------------|
| 99% | ~7,2 h |
| 99,9% | ~43 min |
| 99,99% | ~4,3 min |

## Exemplo: SLI e burn rate no Prometheus
```promql
# SLI de disponibilidade em 30 dias
sum(rate(http_requests_total{status!~"5.."}[30d])) / sum(rate(http_requests_total[30d]))
```
```yaml
- alert: ErrorBudgetBurnRapido
  expr: |
    (sum(rate(http_requests_total{status=~"5.."}[1h])) / sum(rate(http_requests_total[1h]))) > (14.4 * 0.001)
  for: 2m
  labels: { severity: page }
```
Cálculo:
```python
slo = 0.999
minutos_mes = 30 * 24 * 60
print(f"Budget: {(1 - slo) * minutos_mes:.1f} min")        # 43.2
print(f"Consumido com 20 min fora: {20 / ((1 - slo) * minutos_mes):.0%}")  # 46%
```

## Exercício
1. Defina 2 SLIs e SLOs (disponibilidade e latência) para o projeto e calcule o budget mensal.
2. Se 30 minutos de indisponibilidade ocorreram no mês com SLO 99,9%, qual a política a seguir?

## Checklist
- [ ] Diferencio SLI, SLO e SLA
- [ ] Calculo error budgets
- [ ] Sei alertar por burn rate
