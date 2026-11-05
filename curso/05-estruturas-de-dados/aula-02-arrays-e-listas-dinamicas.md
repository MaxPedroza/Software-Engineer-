# Aula 2 — Arrays e listas dinâmicas

**Duração:** ~20 min · **Módulo 5**

## Objetivo
Entender como arrays funcionam na memória e por que `append` é eficiente em média.

## Teoria
- **Array**: elementos de mesmo tamanho em memória contígua. O endereço do item `i` é `base + i * tamanho`, logo o acesso por índice é **O(1)**.
- **Lista dinâmica** (`list` do Python, `ArrayList` do Java): array que cresce. Quando enche, aloca um bloco maior (ex.: ~2×) e copia os itens.
- **Custo amortizado**: a cópia é cara, mas rara; `append` é **O(1) amortizado**.
- Inserir/remover no início ou meio é **O(n)** (deslocamento de elementos).
- Vantagens: acesso rápido, boa localidade de cache. Desvantagens: inserção no meio custosa, realocações.

| Operação | Custo |
|---|---|
| `a[i]` | O(1) |
| `a.append(x)` | O(1) amortizado |
| `a.insert(0, x)` / `a.pop(0)` | O(n) |
| `x in a` | O(n) |

## Exemplo em Python
```python
import sys

a = []
ultimo = sys.getsizeof(a)
for i in range(40):
    a.append(i)
    tam = sys.getsizeof(a)
    if tam != ultimo:          # houve realocação
        print(f"len={len(a):2d} bytes={tam}")
        ultimo = tam

class ListaDinamica:
    def __init__(self):
        self._cap, self._n = 2, 0
        self._dados = [None] * self._cap

    def append(self, x):
        if self._n == self._cap:
            self._cap *= 2
            novo = [None] * self._cap
            novo[:self._n] = self._dados[:self._n]
            self._dados = novo
        self._dados[self._n] = x
        self._n += 1

    def __getitem__(self, i):
        if not 0 <= i < self._n:
            raise IndexError(i)
        return self._dados[i]

    def __len__(self):
        return self._n
```

## Exercício
1. Rode o código e identifique quando a capacidade cresce.
2. Implemente `insert(i, x)` em `ListaDinamica` deslocando elementos.
3. Meça `pop(0)` vs `pop()` em uma lista de 100 mil itens.

## Checklist
- [ ] Explico por que o acesso por índice é O(1)
- [ ] Entendo custo amortizado
- [ ] Sei quando evitar inserções no início
