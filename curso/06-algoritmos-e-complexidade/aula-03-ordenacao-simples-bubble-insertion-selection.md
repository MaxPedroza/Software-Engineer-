# Aula 3 — Ordenação simples (bubble, insertion, selection)

**Duração:** ~25 min · **Módulo 6**

## Objetivo
Implementar os três algoritmos de ordenação quadráticos e saber quando cada um é aceitável.

## Teoria
- **Bubble sort**: compara vizinhos e troca; maiores "flutuam" ao fim. O(n²); com flag de "sem trocas" o melhor caso é O(n).
- **Selection sort**: acha o menor do restante e coloca na posição. Sempre O(n²), mas faz só O(n) trocas.
- **Insertion sort**: insere cada item na parte já ordenada. Pior O(n²), **melhor O(n)** em dados quase ordenados; é rápido para listas pequenas.
- Todos usam O(1) de memória extra (in-place).
- **Estável**: mantém a ordem de itens iguais. Bubble e insertion são estáveis; selection (versão com troca) não é.
- Na prática, usa-se `sorted()` (Timsort, O(n log n), combina insertion + merge).

## Exemplo em Python
```python
def bubble(v):
    v = v[:]
    for fim in range(len(v) - 1, 0, -1):
        trocou = False
        for i in range(fim):
            if v[i] > v[i + 1]:
                v[i], v[i + 1] = v[i + 1], v[i]
                trocou = True
        if not trocou:
            break
    return v

def selection(v):
    v = v[:]
    for i in range(len(v)):
        m = min(range(i, len(v)), key=v.__getitem__)
        v[i], v[m] = v[m], v[i]
    return v

def insertion(v):
    v = v[:]
    for i in range(1, len(v)):
        x, j = v[i], i - 1
        while j >= 0 and v[j] > x:
            v[j + 1] = v[j]
            j -= 1
        v[j + 1] = x
    return v

dados = [5, 2, 9, 1, 5, 6]
assert bubble(dados) == selection(dados) == insertion(dados) == sorted(dados)
print(insertion(dados))  # [1, 2, 5, 5, 6, 9]
```

## Exercício
1. Conte comparações e trocas de cada algoritmo em uma lista aleatória de 1.000 itens.
2. Teste com lista já ordenada: qual é mais rápido? Por quê?
3. Ordene tuplas `(nome, idade)` por idade e verifique a estabilidade.

## Checklist
- [ ] Implemento os três algoritmos
- [ ] Explico estabilidade
- [ ] Sei por que usar `sorted()` na prática
