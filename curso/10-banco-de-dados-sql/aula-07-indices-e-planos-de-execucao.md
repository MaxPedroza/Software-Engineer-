# Aula 7 — Índices e planos de execução

**Duração:** ~30 min · **Módulo 10**

## Objetivo
Acelerar consultas com índices e interpretar planos de execução com `EXPLAIN`.

## Teoria
- Sem índice, o banco faz **Seq Scan** (lê a tabela inteira). Um **índice** (B-tree por padrão) permite localizar linhas rapidamente (**Index Scan**).
- PKs e `UNIQUE` já criam índice. **FKs não** criam automaticamente no PostgreSQL: indexe-as se forem usadas em joins/filtros.
- **Índice composto**: a ordem importa; `(a, b)` ajuda filtros por `a` ou `a` e `b`, mas não só `b`.
- **Índice parcial** (`WHERE`) e **de expressão** (`lower(email)`).
- Outros tipos: Hash, GIN (arrays/JSONB/texto), GiST, BRIN.
- **Custo**: índices ocupam espaço e deixam `INSERT/UPDATE/DELETE` mais lentos. Não indexe tudo.
- `EXPLAIN` mostra o plano estimado; `EXPLAIN ANALYZE` **executa** e mostra tempos reais. Rode `ANALYZE` para atualizar estatísticas.
- Funções sobre a coluna (`WHERE lower(email) = ...`) ignoram índice comum.

## Exemplo
```sql
EXPLAIN ANALYZE
SELECT * FROM tarefas WHERE projeto_id = 42 AND concluida = FALSE;
-- Seq Scan on tarefas  (cost=... ) Execution Time: 85 ms

CREATE INDEX idx_tarefas_projeto_pendentes
  ON tarefas (projeto_id)
  WHERE concluida = FALSE;

EXPLAIN ANALYZE
SELECT * FROM tarefas WHERE projeto_id = 42 AND concluida = FALSE;
-- Index Scan using idx_tarefas_projeto_pendentes ... Execution Time: 0.1 ms

CREATE INDEX idx_usuarios_email_lower ON usuarios (lower(email));
SELECT * FROM usuarios WHERE lower(email) = 'ana@exemplo.com';
```
Gerar massa de teste:
```sql
INSERT INTO tarefas (projeto_id, titulo)
SELECT (random()*1000)::int + 1, 'Tarefa ' || g FROM generate_series(1, 500000) g;
```

## Exercício
1. Gere 500 mil linhas e meça uma consulta antes e depois de criar o índice.
2. Crie `(projeto_id, criada_em)` e verifique se `ORDER BY criada_em` evita ordenação.
3. Mostre um caso em que o índice **não** é usado e explique o motivo.

## Checklist
- [ ] Leio um plano de `EXPLAIN ANALYZE`
- [ ] Crio índices simples, compostos e parciais
- [ ] Conheço o custo de manter índices
