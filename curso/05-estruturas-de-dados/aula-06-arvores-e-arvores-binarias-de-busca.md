# Aula 6 — Árvores e árvores binárias de busca

**Duração:** ~25 min · **Módulo 5**

## Objetivo
Entender árvores, percursos e implementar uma BST (Binary Search Tree).

## Teoria
- **Árvore**: estrutura hierárquica de nós; tem **raiz**, **filhos**, **folhas**; **altura** = maior caminho da raiz a uma folha. Exemplos: sistema de arquivos, DOM do HTML.
- **Árvore binária**: cada nó tem no máximo 2 filhos.
- **BST**: para todo nó, valores à esquerda são **menores** e à direita **maiores**.
- Busca/inserção/remoção: **O(h)**, onde h é a altura. Balanceada: h ≈ log n; degenerada (dados já ordenados): h = n → O(n).
- **Árvores balanceadas** (AVL, rubro-negra) mantêm h ≈ log n com rotações.
- **Percursos**: em-ordem (esq, raiz, dir — gera valores **ordenados**), pré-ordem, pós-ordem, por nível (BFS).

## Exemplo em Python
```python
class No:
    def __init__(self, chave):
        self.chave, self.esq, self.dir = chave, None, None

class BST:
    def __init__(self): self.raiz = None

    def inserir(self, chave):
        self.raiz = self._ins(self.raiz, chave)

    def _ins(self, no, chave):
        if no is None: return No(chave)
        if chave < no.chave: no.esq = self._ins(no.esq, chave)
        elif chave > no.chave: no.dir = self._ins(no.dir, chave)
        return no

    def buscar(self, chave):
        no = self.raiz
        while no:
            if chave == no.chave: return True
            no = no.esq if chave < no.chave else no.dir
        return False

    def em_ordem(self, no="raiz"):
        if no == "raiz": no = self.raiz
        if no:
            yield from self.em_ordem(no.esq)
            yield no.chave
            yield from self.em_ordem(no.dir)

    def altura(self, no="raiz"):
        if no == "raiz": no = self.raiz
        return 0 if no is None else 1 + max(self.altura(no.esq), self.altura(no.dir))

b = BST()
for x in (8, 3, 10, 1, 6, 14): b.inserir(x)
print(list(b.em_ordem()), b.buscar(6), b.altura())  # [1,3,6,8,10,14] True 3
```

## Exercício
1. Insira 1..7 em ordem crescente e veja a altura. Por quê?
2. Implemente `minimo()` e `maximo()`.
3. Implemente `remover(chave)` tratando 0, 1 e 2 filhos.

## Checklist
- [ ] Defino a propriedade da BST
- [ ] Explico por que o em-ordem é ordenado
- [ ] Sei o risco de uma árvore desbalanceada
