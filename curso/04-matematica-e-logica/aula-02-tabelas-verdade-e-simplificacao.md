# Aula 2 — Tabelas-verdade e simplificação de expressões

**Duração:** ~25 min · **Módulo 4**

## Objetivo
Construir tabelas-verdade, verificar equivalências e simplificar expressões booleanas.

## Teoria
- Uma tabela-verdade lista todas as combinações de entradas (2ⁿ linhas para n variáveis) e a saída da expressão.
- Duas expressões são **equivalentes** se têm a mesma tabela.
- Exemplo, p ∧ q e p ∨ q:

| p | q | p ∧ q | p ∨ q |
|---|---|-------|-------|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 1 |

- **Simplificação** usa as leis: absorção `a + ab = a`, idempotência `a + a = a`, `a + ¬a = 1`, `a·¬a = 0`, De Morgan.
- Exemplo: `a·b + a·¬b = a·(b + ¬b) = a·1 = a`.
- Formas normais: **soma de produtos** (SOP, OR de ANDs) e **produto de somas**; cada linha com saída 1 vira um termo AND (mintermo).
- Mapas de Karnaugh agrupam 1s adjacentes para simplificar visualmente (até 4 variáveis).
- Útil em circuitos digitais, condições de `if` e consultas SQL complexas.

## Exemplo em Python
```python
from itertools import product

def tabela(expr, nomes):
    print(*nomes, "saida", sep=" | ")
    for valores in product([False, True], repeat=len(nomes)):
        env = dict(zip(nomes, valores))
        print(*(int(v) for v in valores), int(expr(**env)), sep=" | ")

tabela(lambda a, b: (a and b) or (a and not b), ["a", "b"])

def equivalentes(f, g, n):
    return all(f(*v) == g(*v) for v in product([False, True], repeat=n))

print(equivalentes(lambda a, b: (a and b) or (a and not b),
                   lambda a, b: a, 2))                    # True
print(equivalentes(lambda a, b: not (a and b),
                   lambda a, b: not a and not b, 2))      # False
```

## Exercício
1. Monte à mão a tabela de `p → q` e confira com Python.
2. Simplifique `a·b + ¬a·b + a·¬b` e valide com `equivalentes` (resposta: `a + b`).
3. Escreva uma função que, dada uma expressão, diga se é tautologia, contradição ou contingência.

## Checklist
- [ ] Construo tabelas-verdade de 2 a 3 variáveis
- [ ] Simplifico com absorção e De Morgan
- [ ] Verifico equivalência por código
