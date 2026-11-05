# Aula 4 — Ordenação eficiente (merge, quick, heap)

**Duração:** ~25 min · **Módulo 6**

## Objetivo
Implementar ordenações O(n log n) e comparar suas propriedades.

## Teoria
- **Merge sort**: divide ao meio, ordena cada metade e **intercala**. Sempre O(n log n); estável; usa O(n) de memória extra.
- **Quick sort**: escolhe um **pivô**, separa menores e maiores, ordena recursivamente. Médio O(n log n); pior caso O(n²) com pivô ruim (ex.: sempre o primeiro em lista ordenada). Pivô aleatório/mediana mitiga. In-place na versão clássica; não estável.
- **Heap sort**: monta um heap e extrai o mínimo. O(n log n) garantido; in-place; não estável.
- Limite teórico: ordenação por comparação não passa de Ω(n log n).
- Não comparativos (counting, radix) podem ser O(n) com restrições nos dados.

| Algoritmo | Médio | Pior | Memória | Estável |
|---|---|---|---|---|
| Merge | n log n | n log n | O(n) | sim |
| Quick | n log n | n² | O(log n) | não |
| Heap | n log n | n log n | O(1) | não |

## Exemplo em Python
```python
import heapq, random

def merge_sort(v):
    if len(v) <= 1:
        return v
    m = len(v) // 2
    a, b = merge_sort(v[:m]), merge_sort(v[m:])
    r, i, j = [], 0, 0
    while i < len(a) and j < len(b):
        if a[i] <= b[j]: r.append(a[i]); i += 1
        else: r.append(b[j]); j += 1
    return r + a[i:] + b[j:]

def quick_sort(v):
    if len(v) <= 1:
        return v
    p = random.choice(v)
    return (quick_sort([x for x in v if x < p])
            + [x for x in v if x == p]
            + quick_sort([x for x in v if x > p]))

def heap_sort(v):
    h = v[:]
    heapq.heapify(h)
    return [heapq.heappop(h) for _ in range(len(h))]

dados = [random.randint(0, 100) for _ in range(50)]
assert merge_sort(dados) == quick_sort(dados) == heap_sort(dados) == sorted(dados)
```

## Exercício
1. Meça os três com n = 10⁵ e compare com bubble sort em n = 5.000.
2. Faça o quick sort usar sempre o primeiro elemento como pivô e teste em lista ordenada (observe o limite de recursão).
3. Implemente o merge in-place com índices.

## Checklist
- [ ] Explico o pior caso do quick sort
- [ ] Sei quando o merge sort é preferível
- [ ] Comparo algoritmos com benchmark
