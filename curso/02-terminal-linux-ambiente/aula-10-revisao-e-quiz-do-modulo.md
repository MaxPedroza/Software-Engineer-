# Aula 10 — Revisão e quiz do módulo

**Duração:** ~20 min · **Módulo 2**

## Resumo
- Terminal é a interface de texto; o shell interpreta comandos; CLIs permitem automação.
- Navegação: `ls`, `cd`, `mkdir -p`, `cp -r`, `mv`, `rm` (sem lixeira).
- Busca: `cat`, `less`, `head`, `tail`, `grep`, `find`.
- Pipes (`|`) e redirecionamentos (`>`, `>>`, `2>`) compõem ferramentas pequenas.
- Permissões `rwx` em octal (`755`, `644`); `PATH` e `export` controlam o ambiente.
- Gerenciadores de pacotes: apt, brew, winget.
- Scripts Bash: shebang, `if`, `for`, funções, `set -euo pipefail`.
- VS Code, `.editorconfig`, WSL e Dev Containers padronizam o ambiente.

## Quiz (responda sem consultar)
1. Qual a diferença entre terminal e shell?
2. O que `cd ..` e `cd ~` fazem?
3. Qual comando mostra as últimas linhas de um log em tempo real?
4. O que faz `grep -rn "TODO" .`?
5. Qual a diferença entre `>` e `>>`?
6. O que faz `cmd1 | cmd2`?
7. O que significa a permissão `755`?
8. Para que serve a variável `PATH`?
9. O que `set -euo pipefail` faz num script?
10. Qual a diferença entre um container e uma VM?

## Gabarito resumido
1. Terminal é a janela; shell interpreta os comandos · 2. Sobe um nível; vai para a home · 3. `tail -f arquivo` · 4. Busca recursivamente "TODO" mostrando arquivo e linha · 5. `>` sobrescreve; `>>` acrescenta · 6. Envia a saída do primeiro como entrada do segundo · 7. dono rwx; grupo e outros r-x · 8. Lista de pastas onde o shell procura executáveis · 9. Aborta em erro, variável indefinida e falha em pipe · 10. Container compartilha o kernel do host (leve); VM virtualiza um SO completo

## Entregável do módulo
Script **`setup.sh`** do projeto contínuo: cria o repositório com a estrutura de pastas (`src/`, `tests/`, `docs/`), verifica/instala dependências (git, python3), usa `set -euo pipefail` e é idempotente (pode rodar duas vezes sem erro).

## Checklist final
- [ ] Acertei 8 ou mais questões
- [ ] `setup.sh` funciona e é idempotente
- [ ] Pronto para o Módulo 3
