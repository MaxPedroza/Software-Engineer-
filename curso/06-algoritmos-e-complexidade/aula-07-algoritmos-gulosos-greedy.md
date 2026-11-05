# Aula 7 — Algoritmos gulosos (greedy)

**Duração:** ~20 min · **Módulo 6**

## Objetivo
Entender quando escolher sempre a melhor opção local leva ao ótimo global.

## Teoria
- **Guloso**: a cada passo toma a decisão que parece melhor **agora**, sem voltar atrás.
- Funciona quando o problema tem **propriedade de escolha gulosa** e **subestrutura ótima**. Quando não tem, o resultado pode ser apenas aproximado.
- Geralmente é simples e rápido (ordenação + varredura: O(n log n)).
- Clássicos que funcionam: **seleção de atividades**, **mochila fracionária**, **Huffman**, **árvore geradora mínima** (Kruskal/Prim), **Dijkstra**.
- Armadilha: **troco** com moedas arbitrárias. Com {1, 5, 10, 25} o guloso é ótimo; com {1, 3, 4} para 6 dá 4+1+1 (3 moedas) em vez de 3+3 (2 moedas).

## Exemplo em Python
```python
def selecao_atividades(atividades):
    """atividades: lista de (inicio, fim). Maximiza quantidade sem sobreposição."""
    escolhidas, fim_atual = [], float("-inf")
    for ini, fim in sorted(atividades, key=lambda a: a[1]):
        if ini >= fim_atual:
            escolhidas.append((ini, fim))
            fim_atual = fim
    return escolhidas

def troco_guloso(valor, moedas):
    res = []
    for m in sorted(moedas, reverse=True):
        while valor >= m:
            valor -= m
            res.append(m)
    return res

print(selecao_atividades([(1, 4), (3, 5), (0, 6), (5, 7), (8, 9), (5, 9)]))
# [(1, 4), (5, 7), (8, 9)]
print(troco_guloso(36, [1, 5, 10, 25]))  # [25, 10, 1]
print(troco_guloso(6, [1, 3, 4]))        # [4, 1, 1]  -> não é ótimo!
```

## Exercício
1. Implemente a mochila fracionária (ordenar por valor/peso).
2. Mostre um contraexemplo em que o guloso falha para o troco.
3. Dados tempos de tarefas, ordene para minimizar o tempo médio de espera (menor primeiro) e prove por exemplo.

## Checklist
- [ ] Explico a escolha gulosa
- [ ] Sei que guloso nem sempre é ótimo
- [ ] Resolvo seleção de atividades
