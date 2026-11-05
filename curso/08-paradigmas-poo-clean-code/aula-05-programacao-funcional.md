# Aula 5 — Programação funcional (imutabilidade, funções puras, map/filter/reduce)

**Duração:** ~25 min · **Módulo 8**

## Objetivo
Aplicar conceitos funcionais para escrever código previsível e fácil de testar.

## Teoria
- **Função pura**: mesmo input → mesmo output, sem efeitos colaterais (não altera globais, não faz I/O).
- **Imutabilidade**: em vez de modificar dados, crie novos. Reduz bugs de estado compartilhado e de concorrência.
- **Funções de primeira classe**: funções podem ser passadas como argumento e retornadas.
- **map** transforma cada elemento; **filter** seleciona; **reduce** agrega em um único valor.
- Em Python, *list comprehensions* costumam ser mais legíveis que `map`/`filter`.

## Exemplo em Python
```python
from functools import reduce
from dataclasses import dataclass, replace

# Impura: altera o argumento
def adicionar_impuro(lista, x):
    lista.append(x)
    return lista

# Pura: devolve nova lista
def adicionar(lista, x):
    return [*lista, x]

nums = [1, 2, 3, 4, 5, 6]
pares   = list(filter(lambda n: n % 2 == 0, nums))   # [2, 4, 6]
quadr   = list(map(lambda n: n * n, pares))          # [4, 16, 36]
soma    = reduce(lambda a, b: a + b, quadr, 0)       # 56
print(soma, sum(n * n for n in nums if n % 2 == 0))  # 56 56

@dataclass(frozen=True)
class Tarefa:
    titulo: str
    concluida: bool = False

t1 = Tarefa("Estudar")
t2 = replace(t1, concluida=True)   # t1 permanece intacta
```

## Exercício
1. Reescreva um laço que soma o salário de funcionários ativos usando `filter` + `reduce`.
2. Converta `concluir(tarefa)` para devolver uma nova `Tarefa` imutável.
3. Identifique o efeito colateral em `def f(x): print(x); return x*2`.

## Checklist
- [ ] Reconheço funções puras e impuras
- [ ] Uso `map`/`filter`/`reduce` ou comprehensions
- [ ] Uso dataclasses imutáveis (`frozen=True`)
