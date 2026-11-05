# Aula 4 — Funções e notação matemática

**Duração:** ~25 min · **Módulo 4**

## Objetivo
Ler notação matemática (somatório, módulo, piso/teto, log) e entender funções e crescimento.

## Teoria
- **Função** f: A → B associa cada elemento do domínio A a exatamente um do contra-domínio B. Imagem = valores efetivamente atingidos.
- Tipos: **injetora** (valores distintos → imagens distintas), **sobrejetora** (imagem = B), **bijetora** (ambas; tem inversa). Funções hash não são injetoras (colisões).
- Notação útil:
  - Somatório: Σᵢ₌₁ⁿ i = n(n+1)/2.
  - Produtório Π: n! = Π i.
  - Módulo: a mod n (resto); piso ⌊x⌋ e teto ⌈x⌉.
  - Potência e logaritmo: log₂(n) = quantas vezes dividir n por 2 até chegar a 1; log₂(1024) = 10.
- **Composição**: (g ∘ f)(x) = g(f(x)).
- Crescimento (base da análise de algoritmos): log n < n < n log n < n² < 2ⁿ < n!.
- Busca binária em 1 milhão de itens: ~20 passos (log₂), contra 1.000.000 da busca linear.

## Exemplo em Python
```python
import math

def f(x):            # f(x) = 2x + 1
    return 2 * x + 1

def g(x):            # g(x) = x²
    return x ** 2

compor = lambda g, f: (lambda x: g(f(x)))
print(compor(g, f)(3))              # g(f(3)) = 49

print(sum(i for i in range(1, 101)), 100 * 101 // 2)   # 5050 5050
print(math.floor(2.7), math.ceil(2.1), 17 % 5, -7 % 3)  # 2 3 2 2
print(math.log2(1024), math.ceil(math.log2(1_000_000)))  # 10.0 20

def injetora(func, dominio):
    imagens = [func(x) for x in dominio]
    return len(set(imagens)) == len(imagens)

print(injetora(f, range(-3, 4)), injetora(g, range(-3, 4)))  # True False

for n in (10, 20, 30):
    print(n, n ** 2, 2 ** n)
```

## Exercício
1. Calcule Σ de 1 a 50 de i² com Python e confira com n(n+1)(2n+1)/6.
2. Mostre que `x % 10` não é injetora no domínio 0..99 e conte sua imagem.
3. Quantos passos faz a busca binária em 1 bilhão de elementos?

## Checklist
- [ ] Leio notação de somatório e logaritmo
- [ ] Classifico funções (injetora, sobrejetora, bijetora)
- [ ] Comparo taxas de crescimento
