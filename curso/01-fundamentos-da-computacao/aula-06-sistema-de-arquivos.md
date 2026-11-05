# Aula 6 — Sistema de arquivos

**Duração:** ~15 min · **Módulo 1**

## Objetivo
Entender como dados são organizados e persistidos em disco.

## Teoria
- **Arquivo**: sequência de bytes com nome e metadados (tamanho, datas, permissões).
- **Diretório**: contêiner que organiza arquivos em uma árvore hierárquica.
- **Caminhos**: *absoluto* (`/home/ana/projeto/app.py`) vs *relativo* (`./app.py`, `../dados`).
- **Sistemas de arquivos**: ext4 (Linux), NTFS (Windows), APFS (macOS). Definem como blocos são alocados, journaling e limites.
- **Inode** (Linux): estrutura com metadados do arquivo; o nome fica no diretório.
- **Links**: *hard link* (outro nome para o mesmo inode) e *symlink* (atalho para um caminho).
- **Buffer e flush**: escritas passam por cache do SO; `fsync` força gravação em disco.
- **Tudo é arquivo** (Linux): dispositivos e sockets também aparecem como arquivos.

### Texto vs binário
Arquivos de texto são bytes interpretados com uma codificação (UTF-8); binários (imagens, executáveis) têm formato próprio.

## Exemplo em Python
```python
from pathlib import Path

p = Path("notas") / "aula.txt"
p.parent.mkdir(exist_ok=True)
p.write_text("olá, mundo\n", encoding="utf-8")
print(p.read_text(encoding="utf-8"), p.stat().st_size)
```

## Exercício
1. Crie uma estrutura de pastas para seu projeto e explique cada uma.
2. Crie um symlink para um arquivo e veja o que ocorre ao apagar o original.

## Checklist
- [ ] Diferencio caminho absoluto e relativo
- [ ] Sei o que são inode, hard link e symlink
- [ ] Sei ler e escrever arquivos com codificação explícita
