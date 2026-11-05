# Aula 8 — GraphQL e gRPC

**Duração:** ~25 min · **Módulo 13**

## Objetivo
Conhecer alternativas ao REST e saber quando cada uma compensa.

## Teoria
### GraphQL
- Um único endpoint (`POST /graphql`); o **cliente escolhe os campos** na consulta, evitando *over-fetching* e *under-fetching* (várias chamadas REST).
- Esquema tipado com `Query` (leitura), `Mutation` (escrita) e `Subscription` (tempo real).
- Cuidados: problema N+1 nos resolvers (use *DataLoader*), limites de profundidade/complexidade, cache HTTP mais difícil.

### gRPC
- RPC sobre **HTTP/2** com **Protocol Buffers** (binário, tipado, compacto). Gera código cliente/servidor a partir do `.proto`.
- Suporta *streaming* uni e bidirecional. Ótimo para comunicação entre microsserviços; limitado em navegadores (precisa de gRPC-Web).

| | REST | GraphQL | gRPC |
|--|------|---------|------|
| Formato | JSON | JSON | Protobuf |
| Contrato | OpenAPI | Schema SDL | `.proto` |
| Melhor para | APIs públicas | Frontends variados | Serviço a serviço |

## Exemplo
GraphQL:
```graphql
type Tarefa { id: ID!  titulo: String!  feita: Boolean! }
type Query { tarefa(id: ID!): Tarefa }
```
```bash
curl -X POST localhost:8000/graphql -H 'Content-Type: application/json' \
  -d '{"query":"{ tarefa(id: 1) { titulo feita } }"}'
```
Python com Strawberry (`pip install "strawberry-graphql[fastapi]"`):
```python
import strawberry
from fastapi import FastAPI
from strawberry.fastapi import GraphQLRouter

@strawberry.type
class Tarefa:
    id: int
    titulo: str

@strawberry.type
class Query:
    @strawberry.field
    def tarefa(self, id: int) -> Tarefa:
        return Tarefa(id=id, titulo="Estudar GraphQL")

app = FastAPI()
app.include_router(GraphQLRouter(strawberry.Schema(query=Query)), prefix="/graphql")
```
gRPC (`tarefas.proto`):
```proto
syntax = "proto3";
service Tarefas { rpc Obter (TarefaId) returns (Tarefa); }
message TarefaId { int32 id = 1; }
message Tarefa { int32 id = 1; string titulo = 2; }
```

## Exercício
1. Rode a consulta GraphQL pedindo só `titulo`, depois `id` e `titulo`.
2. Escolha a tecnologia para: (a) API pública de parceiros; (b) app móvel com telas variadas; (c) serviços internos de alta vazão.

## Checklist
- [ ] Explico over/under-fetching
- [ ] Conheço Protobuf e streaming no gRPC
- [ ] Sei comparar REST, GraphQL e gRPC
