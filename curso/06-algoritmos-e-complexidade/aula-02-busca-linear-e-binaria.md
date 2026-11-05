# Aula 2 — Busca linear e binária

**Duração:** ~20 min · **Módulo 6**

## Objetivo
Implementar e comparar buscas linear e binária.

## Teoria
- **Busca linear**: percorre item a item. **O(n)**; funciona em qualquer coleção, ordenada ou não.
- **Busca binária**: exige dados **ordenados** e acesso por índice. Compara com o meio e descarta metade a cada passo: **O(log n)**. Em 1 bilhão de itens, ~30 comparações.
- Cuidados: erros "off-by-one", laço infinito por atualizar mal `lo/hi`, e overflow do meio em linguagens com inteiros fixos (`lo + (hi - lo) // 2`).
- Se for buscar muitas vezes, vale pagar O(n log n) para ordenar uma vez (ou usar hash).
- Variações: primeira/última ocorrência, ponto de inserção (`bisect` em Python).

## Exemplo em Python
```python
import bisect

def busca_linear(v, alvo):
    for i, x in enumerate(v):
        if x == alvo:
            return i
    return -1

def busca_binaria(v, alvo):
    lo, hi = 0, len(v) - 1
    while lo <= hi:
        meio = lo + (hi - lo) // 2
        if v[meio] == alvo:
            return meio
        if v[meio] < alvo:
            lo = meio + 1
        else:
            hi = meio - 1
    return -1

v = list(range(0, 1_000_000, 2))
print(busca_linear(v, 999_998), busca_binaria(v, 999_998))  # 499999 499999
print(busca_binaria(v, 7))                                   # -1
print(bisect.bisect_left(v, 7))                              # 4 (ponto de inserção)
```

## Exercício
1. Conte quantas comparações a busca binária faz em 1.024 itens (máximo).
2. Modifique para retornar a **primeira** ocorrência em listas com repetidos.
3. Faça benchmark linear vs binária com `timeit` para n = 10³, 10⁵, 10⁶.

## Checklist
- [ ] Sei o pré-requisito da busca binária
- [ ] Implemento sem erros de limites
- [ ] Uso `bisect` quando apropriado
