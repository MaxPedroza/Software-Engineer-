# Aula 9 — Exceções e depuração

**Duração:** ~25 min · **Módulo 3**

## Objetivo
Tratar erros com `try/except` e depurar programas de forma sistemática.

## Teoria
- **Exceção**: evento de erro em tempo de execução que interrompe o fluxo se não for tratada.
- Estrutura: `try` / `except TipoErro as e` / `else` (sem erro) / `finally` (sempre roda).
- Exceções comuns: `ValueError`, `TypeError`, `KeyError`, `IndexError`, `FileNotFoundError`, `ZeroDivisionError`, `json.JSONDecodeError`.
- Capture exceções **específicas**; evite `except:` vazio, que esconde bugs.
- `raise ValueError("mensagem")` sinaliza erro; crie exceções próprias herdando de `Exception`.
- **Depuração**: 1) reproduza o erro, 2) leia o traceback de baixo para cima, 3) formule hipótese, 4) verifique com `print`/`logging`/`breakpoint()` (pdb) ou o depurador do VS Code, 5) corrija e teste.
- `assert cond, "msg"` valida suposições durante o desenvolvimento.
- `logging` é melhor que `print` em programas reais (níveis DEBUG, INFO, ERROR).

## Exemplo em Python
```python
import json
import logging

logging.basicConfig(level=logging.INFO, format="%(levelname)s: %(message)s")

class TarefaNaoEncontrada(Exception):
    pass

def ler_inteiro(texto: str) -> int:
    try:
        return int(texto)
    except ValueError:
        raise ValueError(f"'{texto}' não é um número inteiro") from None

def carregar(caminho):
    try:
        with open(caminho, encoding="utf-8") as f:
            return json.load(f)
    except FileNotFoundError:
        logging.info("arquivo não existe; começando vazio")
        return []
    except json.JSONDecodeError as e:
        logging.error("JSON corrompido: %s", e)
        raise
    finally:
        logging.info("tentativa de leitura finalizada")

def remover(tarefas, id_):
    for t in tarefas:
        if t["id"] == id_:
            tarefas.remove(t)
            return
    raise TarefaNaoEncontrada(f"id {id_} inexistente")

print(carregar("nao_existe.json"))
try:
    ler_inteiro("abc")
except ValueError as e:
    print("Erro:", e)
```

## Exercício
1. Faça `dividir(a, b)` que trate `ZeroDivisionError` e retorne `None` com uma mensagem.
2. Escreva um programa com um bug de índice e use `breakpoint()` para inspecioná-lo.
3. Substitua os `print` de depuração do seu código por `logging`.

## Checklist
- [ ] Uso `try/except/else/finally`
- [ ] Capturo exceções específicas e levanto as minhas
- [ ] Sigo um método para depurar
