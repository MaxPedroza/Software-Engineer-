# Aula 1 — Por que testar e a pirâmide de testes

**Duração:** ~20 min · **Módulo 15**

## Objetivo
Entender o valor dos testes automatizados e distribuir os tipos de teste de forma equilibrada.

## Teoria
- Testes dão **confiança para mudar** o código, documentam o comportamento e detectam regressões cedo (bugs custam mais quanto mais tarde são achados).
- Um bom teste é **F.I.R.S.T.**: Fast, Independent, Repeatable, Self-validating, Timely.
- **Pirâmide de testes**:
  - **Base — unitários**: muitos, rápidos, isolam uma função/classe.
  - **Meio — integração**: verificam módulos juntos (API + banco).
  - **Topo — E2E**: poucos, simulam o usuário no navegador; lentos e frágeis.
- Anti-padrão: o **"cone de sorvete"** (muitos E2E manuais, poucos unitários).
- Estrutura **Arrange-Act-Assert (AAA)**: preparar, executar, verificar.
- Teste verifica **comportamento**, não detalhes de implementação.
- Testes que falham às vezes sem mudança de código são **flaky** e devem ser corrigidos ou removidos.

## Exemplo
```python
# calculadora.py
def dividir(a: float, b: float) -> float:
    if b == 0:
        raise ValueError("divisão por zero")
    return a / b
```
```python
# test_calculadora.py
import pytest
from calculadora import dividir

def test_dividir_numeros_positivos():
    # Arrange
    a, b = 10, 4
    # Act
    resultado = dividir(a, b)
    # Assert
    assert resultado == 2.5

def test_dividir_por_zero_levanta_erro():
    with pytest.raises(ValueError, match="divisão por zero"):
        dividir(1, 0)
```
Execute com `pip install pytest` e `pytest -v`.

## Exercício
1. Classifique em unitário, integração ou E2E: (a) validar um CPF; (b) `POST /tarefas` gravando no banco; (c) login pelo navegador.
2. Escreva 3 testes AAA para uma função `eh_par(n)`.
3. Desenhe a pirâmide ideal para o seu projeto, com proporções aproximadas.

## Checklist
- [ ] Sei justificar o valor dos testes
- [ ] Descrevo a pirâmide de testes
- [ ] Escrevo testes no padrão AAA
