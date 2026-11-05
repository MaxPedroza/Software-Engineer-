# Aula 8 — Observabilidade, segurança e revisão final

**Duração:** ~40 min · **Módulo 24 — Etapa 8**

## Objetivo
Tornar o sistema observável e seguro, e fazer uma revisão final antes da entrega.

## Passo a passo
1. **Logs** estruturados com request id; sem dados pessoais ou segredos.
2. **Métricas** (RED): taxa de requisições, erros e duração (p50/p95), expostas via Prometheus/OpenTelemetry.
3. **Tracing** distribuído de ao menos uma requisição ponta a ponta.
4. **Dashboard e alertas**: ex.: erro 5xx > 2% por 5 min; p95 > 300 ms.
5. **Segurança (OWASP Top 10)**: validação de entrada, consultas parametrizadas, controle de acesso, rate limiting, CORS restrito, cabeçalhos de segurança, dependências atualizadas.
6. **Segredos e acesso**: privilégio mínimo, rotação, 2FA nas contas.
7. **Revisão final**: threat model simples (STRIDE), revisão de código completa, dívida técnica registrada.

### Exemplo de alerta (Prometheus)
```yaml
- alert: AltaTaxaDeErros
  expr: sum(rate(http_requests_total{status=~"5.."}[5m])) / sum(rate(http_requests_total[5m])) > 0.02
  for: 5m
```

### Checklist de segurança
```text
[ ] Senhas com hash forte; JWT com expiração
[ ] Nenhum segredo no Git (rode gitleaks)
[ ] Rate limit no login
[ ] Scan de dependências e imagem sem críticas
[ ] Autorização testada (IDOR)
```

## Entregáveis
- Dashboard (print) e regras de alerta no repositório
- `docs/seguranca.md` com threat model e resultados dos scans
- Lista de dívida técnica e riscos residuais

## Critérios de aceite
- [ ] É possível rastrear um erro de produção pelos logs/trace
- [ ] Pelo menos 2 alertas funcionam (teste forçando falha)
- [ ] Sem vulnerabilidades críticas abertas
