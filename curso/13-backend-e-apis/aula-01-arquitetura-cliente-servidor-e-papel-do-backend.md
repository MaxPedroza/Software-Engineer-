# Aula 1 — Arquitetura cliente-servidor e papel do backend

**Duração:** ~20 min · **Módulo 13**

## Objetivo
Entender o papel do backend e como cliente e servidor se comunicam.

## Teoria
No modelo **cliente-servidor**, clientes (navegador, app móvel, outro serviço) enviam requisições e o servidor responde. O **backend** é responsável por:
- **Regras de negócio** e validação (nunca confie no cliente);
- **Persistência** (bancos, cache, arquivos);
- **Segurança**: autenticação, autorização, proteção de dados;
- **Integrações** com serviços externos, filas e e-mails;
- **Observabilidade**: logs, métricas, health checks.

### Camadas típicas
`Rota/Controller` (HTTP) → `Serviço` (regras) → `Repositório` (dados) → Banco. Separar camadas facilita testes e manutenção.

### Características
- **Sem estado (stateless)**: cada requisição traz o necessário (token), permitindo escalar horizontalmente.
- Contrato claro entre cliente e servidor (API).
- Configuração por variáveis de ambiente (12-factor).

## Exemplo (FastAPI mínimo)
```python
# pip install fastapi uvicorn
from fastapi import FastAPI

app = FastAPI(title="API de Tarefas")

@app.get("/saude")
def saude():
    return {"status": "ok"}
```
```bash
uvicorn main:app --reload --port 8000
curl -i localhost:8000/saude
```

## Exercício
1. Suba a API e consulte `/saude` com `curl -i`; identifique status, cabeçalhos e corpo.
2. Desenhe o fluxo: navegador → Nginx → API → PostgreSQL, indicando onde ocorrem validação e autorização.
3. Por que a validação só no frontend é insuficiente?

## Checklist
- [ ] Explico as responsabilidades do backend
- [ ] Conheço as camadas de uma API
- [ ] Subi uma API FastAPI local
