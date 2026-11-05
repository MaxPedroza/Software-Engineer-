# Aula 3 — Serverless e funções

**Duração:** ~20 min · **Módulo 19**

## Objetivo
Entender o modelo serverless (FaaS) e escrever uma função orientada a eventos.

## Teoria
- **Serverless**: você não gerencia servidores; escala automaticamente (inclusive a zero) e paga por execução.
- **FaaS** (AWS Lambda, Cloud Functions, Azure Functions): função disparada por eventos — HTTP (API Gateway), fila, upload em bucket, agendamento.
- **Vantagens**: sem operação de infra, escala elástica, custo proporcional ao uso.
- **Limites**: **cold start** (latência na primeira chamada), tempo máximo de execução (Lambda: 15 min), sem estado local persistente, risco de *vendor lock-in*, difícil depurar localmente.
- Funções devem ser **stateless** e **idempotentes** (eventos podem ser entregues mais de uma vez).
- Inicialize conexões fora do handler para reaproveitar entre invocações.
- Bom para: tarefas assíncronas, webhooks, ETL leve. Ruim para: cargas constantes e pesadas (VMs/containers saem mais baratos).

## Exemplo: AWS Lambda em Python
```python
import json, os
import boto3

s3 = boto3.client("s3")          # fora do handler: reutilizado
BUCKET = os.environ["BUCKET"]

def handler(event, context):
    corpo = json.loads(event.get("body") or "{}")
    nome = corpo.get("nome", "mundo")
    s3.put_object(Bucket=BUCKET, Key=f"saudacoes/{nome}.txt",
                  Body=f"Olá, {nome}!".encode())
    return {
        "statusCode": 200,
        "headers": {"Content-Type": "application/json"},
        "body": json.dumps({"mensagem": f"Olá, {nome}!"}),
    }
```
Teste local:
```python
print(handler({"body": '{"nome": "Ana"}'}, None))  # requer BUCKET e credenciais
```

## Exercício
1. Implemente uma função acionada por upload de imagem que grava o tamanho do arquivo em log. Torne-a idempotente.
2. Calcule o custo mensal de 5 milhões de invocações de 200 ms com 256 MB vs. uma VM fixa (use a calculadora do provedor).

## Checklist
- [ ] Explico FaaS e cold start
- [ ] Escrevo handlers stateless e idempotentes
- [ ] Sei quando serverless não compensa
