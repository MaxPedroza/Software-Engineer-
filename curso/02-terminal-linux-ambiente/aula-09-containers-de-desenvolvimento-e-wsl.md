# Aula 9 — Containers de desenvolvimento e WSL

**Duração:** ~25 min · **Módulo 2**

## Objetivo
Entender containers e usar WSL ou Dev Containers para ter ambientes idênticos em qualquer máquina.

## Teoria
- Problema clássico: "na minha máquina funciona". Solução: padronizar o ambiente.
- **WSL 2** (Windows Subsystem for Linux): roda um kernel Linux real no Windows. Instalação: `wsl --install` (PowerShell como admin). Arquivos do projeto devem ficar no sistema Linux (`~/projetos`), não em `/mnt/c`, por desempenho.
- **Container**: processo isolado que compartilha o kernel do host, empacotando app + dependências. Mais leve que uma VM (que virtualiza um SO completo).
- **Imagem** (receita imutável) → **container** (instância em execução). Definida por um `Dockerfile`.
- **Dev Container**: pasta `.devcontainer/` que descreve o ambiente; o VS Code reabre o projeto dentro do container (`Dev Containers: Reopen in Container`). Codespaces usa o mesmo padrão.

## Exemplo
`.devcontainer/devcontainer.json`:
```json
{
  "name": "meu-projeto",
  "image": "mcr.microsoft.com/devcontainers/python:3.12",
  "postCreateCommand": "bash setup.sh",
  "customizations": {
    "vscode": { "extensions": ["ms-python.python"] }
  }
}
```
Comandos Docker básicos:
```bash
docker run --rm -it python:3.12-slim python -c "print('olá do container')"
docker ps            # containers ativos
docker images        # imagens locais
```

## Exercício
1. Verifique sua versão: `wsl -l -v` (Windows) ou `docker --version`.
2. Rode o comando `docker run` acima e explique o que `--rm` e `-it` fazem.
3. Crie `.devcontainer/devcontainer.json` para o projeto contínuo, chamando o `setup.sh`.

## Checklist
- [ ] Diferencio container de VM
- [ ] Sei o que é imagem, container e Dockerfile
- [ ] Criei um `devcontainer.json`
