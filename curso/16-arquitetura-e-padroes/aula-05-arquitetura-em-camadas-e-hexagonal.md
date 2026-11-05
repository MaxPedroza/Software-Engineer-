# Aula 5 — Arquitetura em camadas e hexagonal (ports and adapters)

**Duração:** ~25 min · **Módulo 16**

## Objetivo
Organizar o sistema isolando o domínio de detalhes de infraestrutura.

## Teoria
- **Camadas**: apresentação → aplicação/serviço → domínio → persistência. Cada camada só depende da inferior. Simples, mas o domínio acaba dependendo do banco.
- **Hexagonal** (Alistair Cockburn), também *Clean/Onion Architecture*: o **domínio fica no centro** e não conhece frameworks, banco ou HTTP.
  - **Portas (ports)**: interfaces que o núcleo define. *Entrada* (casos de uso) e *saída* (repositório, e-mail).
  - **Adaptadores (adapters)**: implementações externas (FastAPI, SQLAlchemy, SMTP).
- **Regra da dependência**: dependências apontam **para dentro** (inversão de dependência, o "D" do SOLID).
- Benefícios: domínio testável sem banco, troca de tecnologia, foco no negócio. Custo: mais arquivos e indireção.

```text
src/
  dominio/        # entidades e regras (sem imports de framework)
  aplicacao/      # casos de uso + portas
  adaptadores/    # api (FastAPI), persistencia (SQL/memória)
```

## Exemplo em Python
```python
# dominio/tarefa.py
from dataclasses import dataclass

@dataclass
class Tarefa:
    id: int
    titulo: str
    feita: bool = False

    def concluir(self):
        if self.feita:
            raise ValueError("tarefa já concluída")
        self.feita = True

# aplicacao/portas.py
from typing import Protocol
class RepositorioTarefas(Protocol):          # porta de saída
    def obter(self, id: int) -> Tarefa | None: ...
    def salvar(self, t: Tarefa) -> None: ...

# aplicacao/casos_de_uso.py
class ConcluirTarefa:                        # porta de entrada (caso de uso)
    def __init__(self, repo: RepositorioTarefas): self.repo = repo
    def executar(self, id: int) -> Tarefa:
        t = self.repo.obter(id)
        if t is None:
            raise LookupError("não encontrada")
        t.concluir()
        self.repo.salvar(t)
        return t

# adaptadores/persistencia/memoria.py
class RepositorioMemoria:                    # adaptador (também serve de fake nos testes)
    def __init__(self): self._d: dict[int, Tarefa] = {}
    def obter(self, id): return self._d.get(id)
    def salvar(self, t): self._d[t.id] = t
```
O adaptador FastAPI instancia `ConcluirTarefa(RepositorioSql(...))` na borda (composição raiz).

## Exercício
1. Reorganize o projeto nas pastas acima, movendo regras de negócio das rotas para o domínio.
2. Teste `ConcluirTarefa` com `RepositorioMemoria`, sem banco.
3. Crie um segundo adaptador de persistência (arquivo JSON) sem mexer no domínio.

## Checklist
- [ ] Explico portas e adaptadores
- [ ] Respeito a regra da dependência
- [ ] Testo casos de uso sem infraestrutura
