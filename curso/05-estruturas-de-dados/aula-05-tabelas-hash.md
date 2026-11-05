# Aula 5 — Tabelas hash

**Duração:** ~25 min · **Módulo 5**

## Objetivo
Entender como dicionários e sets alcançam busca O(1) média e implementar uma tabela hash.

## Teoria
- **Função hash**: converte uma chave em um inteiro; `índice = hash(chave) % tamanho`. Deve ser determinística e distribuir bem.
- **Colisão**: chaves diferentes no mesmo índice. Soluções:
  - **Encadeamento (chaining)**: cada posição guarda uma lista de pares.
  - **Endereçamento aberto**: procura outra posição (probing linear/quadrático).
- **Fator de carga** = itens / tamanho. Acima de ~0,7 faz-se **rehash** (dobra a tabela e reinsere).
- Custo: média O(1) para inserir/buscar/remover; pior caso O(n) se tudo colidir.
- Chaves precisam ser **imutáveis/hasheáveis** (em Python, `list` não pode ser chave; `tuple` pode).
- Hash criptográfico (SHA-256) é outro conceito: aqui o objetivo é velocidade.

## Exemplo em Python
```python
class TabelaHash:
    def __init__(self, capacidade=8):
        self._b = [[] for _ in range(capacidade)]
        self._n = 0

    def _idx(self, chave):
        return hash(chave) % len(self._b)

    def put(self, chave, valor):
        bucket = self._b[self._idx(chave)]
        for i, (k, _) in enumerate(bucket):
            if k == chave:
                bucket[i] = (chave, valor)
                return
        bucket.append((chave, valor))
        self._n += 1
        if self._n / len(self._b) > 0.7:
            self._rehash()

    def get(self, chave, padrao=None):
        for k, v in self._b[self._idx(chave)]:
            if k == chave:
                return v
        return padrao

    def _rehash(self):
        antigos = [p for b in self._b for p in b]
        self._b = [[] for _ in range(len(self._b) * 2)]
        self._n = 0
        for k, v in antigos:
            self.put(k, v)

t = TabelaHash()
for i in range(20): t.put(f"tarefa{i}", i)
print(t.get("tarefa7"), len(t._b))  # 7 32
```

## Exercício
1. Implemente `remove(chave)`.
2. Conte a frequência de palavras de um texto com `dict`.
3. Resolva "dois números que somam alvo" em O(n) usando hash.

## Checklist
- [ ] Explico colisão e fator de carga
- [ ] Sei por que a chave deve ser imutável
- [ ] Usei hash para reduzir O(n²) para O(n)
