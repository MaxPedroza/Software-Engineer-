# Aula 6 — Divisão e conquista

**Duração:** ~20 min · **Módulo 6**

## Objetivo
Aplicar o paradigma de dividir um problema, resolver as partes e combinar os resultados.

## Teoria
- Três etapas: **dividir** em subproblemas menores e independentes, **conquistar** (resolver, recursivamente) e **combinar**.
- Exemplos: merge sort, quick sort, busca binária, exponenciação rápida, multiplicação de Karatsuba, FFT.
- **Recorrência**: `T(n) = a·T(n/b) + f(n)`. Merge sort: `T(n) = 2T(n/2) + O(n)` → **O(n log n)**. Busca binária: `T(n) = T(n/2) + O(1)` → O(log n).
- **Teorema mestre** resume os casos conforme o custo da divisão/combinação vs o número de subproblemas.
- Diferença para programação dinâmica: aqui os subproblemas **não se repetem**; na PD, sim.

## Exemplo em Python
```python
def potencia(base, exp):
    """Exponenciação rápida: O(log exp) multiplicações."""
    if exp == 0:
        return 1
    meia = potencia(base, exp // 2)
    return meia * meia if exp % 2 == 0 else meia * meia * base

def maior_soma_subarray(v, lo=0, hi=None):
    """Soma máxima de subvetor contíguo em O(n log n)."""
    if hi is None:
        hi = len(v) - 1
    if lo == hi:
        return v[lo]
    meio = (lo + hi) // 2
    esq = maior_soma_subarray(v, lo, meio)
    dir_ = maior_soma_subarray(v, meio + 1, hi)
    s, melhor_e = 0, float("-inf")
    for i in range(meio, lo - 1, -1):
        s += v[i]; melhor_e = max(melhor_e, s)
    s, melhor_d = 0, float("-inf")
    for i in range(meio + 1, hi + 1):
        s += v[i]; melhor_d = max(melhor_d, s)
    return max(esq, dir_, melhor_e + melhor_d)

print(potencia(2, 30))                                    # 1073741824
print(maior_soma_subarray([-2, 1, -3, 4, -1, 2, 1, -5, 4]))  # 6
```

## Exercício
1. Escreva a recorrência da `potencia` e resolva-a.
2. Encontre o máximo de uma lista dividindo-a ao meio.
3. Conte inversões de uma lista adaptando o merge sort.

## Checklist
- [ ] Reconheço as três etapas do paradigma
- [ ] Escrevo uma recorrência simples
- [ ] Distingo divisão e conquista de PD
