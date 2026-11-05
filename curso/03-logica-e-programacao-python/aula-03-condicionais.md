# Aula 3 — Condicionais

**Duração:** ~20 min · **Módulo 3**

## Objetivo
Controlar o fluxo do programa com `if`, `elif`, `else` e expressões booleanas.

## Teoria
- Estrutura: `if cond:` / `elif cond:` / `else:` — o bloco é definido pela indentação.
- Valores **falsy**: `False`, `None`, `0`, `0.0`, `""`, `[]`, `{}`, `()`, `set()`. O resto é **truthy**.
- Operadores lógicos fazem **curto-circuito**: em `a and b`, `b` só é avaliado se `a` for verdadeiro.
- Comparação encadeada: `18 <= idade < 65`.
- `in` testa pertinência: `"a" in "banana"`.
- Expressão condicional: `x = "par" if n % 2 == 0 else "ímpar"`.
- `match/case` (Python 3.10+) para múltiplos casos.
- Use **guard clauses** (retornos/saídas antecipadas) para evitar aninhamento profundo.

## Exemplo em Python
```python
def classificar(nota: float) -> str:
    if nota < 0 or nota > 10:
        return "inválida"
    if nota >= 7:
        return "aprovado"
    elif nota >= 5:
        return "recuperação"
    return "reprovado"

for n in (9.5, 6, 3, 11):
    print(n, classificar(n))

ano = 2024
bissexto = (ano % 4 == 0 and ano % 100 != 0) or ano % 400 == 0
print(ano, "bissexto" if bissexto else "comum")

comando = "listar"
match comando:
    case "adicionar" | "add":
        print("adicionando")
    case "listar":
        print("listando")
    case _:
        print("desconhecido")
```

## Exercício
1. Escreva um programa que leia três lados e diga se formam triângulo (cada lado < soma dos outros) e o tipo (equilátero, isósceles, escaleno).
2. Implemente `fizzbuzz_valor(n)` que retorna "Fizz", "Buzz", "FizzBuzz" ou o número.
3. Reescreva o `classificar` usando `match` com guards ou explique por que `if` é melhor aqui.

## Checklist
- [ ] Uso `if/elif/else` e comparações encadeadas
- [ ] Conheço valores truthy e falsy
- [ ] Evito aninhamento com guard clauses
