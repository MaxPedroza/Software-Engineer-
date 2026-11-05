# Aula 8 — Grafos e representações

**Duração:** ~25 min · **Módulo 5**

## Objetivo
Modelar problemas como grafos e escolher a representação adequada.

## Teoria
- **Grafo** G = (V, E): vértices (nós) e arestas (conexões). Modelam redes sociais, mapas, dependências, a web.
- **Direcionado** vs **não direcionado**; **ponderado** (arestas com peso) vs não ponderado.
- Conceitos: **grau**, **caminho**, **ciclo**, **componente conexo**, **DAG** (grafo direcionado acíclico — ex.: dependências de build).
- **Matriz de adjacência**: `M[i][j]=1` se há aresta. Memória O(V²); checar aresta O(1). Boa para grafos densos.
- **Lista de adjacência**: para cada vértice, lista de vizinhos. Memória O(V+E); listar vizinhos é rápido. Boa para grafos esparsos (a maioria).
- Percursos básicos: BFS (fila) e DFS (pilha/recursão), com conjunto de visitados.

## Exemplo em Python
```python
from collections import defaultdict, deque

class Grafo:
    def __init__(self, direcionado=False):
        self.adj = defaultdict(list)
        self.dir = direcionado

    def aresta(self, u, v):
        self.adj[u].append(v)
        if not self.dir:
            self.adj[v].append(u)
        self.adj.setdefault(v, self.adj[v])

    def bfs(self, origem):
        vis, fila, ordem = {origem}, deque([origem]), []
        while fila:
            u = fila.popleft()
            ordem.append(u)
            for v in self.adj[u]:
                if v not in vis:
                    vis.add(v)
                    fila.append(v)
        return ordem

g = Grafo()
for u, v in [("A", "B"), ("A", "C"), ("B", "D"), ("C", "D"), ("D", "E")]:
    g.aresta(u, v)
print(g.bfs("A"))  # ['A', 'B', 'C', 'D', 'E']

nomes = ["A", "B", "C"]
matriz = [[0, 1, 1], [1, 0, 0], [1, 0, 0]]  # A-B e A-C
```

## Exercício
1. Desenhe um grafo de 6 vértices e represente-o das duas formas.
2. Calcule o grau de cada vértice com a lista de adjacência.
3. Modele dependências entre módulos do curso como DAG e liste os pré-requisitos do Módulo 7.

## Checklist
- [ ] Diferencio grafo direcionado e ponderado
- [ ] Escolho entre matriz e lista de adjacência
- [ ] Implemento um BFS simples
