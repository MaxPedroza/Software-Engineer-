# Aula 6 — Pull Requests e code review

**Duração:** ~25 min · **Módulo 7**

## Objetivo
Propor mudanças via Pull Request e conduzir/receber revisões de qualidade.

## Teoria
- **Pull Request (PR)**: pedido para integrar uma branch em outra, com discussão, revisão e checagens automáticas (CI).
- **PR bom**: pequeno e focado (idealmente < 400 linhas), título claro, descrição com **o quê**, **por quê**, como testar e issue relacionada (`Closes #12`). Use *Draft PR* para trabalho em andamento.
- **Revisão**: o revisor avalia correção, legibilidade, testes, segurança e desempenho. Estados: *Comment*, *Approve*, *Request changes*.
- **Boas práticas do revisor**: critique o código, não a pessoa; faça perguntas; separe o obrigatório do "nit"; elogie o que está bom.
- **Boas práticas do autor**: autorrevise antes; responda a todos os comentários; novos commits (ou fixup) para os ajustes.
- Formas de integrar: **Merge commit**, **Squash and merge** (um commit limpo) e **Rebase and merge**.
- **Proteção de branch**: exige aprovações e CI verde antes do merge.

## Exemplo
```bash
git switch -c feature/ordenar-tarefas
# ... commits ...
git push -u origin feature/ordenar-tarefas

# Com a GitHub CLI
gh pr create --title "Adiciona ordenação de tarefas" \
  --body "Ordena por prioridade e data.\n\nCloses #12\n\nComo testar: pytest tests/test_ordenacao.py"
gh pr checks
gh pr view --web

# Revisor
gh pr checkout 15
gh pr review 15 --approve --body "LGTM, ótimos testes!"

# Ajustes após o review
git commit -am "Trata lista vazia na ordenação"
git push
gh pr merge 15 --squash --delete-branch
```

## Exercício
1. Abra um PR do seu projeto com descrição completa (o quê, por quê, como testar).
2. Peça a um colega (ou use outra conta) para deixar 3 comentários e responda a todos.
3. Escreva um comentário construtivo para o trecho: `if x == True:`.

## Checklist
- [ ] Abro PRs pequenos e bem descritos
- [ ] Faço revisão respeitosa e objetiva
- [ ] Sei escolher entre merge, squash e rebase
