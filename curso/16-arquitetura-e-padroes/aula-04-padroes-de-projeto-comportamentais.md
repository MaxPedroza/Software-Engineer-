# Aula 4 — Padrões de projeto: comportamentais

**Duração:** ~20 min · **Módulo 16**

## Objetivo
Aplicar Strategy, Observer e Command para organizar responsabilidades e comunicação entre objetos.

## Teoria
Padrões **comportamentais** definem como objetos interagem e distribuem responsabilidades.
- **Strategy**: família de algoritmos intercambiáveis atrás de uma interface; elimina `if/elif` extensos (princípio aberto/fechado).
- **Observer**: um sujeito notifica vários observadores sobre mudanças (base de eventos e pub/sub).
- **Command**: encapsula uma ação como objeto (fila, desfazer/refazer, log).
- **State**: o comportamento muda conforme o estado interno.
- **Template Method**: define o esqueleto de um algoritmo; subclasses preenchem passos.
- **Chain of Responsibility**: requisição passa por uma cadeia de handlers (middlewares).
- **Iterator**: percorre coleções sem expor sua estrutura (`__iter__` em Python).
- Em linguagens com funções de primeira classe, Strategy e Command costumam ser simples funções.

## Exemplo em Python
```python
from typing import Callable, Protocol

# Strategy
class Desconto(Protocol):
    def __call__(self, valor: float) -> float: ...

def sem_desconto(v): return v
def black_friday(v): return v * 0.7
def cupom_10(v): return v - 10

def total(valor: float, desconto: Desconto = sem_desconto) -> float:
    return max(desconto(valor), 0)

# Observer
class Evento:
    def __init__(self): self._ouvintes: list[Callable] = []
    def inscrever(self, fn): self._ouvintes.append(fn)
    def emitir(self, *args): [fn(*args) for fn in self._ouvintes]

tarefa_concluida = Evento()
tarefa_concluida.inscrever(lambda t: print(f"E-mail: '{t}' concluída"))
tarefa_concluida.inscrever(lambda t: print(f"Métrica: +1 concluída"))
tarefa_concluida.emitir("Entregar relatório")

# Command com desfazer
class Pilha:
    def __init__(self): self.itens, self.historico = [], []
    def executar(self, cmd, desfazer): cmd(); self.historico.append(desfazer)
    def desfazer(self): self.historico.pop()()

p = Pilha()
p.executar(lambda: p.itens.append("a"), lambda: p.itens.pop())
p.desfazer()
print(total(100, black_friday))  # 70.0
```

## Exercício
1. Adicione uma estratégia `frete_gratis` e um teste para cada estratégia.
2. Faça o Observer remover ouvintes (`cancelar`) e trate exceções de um ouvinte sem afetar os outros.
3. Substitua um `if/elif` do seu projeto por Strategy.

## Checklist
- [ ] Aplico Strategy no lugar de condicionais longas
- [ ] Implemento Observer/eventos
- [ ] Entendo Command e Chain of Responsibility
