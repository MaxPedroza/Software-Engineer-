# Aula 6 — Princípios SOLID

**Duração:** ~30 min · **Módulo 8**

## Objetivo
Aplicar os cinco princípios SOLID para criar classes coesas e com baixo acoplamento.

## Teoria
- **S — Responsabilidade Única**: uma classe tem um único motivo para mudar.
- **O — Aberto/Fechado**: aberta para extensão, fechada para modificação (adicione código novo, não edite o antigo).
- **L — Substituição de Liskov**: subtipos devem poder substituir o tipo base sem quebrar o comportamento esperado.
- **I — Segregação de Interfaces**: várias interfaces pequenas são melhores que uma grande.
- **D — Inversão de Dependência**: dependa de abstrações, não de implementações concretas.

## Exemplo em Python (O e D)
```python
from abc import ABC, abstractmethod

class Desconto(ABC):
    @abstractmethod
    def aplicar(self, valor: float) -> float: ...

class SemDesconto(Desconto):
    def aplicar(self, valor): return valor

class BlackFriday(Desconto):
    def aplicar(self, valor): return valor * 0.7

class Pedido:
    def __init__(self, valor: float, desconto: Desconto):  # depende da abstração
        self.valor = valor
        self.desconto = desconto
    def total(self) -> float:
        return self.desconto.aplicar(self.valor)

print(Pedido(100, BlackFriday()).total())  # 70.0
```
Novos descontos entram criando classes, sem alterar `Pedido` (Aberto/Fechado).

**Violação de Liskov clássica:** `Quadrado(Retangulo)` que altera largura e altura juntas quebra expectativas de quem usa `Retangulo`.

## Exercício
1. Separe uma classe `Relatorio` que calcula, formata e envia e-mail em três classes (S).
2. Remova um `if tipo == "pix"` de um `Pagamento` usando polimorfismo (O).
3. Faça `ServicoTarefas` receber um `Repositorio` abstrato (D).

## Checklist
- [ ] Explico cada letra do SOLID com um exemplo
- [ ] Identifico violações de SRP e OCP
- [ ] Dependo de abstrações nas minhas classes
