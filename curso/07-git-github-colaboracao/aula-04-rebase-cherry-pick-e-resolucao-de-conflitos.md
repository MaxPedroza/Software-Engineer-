# Aula 4 — Rebase, cherry-pick e resolução de conflitos

**Duração:** ~25 min · **Módulo 7**

## Objetivo
Reescrever e reaplicar commits com segurança e resolver conflitos.

## Teoria
- **Rebase**: reaplica os commits da sua branch sobre outra base, gerando histórico **linear**. Cria commits novos (hashes mudam).
- **Regra de ouro**: nunca faça rebase de commits já publicados e usados por outras pessoas.
- `git rebase -i HEAD~3` permite **squash**, reordenar, editar e remover commits antes do PR.
- **Cherry-pick**: copia um commit específico para a branch atual (`git cherry-pick <hash>`), útil em hotfixes.
- **Conflito**: edite o arquivo, mantenha o conteúdo correto, remova os marcadores, `git add`, depois `git rebase --continue` (ou `git merge --continue`/`git commit`). Para desistir: `--abort`.
- `git reflog` mostra onde o `HEAD` esteve — salva commits "perdidos".

## Exemplo
```bash
# Atualizar a feature com as novidades da main
git switch feature/login
git fetch origin
git rebase origin/main

# Se houver conflito:
git status                     # lista "both modified"
# edite o arquivo e remova <<<<<<<, =======, >>>>>>>
git add arquivo.py
git rebase --continue
# ou desistir
git rebase --abort

# Limpar os 3 últimos commits antes do PR
git rebase -i HEAD~3           # troque "pick" por "squash" ou "reword"

# Levar só uma correção para outra branch
git switch release/1.0
git cherry-pick a1b2c3d

# Recuperar de um erro
git reflog
git reset --hard HEAD@{2}
```

## Exercício
1. Crie duas branches que editam a mesma linha, provoque o conflito e resolva-o em merge e depois em rebase.
2. Faça 3 commits "wip" e una-os em um só com `rebase -i`.
3. Use `cherry-pick` para copiar um commit para outra branch.

## Checklist
- [ ] Sei quando usar merge e quando usar rebase
- [ ] Resolvo conflitos sem perder código
- [ ] Conheço a regra de ouro do rebase
