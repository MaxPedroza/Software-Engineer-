# Aula 3 — Docker Compose e redes de containers

**Duração:** ~20 min · **Módulo 18**

## Objetivo
Orquestrar vários containers locais (app, banco, cache) com Docker Compose.

## Teoria
- **Compose** descreve serviços, redes e volumes em um `compose.yaml`.
- Containers na mesma rede Compose se acham pelo **nome do serviço** (DNS interno): a API usa `db:5432`, não `localhost`.
- `ports` publica porta no host; serviços internos (banco) não precisam publicar.
- **Volumes** persistem dados além do ciclo de vida do container.
- `depends_on` com `condition: service_healthy` espera o healthcheck.
- Configuração via variáveis de ambiente/`.env`; nunca commite segredos.

## Exemplo
```yaml
services:
  api:
    build: .
    ports: ["8000:8000"]
    environment:
      DATABASE_URL: postgresql://app:${DB_PASSWORD}@db:5432/appdb
      REDIS_URL: redis://cache:6379
    depends_on:
      db:
        condition: service_healthy
      cache:
        condition: service_started
    networks: [backend]

  db:
    image: postgres:16-alpine
    environment:
      POSTGRES_USER: app
      POSTGRES_PASSWORD: ${DB_PASSWORD}
      POSTGRES_DB: appdb
    volumes: [dados:/var/lib/postgresql/data]
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U app -d appdb"]
      interval: 5s
      retries: 5
    networks: [backend]

  cache:
    image: redis:7-alpine
    networks: [backend]

volumes:
  dados:
networks:
  backend:
```
```bash
echo "DB_PASSWORD=troque-me" > .env
docker compose up -d --build
docker compose ps
docker compose logs -f api
docker compose down        # -v apaga os volumes
```

## Exercício
1. Suba a stack, crie dados, rode `docker compose down` e `up` de novo: os dados persistem? Teste com `down -v`.
2. Adicione um serviço `worker` que consome da mesma rede e acessa o Redis.

## Checklist
- [ ] Escrevo um compose com app, banco e cache
- [ ] Sei que serviços se resolvem por nome
- [ ] Uso volumes e healthchecks
