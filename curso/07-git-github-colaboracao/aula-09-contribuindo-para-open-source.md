# Aula 9 — Contribuindo para open source

**Duração:** ~20 min · **Módulo 7**

## Objetivo
Fazer sua primeira contribuição a um projeto open source de forma respeitosa e eficaz.

## Teoria
- **Open source**: código com licença que permite uso, estudo, modificação e distribuição (MIT, Apache-2.0, GPL). Sem licença, o código **não** é livre para reutilização.
- Arquivos importantes: `README.md`, `LICENSE`, **`CONTRIBUTING.md`** (como contribuir), **`CODE_OF_CONDUCT.md`** (convivência), `SECURITY.md`.
- Como começar: procure issues com labels `good first issue` e `help wanted`; contribuições também incluem documentação, traduções, testes e triagem de bugs.
- **Fluxo**: ler CONTRIBUTING → comentar na issue que vai trabalhar → fork → clonar → branch → mudança + testes → PR pequeno → responder ao review com paciência.
- Etiqueta: seja educado, pesquise antes de perguntar, siga o estilo do projeto, não abra PR enorme sem discutir antes. Mantenedores são, muitas vezes, voluntários.
- Alguns projetos exigem **DCO** (`git commit -s`) ou CLA.

## Exemplo
```bash
gh repo fork dono/projeto --clone
cd projeto
git remote -v                       # origin = fork, upstream = original
git switch -c docs/corrige-typo-readme

# edite o arquivo, rode os testes/linters do projeto
git commit -s -m "docs: corrige erro de digitação no README"
git push -u origin docs/corrige-typo-readme

gh pr create --repo dono/projeto \
  --title "docs: corrige erro de digitação no README" \
  --body "Corrige 'ambeinte' para 'ambiente'. Closes #34"

# Manter o fork atualizado
git fetch upstream
git switch main
git merge --ff-only upstream/main
```

## Exercício
1. Escolha um projeto e leia README, LICENSE e CONTRIBUTING; resuma as regras em 5 linhas.
2. Encontre 3 issues `good first issue` e escolha uma.
3. Faça uma contribuição pequena (ex.: documentação) e abra o PR.

## Checklist
- [ ] Sei ler a licença e o CONTRIBUTING de um projeto
- [ ] Encontro issues adequadas para iniciantes
- [ ] Abri (ou preparei) um PR em projeto externo
