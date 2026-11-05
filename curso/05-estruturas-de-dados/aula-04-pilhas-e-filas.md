# Aula 4 — Pilhas e filas

**Duração:** ~20 min · **Módulo 5**

## Objetivo
Dominar os TADs pilha (LIFO) e fila (FIFO) e suas implementações eficientes.

## Teoria
- **Pilha (stack)**: último a entrar, primeiro a sair (**LIFO**). Operações: `push`, `pop`, `peek`. Usos: desfazer/refazer, pilha de chamadas, validação de parênteses, DFS.
- **Fila (queue)**: primeiro a entrar, primeiro a sair (**FIFO**). Operações: `enqueue`, `dequeue`. Usos: filas de tarefas, impressão, BFS, buffers.
- **Deque**: inserção/remoção nas duas pontas em O(1).
- Pilha com `list` (`append`/`pop`) é O(1). Fila com `list.pop(0)` é **O(n)** — use `collections.deque` ou lista ligada com cauda.

## Exemplo em Python
```python
from collections import deque

class Pilha:
    def __init__(self): self._d = []
    def push(self, x): self._d.append(x)
    def pop(self):
        if not self._d: raise IndexError("pilha vazia")
        return self._d.pop()
    def peek(self): return self._d[-1]
    def vazia(self): return not self._d

class Fila:
    def __init__(self): self._d = deque()
    def enqueue(self, x): self._d.append(x)
    def dequeue(self):
        if not self._d: raise IndexError("fila vazia")
        return self._d.popleft()
    def vazia(self): return not self._d

def balanceado(s):
    pares = {")": "(", "]": "[", "}": "{"}
    p = Pilha()
    for c in s:
        if c in "([{": p.push(c)
        elif c in pares:
            if p.vazia() or p.pop() != pares[c]: return False
    return p.vazia()

print(balanceado("{[()]}"), balanceado("(]"))  # True False
```

## Exercício
1. Use a `Pilha` para avaliar uma expressão pós-fixa (`3 4 + 2 *` = 14).
2. Implemente uma fila com duas pilhas.
3. Simule um atendimento: 5 clientes chegam e são atendidos em ordem.

## Checklist
- [ ] Diferencio LIFO e FIFO
- [ ] Sei por que `pop(0)` é ruim para filas
- [ ] Resolvi o problema dos parênteses balanceados
