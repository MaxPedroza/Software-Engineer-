# Aula 9 — Algoritmos em grafos (BFS, DFS, Dijkstra)

**Duração:** ~25 min · **Módulo 6**

## Objetivo
Percorrer grafos e encontrar caminhos mínimos.

## Teoria
- **BFS (largura)**: usa **fila**; visita por camadas. Em grafos não ponderados dá o **menor caminho** (em número de arestas). O(V+E).
- **DFS (profundidade)**: usa **pilha/recursão**; vai fundo antes de voltar. Usos: detectar ciclos, componentes conexos, ordenação topológica. O(V+E).
- **Dijkstra**: caminho mínimo com pesos **não negativos**. Usa fila de prioridade (heap); relaxa arestas. O((V+E) log V).
- Pesos negativos exigem **Bellman-Ford**; todos os pares: **Floyd-Warshall**.
- Sempre mantenha um conjunto de **visitados** para não entrar em loop.

## Exemplo em Python
```python
import heapq
from collections import deque

def bfs_distancias(adj, origem):
    dist = {origem: 0}
    fila = deque([origem])
    while fila:
        u = fila.popleft()
        for v in adj[u]:
            if v not in dist:
                dist[v] = dist[u] + 1
                fila.append(v)
    return dist

def dfs(adj, u, vis=None):
    vis = vis if vis is not None else set()
    vis.add(u)
    for v in adj[u]:
        if v not in vis:
            dfs(adj, v, vis)
    return vis

def dijkstra(adj, origem):
    dist = {origem: 0}
    heap = [(0, origem)]
    while heap:
        d, u = heapq.heappop(heap)
        if d > dist.get(u, float("inf")):
            continue                      # entrada obsoleta
        for v, peso in adj[u]:
            nd = d + peso
            if nd < dist.get(v, float("inf")):
                dist[v] = nd
                heapq.heappush(heap, (nd, v))
    return dist

nao_pond = {"A": ["B", "C"], "B": ["D"], "C": ["D"], "D": []}
pond = {"A": [("B", 4), ("C", 1)], "C": [("B", 2), ("D", 7)], "B": [("D", 1)], "D": []}
print(bfs_distancias(nao_pond, "A"))   # {'A': 0, 'B': 1, 'C': 1, 'D': 2}
print(sorted(dfs(nao_pond, "A")))      # ['A', 'B', 'C', 'D']
print(dijkstra(pond, "A"))             # {'A': 0, 'B': 3, 'C': 1, 'D': 4}
```

## Exercício
1. Use BFS para achar o caminho (não só a distância) em um labirinto em grade.
2. Detecte ciclo em grafo direcionado com DFS.
3. Por que Dijkstra falha com aresta de peso negativo? Dê um exemplo.

## Checklist
- [ ] Escolho BFS ou DFS conforme o problema
- [ ] Implemento Dijkstra com heap
- [ ] Conheço a limitação dos pesos negativos
