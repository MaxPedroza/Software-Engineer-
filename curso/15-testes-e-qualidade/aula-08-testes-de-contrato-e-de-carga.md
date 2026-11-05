# Aula 8 — Testes de contrato e de carga

**Duração:** ~20 min · **Módulo 15**

## Objetivo
Garantir compatibilidade entre serviços e medir o comportamento sob carga.

## Teoria
### Testes de contrato
- Verificam que **consumidor** e **provedor** de uma API concordam sobre formato de requisição/resposta, sem subir tudo (alternativa barata a E2E em microsserviços).
- **Consumer-driven contracts** (Pact): o consumidor define o que espera; o provedor valida o contrato em seu CI.
- Em APIs REST/FastAPI, o esquema **OpenAPI** pode servir de contrato; ferramentas como Schemathesis geram testes a partir dele.

### Testes de carga
- **Carga**: tráfego esperado. **Estresse**: acima do limite. **Pico (spike)**, **resistência (soak)**: longa duração.
- Métricas: **latência** (p50, p95, p99), **vazão** (req/s), **taxa de erro**. Prefira percentis à média.
- Ferramentas: **k6**, Locust, JMeter. Defina **thresholds** (SLOs) que quebram o build.
- Teste em ambiente parecido com produção; nunca contra produção sem planejamento.

## Exemplo
```python
# test_contrato.py — valida o formato da resposta (schema)
from pydantic import BaseModel, ValidationError
import requests

class TarefaContrato(BaseModel):
    id: int
    titulo: str
    feita: bool

def test_contrato_get_tarefa():
    r = requests.get("http://localhost:8000/tarefas/1", timeout=5)
    assert r.status_code == 200
    TarefaContrato.model_validate(r.json())   # falha se o contrato quebrar
```
```js
// carga.js — rode com: k6 run carga.js
import http from 'k6/http';
import { check, sleep } from 'k6';

export const options = {
  stages: [
    { duration: '30s', target: 20 },
    { duration: '1m', target: 20 },
    { duration: '10s', target: 0 },
  ],
  thresholds: {
    http_req_failed: ['rate<0.01'],
    http_req_duration: ['p(95)<300'],
  },
};

export default function () {
  const r = http.get('http://localhost:8000/tarefas');
  check(r, { 'status 200': (res) => res.status === 200 });
  sleep(1);
}
```

## Exercício
1. Escreva um teste de contrato para `POST /tarefas` (corpo e status).
2. Rode o k6 contra a API e registre p95 e taxa de erro.
3. Aumente o alvo para 200 usuários virtuais: onde o sistema degrada primeiro?

## Checklist
- [ ] Explico testes de contrato e seu valor
- [ ] Diferencio carga, estresse e pico
- [ ] Analiso p95/p99 em vez de só a média
