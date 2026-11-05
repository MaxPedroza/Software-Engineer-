# Aula 5 — Replicação, particionamento (sharding) e consistência

**Duração:** ~25 min · **Módulo 17**

## Objetivo
Distribuir dados entre nós e compreender os trade-offs de consistência.

## Teoria
### Replicação
- **Líder–seguidor**: escritas no líder, leituras nos seguidores (podem estar atrasados — *replication lag*).
- **Multi-líder / sem líder**: maior disponibilidade, exigem resolução de conflitos.
- Síncrona = mais durável e lenta; assíncrona = rápida e pode perder dados no failover.

### Particionamento (sharding)
- Por **faixa** (range): bom para consultas por intervalo, risco de *hot spots*.
- Por **hash**: distribui bem, ruim para ranges.
- **Hash consistente**: adicionar/remover nós move poucas chaves.
- Consultas e transações entre shards são caras.

### CAP e consistência
Em partição de rede é preciso escolher **C** (consistência) ou **A** (disponibilidade). **PACELC**: mesmo sem partição há trade-off entre latência e consistência.
- **Forte (linearizável)**, **eventual**, **read-your-writes**, **monotonic reads**.
- Quóruns: com N réplicas, `R + W > N` garante leitura do dado mais recente.

## Exemplo: hash consistente
```python
import bisect, hashlib

def h(s): return int(hashlib.md5(s.encode()).hexdigest(), 16)

class Anel:
    def __init__(self, nos, vnodes=100):
        self.anel = sorted((h(f"{n}#{i}"), n) for n in nos for i in range(vnodes))
        self.chaves = [k for k, _ in self.anel]

    def no_para(self, chave):
        i = bisect.bisect(self.chaves, h(chave)) % len(self.anel)
        return self.anel[i][1]

a = Anel(["db1", "db2", "db3"])
print(a.no_para("usuario:42"))
```

## Exercício
1. Distribua 10.000 chaves no anel com 3 nós, depois adicione `db4` e conte quantas chaves mudaram de nó (esperado ≈ 25%).
2. Com N=5, quais valores de R e W garantem leitura forte? Qual combinação favorece leitura rápida?

## Checklist
- [ ] Entendo replicação e lag
- [ ] Sei comparar sharding por hash e por faixa
- [ ] Explico CAP e quóruns
