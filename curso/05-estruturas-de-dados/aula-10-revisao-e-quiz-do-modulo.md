# Aula 10 — Revisão e quiz do módulo

**Duração:** ~20 min · **Módulo 5**

## Resumo
- Estruturas de dados são trade-offs entre tempo, memória e simplicidade; TAD ≠ implementação.
- Arrays: acesso O(1), `append` O(1) amortizado, inserção no meio O(n).
- Listas ligadas: inserção nas pontas O(1), acesso O(n).
- Pilha = LIFO; fila = FIFO (use `deque`, não `pop(0)`).
- Hash: busca O(1) média; colisões tratadas por encadeamento ou endereçamento aberto.
- BST: operações O(h); desbalanceada degenera para O(n); em-ordem é ordenado.
- Heap: topo mínimo/máximo, push/pop O(log n).
- Grafos: lista de adjacência para grafos esparsos; BFS usa fila.
- Trie: busca por prefixo em O(m).

## Quiz (responda sem consultar)
1. O que diferencia um TAD de sua implementação?
2. Por que `append` em lista dinâmica é O(1) amortizado?
3. Qual o custo de inserir no início de um array? E de uma lista ligada?
4. Cite dois usos de pilha.
5. Por que `list.pop(0)` é ruim para implementar fila?
6. O que é uma colisão em tabela hash e como tratá-la?
7. Qual percurso de uma BST devolve os valores em ordem crescente?
8. Qual a posição dos filhos do índice `i` em um heap em array?
9. Quando preferir lista de adjacência a matriz de adjacência?
10. Que estrutura usar para autocompletar e qual seu custo?

## Gabarito resumido
1. Interface (o quê) vs forma de armazenar (como) · 2. Realocações raras, custo diluído · 3. O(n) vs O(1) · 4. Desfazer, parênteses balanceados, pilha de chamadas, DFS · 5. Desloca todos os itens, O(n) · 6. Chaves distintas no mesmo índice; encadeamento ou probing · 7. Em-ordem · 8. `2i+1` e `2i+2` · 9. Grafos esparsos (menos memória) · 10. Trie, O(m) no tamanho do prefixo

## Entregável do módulo
Implementações próprias de **pilha, fila, hash e BST**, com testes automatizados (ex.: `unittest` ou `pytest`) cobrindo casos normais e de borda (vazio, duplicados, chave inexistente). Inclua o início do **índice de busca de tarefas** (hash + trie) comparado com busca linear.

## Checklist final
- [ ] Acertei 8 ou mais questões
- [ ] Entreguei as quatro estruturas com testes
- [ ] Pronto para o Módulo 6
