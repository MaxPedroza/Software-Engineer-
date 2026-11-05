# Aula 6 — Métricas de engenharia (DORA, lead time)

**Duração:** ~20 min · **Módulo 21**

## Objetivo
Medir a entrega de software com métricas que orientam melhorias, não punições.

## Teoria
### Métricas DORA
| Métrica | Mede | Pergunta |
|---------|------|----------|
| **Lead time for changes** | Tempo do commit até produção | Quão rápido entregamos? |
| **Deployment frequency** | Frequência de deploys | Com que ritmo? |
| **Change failure rate** | % de deploys que causam falha | Quão estável? |
| **Time to restore (MTTR)** | Tempo para recuperar de falha | Quão resiliente? |

As duas primeiras medem **velocidade**, as duas últimas **estabilidade**; times de alto desempenho melhoram ambas. (Versões recentes do DORA renomearam algumas, ex.: *failed deployment recovery time*.)

### Outras métricas
- **Cycle time** (início do trabalho → pronto), **WIP**, **throughput**.
- Tempo de revisão de PR, cobertura de testes, testes instáveis (*flaky*).
- **SPACE** e DevEx: satisfação e fluxo do desenvolvedor.

### Cuidados (Lei de Goodhart)
"Quando uma medida vira meta, deixa de ser boa medida." Evite medir linhas de código, commits ou velocidade individual. Meça equipes e tendências.

## Exemplo: lead time
```python
from datetime import datetime
deploys = [("2025-03-01T10:00", "2025-03-02T15:00"),   # commit, produção
           ("2025-03-03T09:00", "2025-03-03T17:00")]
fmt = "%Y-%m-%dT%H:%M"
horas = [(datetime.strptime(d, fmt) - datetime.strptime(c, fmt)).total_seconds() / 3600
         for c, d in deploys]
print(f"Lead time médio: {sum(horas)/len(horas):.1f} h")
```

## Exercício
1. Calcule as 4 métricas DORA do seu projeto no último mês (use o histórico de PRs/deploys).
2. Escolha uma delas e proponha uma ação para melhorá-la.

## Checklist
- [ ] Cito e defino as 4 métricas DORA
- [ ] Diferencio lead time e cycle time
- [ ] Evito métricas individuais de vaidade
