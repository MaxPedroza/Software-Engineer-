# Aula 1 — Paradigmas de programação

**Duração:** ~20 min · **Módulo 8**

## Objetivo
Reconhecer os principais paradigmas e saber escolher o estilo adequado para cada problema.

## Teoria
Um **paradigma** é um modo de organizar e pensar o código. Linguagens modernas costumam ser **multiparadigma**.
- **Imperativo/procedural**: sequência de comandos que mudam estado; código dividido em funções (C, Python procedural).
- **Orientado a objetos (POO)**: dados e comportamento juntos em objetos que trocam mensagens (Java, Python, C#).
- **Funcional**: computação como composição de funções puras, sem mutação de estado (Haskell, Elixir; recursos em Python/JS).
- **Declarativo**: descreve *o quê*, não *como* (SQL, HTML).

Não existe paradigma "melhor": POO modela bem entidades com ciclo de vida; funcional brilha em transformação de dados; procedural é ótimo para scripts simples.

## Exemplo em Python
Somar o preço dos itens caros, em três estilos:
```python
itens = [{"preco": 10}, {"preco": 250}, {"preco": 90}]

# Imperativo
total = 0
for i in itens:
    if i["preco"] > 50:
        total += i["preco"]

# Funcional
total_f = sum(i["preco"] for i in itens if i["preco"] > 50)

# POO
class Carrinho:
    def __init__(self, itens):
        self.itens = itens
    def total_caros(self, minimo=50):
        return sum(i["preco"] for i in self.itens if i["preco"] > minimo)

print(total, total_f, Carrinho(itens).total_caros())  # 340 340 340
```

## Exercício
1. Reescreva o cálculo de média de uma lista de notas em estilo imperativo e funcional.
2. Classifique em paradigma: uma consulta SQL, uma classe `ContaBancaria`, uma função `map`.
3. Em qual estilo você implementaria a CLI de tarefas? Justifique em 3 linhas.

## Checklist
- [ ] Diferencio imperativo, POO, funcional e declarativo
- [ ] Sei que linguagens podem misturar paradigmas
- [ ] Escolho o estilo conforme o problema
