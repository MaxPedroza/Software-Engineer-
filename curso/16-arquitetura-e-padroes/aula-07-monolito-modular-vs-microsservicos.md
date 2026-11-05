# Aula 7 — Monolito modular vs microsserviços

**Duração:** ~20 min · **Módulo 16**

## Objetivo
Comparar estilos de implantação e decidir com critérios, evitando complexidade prematura.

## Teoria
| | Monolito modular | Microsserviços |
|--|------------------|----------------|
| Implantação | Uma unidade | Vários serviços independentes |
| Comunicação | Chamada de função | Rede (HTTP/gRPC/mensagens) |
| Dados | Banco único (esquemas por módulo) | Banco por serviço |
| Complexidade operacional | Baixa | Alta (observabilidade, deploy, resiliência) |
| Escala | Do sistema inteiro | Por serviço |
| Times | Poucos | Muitos, autônomos |

- **Monolito modular**: módulos com fronteiras claras (alinhados a bounded contexts), comunicando-se por interfaces públicas; base para extrair serviços depois.
- **Microsserviços** trazem: latência, falhas parciais, consistência eventual, transações distribuídas (Saga), versionamento de contratos. Ver "Falácias da computação distribuída".
- **Heurística**: comece com monolito modular; extraia um serviço quando houver razão concreta (escala distinta, time independente, ciclo de deploy).
- Anti-padrão: **monolito distribuído** (serviços acoplados que precisam ser implantados juntos).
- Padrões de apoio: API Gateway, circuit breaker, retry com backoff, idempotência.

## Exemplo: fronteira de módulo em Python
```python
# modulos/tarefas/__init__.py — única API pública do módulo
from .servico import criar_tarefa, listar_tarefas
__all__ = ["criar_tarefa", "listar_tarefas"]

# modulos/notificacoes/servico.py
from modulos import tarefas            # usa só a API pública
# from modulos.tarefas.repositorio import ...   # PROIBIDO: acesso interno
```
Teste de arquitetura (impede violações de fronteira):
```python
import ast, pathlib

def test_notificacoes_nao_acessa_internos_de_tarefas():
    for arq in pathlib.Path("modulos/notificacoes").rglob("*.py"):
        for no in ast.walk(ast.parse(arq.read_text())):
            if isinstance(no, ast.ImportFrom) and (no.module or "").startswith("modulos.tarefas."):
                raise AssertionError(f"{arq}: importa interno de tarefas")
```

## Exercício
1. Divida o sistema de tarefas em 3 módulos com APIs públicas e sem dependências cíclicas.
2. Liste 3 razões válidas e 3 inválidas para extrair um microsserviço.
3. Descreva como seria a chamada entre dois serviços e o que acontece se um deles cair.

## Checklist
- [ ] Comparo monolito modular e microsserviços
- [ ] Defino fronteiras de módulos
- [ ] Reconheço o monolito distribuído
