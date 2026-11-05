# Aula 5 — Testes, documentação e refatoração com IA

**Duração:** ~25 min · **Módulo 22**

## Objetivo
Usar IA para tarefas de apoio mantendo a verificação humana.

## Teoria
### Testes
- Gere **casos de teste e casos-limite** a partir da especificação, não só da implementação.
- Peça testes parametrizados e propriedades; valide que os testes **falham** ao quebrar o código (mutação manual).
- Cuidado com testes "espelho" que repetem a lógica do código.

### Documentação
- Docstrings, README, changelog e explicação de código legado.
- Revise a precisão: a IA descreve o que *acha* que o código faz.

### Refatoração
- Faça **em passos pequenos**, sempre com **testes de caracterização** antes.
- Peça uma mudança por vez (extrair função, renomear, remover duplicação) e rode os testes a cada passo.
- Use para migrações mecânicas (ex.: callbacks → async/await), revisando o diff.

## Exemplo: do código ao teste parametrizado
```python
def fatiar(lista: list, tamanho: int) -> list[list]:
    if tamanho <= 0:
        raise ValueError("tamanho deve ser > 0")
    return [lista[i:i + tamanho] for i in range(0, len(lista), tamanho)]
```
Prompt: *"Gere testes pytest parametrizados para `fatiar`, incluindo lista vazia, tamanho maior que a lista e tamanho inválido."*
```python
import pytest

@pytest.mark.parametrize("lista,tam,esperado", [
    ([], 3, []),
    ([1, 2, 3], 5, [[1, 2, 3]]),
    ([1, 2, 3, 4], 2, [[1, 2], [3, 4]]),
    ([1, 2, 3], 2, [[1, 2], [3]]),
])
def test_fatiar(lista, tam, esperado):
    assert fatiar(lista, tam) == esperado

@pytest.mark.parametrize("tam", [0, -1])
def test_fatiar_tamanho_invalido(tam):
    with pytest.raises(ValueError):
        fatiar([1], tam)
```

## Exercício
1. Escolha uma função sem testes: gere testes com IA, rode-os e quebre o código de propósito para ver se detectam.
2. Refatore uma função longa em 3 passos com a IA, rodando os testes em cada um.

## Checklist
- [ ] Testes derivados da especificação
- [ ] Refatoro em passos com testes verdes
- [ ] Reviso a documentação gerada
