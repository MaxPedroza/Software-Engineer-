# Aula 4 — Implementação do backend

**Duração:** ~40 min · **Módulo 24 — Etapa 4**

## Objetivo
Implementar a API seguindo o contrato, com camadas claras, validação e autenticação.

## Passo a passo
1. **Estrutura em camadas**: `routes/controllers` → `services` (regras de negócio) → `repositories` (acesso a dados).
2. **Configuração** por variáveis de ambiente (12-factor); nunca versionar segredos (`.env.example`).
3. **Autenticação**: cadastro/login, senha com hash (argon2/bcrypt), JWT com expiração; autorização por dono do recurso.
4. **Validação** de entrada (schemas) e tratamento global de erros no formato definido.
5. **Endpoints Must** primeiro, um por PR pequeno, com revisão.
6. **Paginação, filtros e ordenação**; health check em `/health`.
7. **Logs estruturados** (JSON) com request id.

### Esqueleto (FastAPI)
```python
@router.post("/v1/tarefas", status_code=201)
def criar(dados: TarefaIn, user=Depends(usuario_atual), svc: TarefaService = Depends()):
    return svc.criar(user.id, dados)
```

### Fluxo por história
`issue → branch feature/us-01 → código + teste → PR → revisão → merge na main`

## Entregáveis
- API rodando localmente e em Docker, aderente ao `openapi.yaml`
- `.env.example`, `Dockerfile` e `docker-compose.yml`
- PRs vinculados às issues do backlog

## Critérios de aceite
- [ ] Todos os endpoints Must implementados e conforme o contrato
- [ ] Nenhum segredo no repositório; senhas com hash
- [ ] Usuário não acessa dados de outro usuário
- [ ] `/health` responde 200 e erros seguem o formato padrão
