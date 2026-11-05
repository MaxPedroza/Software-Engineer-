# Aula 6 — Normalização e desnormalização

**Duração:** ~25 min · **Módulo 10**

## Objetivo
Eliminar redundância com as formas normais e saber quando desnormalizar de propósito.

## Teoria
Redundância gera **anomalias** de inserção, atualização e exclusão.
- **1FN**: valores atômicos, sem listas em uma coluna nem grupos repetidos.
- **2FN**: 1FN + nenhum atributo depende de **parte** da chave composta.
- **3FN**: 2FN + nenhum atributo não-chave depende de outro atributo não-chave (sem dependência transitiva).
- Em resumo: "cada atributo depende da chave, de toda a chave e nada além da chave".
- **Desnormalização**: duplicar dados deliberadamente para acelerar leituras (colunas calculadas, tabelas de resumo, views materializadas). Custo: mais complexidade e risco de inconsistência.
- Regra: normalize primeiro (3FN); desnormalize só com medição que justifique.

## Exemplo
Tabela ruim:
```sql
CREATE TABLE pedidos_ruim (
  pedido_id     INT,
  cliente_nome  TEXT,
  cliente_cidade TEXT,
  produtos      TEXT   -- 'caneta, lapis' viola 1FN
);
```
Normalizada:
```sql
CREATE TABLE clientes (
  id     SERIAL PRIMARY KEY,
  nome   TEXT NOT NULL,
  cidade TEXT NOT NULL
);
CREATE TABLE pedidos (
  id         SERIAL PRIMARY KEY,
  cliente_id INT NOT NULL REFERENCES clientes(id)
);
CREATE TABLE produtos (id SERIAL PRIMARY KEY, nome TEXT NOT NULL, preco NUMERIC(10,2) NOT NULL);
CREATE TABLE itens_pedido (
  pedido_id  INT REFERENCES pedidos(id),
  produto_id INT REFERENCES produtos(id),
  quantidade INT NOT NULL CHECK (quantidade > 0),
  PRIMARY KEY (pedido_id, produto_id)
);
```
Desnormalização controlada com view materializada:
```sql
CREATE MATERIALIZED VIEW vendas_por_cliente AS
SELECT p.cliente_id, SUM(i.quantidade * pr.preco) AS total
FROM pedidos p
JOIN itens_pedido i ON i.pedido_id = p.id
JOIN produtos pr ON pr.id = i.produto_id
GROUP BY p.cliente_id;
-- REFRESH MATERIALIZED VIEW vendas_por_cliente;
```

## Exercício
1. Aponte as violações de 1FN, 2FN e 3FN em uma planilha de matrículas (aluno, curso, professor, sala do professor).
2. Normalize até a 3FN e escreva os `CREATE TABLE`.
3. Dê um exemplo de desnormalização justificável.

## Checklist
- [ ] Explico 1FN, 2FN e 3FN
- [ ] Reconheço anomalias de atualização
- [ ] Sei quando e como desnormalizar
