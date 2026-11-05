# Aula 7 — Heaps e filas de prioridade

**Duração:** ~20 min · **Módulo 5**

## Objetivo
Usar heaps para obter sempre o menor (ou maior) elemento de forma eficiente.

## Teoria
- **Fila de prioridade**: TAD em que `pop` retorna o elemento de maior prioridade, não o mais antigo.
- **Heap binário**: árvore binária **completa** onde todo pai ≤ filhos (**min-heap**) ou ≥ (**max-heap**). Não é uma árvore ordenada: só o topo é garantido.
- Armazenada em array: para o índice `i`, filhos em `2i+1` e `2i+2`, pai em `(i-1)//2`.
- `push`: coloca no fim e **sobe** (sift-up) — O(log n). `pop`: troca raiz com o último, remove e **desce** (sift-down) — O(log n). `peek`: O(1).
- Construir heap de n itens: O(n). Usos: agendador de tarefas, Dijkstra, top-k, heapsort.
- Em Python: módulo `heapq` (min-heap).

## Exemplo em Python
```python
import heapq

class MinHeap:
    def __init__(self): self.a = []

    def push(self, x):
        a = self.a
        a.append(x)
        i = len(a) - 1
        while i > 0 and a[(i - 1) // 2] > a[i]:
            p = (i - 1) // 2
            a[p], a[i] = a[i], a[p]
            i = p

    def pop(self):
        a = self.a
        a[0], a[-1] = a[-1], a[0]
        menor = a.pop()
        i = 0
        while True:
            e, d, m = 2 * i + 1, 2 * i + 2, i
            if e < len(a) and a[e] < a[m]: m = e
            if d < len(a) and a[d] < a[m]: m = d
            if m == i: break
            a[i], a[m] = a[m], a[i]
            i = m
        return menor

h = MinHeap()
for x in (5, 2, 8, 1, 9): h.push(x)
print([h.pop() for _ in range(5)])  # [1, 2, 5, 8, 9]

tarefas = []
heapq.heappush(tarefas, (2, "escrever testes"))
heapq.heappush(tarefas, (1, "corrigir bug"))
print(heapq.heappop(tarefas))  # (1, 'corrigir bug')
print(heapq.nlargest(2, [4, 9, 1, 7]))  # [9, 7]
```

## Exercício
1. Faça `pop()` tratar heap vazia com `IndexError`.
2. Use `heapq` para achar os 3 maiores de uma lista de 1 milhão de números.
3. Simule um agendador com prioridades e desempate por ordem de chegada.

## Checklist
- [ ] Explico a propriedade do heap
- [ ] Sei mapear índices pai/filho no array
- [ ] Uso `heapq` em problemas top-k
