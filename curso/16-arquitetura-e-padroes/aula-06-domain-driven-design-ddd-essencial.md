# Aula 6 — Domain-Driven Design (DDD) essencial

**Duração:** ~25 min · **Módulo 16**

## Objetivo
Modelar o domínio com a linguagem do negócio usando os blocos táticos e estratégicos do DDD.

## Teoria
### Estratégico
- **Linguagem ubíqua**: vocabulário comum entre desenvolvedores e especialistas, usado no código.
- **Domínio e subdomínios**: *core* (diferencial), *suporte* e *genérico* (compre/reuse).
- **Contexto delimitado (Bounded Context)**: fronteira onde um modelo e seus termos têm significado único. "Cliente" em Vendas ≠ "Cliente" em Suporte.
- **Context Map**: relações entre contextos (parceria, cliente-fornecedor, camada anticorrupção).

### Tático
- **Entidade**: tem identidade e ciclo de vida (`Pedido`).
- **Objeto de valor**: definido pelos atributos, imutável (`Dinheiro`, `Email`).
- **Agregado**: grupo de objetos tratado como unidade de consistência, com uma **raiz** que garante invariantes; referências externas só à raiz.
- **Repositório**: abstração de persistência de agregados.
- **Serviço de domínio** e **eventos de domínio** (`PedidoConfirmado`).
- Evite o **modelo anêmico** (só dados, sem comportamento).

## Exemplo em Python
```python
from dataclasses import dataclass, field

@dataclass(frozen=True)
class Dinheiro:                        # objeto de valor
    centavos: int
    def __add__(self, o): return Dinheiro(self.centavos + o.centavos)

@dataclass
class ItemPedido:
    produto_id: int
    preco: Dinheiro
    quantidade: int

@dataclass
class Pedido:                          # raiz do agregado
    id: int
    itens: list[ItemPedido] = field(default_factory=list)
    confirmado: bool = False
    eventos: list[str] = field(default_factory=list)

    def adicionar_item(self, item: ItemPedido):
        if self.confirmado:
            raise ValueError("pedido confirmado não pode mudar")   # invariante
        if item.quantidade <= 0:
            raise ValueError("quantidade inválida")
        self.itens.append(item)

    def total(self) -> Dinheiro:
        total = Dinheiro(0)
        for i in self.itens:
            total += Dinheiro(i.preco.centavos * i.quantidade)
        return total

    def confirmar(self):
        if not self.itens:
            raise ValueError("pedido vazio")
        self.confirmado = True
        self.eventos.append("PedidoConfirmado")
```

## Exercício
1. Escreva a linguagem ubíqua (10 termos) do sistema de tarefas.
2. Identifique entidades, objetos de valor e a raiz do agregado em um `Projeto` com `Tarefas`.
3. Proponha dois bounded contexts e explique um termo que muda de sentido entre eles.

## Checklist
- [ ] Uso linguagem ubíqua no código
- [ ] Diferencio entidade, objeto de valor e agregado
- [ ] Identifico bounded contexts
