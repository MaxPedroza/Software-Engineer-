# Aula 7 — Teorema CAP e consistência eventual

**Duração:** ~20 min · **Módulo 11**

## Objetivo
Compreender os trade-offs de sistemas distribuídos de dados.

## Teoria
O **teorema CAP**: diante de uma **partição de rede** (P), um sistema distribuído precisa escolher entre:
- **Consistência (C)**: toda leitura vê a escrita mais recente.
- **Disponibilidade (A)**: toda requisição recebe resposta (possivelmente desatualizada).

Como partições ocorrem na prática, a escolha real é **CP** ou **AP**:
| Tipo | Comportamento na partição | Exemplos |
|------|---------------------------|----------|
| CP | Recusa/atrasa requisições para não divergir | MongoDB (padrão), etcd, HBase |
| AP | Responde sempre; réplicas divergem e reconciliam | Cassandra, DynamoDB (leitura eventual) |

- **Consistência eventual**: sem novas escritas, todas as réplicas convergem para o mesmo valor.
- **PACELC**: mesmo sem partição, há trade-off entre latência (L) e consistência (C).
- **ACID vs BASE**: ACID prioriza correção transacional; BASE (*Basically Available, Soft state, Eventually consistent*) prioriza disponibilidade.
- Níveis ajustáveis: em Cassandra, com fator de replicação N, leitura R e escrita W com **R + W > N** garantem leitura consistente.

## Exemplo
```
N = 3 réplicas
W = 2, R = 2  -> R + W = 4 > 3  : leitura vê a última escrita (quórum)
W = 1, R = 1  -> R + W = 2 <= 3 : rápido, mas pode ler dado antigo
```
```
cqlsh> CONSISTENCY QUORUM;
```

## Exercício
1. Classifique como CP ou AP e justifique: (a) saldo bancário; (b) contador de curtidas; (c) carrinho de compras.
2. Com N = 5, qual o menor W para R = 2 garantir consistência forte?

## Checklist
- [ ] Explico CAP e por que P é inevitável
- [ ] Sei o que é consistência eventual
- [ ] Sei usar quórum (R + W > N)
