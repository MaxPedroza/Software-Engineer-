# Aula 5 — Permissões, usuários e variáveis de ambiente

**Duração:** ~25 min · **Módulo 2**

## Objetivo
Interpretar e alterar permissões de arquivos e usar variáveis de ambiente e o `PATH`.

## Teoria
- Cada arquivo tem **dono**, **grupo** e permissões para **u**(dono), **g**(grupo), **o**(outros): `r`=4, `w`=2, `x`=1.
- `ls -l` mostra `-rwxr-xr--`: tipo (`-` arquivo, `d` pasta) + 3 trios.
- `chmod 755 f` (rwxr-xr-x), `chmod 600 f` (só dono lê/escreve), `chmod +x script.sh`, `chown user:grupo f`.
- `sudo` executa como administrador (root): use com cautela e apenas quando necessário.
- **Variáveis de ambiente**: pares chave=valor herdados por processos filhos. `export NOME=valor`, `echo "$NOME"`, `env` lista todas.
- `PATH` é a lista de pastas onde o shell procura executáveis. Para persistir: adicione `export` ao `~/.bashrc`.
- **Nunca** coloque segredos (tokens, senhas) no código; use variáveis de ambiente ou arquivos `.env` fora do Git.

## Exemplo em Bash
```bash
echo 'echo "oi"' > oi.sh
ls -l oi.sh            # -rw-r--r--
./oi.sh                # Permission denied
chmod +x oi.sh && ./oi.sh

chmod 600 chave.txt 2>/dev/null
export APP_ENV=dev
bash -c 'echo "Ambiente: $APP_ENV"'   # filho herda a variável

export PATH="$HOME/bin:$PATH"
echo "$PATH" | tr ':' '\n'
```

## Exercício
1. Crie um script que imprime a data, torne-o executável e rode-o.
2. Converta `rw-r-----` para notação octal (resposta: 640) e aplique com `chmod`.
3. Crie `~/bin`, coloque o script lá, adicione ao `PATH` e execute-o de qualquer pasta.

## Checklist
- [ ] Leio a saída de `ls -l`
- [ ] Uso `chmod` em octal e simbólico
- [ ] Sei usar `export` e o `PATH`
