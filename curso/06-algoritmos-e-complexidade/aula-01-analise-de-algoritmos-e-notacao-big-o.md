# Aula 1 — Análise de algoritmos e notação Big-O

**Duração:** ~25 min · **Módulo 6**

## Objetivo
Medir e comparar a eficiência de algoritmos de forma independente de máquina.

## Teoria
- **Algoritmo**: sequência finita e precisa de passos que resolve um problema.
- **Complexidade de tempo**: como o número de operações cresce com o tamanho da entrada `n`. **Complexidade de espaço**: como a memória cresce.
- **Big-O** descreve o limite superior (geralmente o pior caso) ignorando constantes e termos menores: `3n² + 5n + 2` → **O(n²)**.
- Classes comuns, da mais rápida à mais lenta:

| Notação | Nome | Exemplo |
|---|---|---|
| O(1) | constante | acesso por índice |
| O(log n) | logarítmica | busca binária |
| O(n) | linear | percorrer lista |
| O(n log n) | linearítmica | merge sort |
| O(n²) | quadrática | dois laços aninhados |
| O(2ⁿ) | exponencial | subconjuntos |

- Também existem **melhor caso**, **caso médio** e **pior caso**; Ω e Θ são os limites inferior e justo.

## Exemplo em Python
```python
import time

def tem_duplicado_quadratico(v):        # O(n²)
    for i in range(len(v)):
        for j in range(i + 1, len(v)):
            if v[i] == v[j]:
                return True
    return False

def tem_duplicado_linear(v):            # O(n) tempo, O(n) espaço
    vistos = set()
    for x in v:
        if x in vistos:
            return True
        vistos.add(x)
    return False

for n in (1000, 2000, 4000):
    v = list(range(n))                  # pior caso: sem duplicados
    for f in (tem_duplicado_quadratico, tem_duplicado_linear):
        t = time.perf_counter(); f(v)
        print(n, f.__name__, round(time.perf_counter() - t, 5))
```

## Exercício
1. Dê a complexidade de: (a) um laço simples até `n`; (b) dois laços aninhados até `n`; (c) um laço que dobra `i` a cada passo.
2. Rode o exemplo: quando `n` dobra, quanto cada tempo cresce?
3. Simplifique `5n³ + 100n + 7` para Big-O.

## Checklist
- [ ] Explico o que Big-O ignora
- [ ] Reconheço O(1), O(n), O(n²) e O(log n) no código
- [ ] Entendo o trade-off tempo × espaço
