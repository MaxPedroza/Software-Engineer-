# Aula 7 — Clean Code: nomes, funções e comentários

**Duração:** ~25 min · **Módulo 8**

## Objetivo
Escrever código que comunica a intenção e é fácil de ler por outras pessoas.

## Teoria
- **Nomes** revelam intenção: `dias_ate_vencimento` em vez de `d`. Evite abreviações obscuras e nomes enganosos. Classes são substantivos; funções são verbos.
- **Funções** pequenas, fazendo **uma coisa**, com poucos parâmetros (idealmente ≤ 3) e um só nível de abstração. Evite *flag arguments* booleanos.
- **Comentários**: não explique *o que* o código faz (renomeie/extraia); explique o **porquê** de decisões não óbvias. Comentário desatualizado é pior que nenhum.
- Evite números mágicos: use constantes nomeadas.
- Regra do escoteiro: deixe o código um pouco mais limpo do que encontrou.

## Exemplo em Python
Antes:
```python
def calc(l, t):
    # percorre lista
    r = 0
    for i in l:
        if i[1] == t:
            r += i[0] * 0.9
    return r
```
Depois:
```python
DESCONTO_FIDELIDADE = 0.9

def total_por_categoria(itens, categoria):
    return sum(
        item.preco * DESCONTO_FIDELIDADE
        for item in itens
        if item.categoria == categoria
    )
```
Se o desconto for uma regra de negócio, um comentário de *porquê* ajuda:
```python
# Contrato com parceiros: 10% fixo, independente do volume.
```

## Exercício
1. Renomeie: `def proc(x, f)`, `lst2`, `flag`, `data1` em um trecho seu.
2. Quebre uma função de 30+ linhas em funções com um único propósito.
3. Remova três comentários redundantes tornando o código autoexplicativo.

## Checklist
- [ ] Nomes revelam intenção
- [ ] Funções pequenas e com uma responsabilidade
- [ ] Comentários explicam o porquê, não o quê
