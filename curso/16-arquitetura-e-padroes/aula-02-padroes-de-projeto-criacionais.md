# Aula 2 — Padrões de projeto: criacionais

**Duração:** ~20 min · **Módulo 16**

## Objetivo
Reconhecer e aplicar os padrões criacionais mais úteis: Factory Method, Builder e Singleton.

## Teoria
- **Padrões de projeto** (GoF) são soluções reutilizáveis para problemas recorrentes de design. Use-os para resolver um problema real, não por moda.
- **Criacionais** abstraem a criação de objetos:
  - **Factory Method / Simple Factory**: delega a escolha da classe concreta a uma fábrica; o cliente depende da interface.
  - **Abstract Factory**: cria famílias de objetos relacionados.
  - **Builder**: constrói objetos complexos passo a passo (evita construtores com muitos parâmetros).
  - **Singleton**: uma única instância global. Cuidado: estado global dificulta testes; prefira injeção de dependência.
  - **Prototype**: cria objetos clonando um existente.

## Exemplo em Python
```python
from abc import ABC, abstractmethod
from dataclasses import dataclass

class Notificador(ABC):
    @abstractmethod
    def enviar(self, msg: str) -> None: ...

class Email(Notificador):
    def enviar(self, msg): print(f"[email] {msg}")

class Sms(Notificador):
    def enviar(self, msg): print(f"[sms] {msg}")

def criar_notificador(canal: str) -> Notificador:   # Factory
    canais = {"email": Email, "sms": Sms}
    try:
        return canais[canal]()
    except KeyError:
        raise ValueError(f"canal desconhecido: {canal}")

@dataclass
class Consulta:
    tabela: str
    filtros: list[str]
    limite: int | None

class ConsultaBuilder:                             # Builder fluente
    def __init__(self, tabela): self._t, self._f, self._l = tabela, [], None
    def onde(self, cond): self._f.append(cond); return self
    def limite(self, n): self._l = n; return self
    def construir(self): return Consulta(self._t, self._f, self._l)

criar_notificador("email").enviar("Tarefa criada")
q = ConsultaBuilder("tarefas").onde("feita = false").limite(10).construir()
```

## Exercício
1. Adicione o canal `push` à fábrica sem alterar o código cliente.
2. Crie um `TarefaBuilder` com título, prazo, prioridade e tags, validando em `construir()`.
3. Explique por que o Singleton atrapalha testes e como evitá-lo.

## Checklist
- [ ] Aplico Factory para desacoplar criação
- [ ] Uso Builder para objetos complexos
- [ ] Conheço os riscos do Singleton
