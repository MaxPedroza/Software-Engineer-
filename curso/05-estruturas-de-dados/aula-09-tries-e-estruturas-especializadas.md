# Aula 9 — Tries e estruturas especializadas

**Duração:** ~25 min · **Módulo 5**

## Objetivo
Implementar uma trie para busca por prefixo e conhecer outras estruturas especializadas.

## Teoria
- **Trie (árvore de prefixos)**: cada aresta é um caractere; o caminho da raiz até um nó marcado como "fim" forma uma palavra.
- Inserir/buscar palavra de tamanho m: **O(m)**, independente do número de palavras. Ideal para **autocompletar** e dicionários.
- Custo: memória alta (muitos nós/dicionários).
- Outras estruturas:
  - **Union-Find (DSU)**: agrupa elementos e responde "estão no mesmo grupo?" quase em O(1); usado em componentes conexos.
  - **Bloom filter**: "talvez presente / definitivamente ausente" com pouca memória; admite falsos positivos.
  - **Árvore de segmentos / Fenwick**: consultas de intervalo.
  - **LRU cache**: dict + lista dupla (`OrderedDict` em Python).

## Exemplo em Python
```python
class Trie:
    def __init__(self):
        self.filhos, self.fim = {}, False

    def inserir(self, palavra):
        no = self
        for c in palavra:
            no = no.filhos.setdefault(c, Trie())
        no.fim = True

    def _no(self, prefixo):
        no = self
        for c in prefixo:
            no = no.filhos.get(c)
            if no is None:
                return None
        return no

    def contem(self, palavra):
        no = self._no(palavra)
        return bool(no and no.fim)

    def autocompletar(self, prefixo):
        no = self._no(prefixo)
        resultado = []
        def dfs(n, acc):
            if n.fim: resultado.append(acc)
            for c, f in sorted(n.filhos.items()):
                dfs(f, acc + c)
        if no: dfs(no, prefixo)
        return resultado

t = Trie()
for p in ["tarefa", "tarde", "teste", "tabela"]: t.inserir(p)
print(t.autocompletar("tar"))  # ['tarde', 'tarefa']
print(t.contem("tar"))         # False
```

## Exercício
1. Adicione `remover(palavra)`.
2. Limite `autocompletar` aos 5 primeiros resultados.
3. Implemente Union-Find com compressão de caminho e use-o para contar componentes de um grafo.

## Checklist
- [ ] Explico por que a trie é O(m)
- [ ] Implemento autocompletar
- [ ] Conheço ao menos duas outras estruturas especializadas
