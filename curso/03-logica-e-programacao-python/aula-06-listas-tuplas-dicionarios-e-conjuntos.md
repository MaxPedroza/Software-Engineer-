# Aula 6 — Listas, tuplas, dicionários e conjuntos

**Duração:** ~30 min · **Módulo 3**

## Objetivo
Escolher e usar as estruturas de dados nativas do Python.

## Teoria
| Estrutura | Sintaxe | Mutável | Ordenada | Característica |
|-----------|---------|---------|----------|----------------|
| `list` | `[1, 2]` | sim | sim | sequência geral, permite repetidos |
| `tuple` | `(1, 2)` | não | sim | registro fixo, pode ser chave de dict |
| `dict` | `{"a": 1}` | sim | por inserção | chave → valor, busca O(1) |
| `set` | `{1, 2}` | sim | não | elementos únicos, operações de conjunto |

- Listas: `append`, `extend`, `insert`, `pop`, `remove`, `sort()` (in-place), `sorted()` (nova), fatiamento `l[1:3]`, `l[::-1]`.
- Dicionários: `d[k]` (KeyError se faltar), `d.get(k, padrão)`, `d.items()`, `d.setdefault`, `del d[k]`.
- Conjuntos: `|` união, `&` interseção, `-` diferença; ideais para remover duplicados e testar pertinência.
- Desempacotamento: `a, b = (1, 2)`; `primeiro, *resto = lista`.
- Cópia: `b = a` aponta para a mesma lista; use `a.copy()` ou `a[:]`.

## Exemplo em Python
```python
tarefas = [
    {"id": 1, "titulo": "Estudar", "feita": False},
    {"id": 2, "titulo": "Treinar", "feita": True},
]
tarefas.append({"id": 3, "titulo": "Ler", "feita": False})
pendentes = [t["titulo"] for t in tarefas if not t["feita"]]
print(pendentes)  # ['Estudar', 'Ler']

texto = "a vida é bela e a vida é curta"
freq = {}
for palavra in texto.split():
    freq[palavra] = freq.get(palavra, 0) + 1
print(freq["vida"])  # 2

a, b = {1, 2, 3, 4}, {3, 4, 5}
print(a & b, a | b, a - b)
print(list(dict.fromkeys([3, 1, 3, 2, 1])))  # [3, 1, 2] sem duplicados, mantém a ordem
ponto = (2, 5)
x, y = ponto
```

## Exercício
1. Dada uma lista de números, produza listas separadas de pares e ímpares e a soma de cada uma.
2. Conte a frequência de letras de uma frase e mostre as 3 mais comuns (`sorted(..., key=..., reverse=True)`).
3. Dadas duas listas de e-mails, encontre os que aparecem nas duas e os exclusivos da primeira.

## Checklist
- [ ] Sei escolher entre lista, tupla, dict e set
- [ ] Uso `.get()` e `.items()` em dicionários
- [ ] Entendo cópia vs referência
