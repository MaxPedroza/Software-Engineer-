# Aula 6 — Busca full-text (Elasticsearch/OpenSearch)

**Duração:** ~25 min · **Módulo 11**

## Objetivo
Entender índice invertido e fazer buscas por relevância com Elasticsearch/OpenSearch.

## Teoria
- **Índice invertido**: mapeia cada termo para os documentos que o contêm (como o índice remissivo de um livro).
- **Analisador**: tokeniza, converte para minúsculas, remove acentos/stopwords e aplica *stemming* (ex.: analisador `portuguese`).
- **Relevância**: pontuação por BM25 — termos raros e frequentes no documento pesam mais.
- Dados em **índices** divididos em **shards** (escala) com **réplicas** (disponibilidade).
- Não é banco principal: mantenha a fonte da verdade no banco transacional e sincronize o índice (eventos, jobs ou CDC). Consistência é eventual (*refresh* ~1 s).

## Exemplo
```bash
curl -X PUT localhost:9200/tarefas -H 'Content-Type: application/json' -d '{
  "mappings": { "properties": {
    "titulo": { "type": "text", "analyzer": "portuguese" },
    "status": { "type": "keyword" } } } }'

curl -X POST localhost:9200/tarefas/_doc/1 -H 'Content-Type: application/json' \
  -d '{"titulo":"Estudar bancos de dados","status":"aberta"}'

curl -X GET 'localhost:9200/tarefas/_search' -H 'Content-Type: application/json' -d '{
  "query": { "bool": {
    "must":   { "match": { "titulo": "banco de dado" } },
    "filter": { "term":  { "status": "aberta" } } } } }'
```
`must` calcula relevância; `filter` apenas filtra (e é cacheável).

## Exercício
1. Indexe 5 tarefas e busque por uma palavra no plural/singular. O stemming ajudou?
2. Compare `text` com `keyword` ao filtrar por `status`.
3. Descreva como manteria o índice sincronizado quando uma tarefa é editada.

## Checklist
- [ ] Explico índice invertido e analisadores
- [ ] Diferencio `match` de `term` e `text` de `keyword`
- [ ] Sei que o índice não é a fonte da verdade
