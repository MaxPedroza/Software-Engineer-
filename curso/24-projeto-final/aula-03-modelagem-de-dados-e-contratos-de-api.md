# Aula 3 — Modelagem de dados e contratos de API

**Duração:** ~30 min · **Módulo 24 — Etapa 3**

## Objetivo
Projetar o modelo relacional e o contrato OpenAPI antes de implementar.

## Passo a passo
1. **Entidades e relações**: derive das histórias de usuário; desenhe o diagrama ER.
2. **Normalização** até a 3FN; defina chaves, `NOT NULL`, `UNIQUE`, `CHECK` e chaves estrangeiras.
3. **Índices** para as consultas mais frequentes (listagens, filtros, FKs).
4. **Migrations** versionadas (Alembic, Flyway, Prisma etc.), com seed de dados de exemplo.
5. **Contrato OpenAPI 3**: recursos, métodos, status codes, schemas, erros padronizados, paginação e autenticação (JWT).
6. **Versionamento** (`/v1`) e idempotência para operações críticas (`Idempotency-Key`).

### Exemplo de migration
```sql
CREATE TABLE tarefas (
  id BIGSERIAL PRIMARY KEY,
  usuario_id BIGINT NOT NULL REFERENCES usuarios(id),
  titulo VARCHAR(120) NOT NULL,
  status VARCHAR(12) NOT NULL DEFAULT 'aberta' CHECK (status IN ('aberta','feita')),
  prazo DATE,
  criada_em TIMESTAMPTZ NOT NULL DEFAULT now()
);
CREATE INDEX idx_tarefas_usuario_status ON tarefas (usuario_id, status);
```

### Exemplo de contrato
```yaml
/v1/tarefas:
  get:
    parameters: [{name: page, in: query}, {name: size, in: query}]
    responses: {"200": {description: Lista paginada}, "401": {description: Não autenticado}}
```

## Entregáveis
- `docs/modelo-er.md` (diagrama) e pasta `migrations/`
- `openapi.yaml` validado por linter (ex.: Spectral)

## Critérios de aceite
- [ ] Migrations rodam do zero em banco vazio
- [ ] Toda história Must é coberta por ao menos um endpoint
- [ ] Erros seguem um formato único (ex.: RFC 7807)
- [ ] O contrato é validado sem avisos críticos
