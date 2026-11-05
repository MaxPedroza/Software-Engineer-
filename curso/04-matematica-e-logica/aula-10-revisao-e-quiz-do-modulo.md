# Aula 10 — Revisão e quiz do módulo

**Duração:** ~20 min · **Módulo 4**

## Resumo
- Conectivos: ¬, ∧, ∨, →, ↔; De Morgan; tautologia e contradição.
- Tabelas-verdade têm 2ⁿ linhas; simplifique com absorção e De Morgan.
- Conjuntos: ∪, ∩, −, Δ, produto cartesiano; relações são subconjuntos de A × B.
- Funções: injetora, sobrejetora, bijetora; crescimento log n < n < n² < 2ⁿ.
- Contagem: arranjo (ordem importa) vs combinação C(n,k).
- Probabilidade, independência, Bayes; média, mediana e desvio padrão.
- Bases 2, 10 e 16; complemento de dois; operações bit a bit.
- Vetores, produto escalar e produto de matrizes.
- Grafos: lista de adjacência, BFS (fila) e DFS (pilha).

## Quiz (responda sem consultar)
1. Escreva a negação de `p ∧ q` usando De Morgan.
2. Quantas linhas tem a tabela-verdade de 4 variáveis?
3. Quando `p → q` é falsa?
4. Qual o tamanho de A × B se |A| = 3 e |B| = 4?
5. Quantos passos faz, no máximo, a busca binária em 1.024 elementos?
6. Calcule C(5, 2).
7. Qual a probabilidade de a soma de dois dados ser 7?
8. Converta `1101₂` para decimal e `255` para hexadecimal.
9. Qual a representação de −1 em 8 bits (complemento de dois)?
10. Qual estrutura BFS usa e o que ela garante?

## Gabarito resumido
1. ¬p ∨ ¬q · 2. 16 · 3. Só quando p é V e q é F · 4. 12 · 5. 10 (log₂ 1024), +1 de comparação final · 6. 10 · 7. 6/36 = 1/6 · 8. 13 e `FF` · 9. `11111111` · 10. Fila; menor caminho em número de arestas

## Entregável do módulo
**Biblioteca pequena de utilitários matemáticos** (`matutils/`) com: avaliador de expressões booleanas e gerador de tabela-verdade, conversor de bases (2–16), funções de combinatória e BFS/DFS — além de testes simples com `assert` (ou `pytest`) para cada função.

## Checklist final
- [ ] Acertei 8 ou mais questões
- [ ] A biblioteca roda com testes passando
- [ ] Pronto para o Módulo 5
