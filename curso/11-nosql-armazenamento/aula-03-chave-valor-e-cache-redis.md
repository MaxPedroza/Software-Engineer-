# Aula 3 — Chave-valor e cache (Redis)

**Duração:** ~25 min · **Módulo 11**

## Objetivo
Usar o Redis como cache e estrutura de dados em memória, aplicando TTL e o padrão cache-aside.

## Teoria
- Redis guarda dados **em memória**, com latência de microssegundos; pode persistir em disco (RDB/AOF).
- Estruturas: strings, hashes, listas, sets, sorted sets, streams.
- **TTL** (`EXPIRE`) remove chaves automaticamente.
- **Cache-aside**: a aplicação consulta o cache; em *miss*, lê do banco, grava no cache com TTL e devolve.
- Problemas: **invalidação** (dado velho), *cache stampede* (muitos misses simultâneos) e uso de memória (política de *eviction*, ex.: `allkeys-lru`).

## Exemplo (redis-cli)
```
SET tarefa:1 "Estudar Redis" EX 60
GET tarefa:1
TTL tarefa:1
HSET usuario:7 nome Ana plano pro
HGETALL usuario:7
INCR visitas:home
ZADD ranking 150 ana 90 bruno
ZREVRANGE ranking 0 2 WITHSCORES
DEL tarefa:1
```
Cache-aside em Python:
```python
import json, redis
r = redis.Redis(decode_responses=True)

def obter_tarefa(id, db):
    chave = f"tarefa:{id}"
    if (v := r.get(chave)):
        return json.loads(v)
    tarefa = db.buscar_tarefa(id)
    r.set(chave, json.dumps(tarefa), ex=60)
    return tarefa
```

## Exercício
1. Suba o Redis (`docker run -p 6379:6379 redis`) e teste `SET ... EX 10`; confira o `TTL` e a expiração.
2. Implemente o cache-aside na listagem de tarefas e invalide a chave ao atualizar uma tarefa.
3. Por que não guardar a única cópia de dados importantes só no Redis?

## Checklist
- [ ] Uso comandos básicos e estruturas do Redis
- [ ] Sei aplicar cache-aside com TTL
- [ ] Conheço os riscos de invalidação
