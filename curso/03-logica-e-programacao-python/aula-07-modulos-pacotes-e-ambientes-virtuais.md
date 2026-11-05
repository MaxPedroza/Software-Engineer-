# Aula 7 — Módulos, pacotes e ambientes virtuais

**Duração:** ~25 min · **Módulo 3**

## Objetivo
Organizar código em módulos e pacotes e isolar dependências com `venv` e `pip`.

## Teoria
- **Módulo**: arquivo `.py`. **Pacote**: pasta de módulos (com `__init__.py`, opcional em pacotes de namespace).
- Importações: `import math`, `from math import sqrt`, `import json as js`. Evite `from x import *`.
- Biblioteca padrão ("baterias incluídas"): `math`, `random`, `datetime`, `pathlib`, `json`, `csv`, `argparse`, `collections`.
- `if __name__ == "__main__":` executa código só quando o arquivo é rodado diretamente, não ao ser importado.
- **Ambiente virtual**: pasta isolada com seu próprio Python e pacotes, evitando conflito entre projetos.
- `pip install pacote`, `pip freeze > requirements.txt`, `pip install -r requirements.txt`.
- Inclua `.venv/` no `.gitignore`.

## Exemplo
Estrutura:
```
tarefas/
├── tarefas/
│   ├── __init__.py
│   └── calculos.py
└── main.py
```
`tarefas/calculos.py`:
```python
def media(valores):
    return sum(valores) / len(valores)

if __name__ == "__main__":
    print(media([1, 2, 3]))   # só roda ao executar este arquivo
```
`main.py`:
```python
from tarefas.calculos import media
from datetime import date

print(media([8, 9]), date.today().isoformat())
```
Ambiente virtual (Bash):
```bash
python3 -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install requests
pip freeze > requirements.txt
deactivate
```

## Exercício
1. Crie o pacote acima e execute `python3 main.py`; depois `python3 tarefas/calculos.py`. O que muda?
2. Crie um `.venv`, instale `requests` e confirme com `pip list` e `which python`.
3. Use `random.choice` e `datetime` num script que sorteia uma tarefa e mostra o dia da semana.

## Checklist
- [ ] Crio e importo módulos e pacotes
- [ ] Entendo `__name__ == "__main__"`
- [ ] Uso `venv` e `requirements.txt`
