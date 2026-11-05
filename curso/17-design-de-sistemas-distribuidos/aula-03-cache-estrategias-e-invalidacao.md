# Aula 3 — Cache: estratégias e invalidação

**Duração:** ~20 min · **Módulo 17**

## Objetivo
Aplicar padrões de cache e lidar com invalidação e problemas como stampede.

## Teoria
| Estratégia | Funcionamento | Observação |
|-----------|---------------|------------|
| **Cache-aside** | App consulta cache; em miss lê o banco e preenche | Mais comum |
| **Read-through** | Cache carrega sozinho do banco | Menos código na app |
| **Write-through** | Escreve no cache e no banco juntos | Consistente, escrita mais lenta |
| **Write-back** | Escreve no cache e persiste depois | Rápido, risco de perda |

### Invalidação
- **TTL**: expira após tempo fixo (simples, pode servir dado velho).
- **Invalidação explícita**: apagar a chave ao atualizar o dado.
- Despejo (eviction): LRU, LFU.

### Problemas
- **Cache stampede**: chave popular expira e muitas requisições vão ao banco. Mitigue com lock por chave, TTL com jitter, refresh antecipado.
- **Cache penetration**: consultas por chaves inexistentes; cache valores negativos ou use Bloom filter.

## Exemplo: cache-aside com Redis
```python
import json, random, redis

r = redis.Redis(decode_responses=True)

def get_usuario(uid, db):
    chave = f"usuario:{uid}"
    if (v := r.get(chave)):
        return json.loads(v)
    usuario = db.buscar_usuario(uid)
    ttl = 300 + random.randint(0, 60)  # jitter
    r.setex(chave, ttl, json.dumps(usuario))
    return usuario

def atualizar_usuario(uid, dados, db):
    db.atualizar_usuario(uid, dados)
    r.delete(f"usuario:{uid}")  # invalida
```

## Exercício
1. Implemente `get_usuario` e meça o tempo com e sem cache em 1.000 leituras.
2. Qual estratégia para um contador de curtidas que tolera pequena perda? E para saldo bancário? Justifique.

## Checklist
- [ ] Conheço as 4 estratégias de cache
- [ ] Sei invalidar com TTL e explicitamente
- [ ] Sei mitigar stampede
