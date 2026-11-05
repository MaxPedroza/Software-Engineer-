# Aula 5 — Análise combinatória

**Duração:** ~25 min · **Módulo 4**

## Objetivo
Contar possibilidades com princípio multiplicativo, permutações, arranjos e combinações.

## Teoria
- **Princípio multiplicativo**: se há m modos de fazer uma coisa e n de outra, há m·n modos de fazer ambas. Ex.: senha de 4 dígitos = 10⁴ = 10.000.
- **Fatorial**: n! = n·(n−1)·…·1; 0! = 1.
- **Permutação** (ordem importa, usa todos): P(n) = n!. Anagramas de "CASA" (A repete): 4!/2! = 12.
- **Arranjo** (ordem importa, escolhe k de n): A(n,k) = n!/(n−k)!.
- **Combinação** (ordem não importa): C(n,k) = n!/(k!(n−k)!).
- Escolha: "ordem importa?" sim → arranjo; não → combinação.
- Com repetição permitida: n^k (ex.: senhas).
- Aplicações: tamanho de espaço de senhas (segurança), casos de teste, número de comparações em pares (n(n−1)/2), crescimento exponencial/fatorial de força bruta.

## Exemplo em Python
```python
import math
from itertools import permutations, combinations

print(math.factorial(5))        # 120
print(math.perm(5, 2))          # arranjo A(5,2) = 20
print(math.comb(5, 2))          # combinação C(5,2) = 10

print(len(list(permutations("ABC"))))      # 6
print(list(combinations("ABCD", 2)))       # 6 pares

# Espaço de senhas
print(10 ** 4)                  # 4 dígitos
print(62 ** 8)                  # 8 caracteres alfanuméricos: ~2,18e14

# Apertos de mão entre 10 pessoas
n = 10
print(math.comb(n, 2), n * (n - 1) // 2)    # 45 45

# Mega-Sena: escolher 6 de 60
print(math.comb(60, 6))         # 50063860
```

## Exercício
1. De quantas maneiras 5 pessoas podem sentar em fila? E escolher 3 delas para um comitê?
2. Quantas senhas de 6 caracteres com letras minúsculas e dígitos existem? Quanto tempo levaria testando 10⁹ por segundo?
3. Quantos pares de testes existem em um conjunto de 12 funcionalidades combinadas duas a duas?

## Checklist
- [ ] Aplico o princípio multiplicativo
- [ ] Diferencio arranjo e combinação
- [ ] Calculo com `math.perm` e `math.comb`
