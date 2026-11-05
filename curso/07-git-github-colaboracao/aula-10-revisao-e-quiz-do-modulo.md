# Aula 10 — Revisão e quiz do módulo

**Duração:** ~20 min · **Módulo 7**

## Resumo
- VCS guarda histórico, permite trabalho paralelo e colaboração; Git é distribuído; GitHub é uma plataforma.
- Ciclo básico: working directory → `add` (staging) → `commit` (repositório).
- Branches são ponteiros baratos; merge pode ser fast-forward ou merge commit.
- Rebase gera histórico linear (nunca em commits públicos); cherry-pick copia commits; `reflog` recupera erros.
- `origin` = seu repositório remoto; `upstream` = original em um fork; `fetch` baixa, `pull` baixa e integra.
- PR pequeno, bem descrito, revisado com respeito e CI verde.
- Fluxos: trunk-based/GitHub Flow (integração frequente) vs GitFlow (releases planejados).
- Issues + Conventional Commits + `Closes #n` mantêm rastreabilidade.
- Open source: leia CONTRIBUTING e a licença; comece pequeno.

## Quiz (responda sem consultar)
1. Qual a diferença entre Git e GitHub?
2. Quais são as três áreas do Git?
3. O que `git diff --staged` mostra?
4. O que é um merge fast-forward?
5. Por que não se deve fazer rebase de commits já publicados?
6. Para que serve o `git cherry-pick`?
7. Qual a diferença entre `git fetch` e `git pull`?
8. O que é um fork e o que é o remoto `upstream`?
9. Cite duas características de um bom Pull Request.
10. Escreva uma mensagem de commit em Conventional Commits para a correção de um bug no login.

## Gabarito resumido
1. Git: ferramenta de versionamento; GitHub: plataforma de hospedagem/colaboração · 2. Working directory, staging area, repositório · 3. Diferenças entre o stage e o último commit · 4. A branch de destino apenas avança o ponteiro, sem merge commit · 5. Reescreve hashes e quebra o histórico dos colegas · 6. Aplicar um commit específico na branch atual · 7. `fetch` só baixa; `pull` baixa e integra (merge/rebase) · 8. Cópia do repositório na sua conta; `upstream` aponta para o original · 9. Pequeno/focado, descrição clara, testes, CI verde, issue ligada · 10. Ex.: `fix(auth): corrige erro de login com e-mail em maiúsculas`

## Entregável do módulo
**Repositório no GitHub** com o projeto contínuo, contendo: histórico limpo (commits no padrão Conventional Commits), ao menos 3 branches de funcionalidade integradas via **PRs revisados**, **issues** organizadas com labels e um quadro de **Project**, além de `README.md`, `.gitignore` e `LICENSE`.

## Checklist final
- [ ] Acertei 8 ou mais questões
- [ ] Publiquei o repositório com PRs e issues
- [ ] Pronto para o próximo módulo
