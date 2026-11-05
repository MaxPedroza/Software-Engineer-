# Aula 3 — Mocks, stubs e injeção de dependência

**Duração:** ~20 min · **Módulo 15**

## Objetivo
Isolar a unidade testada de dependências externas usando test doubles e injeção de dependência.

## Teoria
- **Test doubles**:
  - **Dummy**: preenche parâmetro, não é usado.
  - **Stub**: devolve respostas fixas.
  - **Fake**: implementação simples funcional (repositório em memória).
  - **Mock**: verifica **interações** (foi chamado? com quais argumentos?).
  - **Spy**: registra chamadas reais.
- **Injeção de dependência (DI)**: receber dependências por parâmetro/construtor em vez de criá-las dentro da classe. Torna o código testável e desacoplado.
- Prefira **fakes** e stubs; mocks demais acoplam o teste à implementação.
- Mocke apenas **fronteiras** (HTTP, e-mail, relógio, banco), nunca o código que você quer testar.
- `unittest.mock` (`Mock`, `patch`) e `pytest-mock` (`mocker`).

## Exemplo
```python
# notificador.py
class Notificador:
    def __init__(self, enviador):
        self.enviador = enviador          # dependência injetada

    def avisar_atraso(self, email: str, titulo: str) -> bool:
        if "@" not in email:
            return False
        self.enviador.enviar(email, f"Tarefa atrasada: {titulo}")
        return True
```
```python
# test_notificador.py
from unittest.mock import Mock
from notificador import Notificador

def test_envia_email_quando_endereco_valido():
    enviador = Mock()
    n = Notificador(enviador)

    assert n.avisar_atraso("ana@x.com", "relatório") is True
    enviador.enviar.assert_called_once_with("ana@x.com", "Tarefa atrasada: relatório")

def test_nao_envia_quando_email_invalido():
    enviador = Mock()
    assert Notificador(enviador).avisar_atraso("invalido", "x") is False
    enviador.enviar.assert_not_called()

class EnviadorFake:                      # fake: guarda em memória
    def __init__(self): self.enviados = []
    def enviar(self, para, msg): self.enviados.append((para, msg))

def test_com_fake():
    fake = EnviadorFake()
    Notificador(fake).avisar_atraso("a@b.com", "t")
    assert len(fake.enviados) == 1
```

## Exercício
1. Refatore uma função que chama `requests.get` internamente para receber o cliente HTTP por parâmetro e teste com um stub.
2. Teste uma função dependente de `datetime.now()` injetando um relógio.
3. Explique quando um fake é melhor que um mock.

## Checklist
- [ ] Diferencio stub, fake, mock e spy
- [ ] Aplico injeção de dependência
- [ ] Mocko apenas fronteiras do sistema
