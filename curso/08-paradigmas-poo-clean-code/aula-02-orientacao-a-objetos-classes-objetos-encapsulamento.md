# Aula 2 — Orientação a objetos: classes, objetos, encapsulamento

**Duração:** ~25 min · **Módulo 8**

## Objetivo
Modelar entidades com classes e proteger o estado interno por meio de encapsulamento.

## Teoria
- **Classe**: molde que define atributos (dados) e métodos (comportamento).
- **Objeto/instância**: valor criado a partir da classe, com estado próprio.
- **Encapsulamento**: esconder detalhes internos e expor uma interface pequena, garantindo que o objeto nunca fique em estado inválido.
- Em Python, a convenção `_atributo` indica uso interno; `@property` expõe leitura/validação controlada.
- Prefira **"Tell, don't ask"**: peça ao objeto para fazer algo em vez de ler seus dados e decidir por fora.

## Exemplo em Python
```python
class ContaBancaria:
    def __init__(self, titular: str, saldo: float = 0.0):
        self.titular = titular
        self._saldo = saldo

    @property
    def saldo(self) -> float:
        return self._saldo

    def depositar(self, valor: float) -> None:
        if valor <= 0:
            raise ValueError("valor deve ser positivo")
        self._saldo += valor

    def sacar(self, valor: float) -> None:
        if valor > self._saldo:
            raise ValueError("saldo insuficiente")
        self._saldo -= valor

conta = ContaBancaria("Ana", 100)
conta.depositar(50)
conta.sacar(30)
print(conta.saldo)  # 120
# conta.saldo = 1_000_000  -> AttributeError (sem setter)
```

## Exercício
1. Crie a classe `Tarefa` com `titulo`, `concluida` e método `concluir()`; título vazio deve lançar erro.
2. Impeça que `concluida` seja alterada diretamente de fora.
3. Adicione `__repr__` para imprimir a tarefa de forma legível.

## Checklist
- [ ] Diferencio classe e objeto
- [ ] Uso `@property` e atributos internos
- [ ] Meus objetos validam seu próprio estado
