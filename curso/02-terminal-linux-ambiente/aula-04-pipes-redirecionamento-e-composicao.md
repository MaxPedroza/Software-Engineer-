# Aula 4 — Pipes, redirecionamento e composição de comandos

**Duração:** ~25 min · **Módulo 2**

## Objetivo
Combinar comandos pequenos em fluxos poderosos usando pipes e redirecionamentos.

## Teoria
- Todo processo tem três fluxos: **stdin** (0), **stdout** (1) e **stderr** (2).
- `>` sobrescreve, `>>` acrescenta, `<` lê de arquivo, `2>` redireciona erros, `2>&1` junta erro e saída, `/dev/null` descarta.
- **Pipe** `|` liga a stdout de um comando à stdin do próximo (filosofia Unix: ferramentas pequenas, uma coisa bem feita).
- Ferramentas de filtro: `sort`, `uniq -c`, `cut -d, -f1`, `tr`, `wc`, `head`, `tee` (grava e repassa), `xargs`.
- Encadeamento: `a && b` (b só se a der certo), `a || b` (b se a falhar), `a; b` (sempre).

## Exemplo em Bash
```bash
cat > acessos.txt <<'EOF'
10.0.0.1 GET /home
10.0.0.2 GET /login
10.0.0.1 POST /login
10.0.0.1 GET /home
EOF

# Top IPs por quantidade de acessos
cut -d' ' -f1 acessos.txt | sort | uniq -c | sort -rn

ls /nao-existe 2> erros.txt || echo "falhou"
grep GET acessos.txt | tee gets.txt | wc -l
mkdir build && cd build && echo "ok"
find . -name "*.txt" | xargs wc -l
```

## Exercício
1. Mostre quantas requisições `GET` e `POST` existem em `acessos.txt` (`cut`, `sort`, `uniq -c`).
2. Execute `ls /etc /nao-existe` enviando a saída para `ok.txt` e o erro para `erro.txt`.
3. Liste as 3 maiores pastas de `~` com `du -sh * | sort -rh | head -3`.

## Checklist
- [ ] Entendo stdin, stdout e stderr
- [ ] Uso `>`, `>>`, `2>` e `|`
- [ ] Componho `sort | uniq -c` e `&&`/`||`
