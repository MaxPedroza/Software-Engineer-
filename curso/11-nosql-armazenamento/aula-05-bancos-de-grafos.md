# Aula 5 — Bancos de grafos

**Duração:** ~20 min · **Módulo 11**

## Objetivo
Modelar dados como nós e relacionamentos e consultá-los com Cypher.

## Teoria
- Um grafo tem **nós** (entidades), **relacionamentos** (arestas, com direção e tipo) e **propriedades** em ambos.
- Em bancos de grafos nativos (Neo4j), percorrer relacionamentos é barato (*index-free adjacency*), mesmo com muitos saltos. Em SQL, cada salto vira um `JOIN` e o custo explode.
- Casos de uso: redes sociais, recomendação, detecção de fraude, rotas, dependências entre serviços, controle de acesso.
- Quando **não** usar: dados tabulares simples, agregações em massa.

## Exemplo (Cypher)
```cypher
CREATE (ana:Pessoa {nome:"Ana"}), (bia:Pessoa {nome:"Bia"}), (caio:Pessoa {nome:"Caio"})
CREATE (ana)-[:SEGUE]->(bia), (bia)-[:SEGUE]->(caio);

// Amigos de amigos que Ana ainda não segue
MATCH (a:Pessoa {nome:"Ana"})-[:SEGUE]->()-[:SEGUE]->(sugestao)
WHERE NOT (a)-[:SEGUE]->(sugestao) AND sugestao <> a
RETURN DISTINCT sugestao.nome;

// Menor caminho
MATCH p = shortestPath((:Pessoa {nome:"Ana"})-[:SEGUE*..5]->(:Pessoa {nome:"Caio"}))
RETURN length(p);
```

## Exercício
1. Modele em grafo: usuários, tarefas, projetos e a relação "depende de" entre tarefas.
2. Escreva em Cypher: todas as tarefas bloqueadas direta ou indiretamente por uma tarefa X (`-[:DEPENDE_DE*]->`).
3. Compare com o equivalente SQL (CTE recursiva).

## Checklist
- [ ] Conheço nós, relacionamentos e propriedades
- [ ] Leio consultas Cypher simples
- [ ] Sei quando um grafo compensa
