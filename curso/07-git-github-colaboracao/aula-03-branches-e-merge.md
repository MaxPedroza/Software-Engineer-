# Aula 3 — Branches e merge

**Duração:** ~25 min · **Módulo 7**

## Objetivo
Trabalhar em linhas de desenvolvimento paralelas e integrá-las com merge.

## Teoria
- **Branch** é um ponteiro leve para um commit; criar branches é barato. `HEAD` indica a branch atual.
- Use uma branch por funcionalidade/correção, mantendo `main` estável.
- Comandos: `git branch`, `git switch -c nome` (cria e troca), `git switch nome`, `git branch -d nome`.
- **Merge** integra o histórico de outra branch:
  - **Fast-forward**: `main` não andou; o ponteiro apenas avança.
  - **Merge commit (3-way)**: histórico divergiu; cria um commit com dois pais.
- **Conflito**: as duas branches alteraram as mesmas linhas; o Git marca `<<<<<<<`, `=======`, `>>>>>>>` e você resolve manualmente (aula 4).
- `git merge --no-ff` força um merge commit mesmo quando seria fast-forward.

## Exemplo
```bash
git switch -c feature/filtro-tarefas
echo "def filtrar(): pass" > filtro.py
git add filtro.py
git commit -m "Cria esqueleto do filtro de tarefas"

git switch main
git merge feature/filtro-tarefas        # fast-forward
git branch -d feature/filtro-tarefas

# Divergência
git switch -c feature/b
echo "b" > b.txt && git add b.txt && git commit -m "Adiciona b"
git switch main
echo "c" > c.txt && git add c.txt && git commit -m "Adiciona c"
git merge feature/b -m "Integra feature/b"   # merge commit
git log --oneline --graph --all
```

## Exercício
1. Crie duas branches a partir de `main`, com um commit em cada, e integre as duas.
2. Gere um merge fast-forward e outro com `--no-ff` e compare no `git log --graph`.
3. Apague as branches já integradas.

## Checklist
- [ ] Crio e troco de branch com `switch`
- [ ] Diferencio fast-forward de merge commit
- [ ] Mantenho `main` estável
