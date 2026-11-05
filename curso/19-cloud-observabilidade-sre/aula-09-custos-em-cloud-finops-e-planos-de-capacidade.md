# Aula 9 — Custos em cloud (FinOps) e planos de capacidade

**Duração:** ~20 min · **Módulo 19**

## Objetivo
Controlar custos em nuvem e planejar capacidade com base em dados.

## Teoria
- **FinOps**: prática que une engenharia, finanças e negócio para gastar de forma eficiente. Fases: **informar** (visibilidade), **otimizar**, **operar**.
- **Tags/labels** obrigatórias (`time`, `ambiente`, `serviço`) para rateio de custos.
- **Alavancas de economia**:
  - *Right-sizing*: ajustar instâncias ao uso real.
  - **Modelos de compra**: sob demanda, **reservas/Savings Plans** (carga estável, até ~70% de desconto), **spot** (tolerante a interrupção).
  - Desligar ambientes fora do horário; ciclo de vida em storage (S3 → classes frias).
  - Custos ocultos: **transferência de dados (egress)**, NAT gateways, logs e métricas de alta cardinalidade.
- **Orçamentos e alertas** de gasto; detecção de anomalias.
- **Planejamento de capacidade**: medir uso atual, projetar crescimento, manter margem (headroom 30–50%), fazer testes de carga e usar autoscaling com limites.

## Exemplo: estimativa e orçamento
```python
instancias, preco_hora = 6, 0.096        # sob demanda
horas_mes = 730
sob_demanda = instancias * preco_hora * horas_mes
reservado = sob_demanda * 0.6            # ~40% de desconto
print(f"Sob demanda: US$ {sob_demanda:.0f} | Reservado: US$ {reservado:.0f}")

# capacidade
qps_atual, crescimento_mensal, qps_por_instancia = 800, 0.10, 250
for m in (0, 3, 6, 12):
    qps = qps_atual * (1 + crescimento_mensal) ** m
    n = -(-qps * 1.4 // qps_por_instancia)  # 40% de margem
    print(f"mês {m}: {qps:.0f} QPS -> {int(n)} instâncias")
```
Orçamento com Terraform:
```hcl
resource "aws_budgets_budget" "mensal" {
  name         = "orcamento-mensal"
  budget_type  = "COST"
  limit_amount = "500"
  limit_unit   = "USD"
  time_unit    = "MONTHLY"
  notification {
    comparison_operator        = "GREATER_THAN"
    threshold                  = 80
    threshold_type             = "PERCENTAGE"
    notification_type          = "ACTUAL"
    subscriber_email_addresses = ["time@exemplo.com"]
  }
}
```

## Exercício
1. Estime o custo mensal da arquitetura do projeto (compute, banco, storage, egress) com a calculadora do provedor.
2. Projete a capacidade para 12 meses com crescimento de 10% ao mês e proponha 3 economias.

## Checklist
- [ ] Uso tags para rateio de custos
- [ ] Conheço reservas, spot e right-sizing
- [ ] Planejo capacidade com margem
