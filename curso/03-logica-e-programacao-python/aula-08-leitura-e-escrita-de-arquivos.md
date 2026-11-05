# Aula 8 — Leitura e escrita de arquivos (texto, JSON, CSV)

**Duração:** ~30 min · **Módulo 3**

## Objetivo
Persistir e carregar dados em arquivos de texto, JSON e CSV.

## Teoria
- Abra arquivos com `with open(caminho, modo, encoding="utf-8") as f:` — fecha automaticamente.
- Modos: `"r"` leitura, `"w"` escrita (apaga), `"a"` acrescenta, `"x"` cria (erro se existir); `"b"` para binário.
- Leitura: `f.read()`, `f.readlines()`, ou iterar `for linha in f` (eficiente em memória).
- `pathlib.Path` é a forma moderna de lidar com caminhos: `Path("dados") / "t.json"`, `.exists()`, `.read_text()`.
- **JSON**: `json.dump(obj, f)` / `json.load(f)`; `json.dumps`/`loads` trabalham com strings. Mapeia dict↔objeto, list↔array.
- **CSV**: módulo `csv` com `reader`/`writer` ou `DictReader`/`DictWriter`; use `newline=""` ao abrir.
- Sempre declare `encoding="utf-8"` e trate arquivo inexistente.

## Exemplo em Python
```python
import csv
import json
from pathlib import Path

arquivo = Path("tarefas.json")

def carregar():
    if not arquivo.exists():
        return []
    with arquivo.open(encoding="utf-8") as f:
        return json.load(f)

def salvar(tarefas):
    with arquivo.open("w", encoding="utf-8") as f:
        json.dump(tarefas, f, ensure_ascii=False, indent=2)

tarefas = carregar()
tarefas.append({"id": len(tarefas) + 1, "titulo": "Ler aula 8", "feita": False})
salvar(tarefas)

with open("tarefas.csv", "w", newline="", encoding="utf-8") as f:
    w = csv.DictWriter(f, fieldnames=["id", "titulo", "feita"])
    w.writeheader()
    w.writerows(tarefas)

with open("tarefas.csv", encoding="utf-8") as f:
    for linha in csv.DictReader(f):
        print(linha["id"], linha["titulo"])
```

## Exercício
1. Escreva um programa que registre linhas de log com data em `log.txt` usando modo `"a"`.
2. Leia um CSV de notas (`nome,nota`) e imprima a média e o melhor aluno.
3. Converta `tarefas.json` em `tarefas.csv` e vice-versa.

## Checklist
- [ ] Uso `with open` com `encoding`
- [ ] Leio e gravo JSON e CSV
- [ ] Tratei o caso de arquivo inexistente
