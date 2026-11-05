# Aula 6 — Probabilidade e estatística básica

**Duração:** ~30 min · **Módulo 4**

## Objetivo
Calcular probabilidades simples e resumir dados com média, mediana, moda e desvio padrão.

## Teoria
- **Espaço amostral** Ω: todos os resultados possíveis. **Evento**: subconjunto de Ω.
- P(A) = casos favoráveis / casos possíveis (resultados equiprováveis); 0 ≤ P ≤ 1.
- Complemento: P(¬A) = 1 − P(A). União: P(A∪B) = P(A) + P(B) − P(A∩B).
- **Independência**: P(A∩B) = P(A)·P(B). **Condicional**: P(A|B) = P(A∩B)/P(B).
- **Teorema de Bayes**: P(A|B) = P(B|A)·P(A)/P(B) (base de filtros de spam e diagnósticos).
- Estatística descritiva:
  - **Média** (sensível a outliers), **mediana** (valor central, robusta), **moda** (mais frequente).
  - **Variância** e **desvio padrão**: dispersão em torno da média.
  - **Percentis**: p95 de latência = 95% das requisições são mais rápidas.
- **Lei dos grandes números**: com muitas repetições, a frequência se aproxima da probabilidade.

## Exemplo em Python
```python
import random
import statistics as st

# Dois dados somam 7: 6 casos em 36
dados = [(a, b) for a in range(1, 7) for b in range(1, 7)]
print(sum(1 for a, b in dados if a + b == 7) / len(dados))   # 0.1666...

# Simulação (Monte Carlo)
random.seed(42)
n = 100_000
soma7 = sum(random.randint(1, 6) + random.randint(1, 6) == 7 for _ in range(n))
print(soma7 / n)                                             # ≈ 0.167

# Bayes: doença 1%, sensibilidade 99%, falso positivo 5%
p_d, p_pos_d, p_pos_nd = 0.01, 0.99, 0.05
p_pos = p_pos_d * p_d + p_pos_nd * (1 - p_d)
print(round(p_pos_d * p_d / p_pos, 3))                       # ≈ 0.167

latencias = [120, 130, 125, 140, 135, 2000]    # ms, com outlier
print(st.mean(latencias), st.median(latencias), round(st.pstdev(latencias), 1))
```

## Exercício
1. Qual a probabilidade de tirar pelo menos uma cara em 3 lançamentos de moeda? (use o complemento)
2. Simule 10.000 lançamentos de um dado e compare a frequência de cada face com 1/6.
3. Explique por que a mediana descreve melhor as latências do exemplo do que a média.

## Checklist
- [ ] Calculo probabilidades simples e complementares
- [ ] Entendo independência e probabilidade condicional
- [ ] Uso média, mediana e desvio padrão
