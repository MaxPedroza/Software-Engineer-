# Aula 5 — Agregações, GROUP BY e funções de janela

**Duração:** ~30 min · **Módulo 10**

## Objetivo
Resumir dados com agregações e calcular métricas por linha com funções de janela.

## Teoria
- **Agregações**: `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`. `COUNT(*)` conta linhas; `COUNT(col)` ignora `NULL`.
- **GROUP BY** agrupa linhas; toda coluna no `SELECT` deve estar no `GROUP BY` ou em uma agregação.
- **WHERE** filtra linhas *antes* de agrupar; **HAVING** filtra grupos *depois*.
- **Funções de janela** calculam sobre um conjunto de linhas **sem colapsá-las**: `função() OVER (PARTITION BY ... ORDER BY ...)`.
- Comuns: `ROW_NUMBER()`, `RANK()`, `LAG()/LEAD()`, `SUM() OVER` (soma acumulada).

## Exemplo
```sql
-- Tarefas por projeto, só projetos com 3+ tarefas
SELECT projeto_id,
       COUNT(*) AS total,
       COUNT(*) FILTER (WHERE concluida) AS feitas
FROM tarefas
GROUP BY projeto_id
HAVING COUNT(*) >= 3
ORDER BY total DESC;

-- Ranking das tarefas mais recentes por projeto
SELECT projeto_id, titulo, criada_em,
       ROW_NUMBER() OVER (PARTITION BY projeto_id ORDER BY criada_em DESC) AS pos
FROM tarefas;

-- Apenas a mais recente de cada projeto
SELECT * FROM (
  SELECT t.*, ROW_NUMBER() OVER (PARTITION BY projeto_id ORDER BY criada_em DESC) AS pos
  FROM tarefas t
) x WHERE pos = 1;

-- Total acumulado de tarefas criadas por dia
SELECT criada_em::date AS dia,
       COUNT(*) AS no_dia,
       SUM(COUNT(*)) OVER (ORDER BY criada_em::date) AS acumulado
FROM tarefas
GROUP BY criada_em::date;
```

## Exercício
1. Calcule a porcentagem de tarefas concluídas por projeto.
2. Liste os 2 projetos mais recentes de cada usuário com `ROW_NUMBER`.
3. Use `LAG` para mostrar a diferença de tarefas criadas entre dias consecutivos.

## Checklist
- [ ] Uso `GROUP BY` e `HAVING` corretamente
- [ ] Diferencio `WHERE` de `HAVING`
- [ ] Escrevo funções de janela com `OVER`
