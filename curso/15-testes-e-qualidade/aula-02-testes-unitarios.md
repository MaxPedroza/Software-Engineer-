# Aula 2 — Testes unitários

**Duração:** ~20 min · **Módulo 15**

## Objetivo
Escrever testes unitários claros com pytest, usando fixtures e parametrização.

## Teoria
- **Teste unitário** exercita uma unidade pequena (função/classe) de forma isolada, rápida e determinística.
- pytest descobre arquivos `test_*.py` e funções `test_*`; usa `assert` simples com relatório detalhado.
- **Fixtures** (`@pytest.fixture`) preparam dados/objetos reutilizáveis; `tmp_path` fornece diretório temporário.
- **Parametrização** (`@pytest.mark.parametrize`) roda o mesmo teste com várias entradas.
- Cubra: caso feliz, **casos de borda** (vazio, zero, limites) e **erros esperados**.
- Um teste = um motivo para falhar; nomes descritivos (`test_<unidade>_<situacao>_<resultado>`).
- Use `pytest.approx` para floats.

## Exemplo
```python
# tarefas.py
from dataclasses import dataclass, field

@dataclass
class Tarefa:
    titulo: str
    feita: bool = False

@dataclass
class ListaDeTarefas:
    itens: list[Tarefa] = field(default_factory=list)

    def adicionar(self, titulo: str) -> Tarefa:
        if not titulo.strip():
            raise ValueError("título obrigatório")
        t = Tarefa(titulo.strip())
        self.itens.append(t)
        return t

    def pendentes(self) -> list[Tarefa]:
        return [t for t in self.itens if not t.feita]
```
```python
# test_tarefas.py
import pytest
from tarefas import ListaDeTarefas

@pytest.fixture
def lista():
    return ListaDeTarefas()

def test_adicionar_remove_espacos(lista):
    assert lista.adicionar("  estudar  ").titulo == "estudar"

@pytest.mark.parametrize("titulo", ["", "   "])
def test_adicionar_titulo_vazio_falha(lista, titulo):
    with pytest.raises(ValueError):
        lista.adicionar(titulo)

def test_pendentes_ignora_feitas(lista):
    t = lista.adicionar("a")
    lista.adicionar("b")
    t.feita = True
    assert [x.titulo for x in lista.pendentes()] == ["b"]
```

## Exercício
1. Adicione o método `concluir(titulo)` e teste caso feliz e tarefa inexistente.
2. Parametrize um teste com 5 entradas para uma função `slugify`.
3. Escreva um teste que falha, veja a mensagem do pytest e corrija.

## Checklist
- [ ] Uso fixtures e parametrização
- [ ] Testo bordas e erros
- [ ] Nomeio testes de forma descritiva
