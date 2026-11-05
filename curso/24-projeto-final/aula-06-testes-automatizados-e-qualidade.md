# Aula 6 — Testes automatizados e qualidade

**Duração:** ~35 min · **Módulo 24 — Etapa 6**

## Objetivo
Criar uma suíte de testes em camadas e gates de qualidade automatizados.

## Passo a passo
1. **Pirâmide**: muitos testes unitários, alguns de integração (API + banco real em contêiner), poucos E2E.
2. **Unitários** das regras de negócio (services), com mocks apenas nas bordas.
3. **Integração**: endpoints com banco de teste descartável (Testcontainers/docker compose).
4. **Contrato**: valide respostas contra o `openapi.yaml`.
5. **E2E** (Playwright/Cypress) para 2–3 jornadas críticas.
6. **Qualidade estática**: linter, formatador, tipagem, análise de dependências vulneráveis.
7. **Cobertura** mínima ≥ 80% nas regras de negócio; teste de carga simples (k6) no endpoint crítico.

### Exemplo (pytest)
```python
def test_usuario_nao_ve_tarefa_de_outro(client, token_ana, tarefa_de_bia):
    r = client.get(f"/v1/tarefas/{tarefa_de_bia.id}", headers=token_ana)
    assert r.status_code == 404
```

### Exemplo k6
```js
export const options = { vus: 20, duration: '30s', thresholds: { http_req_duration: ['p(95)<300'] } };
```

## Entregáveis
- Pastas `tests/unit`, `tests/integration`, `tests/e2e`
- Relatório de cobertura e script `make test`
- Resultado do teste de carga em `docs/`

## Critérios de aceite
- [ ] Cobertura ≥ 80% e todos os testes passam do zero
- [ ] Há teste para cada regra de autorização
- [ ] E2E cobre login e a jornada principal
- [ ] Lint e checagem de tipos sem erros
