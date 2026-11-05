# Aula 8 — Programação dinâmica

**Duração:** ~25 min · **Módulo 6**

## Objetivo
Resolver problemas com subproblemas sobrepostos guardando resultados já calculados.

## Teoria
- **Programação dinâmica (PD)** aplica-se quando há **subestrutura ótima** e **subproblemas sobrepostos**.
- Duas formas:
  - **Top-down (memoização)**: recursão + cache.
  - **Bottom-up (tabulação)**: preenche uma tabela dos casos menores aos maiores.
- Receita: (1) defina o estado; (2) escreva a recorrência; (3) defina os casos base; (4) escolha a ordem de cálculo; (5) otimize espaço se possível.
- Reduz custos exponenciais para polinomiais: Fibonacci O(2ⁿ) → O(n).
- Clássicos: troco mínimo, mochila 0/1, maior subsequência comum (LCS), distância de edição.

## Exemplo em Python
```python
def troco_minimo(valor, moedas):
    INF = float("inf")
    dp = [0] + [INF] * valor            # dp[v] = mínimo de moedas para v
    for v in range(1, valor + 1):
        for m in moedas:
            if m <= v and dp[v - m] + 1 < dp[v]:
                dp[v] = dp[v - m] + 1
    return dp[valor] if dp[valor] != INF else -1

def lcs(a, b):
    dp = [[0] * (len(b) + 1) for _ in range(len(a) + 1)]
    for i in range(1, len(a) + 1):
        for j in range(1, len(b) + 1):
            if a[i - 1] == b[j - 1]:
                dp[i][j] = dp[i - 1][j - 1] + 1
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])
    return dp[-1][-1]

def mochila(pesos, valores, cap):
    dp = [0] * (cap + 1)
    for p, v in zip(pesos, valores):
        for c in range(cap, p - 1, -1):  # de trás p/ frente: cada item 1x
            dp[c] = max(dp[c], dp[c - p] + v)
    return dp[cap]

print(troco_minimo(6, [1, 3, 4]))          # 2  (o guloso errou)
print(lcs("ABCBDAB", "BDCABA"))            # 4
print(mochila([1, 3, 4, 5], [1, 4, 5, 7], 7))  # 9
```

## Exercício
1. Calcule Fibonacci(80) bottom-up com apenas duas variáveis.
2. Implemente a distância de edição (Levenshtein) entre "kitten" e "sitting" (resultado 3).
3. Conte caminhos em uma grade n×m movendo-se só para direita/baixo.

## Checklist
- [ ] Identifico subproblemas sobrepostos
- [ ] Escrevo a recorrência e os casos base
- [ ] Diferencio memoização de tabulação
