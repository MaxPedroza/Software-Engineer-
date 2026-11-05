# Aula 2 — Git básico: init, add, commit, log, diff

**Duração:** ~25 min · **Módulo 7**

## Objetivo
Dominar o ciclo básico de versionar um projeto localmente.

## Teoria
- `git init` cria o repositório (pasta oculta `.git`).
- `git status` mostra o estado: arquivos *untracked*, *modified*, *staged*.
- `git add` move mudanças para a **staging area**; `git commit` grava um snapshot com mensagem.
- `git log` mostra o histórico; `git diff` compara.
- Arquivos a ignorar (`__pycache__/`, `.env`, `node_modules/`) vão no **`.gitignore`**. Nunca versione segredos.
- Desfazer: `git restore <arq>` (descarta mudança local), `git restore --staged <arq>` (tira do stage), `git commit --amend` (corrige o último commit local).

## Exemplo
```bash
mkdir meu-projeto && cd meu-projeto
git init
echo "# Meu projeto" > README.md
printf "__pycache__/\n.env\n" > .gitignore
git status
git add README.md .gitignore
git commit -m "Adiciona README e .gitignore"

echo "Gerenciador de tarefas" >> README.md
git diff                  # mudanças ainda não staged
git add README.md
git diff --staged         # mudanças já staged
git commit -m "Descreve o projeto no README"

git log --oneline --graph
git show HEAD             # detalhes do último commit
git restore README.md     # (se houver mudança não commitada)
```

## Exercício
1. Crie um repositório, faça 3 commits pequenos e coerentes.
2. Edite um arquivo, use `git diff`, depois descarte com `git restore`.
3. Crie um arquivo `.env` e confirme que o `.gitignore` o oculta no `git status`.

## Checklist
- [ ] Executo init → add → commit sem consultar
- [ ] Leio `git status`, `diff` e `log`
- [ ] Uso `.gitignore` corretamente
