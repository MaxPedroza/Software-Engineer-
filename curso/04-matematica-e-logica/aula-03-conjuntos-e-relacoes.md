# Aula 3 — Conjuntos e relações

**Duração:** ~25 min · **Módulo 4**

## Objetivo
Dominar operações de conjuntos e entender relações, base dos bancos de dados relacionais.

## Teoria
- **Conjunto**: coleção de elementos distintos, sem ordem. Notação: A = {1, 2, 3}; x ∈ A; ∅ vazio; |A| cardinalidade.
- Subconjunto: A ⊆ B. Operações: união A ∪ B, interseção A ∩ B, diferença A − B, diferença simétrica A Δ B, complemento.
- **Produto cartesiano** A × B: todos os pares (a, b). |A × B| = |A|·|B|.
- **Relação** de A em B: subconjunto de A × B. Ex.: "aluno matriculado em disciplina".
- Propriedades de uma relação em A: **reflexiva** (a R a), **simétrica**, **transitiva**; equivalência = as três.
- Conexão com SQL: tabela = relação; `UNION`, `INTERSECT`, `EXCEPT` = operações de conjuntos; `JOIN` ≈ produto cartesiano filtrado.

## Exemplo em Python
```python
A = {1, 2, 3, 4}
B = {3, 4, 5}
print(A | B, A & B, A - B, A ^ B)   # união, interseção, diferença, simétrica
print({1, 2} <= A)                  # subconjunto → True

from itertools import product
alunos = ["Ana", "Beto"]
cursos = ["Python", "SQL"]
print(list(product(alunos, cursos)))   # produto cartesiano (4 pares)

matriculas = {("Ana", "Python"), ("Ana", "SQL"), ("Beto", "SQL")}

def reflexiva(rel, universo):
    return all((x, x) in rel for x in universo)

def simetrica(rel):
    return all((b, a) in rel for a, b in rel)

def transitiva(rel):
    return all((a, d) in rel
               for a, b in rel for c, d in rel if b == c)

R = {(1, 1), (2, 2), (1, 2), (2, 1)}
print(reflexiva(R, {1, 2}), simetrica(R), transitiva(R))  # True True True
print([c for a, c in matriculas if a == "Ana"])  # cursos de Ana
```

## Exercício
1. Dados A = {1..6} e B = {2, 4, 6, 8}, calcule A ∩ B, A − B e A Δ B à mão e em Python.
2. Verifique se "é divisor de" em {1, 2, 3, 6} é reflexiva e transitiva (é simétrica?).
3. Modele "aluno × disciplina" como conjunto de pares e liste alunos sem matrícula em SQL.

## Checklist
- [ ] Faço operações de conjuntos
- [ ] Entendo produto cartesiano e relação
- [ ] Testo reflexividade, simetria e transitividade
