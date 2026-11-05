# Aula 7 — Cobertura, mutation testing e testes de propriedade

**Duração:** ~20 min · **Módulo 15**

## Objetivo
Medir a qualidade da suíte além da simples cobertura de linhas.

## Teoria
- **Cobertura**: % de linhas/ramos executados pelos testes. Ferramenta: `pytest-cov`.
  - `pytest --cov=src --cov-branch --cov-report=term-missing --cov-fail-under=80`
- Cobertura alta **não garante** bons testes: um teste sem `assert` já cobre linhas. Use como indicador de lacunas, não como meta única.
- **Mutation testing**: a ferramenta altera o código (ex.: `>` vira `>=`) e roda os testes; se nenhum falha, o "mutante sobreviveu" e há teste fraco. Ferramentas: `mutmut` (Python), Stryker (JS). Métrica: *mutation score*.
- **Testes de propriedade** (property-based): em vez de exemplos fixos, declara-se uma **propriedade** válida para qualquer entrada e a biblioteca gera centenas de casos, reduzindo o caso falho ao mínimo. Python: **Hypothesis**.

## Exemplo
```python
# ordenar.py
def maior_ou_igual_18(idade: int) -> bool:
    return idade >= 18
```
```python
# test_ordenar.py  (pip install hypothesis pytest pytest-cov)
from hypothesis import given, strategies as st
from ordenar import maior_ou_igual_18

def test_limite():            # mata o mutante '>=' -> '>'
    assert maior_ou_igual_18(18) is True
    assert maior_ou_igual_18(17) is False

@given(st.lists(st.integers()))
def test_sorted_e_idempotente(xs):
    assert sorted(sorted(xs)) == sorted(xs)

@given(st.lists(st.integers()))
def test_sorted_preserva_tamanho_e_ordem(xs):
    r = sorted(xs)
    assert len(r) == len(xs)
    assert all(a <= b for a, b in zip(r, r[1:]))

@given(st.text())
def test_inverter_duas_vezes_devolve_original(s):
    assert s[::-1][::-1] == s
```
Rodar mutação: `pip install mutmut && mutmut run && mutmut results`.

## Exercício
1. Meça a cobertura do seu backend e identifique 3 linhas/ramos não cobertos.
2. Escreva um teste com Hypothesis para `slugify` (resultado nunca contém espaços).
3. Remova o `assert` de um teste: a cobertura mudou? O que isso ensina?

## Checklist
- [ ] Gero relatório de cobertura com ramos
- [ ] Sei o que é mutante sobrevivente
- [ ] Escrevo uma propriedade com Hypothesis
