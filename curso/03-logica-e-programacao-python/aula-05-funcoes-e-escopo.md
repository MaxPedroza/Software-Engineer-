# Aula 5 — Funções e escopo

**Duração:** ~25 min · **Módulo 3**

## Objetivo
Criar funções reutilizáveis, entender parâmetros, retorno e escopo de variáveis.

## Teoria
- Função: bloco nomeado e reutilizável. Princípios: **uma responsabilidade**, nome de verbo, poucos parâmetros (DRY).
- `def nome(params): ... return valor`. Sem `return`, retorna `None`.
- Parâmetros: posicionais, nomeados (`f(b=2)`), **padrão** (`def f(x, sep=",")`), `*args` e `**kwargs`.
- **Cuidado**: nunca use valor padrão mutável (`def f(l=[])`); use `None` e crie dentro.
- **Escopo (LEGB)**: Local → Enclosing → Global → Built-in. Variáveis criadas dentro da função são locais; `global` evita-se.
- Docstrings e *type hints* documentam: `def f(x: int) -> int:`.
- Funções são valores: podem ser passadas como argumento (`sorted(lista, key=len)`) e `lambda` cria funções curtas.
- **Recursão**: função que chama a si mesma, com caso base.

## Exemplo em Python
```python
def media(*notas: float) -> float:
    """Retorna a média das notas."""
    if not notas:
        raise ValueError("informe ao menos uma nota")
    return sum(notas) / len(notas)

def adicionar(item, lista=None):
    if lista is None:
        lista = []
    lista.append(item)
    return lista

def fatorial(n: int) -> int:
    return 1 if n <= 1 else n * fatorial(n - 1)

x = 10
def mostrar():
    x = 5          # local, não altera o global
    return x

print(media(7, 8, 9.5))
print(adicionar("a"), adicionar("b"))   # ['a'] ['b']
print(fatorial(5), mostrar(), x)        # 120 5 10
print(sorted(["banana", "kiwi", "uva"], key=len))
```

## Exercício
1. Escreva `eh_palindromo(texto)` ignorando espaços e maiúsculas.
2. Escreva `celsius_para_fahrenheit` e `fahrenheit_para_celsius` com type hints e docstrings.
3. Mostre o bug de `def f(l=[])` chamando-a duas vezes e corrija-o.

## Checklist
- [ ] Crio funções com parâmetros padrão e retorno
- [ ] Entendo escopo local e global
- [ ] Evito argumentos padrão mutáveis
