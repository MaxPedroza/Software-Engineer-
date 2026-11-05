# Aula 1 — Limites do modelo relacional e surgimento do NoSQL

**Duração:** ~20 min · **Módulo 11**

## Objetivo
Entender onde o modelo relacional sofre e quais famílias de NoSQL surgiram para resolver cada problema.

## Teoria
O modelo relacional (tabelas, joins, ACID) segue excelente para a maioria dos sistemas. Os limites aparecem em cenários específicos:
- **Escala de escrita horizontal**: particionar (sharding) um banco relacional é difícil, principalmente com joins e transações entre partições.
- **Esquema rígido**: dados heterogêneos ou que mudam rápido exigem migrações constantes.
- **Impedância objeto-relacional**: um agregado (pedido + itens) vira várias tabelas.
- **Padrões de acesso especiais**: grafos, séries temporais, busca textual e cache de baixíssima latência.

### Famílias de NoSQL
| Família | Exemplo | Bom para |
|---------|---------|----------|
| Documento | MongoDB | Agregados com esquema flexível |
| Chave-valor | Redis | Cache, sessões, contadores |
| Colunar / séries | Cassandra, TimescaleDB | Alto volume de escrita, métricas |
| Grafo | Neo4j | Relacionamentos profundos |
| Busca | Elasticsearch | Full-text, relevância |

NoSQL ("Not Only SQL") **não** significa "sem esquema" nem "melhor": normalmente troca joins e consistência forte por escala, flexibilidade ou desempenho específico. A tendência atual é a **persistência poliglota**: usar mais de um banco, cada um para o que faz melhor.

## Exemplo
O mesmo pedido, em relacional e em documento:
```sql
-- Relacional: 2 tabelas + join
SELECT p.id, i.produto, i.qtd FROM pedidos p JOIN itens i ON i.pedido_id = p.id;
```
```json
{ "_id": 1, "cliente": "Ana", "itens": [{ "produto": "Livro", "qtd": 2 }] }
```

## Exercício
1. Para cada caso, indique a família de banco mais adequada: (a) carrinho de compras temporário; (b) "amigos de amigos"; (c) busca de produtos por texto; (d) temperatura de sensores a cada segundo.
2. Cite um motivo para **não** trocar o PostgreSQL do projeto por NoSQL.

## Checklist
- [ ] Sei apontar limites do modelo relacional
- [ ] Conheço as 5 famílias de NoSQL
- [ ] Entendo persistência poliglota
