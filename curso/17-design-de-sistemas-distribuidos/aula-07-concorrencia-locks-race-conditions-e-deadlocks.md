# Aula 7 — Concorrência: locks, race conditions e deadlocks

**Duração:** ~25 min · **Módulo 17**

## Objetivo
Evitar condições de corrida em código e em bancos de dados, local e distribuído.

## Teoria
- **Race condition**: resultado depende da ordem de execução. Exemplo clássico: *read-modify-write* (ler saldo, somar, gravar).
- **Controle pessimista**: trava antes (`SELECT ... FOR UPDATE`, mutex).
- **Controle otimista**: lê uma **versão**, grava só se não mudou; em conflito, tenta de novo.
- **Operações atômicas**: `UPDATE t SET n = n + 1`, `INCR` no Redis.
- **Deadlock**: ciclo de espera. Previna adquirindo locks numa **ordem global fixa** e usando timeouts.
- **Lock distribuído**: Redis (`SET chave valor NX PX 30000`) ou etcd/ZooKeeper. Use TTL e *fencing token*, pois um processo pode pausar (GC) e perder o lock sem saber.
- **Idempotência** com chave única evita efeitos duplicados.

## Exemplo: bloqueio otimista em SQL
```sql
CREATE TABLE contas (id INT PRIMARY KEY, saldo NUMERIC, versao INT);

-- app leu saldo=100, versao=7
UPDATE contas
   SET saldo = 100 - 30, versao = versao + 1
 WHERE id = 1 AND versao = 7;
-- 0 linhas afetadas => conflito: reler e tentar novamente
```

Deadlock evitado por ordem de locks:
```python
import threading
la, lb = threading.Lock(), threading.Lock()

def transferir(origem, destino):
    primeiro, segundo = sorted([origem, destino], key=id)
    with primeiro, segundo:
        ...  # sempre adquire na mesma ordem
```

## Exercício
1. Em duas sessões do PostgreSQL, rode `BEGIN; SELECT saldo FROM contas WHERE id=1 FOR UPDATE;` e observe a segunda aguardando.
2. Provoque um deadlock com dois locks em ordens opostas, depois corrija com ordem fixa.

## Checklist
- [ ] Identifico read-modify-write inseguro
- [ ] Sei usar lock otimista e pessimista
- [ ] Previno deadlocks com ordem de locks
