# Aula 6 — Portfólio, GitHub e currículo

**Duração:** ~25 min · **Módulo 23**

## Objetivo
Montar um currículo, um perfil de GitHub e um portfólio que comprovem suas habilidades.

## Teoria
- **Currículo**: 1 página (até 2 para sêniores), foco em **resultados mensuráveis**, sem foto/dados sensíveis desnecessários, compatível com ATS (texto simples, sem tabelas complexas).
- Fórmula de bullet: **verbo de ação + o que fez + resultado**.
- **GitHub**: README de perfil, 3–6 repositórios fixados (pinned), commits claros, issues e PRs.
- **Portfólio**: poucos projetos, bem explicados e *rodando* (demo online).

### Template de currículo
```text
NOME SOBRENOME — Engenheiro(a) de Software
Cidade · email · linkedin.com/in/... · github.com/...

RESUMO (2 linhas)
Dev backend com foco em APIs Python e cloud. Entrego sistemas testados e observáveis.

EXPERIÊNCIA / PROJETOS
Projeto Tarefas (2025) — github.com/.../tarefas
- Reduzi o tempo de resposta da API em 40% com índices e cache (p95: 800ms → 480ms)
- Automatizei testes e deploy com GitHub Actions (cobertura de 85%)

HABILIDADES: Python, SQL, Docker, AWS, Git
FORMAÇÃO / CERTIFICAÇÕES
```

### Template de README de portfólio
```markdown
# Nome do Projeto
Uma frase: o problema que resolve. [Demo](url) · [Vídeo](url)
![screenshot](docs/tela.png)
## Funcionalidades
## Stack e arquitetura (diagrama)
## Como rodar
`docker compose up` e acesse http://localhost:8000
## Testes e CI
## Decisões (ADRs) e aprendizados
```

## Exercício
1. Escreva seu currículo com o template; cada bullet deve ter um número.
2. Crie o README de perfil do GitHub e fixe os melhores repositórios.
3. Reescreva o README do projeto contínuo com o template e peça revisão a um colega.

## Checklist
- [ ] Currículo de 1 página com resultados mensuráveis
- [ ] GitHub organizado com pinned repos
- [ ] Projeto com README profissional e demo
