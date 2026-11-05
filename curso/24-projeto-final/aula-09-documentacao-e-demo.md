# Aula 9 — Documentação e demo

**Duração:** ~30 min · **Módulo 24 — Etapa 9**

## Objetivo
Documentar o projeto para que outra pessoa o rode, entenda e contribua, e gravar uma demo.

## Passo a passo
1. **README profissional** (template abaixo) com badges de CI e cobertura.
2. **Guia de contribuição** (`CONTRIBUTING.md`), `LICENSE` e `CHANGELOG.md`.
3. **Documentação da API**: publique o Swagger/Redoc.
4. **Runbook operacional**: como investigar incidentes, rodar migrations e fazer rollback.
5. **Teste do README**: peça a alguém para clonar e rodar seguindo só o texto.
6. **Roteiro da demo** (3–5 min): problema → jornada principal ao vivo → arquitetura → qualidade/CI → próximos passos.
7. **Grave** com ensaio prévio, áudio claro e dados de exemplo.

### Template de README
```markdown
# Tarefas — gerencie seu dia
[![CI](badge)](link) [![coverage](badge)](link)
[Demo](url) · [API Docs](url) · [Vídeo](url)
## Problema e solução
## Funcionalidades
## Arquitetura (diagrama + link para ADRs)
## Como rodar
git clone ... && cp .env.example .env && docker compose up
## Testes
make test
## Deploy e operação
## Roadmap e licença
```

### Roteiro da demo
```text
0:00 Problema e público · 0:30 Demo ao vivo da jornada · 2:30 Arquitetura
3:30 Testes, CI/CD e observabilidade · 4:30 Aprendizados e próximos passos
```

## Entregáveis
- README, CONTRIBUTING, LICENSE, CHANGELOG, runbook
- Vídeo de demo (3–5 min) com link no README

## Critérios de aceite
- [ ] Alguém externo roda o projeto em menos de 10 minutos
- [ ] Toda decisão importante tem ADR linkado
- [ ] A demo mostra o fluxo principal sem erros
