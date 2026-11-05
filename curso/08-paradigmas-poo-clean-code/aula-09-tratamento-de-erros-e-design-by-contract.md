# Aula 9 — Tratamento de erros e design by contract

**Duração:** ~25 min · **Módulo 8**

## Objetivo
Tratar falhas de forma explícita e definir contratos claros para funções e classes.

## Teoria
- Use **exceções** para situações excepcionais; não use códigos de retorno mágicos (`-1`, `None` ambíguo).
- Capture **exceções específicas**, nunca `except:` nu; não engula erros em silêncio.
- Crie **exceções de domínio** (`SaldoInsuficienteError`) para comunicar o problema de negócio.
- **Fail fast**: valide cedo e falhe perto da causa.
- **Design by Contract** (Meyer): 
  - **Pré-condições**: o que o chamador deve garantir;
  - **Pós-condições**: o que o método garante ao final;
  - **Invariantes**: o que sempre vale para o objeto.
- `assert` serve para invariantes internas (pode ser desativado com `-O`); para validar entrada externa, lance exceções.
- Use `try/finally` ou `with` para liberar recursos.

## Exemplo em Python
```python
class SaldoInsuficienteError(Exception):
    pass

class Conta:
    def __init__(self, saldo: float = 0):
        if saldo < 0:
            raise ValueError("saldo inicial inválido")
        self._saldo = saldo

    def sacar(self, valor: float) -> None:
        # pré-condições
        if valor <= 0:
            raise ValueError("valor deve ser positivo")
        if valor > self._saldo:
            raise SaldoInsuficienteError(f"saldo {self._saldo}, pedido {valor}")
        antes = self._saldo
        self._saldo -= valor
        # pós-condição / invariante
        assert self._saldo == antes - valor and self._saldo >= 0

try:
    Conta(50).sacar(80)
except SaldoInsuficienteError as e:
    print(f"Operação negada: {e}")
```

## Exercício
1. Crie `TarefaNaoEncontradaError` e lance-a ao buscar um id inexistente.
2. Escreva pré/pós-condições e invariante de uma classe `Pilha`.
3. Corrija `try: ... except: pass` para tratar apenas `FileNotFoundError` e registrar o erro.

## Checklist
- [ ] Uso exceções específicas e de domínio
- [ ] Valido entradas cedo (fail fast)
- [ ] Documento pré e pós-condições
