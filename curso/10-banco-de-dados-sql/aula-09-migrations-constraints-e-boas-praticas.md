# Aula 9 — Migrations, constraints e boas práticas

**Duração:** ~25 min · **Módulo 10**

## Objetivo
Evoluir o esquema com migrations versionadas e proteger a integridade com constraints.

## Teoria
- **Migration**: script versionado que altera o esquema (com *up* e, quando possível, *down*). Fica no Git e roda em ordem em todos os ambientes. Ferramentas: Flyway, Liquibase, Alembic, Prisma, node-pg-migrate.
- **Nunca edite** uma migration já aplicada: crie uma nova.
- **Constraints**: `PRIMARY KEY`, `FOREIGN KEY` (com `ON DELETE CASCADE/RESTRICT/SET NULL`), `NOT NULL`, `UNIQUE`, `CHECK`, `DEFAULT`.
- Boas práticas:
  - tipos corretos (`NUMERIC` para dinheiro, `TIMESTAMPTZ` para datas);
  - nomes consistentes (snake_case, plural nas tabelas);
  - indexe as FKs;
  - mudanças em produção em passos pequenos e compatíveis (adicionar coluna nullable → preencher → `NOT NULL`);
  - consultas parametrizadas; menor privilégio para o usuário da aplicação;
  - backups testados.

## Exemplo
`migrations/001_criar_tabelas.sql`
```sql
BEGIN;
CREATE TABLE usuarios (
  id    SERIAL PRIMARY KEY,
  nome  TEXT NOT NULL,
  email TEXT NOT NULL UNIQUE
);
CREATE TABLE projetos (
  id         SERIAL PRIMARY KEY,
  usuario_id INT NOT NULL REFERENCES usuarios(id) ON DELETE CASCADE,
  nome       TEXT NOT NULL
);
CREATE TABLE tarefas (
  id         SERIAL PRIMARY KEY,
  projeto_id INT NOT NULL REFERENCES projetos(id) ON DELETE CASCADE,
  titulo     TEXT NOT NULL CHECK (length(trim(titulo)) > 0),
  concluida  BOOLEAN NOT NULL DEFAULT FALSE,
  criada_em  TIMESTAMPTZ NOT NULL DEFAULT now()
);
CREATE INDEX idx_projetos_usuario ON projetos (usuario_id);
CREATE INDEX idx_tarefas_projeto  ON tarefas (projeto_id);
COMMIT;
```
`migrations/002_adicionar_prazo.sql`
```sql
ALTER TABLE tarefas ADD COLUMN prazo DATE;
```
`migrations/002_adicionar_prazo.down.sql`
```sql
ALTER TABLE tarefas DROP COLUMN prazo;
```

## Exercício
1. Crie as migrations acima e aplique-as em ordem com `psql -f`.
2. Escreva a migration 003 que adiciona `prioridade` com `CHECK (prioridade BETWEEN 1 AND 3)` e `DEFAULT 2`.
3. Teste que um `INSERT` com título vazio é rejeitado.

## Checklist
- [ ] Versiono o esquema com migrations
- [ ] Uso constraints para garantir integridade
- [ ] Faço mudanças de esquema em passos seguros
