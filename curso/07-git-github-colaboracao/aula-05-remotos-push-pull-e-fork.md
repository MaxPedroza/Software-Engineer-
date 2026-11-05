# Aula 5 — Remotos, push, pull e fork

**Duração:** ~25 min · **Módulo 7**

## Objetivo
Sincronizar o repositório local com o GitHub e entender o fluxo de fork.

## Teoria
- **Remoto**: cópia do repositório hospedada em outro lugar; por convenção, `origin`.
- `git clone <url>` copia tudo; `git remote -v` lista remotos.
- `git push` envia commits; `git fetch` baixa sem integrar; `git pull` = `fetch` + `merge` (ou `--rebase`).
- **Branch de rastreamento**: `git push -u origin minha-branch` liga a branch local à remota.
- Autenticação: **SSH** (chave) ou HTTPS com token. Nunca versione tokens.
- **Fork**: cópia do repositório de outra pessoa na sua conta. Convenção: `origin` = seu fork, `upstream` = repositório original.
- `git push --force-with-lease` é a forma segura de forçar push após rebase (nunca `--force` em `main`).

## Exemplo
```bash
# Publicar um projeto local
git remote add origin git@github.com:usuario/meu-projeto.git
git push -u origin main

# Clonar e atualizar
git clone git@github.com:usuario/meu-projeto.git
git fetch origin
git pull --rebase origin main

# Fluxo de fork
git clone git@github.com:voce/projeto-alheio.git
cd projeto-alheio
git remote add upstream git@github.com:dono/projeto-alheio.git
git fetch upstream
git switch main
git merge upstream/main
git push origin main

# Enviar branch nova
git switch -c fix/typo
git push -u origin fix/typo
```

## Exercício
1. Crie um repositório vazio no GitHub e publique seu projeto local.
2. Edite um arquivo pela interface web e traga a mudança com `git pull`.
3. Faça fork de um repositório, configure `upstream` e sincronize a `main`.

## Checklist
- [ ] Diferencio `fetch` de `pull`
- [ ] Publico uma branch com `push -u`
- [ ] Configuro `origin` e `upstream`
