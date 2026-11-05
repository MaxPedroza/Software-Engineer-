# Aula 10 — Revisão e quiz do módulo

**Duração:** ~25 min · **Módulo 10**

## Resumo
- **SGBD** gerencia dados com persistência, integridade e concorrência; modelo relacional usa tabelas, PK e FK.
- **Modelagem ER**: entidades, relacionamentos e cardinalidade; N:N vira tabela associativa.
- **SQL**: CRUD, `WHERE`, `NULL`, `RETURNING`.
- **Joins e subconsultas**: INNER/LEFT, `EXISTS`, CTEs.
- **Agregações**: `GROUP BY`, `HAVING`, funções de janela.
- **Normalização** até 3FN; desnormalização consciente.
- **Índices**: B-tree, compostos, parciais; `EXPLAIN ANALYZE`.
- **Transações**: ACID e níveis de isolamento.
- **Migrations e constraints** protegem e versionam o esquema.

## Quiz
1. Qual a diferença entre PK e FK?
2. Como se representa um relacionamento N:N?
3. Por que `col = NULL` não funciona?
4. Qual a diferença entre INNER JOIN e LEFT JOIN?
5. Qual a diferença entre `WHERE` e `HAVING`?
6. O que uma função de janela faz de diferente de `GROUP BY`?
7. O que a 3FN exige?
8. Quando um índice pode piorar o desempenho?
9. O que significa cada letra de ACID?
10. Por que nunca editar uma migration já aplicada?

## Gabarito resumido
1. PK identifica unicamente a linha; FK referencia a PK de outra tabela.
2. Com uma tabela associativa contendo as duas FKs (PK composta).
3. `NULL` é desconhecido; a comparação resulta em desconhecido; use `IS NULL`.
4. INNER retorna só correspondências; LEFT mantém todas as linhas da esquerda.
5. `WHERE` filtra linhas antes de agrupar; `HAVING` filtra grupos depois.
6. Calcula sobre um conjunto de linhas sem colapsá-las.
7. Atributos não-chave dependem só da chave (sem dependência transitiva), após 1FN e 2FN.
8. Em tabelas com muita escrita ou pouca seletividade: custo de manutenção e espaço.
9. Atomicidade, Consistência, Isolamento, Durabilidade.
10. Ambientes já aplicados divergiriam; crie uma nova migration.

## Entregável do módulo
Persista usuários, projetos e tarefas em PostgreSQL: diagrama ER, migrations versionadas (com constraints e índices em FKs) e um documento com ao menos 3 consultas otimizadas, mostrando `EXPLAIN ANALYZE` antes e depois.

## Checklist final
- [ ] Respondi o quiz sem consulta
- [ ] Modelo ER e tabelas em 3FN
- [ ] Migrations aplicam do zero sem erros
- [ ] Consultas com joins, agregação e janela funcionando
- [ ] Otimizações documentadas com planos de execução
