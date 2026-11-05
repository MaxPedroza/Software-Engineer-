# Aula 3 — Herança, polimorfismo e abstração

**Duração:** ~25 min · **Módulo 8**

## Objetivo
Usar herança, classes abstratas e polimorfismo para tratar tipos diferentes por uma interface comum.

## Teoria
- **Herança**: uma subclasse reutiliza e especializa a superclasse ("é um").
- **Abstração**: expor *o que* um tipo faz, escondendo *como*. Em Python, use `abc.ABC` e `@abstractmethod`.
- **Polimorfismo**: o mesmo método se comporta de forma diferente conforme o objeto; quem chama não precisa saber o tipo concreto.
- Use `super()` para reaproveitar o comportamento do pai.
- Cuidado: hierarquias profundas ficam frágeis (veja a aula 4).

## Exemplo em Python
```python
from abc import ABC, abstractmethod

class Notificador(ABC):
    @abstractmethod
    def enviar(self, mensagem: str) -> None: ...

class Email(Notificador):
    def enviar(self, mensagem: str) -> None:
        print(f"[email] {mensagem}")

class Sms(Notificador):
    def enviar(self, mensagem: str) -> None:
        print(f"[sms] {mensagem[:20]}")

def avisar(canais: list[Notificador], msg: str) -> None:
    for canal in canais:
        canal.enviar(msg)   # polimorfismo

avisar([Email(), Sms()], "Sua tarefa vence amanhã!")
# Notificador() -> TypeError: classe abstrata
```

## Exercício
1. Crie a classe abstrata `Forma` com `area()` e implemente `Circulo` e `Retangulo`.
2. Escreva uma função que soma as áreas de uma lista de formas sem usar `isinstance`.
3. Adicione `Triangulo` sem alterar a função do item 2. O que isso demonstra?

## Checklist
- [ ] Sei criar classes abstratas
- [ ] Uso polimorfismo em vez de cadeias de `if/elif` por tipo
- [ ] Uso `super()` corretamente
