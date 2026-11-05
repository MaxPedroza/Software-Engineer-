# Aula 8 — Issues, Projects e boas mensagens de commit

**Duração:** ~20 min · **Módulo 7**

## Objetivo
Organizar o trabalho com Issues e Projects e escrever commits que contam uma boa história.

## Teoria
- **Issue**: unidade de trabalho rastreável (bug, tarefa, ideia). Bom issue: título claro, contexto, **passos para reproduzir**, comportamento esperado vs atual, critérios de aceite.
- **Labels** (`bug`, `enhancement`, `good first issue`), **assignees** e **milestones** organizam e priorizam.
- **GitHub Projects**: quadro (kanban) ou tabela com colunas como *Backlog → Em andamento → Em revisão → Feito*, ligando issues e PRs.
- **Fechar automaticamente**: `Closes #12` / `Fixes #12` na descrição do PR.
- **Boas mensagens de commit**:
  - Linha de resumo no **imperativo**, até ~50 caracteres: "Adiciona filtro por status".
  - Linha em branco e corpo explicando **por quê** (não só o quê), com linhas de ~72 caracteres.
  - Um commit = uma mudança lógica.
- **Conventional Commits**: `tipo(escopo): descrição` — `feat`, `fix`, `docs`, `refactor`, `test`, `chore`. Mudança incompatível: `feat!:` ou `BREAKING CHANGE:`. Permite gerar changelog e versões automaticamente.

## Exemplo
```bash
git commit -m "feat(tarefas): adiciona filtro por status" \
           -m "Permite listar apenas tarefas concluídas ou pendentes.
Usa dicionário para evitar varredura linear. Closes #12"

git commit -m "fix(api): trata prazo nulo ao ordenar"
git commit -m "docs: explica como rodar os testes"

gh issue create --title "Erro ao ordenar tarefas sem prazo" \
  --body "Passos: 1) criar tarefa sem prazo 2) ordenar. Esperado: vai ao fim. Atual: TypeError." \
  --label bug
gh issue list --label bug
```

## Exercício
1. Escreva uma issue de bug completa para o seu projeto.
2. Reescreva as mensagens ruins: "arrumei", "mudanças", "wip fix stuff".
3. Crie um Project com 4 colunas e três issues.

## Checklist
- [ ] Escrevo issues reproduzíveis
- [ ] Uso Conventional Commits
- [ ] Ligo PRs a issues com `Closes #n`
