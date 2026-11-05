# Aula 6 — Consenso, relógios e ordenação de eventos

**Duração:** ~25 min · **Módulo 17**

## Objetivo
Entender por que relógios físicos não bastam e como nós concordam sobre um valor.

## Teoria
- Relógios de máquinas **derivam** (clock skew); NTP reduz, mas não elimina. Não use timestamps de máquinas diferentes para decidir ordem de escritas.
- **Relação happened-before (Lamport)**: se A causou B, A vem antes. Eventos sem relação causal são **concorrentes**.
- **Relógio lógico de Lamport**: contador; em cada evento `t += 1`; ao receber mensagem `t = max(t, t_msg) + 1`. Garante: A→B implica L(A) < L(B) (a volta não vale).
- **Vector clocks**: um contador por nó; detectam concorrência e são usados para detectar conflitos (ex.: Dynamo).
- **Hybrid logical clocks** e relógios com incerteza (TrueTime do Spanner) combinam tempo físico e lógico.

### Consenso
Nós precisam concordar em um valor mesmo com falhas. **Paxos** e **Raft** toleram falha de minoria (precisa de maioria: 3 nós toleram 1, 5 toleram 2).
- Raft: **eleição de líder** por termos, **replicação de log** pelo líder, commit quando a maioria confirma.
- Usado em etcd, Consul e ZooKeeper (ZAB) para locks, configuração e eleição de líder.
- Problema dos Generais Bizantinos: nós maliciosos exigem outros protocolos (BFT).

## Exemplo: relógio de Lamport
```python
class Lamport:
    def __init__(self): self.t = 0
    def evento(self):
        self.t += 1; return self.t
    def enviar(self):
        return self.evento()
    def receber(self, t_msg):
        self.t = max(self.t, t_msg) + 1; return self.t

a, b = Lamport(), Lamport()
t = a.enviar()        # a: 1
b.evento()            # b: 1 (concorrente)
print(b.receber(t))   # b: 2
```

## Exercício
1. Estenda para vector clocks com 3 nós e implemente `concorrentes(v1, v2)`.
2. Por que um cluster Raft de 4 nós não tolera mais falhas que um de 3?

## Checklist
- [ ] Sei por que timestamps físicos enganam
- [ ] Uso Lamport/vector clocks
- [ ] Explico eleição de líder e maioria no Raft
