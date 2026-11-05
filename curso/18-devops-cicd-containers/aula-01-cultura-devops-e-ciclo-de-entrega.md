# Aula 1 — Cultura DevOps e ciclo de entrega

**Duração:** ~20 min · **Módulo 18**

## Objetivo
Entender a cultura DevOps, o ciclo de entrega e as métricas que medem seu desempenho.

## Teoria
- **DevOps** une desenvolvimento e operação: responsabilidade compartilhada ("you build it, you run it"), automação, feedback rápido e melhoria contínua.
- **Ciclo**: planejar → codificar → build → testar → release → deploy → operar → monitorar → (volta).
- Princípios (CALMS): **C**ultura, **A**utomação, **L**ean, **M**edição, **S**compartilhamento.
- **Integração contínua (CI)**: integrar ao tronco várias vezes ao dia com build e testes automáticos.
- **Entrega contínua**: todo commit aprovado está *pronto* para produção. **Implantação contínua**: vai sozinho para produção.

### Métricas DORA
| Métrica | Mede |
|---------|------|
| Frequência de deploy | Vazão |
| Lead time para mudanças | Do commit à produção |
| Taxa de falha de mudanças | Qualidade |
| Tempo de restauração (MTTR) | Resiliência |

Lotes pequenos e frequentes reduzem risco. Evite silos "dev joga código por cima do muro".

## Exemplo: calculando lead time
```python
from datetime import datetime

deploys = [  # (commit, produção)
    ("2026-03-01T10:00", "2026-03-01T15:30"),
    ("2026-03-02T09:00", "2026-03-03T11:00"),
    ("2026-03-04T14:00", "2026-03-04T16:00"),
]
f = "%Y-%m-%dT%H:%M"
horas = [(datetime.strptime(b, f) - datetime.strptime(a, f)).total_seconds() / 3600
         for a, b in deploys]
print(f"Lead time médio: {sum(horas)/len(horas):.1f} h")
```

## Exercício
1. Desenhe o fluxo atual do seu projeto, do commit à produção, e marque as etapas manuais.
2. Calcule as 4 métricas DORA dos últimos 10 merges do repositório (aproximação é aceitável).

## Checklist
- [ ] Explico a cultura DevOps
- [ ] Diferencio entrega e implantação contínuas
- [ ] Conheço as métricas DORA
