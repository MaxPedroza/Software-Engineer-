# Aula 10 — Revisão e quiz do módulo

**Duração:** ~20 min · **Módulo 6**

## Resumo
- Big-O descreve o crescimento do custo com `n`, ignorando constantes: O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ).
- Busca binária: O(log n), exige dados ordenados.
- Ordenação simples: O(n²); eficiente: merge/heap O(n log n) garantido, quick médio O(n log n).
- Recursão precisa de caso base; backtracking = escolher, explorar, desfazer.
- Divisão e conquista: subproblemas independentes; PD: subproblemas sobrepostos.
- Guloso é rápido, mas só ótimo com a propriedade de escolha gulosa.
- Grafos: BFS (fila, menor caminho sem pesos), DFS (pilha), Dijkstra (heap, pesos ≥ 0).

## Quiz (responda sem consultar)
1. Simplifique `4n² + 10n + 3` para Big-O.
2. Qual a complexidade da busca binária e qual seu pré-requisito?
3. Qual ordenação simples é O(n) em dados já ordenados?
4. Qual o pior caso do quick sort e como evitá-lo?
5. Cite uma vantagem e uma desvantagem do merge sort.
6. O que é o caso base de uma recursão?
7. Qual a diferença entre memoização e tabulação?
8. Dê um exemplo em que o algoritmo guloso do troco falha.
9. Qual estrutura o BFS usa? E o Dijkstra?
10. Por que Dijkstra não funciona com pesos negativos?

## Gabarito resumido
1. O(n²) · 2. O(log n); dados ordenados com acesso por índice · 3. Insertion sort (ou bubble com flag) · 4. O(n²) com pivô ruim; pivô aleatório/mediana · 5. Estável e O(n log n) garantido; usa O(n) de memória extra · 6. Condição que encerra a recursão sem nova chamada · 7. Top-down com cache vs bottom-up com tabela · 8. Moedas {1,3,4}, valor 6: guloso usa 3, ótimo usa 2 · 9. Fila; fila de prioridade (heap) · 10. Assume que um nó finalizado já tem a menor distância, o que uma aresta negativa invalida

## Entregável do módulo
**Relatório** comparando algoritmos (ex.: busca linear vs binária e bubble vs insertion vs merge vs `sorted`) com **gráficos de tempo de execução** para diferentes `n` (use `time.perf_counter` e `matplotlib`), explicando os resultados com Big-O. Inclua a ordenação/filtros otimizados aplicados ao projeto das tarefas.

## Checklist final
- [ ] Acertei 8 ou mais questões
- [ ] Entreguei o relatório com gráficos
- [ ] Pronto para o Módulo 7
