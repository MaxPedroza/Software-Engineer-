# Aula 9 — Introdução a grafos

**Duração:** ~30 min · **Módulo 4**

## Objetivo
Modelar problemas como grafos e percorrê-los com BFS e DFS.

## Teoria
- **Grafo** G = (V, E): vértices (nós) e arestas (conexões). Pode ser **direcionado** ou não, **ponderado** ou não.
- Exemplos: redes sociais, mapas, dependências de pacotes, páginas web, rotas de rede.
- Termos: **grau** (nº de arestas do vértice), **caminho**, **ciclo**, **conexo**, **árvore** (grafo conexo sem ciclos).
- Representações:
  - **Lista de adjacência**: `{vértice: [vizinhos]}`, usa O(V+E) de memória; ideal para grafos esparsos.
  - **Matriz de adjacência**: V×V, consulta de aresta O(1), usa O(V²).
- **BFS** (largura): usa fila; visita por camadas e acha o menor caminho em nº de arestas.
- **DFS** (profundidade): usa pilha/recursão; útil para detectar ciclos e ordenação topológica.
- Complexidade de ambos: O(V + E).

## Exemplo em Python
```python
from collections import deque

grafo = {
    "A": ["B", "C"],
    "B": ["A", "D"],
    "C": ["A", "D"],
    "D": ["B", "C", "E"],
    "E": ["D"],
}

def bfs(grafo, inicio):
    visitados, fila, ordem = {inicio}, deque([inicio]), []
    while fila:
        v = fila.popleft()
        ordem.append(v)
        for w in grafo[v]:
            if w not in visitados:
                visitados.add(w)
                fila.append(w)
    return ordem

def dfs(grafo, v, visitados=None):
    visitados = visitados if visitados is not None else set()
    visitados.add(v)
    for w in grafo[v]:
        if w not in visitados:
            dfs(grafo, w, visitados)
    return visitados

def menor_caminho(grafo, origem, destino):
    anterior, fila = {origem: None}, deque([origem])
    while fila:
        v = fila.popleft()
        if v == destino:
            caminho = []
            while v is not None:
                caminho.append(v)
                v = anterior[v]
            return caminho[::-1]
        for w in grafo[v]:
            if w not in anterior:
                anterior[w] = v
                fila.append(w)
    return None

print(bfs(grafo, "A"))                  # ['A', 'B', 'C', 'D', 'E']
print(sorted(dfs(grafo, "A")))          # ['A', 'B', 'C', 'D', 'E']
print(menor_caminho(grafo, "A", "E"))   # ['A', 'B', 'D', 'E']
print({v: len(vs) for v, vs in grafo.items()})   # graus
```

## Exercício
1. Desenhe um grafo de 6 amigos e escreva sua lista de adjacência; quem tem maior grau?
2. Escreva `conexo(grafo)` usando `dfs` e teste com um grafo desconexo.
3. Modele dependências entre módulos do curso (Módulo 4 depende do 3…) e identifique a ordem de estudo.

## Checklist
- [ ] Modelo problemas como grafos
- [ ] Represento com lista de adjacência
- [ ] Implemento BFS e DFS
