# Aula 8 — Arquitetura orientada a eventos, CQRS e Event Sourcing

**Duração:** ~25 min · **Módulo 16**

## Objetivo
Entender comunicação por eventos e a separação entre escrita e leitura.

## Teoria
- **Arquitetura orientada a eventos (EDA)**: componentes se comunicam publicando **eventos** (fatos passados, ex.: `TarefaConcluida`) em um *broker* (Kafka, RabbitMQ, SNS/SQS). Produtores não conhecem consumidores → baixo acoplamento, escalabilidade.
- Desafios: **consistência eventual**, ordenação, mensagens duplicadas (consumidores **idempotentes**), depuração mais difícil. Padrão **Outbox** garante gravar no banco e publicar o evento atomicamente.
- **CQRS** (Command Query Responsibility Segregation): separa **comandos** (alteram estado) de **consultas** (só leem), com modelos distintos; o lado de leitura pode ser um *read model* otimizado, atualizado por eventos.
- **Event Sourcing**: em vez de guardar o estado atual, guarda-se a **sequência de eventos**; o estado é reconstruído reaplicando-os. Vantagens: auditoria completa, "viagem no tempo". Custos: complexidade, versionamento de eventos, consultas exigem projeções.
- CQRS e Event Sourcing são independentes; use só quando justificados.

## Exemplo em Python
```python
from dataclasses import dataclass

@dataclass(frozen=True)
class Evento:
    tipo: str
    dados: dict

class ContaEventSourced:
    def __init__(self):
        self.eventos: list[Evento] = []
        self.saldo = 0                       # estado derivado

    def _aplicar(self, e: Evento):
        if e.tipo == "Depositado": self.saldo += e.dados["valor"]
        elif e.tipo == "Sacado": self.saldo -= e.dados["valor"]

    def _registrar(self, e: Evento):
        self.eventos.append(e); self._aplicar(e)

    def depositar(self, valor: int): self._registrar(Evento("Depositado", {"valor": valor}))
    def sacar(self, valor: int):
        if valor > self.saldo: raise ValueError("saldo insuficiente")
        self._registrar(Evento("Sacado", {"valor": valor}))

    @classmethod
    def reconstruir(cls, eventos):
        c = cls()
        for e in eventos: c._registrar(e)
        return c

c = ContaEventSourced(); c.depositar(100); c.sacar(30)
assert ContaEventSourced.reconstruir(c.eventos).saldo == 70

# Consumidor idempotente
processados: set[str] = set()
def tratar(id_evento: str, acao):
    if id_evento in processados: return
    acao(); processados.add(id_evento)
```

## Exercício
1. Liste 4 eventos de domínio do sistema de tarefas (nomes no passado).
2. Implemente um *read model* `tarefas_por_usuario` atualizado por eventos.
3. Explique o que acontece se o broker entregar o mesmo evento duas vezes.

## Checklist
- [ ] Diferencio comando, consulta e evento
- [ ] Entendo consistência eventual e idempotência
- [ ] Sei quando evitar CQRS/Event Sourcing
