# Aula 1 — Por que controle de versão

**Duração:** ~15 min · **Módulo 7**

## Objetivo
Entender os problemas que o controle de versão resolve e como o Git os resolve.

## Teoria
- **Controle de versão (VCS)** registra o histórico de mudanças: quem mudou, o quê, quando e por quê.
- Sem VCS: pastas `projeto_final_v2_REAL`, perda de trabalho, sobrescrita entre colegas, nenhuma forma de voltar atrás.
- Benefícios: **histórico e reversão**, **trabalho paralelo** (branches), **colaboração**, **auditoria** e **backup** distribuído.
- Gerações: local (RCS) → centralizado (SVN: um servidor único) → **distribuído** (Git, Mercurial: cada clone tem o histórico completo e funciona offline).
- **Git**: criado por Linus Torvalds em 2005 para o kernel Linux. Guarda *snapshots* do projeto, identificados por hashes SHA.
- **Git ≠ GitHub**: Git é a ferramenta local; GitHub (e GitLab, Bitbucket) são plataformas de hospedagem e colaboração.
- Três áreas: **working directory** → **staging area (index)** → **repositório** (commits).

## Exemplo
```bash
git --version
git config --global user.name "Seu Nome"
git config --global user.email "voce@exemplo.com"
git config --global init.defaultBranch main
git config --list --show-origin | head
```

## Exercício
1. Instale o Git e rode os comandos de configuração acima.
2. Liste três problemas que já teve (ou teria) ao trabalhar em equipe sem VCS.
3. Explique com suas palavras a diferença entre Git e GitHub e entre VCS centralizado e distribuído.

## Checklist
- [ ] Git instalado e configurado
- [ ] Sei diferenciar Git de GitHub
- [ ] Conheço as três áreas do Git
