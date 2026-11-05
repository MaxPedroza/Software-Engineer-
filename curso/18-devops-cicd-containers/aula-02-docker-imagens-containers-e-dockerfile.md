# Aula 2 — Docker: imagens, containers e Dockerfile

**Duração:** ~25 min · **Módulo 18**

## Objetivo
Empacotar uma aplicação em uma imagem Docker enxuta e segura.

## Teoria
- **Container**: processo isolado (namespaces + cgroups) que compartilha o kernel do host; mais leve que VM.
- **Imagem**: modelo imutável em **camadas**; container é a imagem em execução.
- **Dockerfile**: receita de build. Cada instrução gera uma camada em cache — coloque o que muda menos primeiro (dependências antes do código).
- **Multi-stage build** reduz tamanho; **.dockerignore** evita enviar lixo ao build.
- Boas práticas: imagem base pequena com versão fixa, usuário não-root, sem segredos na imagem, uma responsabilidade por container.

## Exemplo
`Dockerfile`:
```dockerfile
FROM python:3.12-slim AS base
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .

FROM python:3.12-slim
WORKDIR /app
RUN useradd -m app
COPY --from=base /usr/local/lib/python3.12/site-packages /usr/local/lib/python3.12/site-packages
COPY --from=base /usr/local/bin /usr/local/bin
COPY --from=base /app .
USER app
EXPOSE 8000
HEALTHCHECK CMD python -c "import urllib.request as u; u.urlopen('http://localhost:8000/health')"
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```
`.dockerignore`:
```
.git
__pycache__
.env
```
Comandos:
```bash
docker build -t minha-api:1.0 .
docker run -d --name api -p 8000:8000 minha-api:1.0
docker logs -f api
docker exec -it api sh
docker stop api && docker rm api
```

## Exercício
1. Containerize a API do projeto e compare o tamanho da imagem com e sem multi-stage (`docker images`).
2. Altere só o código e rebuilde: quais camadas vieram do cache? Por quê?

## Checklist
- [ ] Diferencio imagem de container
- [ ] Escrevo Dockerfile com cache e multi-stage
- [ ] Rodo como não-root e uso .dockerignore
