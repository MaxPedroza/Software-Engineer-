# Aula 8 — Transações, ACID e níveis de isolamento

**Duração:** ~30 min · **Módulo 10**

## Objetivo
Garantir consistência com transações e entender os níveis de isolamento.

## Teoria
**Transação**: conjunto de operações tratadas como uma unidade (`BEGIN` … `COMMIT` ou `ROLLBACK`).

**ACID**:
- **Atomicidade**: tudo ou nada.
- **Consistência**: leva o banco de um estado válido a outro (constraints respeitadas).
- **Isolamento**: transações concorrentes não se interferem indevidamente.
- **Durabilidade**: após o `COMMIT`, os dados sobrevivem a falhas (WAL).

**Anomalias**: *dirty read* (ler dado não confirmado), *non-repeatable read*, *phantom read*.

**Níveis de isolamento** (padrão SQL): Read Uncommitted, **Read Committed**, Repeatable Read, Serializable. No PostgreSQL, o padrão é Read Committed; Read Uncommitted se comporta como Read Committed; o MVCC evita bloqueio entre leitores e escritores.
- Em **Serializable** pode ocorrer erro de serialização: a aplicação deve **repetir** a transação.
- `SELECT ... FOR UPDATE` trava linhas. **Deadlock**: duas transações esperam uma pela outra; o banco aborta uma.

## Exemplo
```sql
CREATE TABLE contas (id INT PRIMARY KEY, saldo NUMERIC(12,2) NOT NULL CHECK (saldo >= 0));
INSERT INTO contas VALUES (1, 500), (2, 100);

BEGIN;
UPDATE contas SET saldo = saldo - 200 WHERE id = 1;
UPDATE contas SET saldo = saldo + 200 WHERE id = 2;
COMMIT;   -- ou ROLLBACK para desfazer

-- Evitar corrida ao ler e depois alterar
BEGIN;
SELECT saldo FROM contas WHERE id = 1 FOR UPDATE;
UPDATE contas SET saldo = saldo - 50 WHERE id = 1;
COMMIT;

BEGIN ISOLATION LEVEL SERIALIZABLE;
-- ...
COMMIT;
```
Uma transferência que viola o `CHECK` (saldo negativo) falha e a transação inteira é revertida.

## Exercício
1. Faça a transferência acima e force erro no segundo `UPDATE`; confirme que nada foi gravado.
2. Em dois terminais `psql`, reproduza non-repeatable read (Read Committed) e veja que Repeatable Read o evita.
3. Provoque um deadlock atualizando duas linhas em ordens opostas.

## Checklist
- [ ] Explico cada letra do ACID
- [ ] Uso `BEGIN/COMMIT/ROLLBACK`
- [ ] Conheço os níveis de isolamento e `FOR UPDATE`
