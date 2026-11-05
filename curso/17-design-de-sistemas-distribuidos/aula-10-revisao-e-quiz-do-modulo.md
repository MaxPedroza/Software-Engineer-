# Aula 10 — Revisão e quiz do módulo

**Duração:** ~25 min · **Módulo 17**

## Resumo
- Comece por requisitos e **estimativas** (QPS, armazenamento, banda).
- Escale com serviços **stateless**, load balancers e, depois, cache.
- Cache-aside + TTL com jitter; cuidado com stampede.
- Mensageria desacopla: filas vs. logs; at-least-once exige idempotência.
- Replicação e sharding trazem trade-offs (CAP/PACELC, quóruns `R+W>N`).
- Relógios físicos derivam; use Lamport/vector clocks e consenso (Raft).
- Concorrência: locks, controle otimista, operações atômicas, ordem de locks.
- Resiliência: timeout, retry com backoff, circuit breaker, backpressure.

## Quiz
1. Qual é o QPS médio de 86 milhões de requisições por dia?
2. Por que serviços stateless facilitam a escala horizontal?
3. O que é cache stampede e uma forma de mitigá-lo?
4. Qual a diferença entre Kafka e RabbitMQ quanto à retenção de mensagens?
5. Por que consumidores at-least-once precisam ser idempotentes?
6. Com N=3 réplicas e W=2, qual R garante leitura forte?
7. Qual vantagem do hash consistente sobre `hash(chave) % N`?
8. Por que não ordenar eventos entre máquinas só por timestamp?
9. Como evitar deadlock entre dois locks?
10. Quando o circuit breaker passa ao estado meio-aberto?

## Gabarito resumido
1. ≈ 1.000 QPS.
2. Qualquer instância atende qualquer requisição; instâncias são descartáveis.
3. Chave popular expira e muitas requisições vão ao banco; lock por chave ou jitter no TTL.
4. Kafka retém o log e permite releitura; RabbitMQ remove após ack.
5. Entregas podem duplicar.
6. R ≥ 2 (R+W > N).
7. Mover só ~1/N das chaves ao mudar nós.
8. Clock skew; use relógios lógicos.
9. Adquirir locks sempre na mesma ordem (e usar timeouts).
10. Após o tempo de espera, para testar uma chamada.

## Entregável do módulo
**Design document** de um sistema de grande escala (ex.: chat ou feed) com: requisitos RF/RNF, estimativas, API, modelo de dados, diagrama de arquitetura, estratégia de cache, replicação/sharding, tratamento de falhas e trade-offs. No projeto contínuo, adicione a fila de notificações e cache distribuído e meça a resiliência com falhas simuladas.

## Checklist final
- [ ] Faço estimativas de capacidade
- [ ] Projeto cache, filas e particionamento
- [ ] Trato concorrência e falhas parciais
- [ ] Entrego o design document com diagramas
