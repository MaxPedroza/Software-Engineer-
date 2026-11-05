# Aula 4 — Mensageria e streaming (Kafka, RabbitMQ)

**Duração:** ~25 min · **Módulo 17**

## Objetivo
Desacoplar serviços com filas e logs de eventos, entendendo garantias de entrega.

## Teoria
- **Fila (RabbitMQ)**: broker entrega mensagens a consumidores, que dão **ack**; a mensagem sai da fila. Bom para tarefas e roteamento flexível (exchanges).
- **Log distribuído (Kafka)**: mensagens ficam retidas em **tópicos** divididos em **partições**; consumidores guardam seu **offset** e podem reler. Ordem só é garantida **dentro da partição**; a chave da mensagem define a partição.
- **Consumer group**: partições são divididas entre consumidores do grupo.

### Garantias de entrega
- *At-most-once*: pode perder.
- *At-least-once*: pode duplicar → consumidores devem ser **idempotentes**.
- *Exactly-once*: efeito único, obtido com idempotência/transações.

### Boas práticas
**Dead-letter queue** para mensagens com falha, retry com backoff, e deduplicação por ID de mensagem.

## Exemplo: Kafka com Docker Compose e Python
```yaml
services:
  kafka:
    image: apache/kafka:3.8.0
    ports: ["9092:9092"]
```
```python
from kafka import KafkaProducer, KafkaConsumer
import json

p = KafkaProducer(bootstrap_servers="localhost:9092",
                  value_serializer=lambda v: json.dumps(v).encode())
p.send("notificacoes", key=b"user-42", value={"id": "n1", "msg": "Olá"})
p.flush()

c = KafkaConsumer("notificacoes", bootstrap_servers="localhost:9092",
                  group_id="envio-email", enable_auto_commit=False)
vistos = set()
for m in c:
    n = json.loads(m.value)
    if n["id"] not in vistos:   # idempotência
        vistos.add(n["id"])
        print("enviando", n)
    c.commit()
```

## Exercício
1. Suba o Kafka, produza 10 mensagens com 2 chaves e verifique a ordem por chave.
2. Por que o consumidor acima ainda pode duplicar após reiniciar? Como persistir os IDs vistos?

## Checklist
- [ ] Diferencio fila de log
- [ ] Entendo at-least-once e idempotência
- [ ] Sei o papel de partições e consumer groups
