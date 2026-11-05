# Aula 2 — Variáveis, tipos e operadores

**Duração:** ~25 min · **Módulo 3**

## Objetivo
Usar variáveis, tipos básicos, conversões e operadores aritméticos, de comparação e lógicos.

## Teoria
- **Variável**: nome que referencia um valor. Python tem tipagem **dinâmica** (o tipo é do valor): `type(x)`.
- Tipos básicos: `int`, `float`, `str`, `bool`, `None`.
- Conversão: `int("5")`, `float("2.5")`, `str(10)`, `bool(0)` → `False`.
- Operadores aritméticos: `+ - * / // % **` (`/` sempre dá `float`; `//` divisão inteira; `%` resto).
- Comparação: `== != < > <= >=`. Lógicos: `and`, `or`, `not`.
- Strings: imutáveis; fatiamento `s[0:3]`, métodos `.upper()`, `.strip()`, `.split()`, `.replace()`.
- Convenção: `snake_case` para nomes; constantes em `MAIUSCULAS`.
- Lembre da Aula 2 do Módulo 1: `0.1 + 0.2 != 0.3`; use `round()` ou `math.isclose`.

## Exemplo em Python
```python
preco = 49.90
quantidade = 3
total = preco * quantidade
print(f"Total: R$ {total:.2f}")      # 149.70

print(17 // 5, 17 % 5, 2 ** 10)      # 3 2 1024
print(type(preco), type(quantidade), type("x"), type(True))

idade = int("21")
maior = idade >= 18 and idade < 65
print(maior)                          # True

nome = "  ana silva "
print(nome.strip().title())           # Ana Silva
print(0.1 + 0.2 == 0.3, round(0.1 + 0.2, 2) == 0.3)   # False True
```

## Exercício
1. Calcule a área e o perímetro de um círculo de raio 5 (use `import math`).
2. Dado `segundos = 3725`, calcule horas, minutos e segundos restantes com `//` e `%`.
3. Preveja e depois confira: `"5" + "3"`, `int("5") + 3`, `"ab" * 3`, `10 / 4`, `10 // 4`.

## Checklist
- [ ] Conheço os tipos básicos e convertê-los
- [ ] Uso `//`, `%` e `**` corretamente
- [ ] Formato números com f-strings
