# Aula 4 — TDD (Test-Driven Development)

**Duração:** ~20 min · **Módulo 15**

## Objetivo
Aplicar o ciclo Red-Green-Refactor para desenvolver funcionalidades guiadas por testes.

## Teoria
- **TDD** inverte a ordem: o teste vem antes do código.
- **Ciclo**:
  1. 🔴 **Red**: escreva um teste que falha (para o motivo certo).
  2. 🟢 **Green**: escreva o código **mais simples** que o faz passar.
  3. 🔵 **Refactor**: melhore o design mantendo os testes verdes.
- Passos pequenos; um comportamento por vez.
- Benefícios: design mais simples e testável, alta cobertura natural, menos medo de refatorar.
- Limitações: exige disciplina; não substitui testes de integração; menos útil em exploração/protótipos.
- **BDD**: variante com linguagem de negócio (Dado/Quando/Então).
- Técnica auxiliar: "triangulação" — adicionar um segundo exemplo para forçar generalização.

## Exemplo: validador de senha
```python
# test_senha.py — RED: escreva primeiro
import pytest
from senha import senha_forte

def test_rejeita_senha_curta():
    assert senha_forte("Ab1") is False

def test_exige_digito():
    assert senha_forte("Abcdefghij") is False

def test_exige_maiuscula():
    assert senha_forte("abcdefg123") is False

def test_aceita_senha_valida():
    assert senha_forte("Abcdefg123") is True
```
```python
# senha.py — GREEN/REFACTOR: evolui a cada teste
def senha_forte(s: str) -> bool:
    return (
        len(s) >= 8
        and any(c.isdigit() for c in s)
        and any(c.isupper() for c in s)
    )
```
Fluxo: rode `pytest` → falha (módulo não existe) → crie `senha_forte` retornando `False` → passe teste a teste, refatorando ao final (ex.: extrair regras em uma lista de funções).

## Exercício
1. Faça por TDD uma função `fizzbuzz(n)`, commitando após cada ciclo.
2. Evolua `senha_forte` para exigir caractere especial, começando pelo teste.
3. Reflita: em que situação do seu projeto TDD não ajudaria?

## Checklist
- [ ] Executo o ciclo Red-Green-Refactor
- [ ] Escrevo o código mínimo para passar
- [ ] Refatoro com testes verdes
