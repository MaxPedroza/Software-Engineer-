# Aula 5 — Recursão e backtracking

**Duração:** ~25 min · **Módulo 6**

## Objetivo
Resolver problemas com funções que chamam a si mesmas e explorar espaços de soluções com retrocesso.

## Teoria
- **Recursão**: função que se resolve em termos de versões menores de si mesma. Precisa de **caso base** (para) e **passo recursivo** (aproxima do base).
- Cada chamada ocupa um **frame** na pilha; Python limita a profundidade (~1000; `sys.getrecursionlimit()`) → `RecursionError`.
- Recursão ingênua pode repetir trabalho (Fibonacci recursivo é O(2ⁿ)); **memoização** (`functools.cache`) resolve.
- **Backtracking**: constrói a solução passo a passo; se um caminho viola as restrições, **desfaz** a última escolha e tenta outra (**escolher → explorar → desfazer**). Usos: permutações, N-rainhas, sudoku, labirintos.
- **Poda**: abandonar cedo ramos que não levam a solução reduz muito o custo.

## Exemplo em Python
```python
from functools import cache

def fatorial(n):
    return 1 if n <= 1 else n * fatorial(n - 1)

@cache
def fib(n):
    return n if n < 2 else fib(n - 1) + fib(n - 2)

def permutacoes(itens):
    res, atual, usado = [], [], [False] * len(itens)
    def rec():
        if len(atual) == len(itens):
            res.append(atual[:])
            return
        for i, x in enumerate(itens):
            if not usado[i]:
                usado[i] = True; atual.append(x)   # escolher
                rec()                              # explorar
                atual.pop(); usado[i] = False      # desfazer
    rec()
    return res

def n_rainhas(n):
    cols, d1, d2, cont = set(), set(), set(), 0
    def rec(l):
        nonlocal cont
        if l == n:
            cont += 1
            return
        for c in range(n):
            if c in cols or l - c in d1 or l + c in d2:
                continue                            # poda
            cols.add(c); d1.add(l - c); d2.add(l + c)
            rec(l + 1)
            cols.remove(c); d1.remove(l - c); d2.remove(l + c)
    rec(0)
    return cont

print(fatorial(5), fib(50), len(permutacoes([1, 2, 3])), n_rainhas(6))  # 120 12586269025 6 4
```

## Exercício
1. Escreva uma função recursiva para somar os dígitos de um inteiro.
2. Gere todos os subconjuntos de `[1,2,3]` com backtracking.
3. Teste `fib` sem `@cache` com n = 35 e compare o tempo.

## Checklist
- [ ] Identifico caso base e passo recursivo
- [ ] Uso memoização para evitar repetição
- [ ] Aplico escolher → explorar → desfazer
