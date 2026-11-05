# Aula 2 — Bancos de documentos (MongoDB)

**Duração:** ~25 min · **Módulo 11**

## Objetivo
Modelar e consultar dados em documentos JSON/BSON usando MongoDB.

## Teoria
- Um **documento** é um objeto JSON (BSON); documentos ficam em **coleções**, dentro de um **banco**.
- Esquema flexível: documentos da mesma coleção podem ter campos diferentes (use validação quando precisar de regras).
- **Embutir vs referenciar**: embuta dados lidos juntos e de tamanho limitado (itens do pedido); referencie dados grandes, compartilhados ou que crescem sem limite.
- **Índices** aceleram consultas; sem índice, há *collection scan*.
- Limite de 16 MB por documento.

## Exemplo (mongosh)
```javascript
use tarefas_db

db.tarefas.insertOne({
  titulo: "Estudar NoSQL", status: "aberta",
  tags: ["estudo", "db"], criada_em: new Date()
})

db.tarefas.find({ status: "aberta", tags: "db" }, { titulo: 1, _id: 0 })

db.tarefas.updateOne({ titulo: "Estudar NoSQL" }, { $set: { status: "feita" } })

db.tarefas.createIndex({ status: 1, criada_em: -1 })
db.tarefas.find({ status: "feita" }).explain("executionStats")

db.tarefas.aggregate([
  { $group: { _id: "$status", total: { $sum: 1 } } }
])
```

## Exercício
1. Insira 5 tarefas com tags diferentes e liste as que têm a tag `db`.
2. Crie um índice em `status` e compare `explain()` antes e depois (`COLLSCAN` vs `IXSCAN`).
3. Modele "projeto com tarefas": embutir ou referenciar? Justifique.

## Checklist
- [ ] Sei criar, consultar e atualizar documentos
- [ ] Sei decidir entre embutir e referenciar
- [ ] Sei criar índices e ler um `explain`
