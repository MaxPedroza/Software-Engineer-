# Aula 3 — SQL básico: SELECT, INSERT, UPDATE, DELETE

**Duração:** ~25 min · **Módulo 10**

## Objetivo
Executar as operações CRUD fundamentais em SQL.

## Teoria
- **INSERT**: cria linhas. **SELECT**: lê. **UPDATE**: altera. **DELETE**: remove.
- Cláusulas do `SELECT`: `WHERE` (filtro), `ORDER BY`, `LIMIT/OFFSET`, `DISTINCT`.
- Operadores: `=`, `<>`, `<`, `>`, `BETWEEN`, `IN`, `LIKE`/`ILIKE`, `IS NULL`.
- `NULL` significa "desconhecido": `col = NULL` nunca é verdadeiro; use `IS NULL`.
- **Sempre use `WHERE` em `UPDATE` e `DELETE`**, senão afeta todas as linhas.
- `RETURNING` (PostgreSQL) devolve as linhas afetadas.
- Em aplicações, use **consultas parametrizadas** para evitar SQL injection.

## Exemplo
```sql
CREATE TABLE tarefas (
  id        SERIAL PRIMARY KEY,
  titulo    TEXT NOT NULL,
  concluida BOOLEAN NOT NULL DEFAULT FALSE,
  prazo     DATE
);

INSERT INTO tarefas (titulo, prazo) VALUES
  ('Estudar SQL', '2026-12-01'),
  ('Ler sobre índices', NULL),
  ('Fazer o projeto', '2026-12-15')
RETURNING id;

SELECT id, titulo
FROM tarefas
WHERE concluida = FALSE AND prazo IS NOT NULL
ORDER BY prazo
LIMIT 10;

UPDATE tarefas SET concluida = TRUE WHERE id = 1;

DELETE FROM tarefas WHERE titulo ILIKE '%índices%';
```

## Exercício
1. Crie a tabela e insira 5 tarefas, duas sem prazo.
2. Liste as tarefas pendentes ordenadas por prazo, com as sem prazo por último (`NULLS LAST`).
3. Marque como concluídas todas com prazo vencido (`prazo < CURRENT_DATE`) e use `RETURNING`.

## Checklist
- [ ] Faço INSERT, SELECT, UPDATE e DELETE
- [ ] Sempre uso `WHERE` em alterações
- [ ] Trato `NULL` com `IS NULL`
