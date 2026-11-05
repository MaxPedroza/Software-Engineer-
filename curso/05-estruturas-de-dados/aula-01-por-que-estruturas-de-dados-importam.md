# Aula 1 — Por que estruturas de dados importam

**Duração:** ~20 min · **Módulo 5**

## Objetivo
Entender que a forma de organizar dados determina a velocidade e a simplicidade do programa.

## Teoria
- **Estrutura de dados** = jeito de armazenar e organizar dados para operações eficientes (inserir, buscar, remover, percorrer).
- Não existe estrutura perfeita: cada uma é um **trade-off** entre tempo, memória e simplicidade.
- **TAD (Tipo Abstrato de Dados)** define *o que* se faz (interface); a estrutura define *como* (implementação). Ex.: a "fila" é o TAD; lista ligada ou array circular são implementações.
- Custos típicos (Big-O, visto no Módulo 6):

| Estrutura | Acesso | Busca | Inserção |
|---|---|---|---|
| Lista (array) | O(1) | O(n) | O(n) no meio |
| Dict/hash | — | O(1) médio | O(1) médio |
| Árvore balanceada | — | O(log n) | O(log n) |

## Exemplo em Python
```python
import time

n = 20_000
dados_lista = list(range(n))
dados_set = set(dados_lista)
alvos = range(n - 1000, n + 1000)

t = time.perf_counter()
achados = sum(1 for x in alvos if x in dados_lista)   # O(n) cada
print("lista:", round(time.perf_counter() - t, 4), "s")

t = time.perf_counter()
achados = sum(1 for x in alvos if x in dados_set)     # O(1) médio
print("set:  ", round(time.perf_counter() - t, 6), "s")
```

## Exercício
1. Rode o exemplo e anote a diferença entre lista e set.
2. Aumente `n` 10× e observe qual tempo cresce mais.
3. Para cada caso, escolha uma estrutura e justifique: (a) desfazer ações do usuário; (b) fila de atendimento; (c) buscar usuário por e-mail.

## Checklist
- [ ] Diferencio TAD de implementação
- [ ] Sei que toda estrutura tem trade-offs
- [ ] Medi o impacto da escolha em código real
