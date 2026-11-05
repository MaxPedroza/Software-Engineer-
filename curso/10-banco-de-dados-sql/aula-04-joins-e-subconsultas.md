# Aula 4 — Joins e subconsultas

**Duração:** ~30 min · **Módulo 10**

## Objetivo
Combinar dados de várias tabelas e usar consultas aninhadas.

## Teoria
- **INNER JOIN**: apenas linhas com correspondência nas duas tabelas.
- **LEFT JOIN**: todas as da esquerda; sem correspondência, colunas da direita ficam `NULL`. `RIGHT` é o espelho; **FULL** mantém ambos os lados.
- **CROSS JOIN**: produto cartesiano.
- Use **aliases** (`u`, `p`) para legibilidade.
- **Subconsulta**: `SELECT` dentro de outro (em `WHERE`, `FROM` ou `SELECT`). `IN`, `EXISTS` e `NOT EXISTS` testam pertinência.
- **CTE** (`WITH`) nomeia subconsultas e melhora a leitura.
- Para achar "sem relação", use `LEFT JOIN ... WHERE x IS NULL` ou `NOT EXISTS`.

## Exemplo
```sql
-- Tarefas com projeto e dono
SELECT u.nome, p.nome AS projeto, t.titulo
FROM tarefas t
JOIN projetos p ON p.id = t.projeto_id
JOIN usuarios u ON u.id = p.usuario_id
WHERE t.concluida = FALSE;

-- Usuários sem nenhum projeto
SELECT u.nome
FROM usuarios u
LEFT JOIN projetos p ON p.usuario_id = u.id
WHERE p.id IS NULL;

-- Projetos que têm ao menos uma tarefa pendente
SELECT p.nome
FROM projetos p
WHERE EXISTS (
  SELECT 1 FROM tarefas t
  WHERE t.projeto_id = p.id AND t.concluida = FALSE
);

-- CTE
WITH pendentes AS (
  SELECT projeto_id, COUNT(*) AS qtd
  FROM tarefas WHERE concluida = FALSE
  GROUP BY projeto_id
)
SELECT p.nome, pe.qtd
FROM projetos p JOIN pendentes pe ON pe.projeto_id = p.id;
```

## Exercício
1. Liste cada projeto com o nome do dono usando `INNER JOIN`.
2. Liste projetos sem tarefas de duas formas: `LEFT JOIN` e `NOT EXISTS`.
3. Reescreva a consulta com `IN` usando `EXISTS` e compare os resultados.

## Checklist
- [ ] Diferencio INNER e LEFT JOIN
- [ ] Uso `EXISTS`/`IN` e CTEs
- [ ] Encontro registros sem correspondência
