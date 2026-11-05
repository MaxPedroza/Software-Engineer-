# Aula 1 — Por que aprender o terminal

**Duração:** ~20 min · **Módulo 2**

## Objetivo
Entender o que é o terminal, o shell e por que a linha de comando é essencial para engenheiros de software.

## Teoria
- **Terminal**: janela de texto que envia e recebe caracteres. **Shell** (Bash, Zsh, PowerShell): programa que interpreta os comandos. **CLI**: interface de linha de comando.
- Por que usar: **automação** (scripts), **reprodutibilidade** (comandos documentados), **servidores** (quase sempre sem interface gráfica), **velocidade** e ferramentas de dev (git, docker, npm, pip) que são CLIs.
- Anatomia de um comando: `comando [opções] [argumentos]`, por exemplo `ls -l /etc`.
- Opções curtas (`-l`) e longas (`--help`). Combinar curtas: `ls -la`.
- Ajuda: `comando --help`, `man comando`, `type comando`.

### Comandos iniciais
| Comando | Função |
|---------|--------|
| `pwd` | mostra o diretório atual |
| `whoami` | usuário atual |
| `echo` | imprime texto |
| `date` | data e hora |
| `clear` | limpa a tela |
| `history` | histórico de comandos |

Atalhos: `Tab` completa nomes, `↑` repete comandos, `Ctrl+C` interrompe, `Ctrl+R` busca no histórico.

## Exemplo em Bash
```bash
echo "Olá, $(whoami)!"
echo "Estou em: $(pwd)"
date +"%d/%m/%Y %H:%M"
ls --help | head -n 5
```

## Exercício
1. Abra o terminal e descubra seu usuário, diretório atual e a data formatada como `AAAA-MM-DD`.
2. Use `man ls` para achar a opção que mostra tamanhos legíveis (`-h`) e teste `ls -lh`.
3. Escreva em 3 linhas por que automação importa para um time de software.

## Checklist
- [ ] Diferencio terminal, shell e CLI
- [ ] Sei a anatomia de um comando
- [ ] Sei buscar ajuda com `--help` e `man`
