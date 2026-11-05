# Aula 4 — Laços de repetição

**Duração:** ~25 min · **Módulo 3**

## Objetivo
Repetir ações com `for` e `while`, controlando o laço com `break`, `continue` e `range`.

## Teoria
- `for x in iterável:` percorre listas, strings, `range`, dicionários, arquivos.
- `range(inicio, fim, passo)`: o **fim é exclusivo**. `range(5)` → 0..4.
- `while cond:` repete enquanto a condição for verdadeira; garanta que algo muda para evitar laço infinito.
- `break` sai do laço; `continue` pula para a próxima iteração; `else` do laço roda se não houve `break`.
- Auxiliares: `enumerate(lista)` (índice + valor), `zip(a, b)` (em paralelo).
- Padrões comuns: **acumulador** (soma), **contador**, **busca** e **validação de entrada**.
- List comprehension: `[x**2 for x in range(5) if x % 2 == 0]`.

## Exemplo em Python
```python
soma = 0
for n in range(1, 101):
    soma += n
print(soma)  # 5050

for i, fruta in enumerate(["maçã", "pera", "uva"], start=1):
    print(i, fruta)

def eh_primo(n: int) -> bool:
    if n < 2:
        return False
    for d in range(2, int(n ** 0.5) + 1):
        if n % d == 0:
            return False
    return True

print([n for n in range(30) if eh_primo(n)])

# Validação de entrada com while
while True:
    texto = input("Digite um número positivo: ")
    if texto.isdigit() and int(texto) > 0:
        break
    print("Inválido, tente de novo.")
```

## Exercício
1. Imprima a tabuada do 7 (de 1 a 10) usando `for`.
2. Calcule o fatorial de `n` com `while` e confira com `math.factorial`.
3. Gere os 15 primeiros termos de Fibonacci e some os pares.

## Checklist
- [ ] Diferencio `for` de `while`
- [ ] Uso `range`, `enumerate`, `break` e `continue`
- [ ] Evito laços infinitos
