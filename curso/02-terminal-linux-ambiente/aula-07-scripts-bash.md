# Aula 7 — Scripts Bash: variáveis, condicionais e loops

**Duração:** ~30 min · **Módulo 2**

## Objetivo
Escrever scripts Bash que automatizam tarefas usando variáveis, `if`, `for`, `while` e funções.

## Teoria
- Primeira linha: **shebang** `#!/usr/bin/env bash`. Torne executável com `chmod +x`.
- Variáveis: `nome="Ana"` (sem espaços ao redor do `=`); uso `"$nome"` (sempre com aspas).
- Argumentos: `$1`, `$2`, `$@` (todos), `$#` (quantidade); `$?` é o código de saída do último comando (0 = sucesso).
- Condicionais: `if [[ condição ]]; then ... elif ... else ... fi`.
  - Testes: `-f` arquivo existe, `-d` pasta existe, `-z` string vazia, `-eq -lt -gt` (números), `==` (texto).
- Laços: `for x in lista; do ... done`, `while cond; do ... done`.
- Funções: `nome() { ...; }`.
- Modo seguro: `set -euo pipefail` aborta em erros, variáveis indefinidas e falhas em pipes.

## Exemplo em Bash
```bash
#!/usr/bin/env bash
set -euo pipefail

criar_pasta() {
  if [[ -d "$1" ]]; then
    echo "já existe: $1"
  else
    mkdir -p "$1" && echo "criada: $1"
  fi
}

if [[ $# -lt 1 ]]; then
  echo "Uso: $0 <nome-do-projeto>" >&2
  exit 1
fi

projeto="$1"
for sub in src tests docs; do
  criar_pasta "$projeto/$sub"
done

contador=0
while [[ $contador -lt 3 ]]; do
  echo "tentativa $contador"
  contador=$((contador + 1))
done
```

## Exercício
1. Salve como `novo.sh`, torne executável e rode `./novo.sh meuapp`, depois sem argumento.
2. Escreva `par_impar.sh` que recebe um número e imprime se é par ou ímpar (`$(( $1 % 2 ))`).
3. Faça um script que percorra `*.txt` e imprima nome e número de linhas de cada arquivo.

## Checklist
- [ ] Uso shebang, variáveis entre aspas e argumentos
- [ ] Escrevo `if`, `for` e `while`
- [ ] Uso `set -euo pipefail` e códigos de saída
