# Aula 6 — Estratégias de deploy: rolling, blue/green e canary

**Duração:** ~25 min · **Módulo 18**

## Objetivo
Escolher uma estratégia de deploy que reduza risco e downtime.

## Teoria
| Estratégia | Como funciona | Prós | Contras |
|-----------|---------------|------|---------|
| **Recreate** | Para tudo, sobe a nova versão | Simples | Downtime |
| **Rolling** | Substitui instâncias aos poucos | Sem downtime, sem custo extra | Duas versões coexistem; rollback lento |
| **Blue/green** | Dois ambientes; troca o tráfego de uma vez | Rollback instantâneo | Custo dobrado |
| **Canary** | Pequena % do tráfego vai à nova versão | Risco mínimo, valida com dados reais | Exige métricas e roteamento |

- Com versões coexistindo, **migrações de banco** devem ser compatíveis com ambas (padrão *expand/contract*: adicionar coluna → migrar código → remover antiga).
- Promova o canary (5% → 25% → 100%) só se métricas (erros, latência) estiverem saudáveis; reverta automaticamente caso contrário.
- Readiness probes evitam enviar tráfego a instâncias que não estão prontas.

## Exemplo: rolling update no Kubernetes
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: api
spec:
  replicas: 4
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 1
      maxSurge: 1
  selector:
    matchLabels: { app: api }
  template:
    metadata:
      labels: { app: api }
    spec:
      containers:
        - name: api
          image: ghcr.io/org/api:2.0.0
          readinessProbe:
            httpGet: { path: /health, port: 8000 }
```
Blue/green simples: dois Deployments (`api-blue`, `api-green`) e o Service troca o seletor:
```bash
kubectl patch service api -p '{"spec":{"selector":{"app":"api","versao":"green"}}}'
kubectl rollout undo deployment/api   # rollback do rolling
```

## Exercício
1. Faça um rolling update trocando a imagem e acompanhe com `kubectl rollout status`.
2. Defina critérios numéricos de promoção/rollback para um canary (taxa de erro, p99).

## Checklist
- [ ] Comparo as 4 estratégias
- [ ] Sei fazer rollback
- [ ] Planejo migrações compatíveis (expand/contract)
