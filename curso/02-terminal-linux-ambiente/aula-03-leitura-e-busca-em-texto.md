# Aula 3 — Leitura e busca em texto (cat, less, grep, find)

**Duração:** ~25 min · **Módulo 2**

## Objetivo
Ler arquivos e localizar conteúdo e arquivos usando `cat`, `less`, `head`, `tail`, `grep` e `find`.

## Teoria
- `cat arq` imprime tudo; `less arq` pagina (`/termo` busca, `q` sai); `head -n 5` e `tail -n 5` mostram início/fim; `tail -f log` acompanha em tempo real; `wc -l` conta linhas.
- **grep** busca linhas que casam com um padrão:
  - `-i` ignora maiúsculas, `-n` mostra nº da linha, `-r` recursivo, `-v` inverte, `-c` conta, `-E` regex estendida.
- **find** busca arquivos por critérios: `-name`, `-type f|d`, `-mtime`, `-size`.
- Regex básica: `^` início, `$` fim, `.` qualquer caractere, `*` repetição, `[0-9]` classe.

## Exemplo em Bash
```bash
printf "ERRO: disco cheio\nINFO: ok\nerro: timeout\n" > app.log

grep -in "erro" app.log          # 1:ERRO..., 3:erro...
grep -c "INFO" app.log           # 1
grep -v "INFO" app.log           # tudo exceto INFO
grep -rn "TODO" --include="*.py" .   # TODOs em arquivos Python

find . -name "*.log" -type f
find . -type f -size +1M -mtime -7   # >1MB, modificados nos últimos 7 dias
```

## Exercício
1. Crie um `app.log` com 6 linhas variadas (INFO, WARN, ERRO) e conte quantas têm ERRO.
2. Encontre todos os arquivos `.md` do repositório do curso com `find`.
3. Use `grep -rn` para listar onde aparece a palavra "Python" nas aulas do Módulo 1.

## Checklist
- [ ] Leio arquivos grandes com `less`, `head` e `tail`
- [ ] Uso `grep` com `-i`, `-n`, `-r`, `-v`
- [ ] Localizo arquivos com `find`
