# Aula 3 — Listas ligadas

**Duração:** ~20 min · **Módulo 5**

## Objetivo
Implementar uma lista ligada simples e saber quando ela é melhor que um array.

## Teoria
- **Lista ligada**: sequência de **nós**; cada nó guarda um valor e uma referência ao próximo. Os nós ficam espalhados na memória.
- **Simples** (só `proximo`), **dupla** (`anterior` e `proximo`), **circular**.
- Inserir/remover no início: **O(1)**. Inserir no fim: O(1) se houver ponteiro para a cauda. Acesso por índice e busca: **O(n)**.
- Remover um nó já conhecido numa lista dupla: O(1).
- Contra: mais memória por elemento e pior localidade de cache; na prática, arrays costumam vencer. Use quando há muitas inserções/remoções nas pontas ou no meio com referência ao nó.

## Exemplo em Python
```python
class No:
    def __init__(self, valor, proximo=None):
        self.valor, self.proximo = valor, proximo

class ListaLigada:
    def __init__(self):
        self.cabeca = None

    def adicionar_inicio(self, valor):
        self.cabeca = No(valor, self.cabeca)

    def adicionar_fim(self, valor):
        novo = No(valor)
        if not self.cabeca:
            self.cabeca = novo
            return
        atual = self.cabeca
        while atual.proximo:
            atual = atual.proximo
        atual.proximo = novo

    def remover(self, valor):
        ant, atual = None, self.cabeca
        while atual:
            if atual.valor == valor:
                if ant: ant.proximo = atual.proximo
                else: self.cabeca = atual.proximo
                return True
            ant, atual = atual, atual.proximo
        return False

    def __iter__(self):
        atual = self.cabeca
        while atual:
            yield atual.valor
            atual = atual.proximo

l = ListaLigada()
for x in (1, 2, 3): l.adicionar_fim(x)
l.adicionar_inicio(0); l.remover(2)
print(list(l))  # [0, 1, 3]
```

## Exercício
1. Adicione um ponteiro `cauda` para tornar `adicionar_fim` O(1).
2. Implemente `inverter()` (reverter a lista in-place).
3. Detecte ciclo com dois ponteiros (lento e rápido — algoritmo de Floyd).

## Checklist
- [ ] Implemento inserção e remoção em lista ligada
- [ ] Comparo lista ligada e array
- [ ] Sei o que muda numa lista dupla
