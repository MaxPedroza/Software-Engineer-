# Aula 1 — Primeiro programa e como pensar como um programador

**Duração:** ~20 min · **Módulo 3**

## Objetivo
Executar o primeiro programa em Python e aprender a decompor problemas em passos.

## Teoria
- **Algoritmo**: sequência finita e não ambígua de passos que resolve um problema.
- Pensamento computacional: **decomposição** (quebrar o problema), **padrões**, **abstração** e **algoritmo**.
- Python é interpretado, de sintaxe clara e usa **indentação** (4 espaços) para delimitar blocos.
- Rodar: `python3 ola.py` ou o modo interativo `python3` (REPL).
- Funções básicas: `print()` exibe, `input()` lê texto do teclado (sempre `str`).
- Comentários começam com `#`.
- Ao ler um erro (traceback), olhe a **última linha** primeiro: ela diz o tipo e a causa.

## Exemplo em Python
```python
# ola.py
nome = input("Qual é o seu nome? ")
ano = int(input("Em que ano você nasceu? "))
idade = 2026 - ano
print(f"Olá, {nome}! Você tem aproximadamente {idade} anos.")
```

Pseudocódigo → código (média de duas notas):
```
1. ler nota1 e nota2
2. media = (nota1 + nota2) / 2
3. mostrar media
```
```python
n1 = float(input("Nota 1: "))
n2 = float(input("Nota 2: "))
print("Média:", (n1 + n2) / 2)
```

## Exercício
1. Rode `ola.py` e provoque um erro digitando letras no ano. Leia a mensagem do `ValueError`.
2. Escreva o pseudocódigo e o programa que converte graus Celsius em Fahrenheit (`F = C * 9/5 + 32`).
3. Decomponha em passos o problema "calcular o troco de uma compra".

## Checklist
- [ ] Executo scripts Python pelo terminal
- [ ] Uso `print`, `input` e f-strings
- [ ] Sei escrever pseudocódigo antes do código
