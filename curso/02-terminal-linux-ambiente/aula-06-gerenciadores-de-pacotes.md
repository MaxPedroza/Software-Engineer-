# Aula 6 — Gerenciadores de pacotes (apt, brew, winget)

**Duração:** ~20 min · **Módulo 2**

## Objetivo
Instalar, atualizar e remover software de forma reproduzível usando gerenciadores de pacotes.

## Teoria
- Um **gerenciador de pacotes** baixa software de repositórios confiáveis, resolve **dependências**, verifica assinaturas e permite atualizar/remover.
- Vantagens sobre baixar instaladores manualmente: segurança, versionamento, automação.

| Sistema | Ferramenta | Instalar | Buscar |
|---------|-----------|----------|--------|
| Debian/Ubuntu/WSL | `apt` | `sudo apt install git` | `apt search git` |
| macOS | Homebrew | `brew install git` | `brew search git` |
| Windows | winget | `winget install Git.Git` | `winget search git` |

- Ciclo no apt: `sudo apt update` (atualiza índice) → `sudo apt upgrade` (atualiza pacotes) → `sudo apt remove pkg`.
- Há também gerenciadores por linguagem: `pip` (Python), `npm` (Node), `cargo` (Rust) — não confunda com os do sistema.
- Boas práticas: instale só de fontes oficiais, registre os pacotes usados no `setup.sh`.

## Exemplo em Bash
```bash
# Instala ferramentas só se ainda não existirem
for pkg in git curl jq; do
  if command -v "$pkg" >/dev/null 2>&1; then
    echo "$pkg já instalado"
  else
    sudo apt install -y "$pkg"
  fi
done

apt list --installed 2>/dev/null | grep -c git
```

## Exercício
1. Instale `tree` e `jq` com o gerenciador do seu sistema e teste `tree` e `echo '{"a":1}' | jq .a`.
2. Descubra a versão instalada do git (`git --version`) e de qual pacote vem (`apt show git` ou `brew info git`).
3. Liste as ferramentas que seu projeto precisará (git, python3, etc.) para o futuro `setup.sh`.

## Checklist
- [ ] Sei por que usar um gerenciador de pacotes
- [ ] Executo `update`/`install`/`remove`
- [ ] Verifico ferramentas com `command -v`
