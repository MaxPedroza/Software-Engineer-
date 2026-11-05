# Aula 2 — Navegação e manipulação de arquivos (ls, cd, cp, mv, rm)

**Duração:** ~25 min · **Módulo 2**

## Objetivo
Navegar pelo sistema de arquivos e criar, copiar, mover e apagar arquivos e pastas com segurança.

## Teoria
- Caminho **absoluto** começa em `/` (`/home/ana/projeto`); **relativo** parte do diretório atual.
- Atalhos: `.` (atual), `..` (pai), `~` (home), `-` (diretório anterior em `cd -`).

| Comando | Função |
|---------|--------|
| `ls -la` | lista inclusive ocultos, em detalhes |
| `cd pasta` | entra em pasta |
| `mkdir -p a/b/c` | cria pastas aninhadas |
| `touch arq.txt` | cria arquivo vazio / atualiza data |
| `cp -r origem destino` | copia (recursivo para pastas) |
| `mv origem destino` | move ou renomeia |
| `rm arq` / `rm -r pasta` | apaga (**sem lixeira!**) |

- Curingas (globbing): `*.txt`, `arq?.log`, `{a,b}.md`.
- Segurança: use `rm -i` para confirmar; nunca rode `rm -rf` com variáveis vazias ou `/`.

## Exemplo em Bash
```bash
mkdir -p projeto/{src,docs,tests}
touch projeto/src/main.py projeto/docs/README.md
cp projeto/docs/README.md projeto/README.md
mv projeto/src/main.py projeto/src/app.py
ls -R projeto
rm -r projeto/tests
```

## Exercício
1. Crie `loja/{src,tests,docs}` com um comando e um arquivo `.gitkeep` em cada pasta (dica: laço ou `touch loja/{src,tests,docs}/.gitkeep`).
2. Copie `loja` para `loja-backup`, renomeie-a para `loja-v1` e depois apague-a.
3. Liste somente arquivos `.md` de um diretório usando glob.

## Checklist
- [ ] Distingo caminho absoluto e relativo
- [ ] Uso `mkdir -p`, `cp -r`, `mv` e `rm` corretamente
- [ ] Sei os riscos do `rm -rf`
