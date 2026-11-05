# Aula 2 — Escalabilidade horizontal e vertical

**Duração:** ~20 min · **Módulo 17**

## Objetivo
Escolher entre escalar verticalmente ou horizontalmente e projetar serviços que escalam.

## Teoria
- **Vertical (scale up)**: máquina maior (mais CPU/RAM). Simples, mas tem teto e é ponto único de falha.
- **Horizontal (scale out)**: mais instâncias atrás de um **load balancer**. Exige serviços **stateless**.

### Load balancing
- Algoritmos: round-robin, least connections, hash consistente (afinidade).
- L4 (TCP) é mais rápido; L7 (HTTP) permite roteamento por path/header.
- **Health checks** removem instâncias doentes do pool.

### Stateless
Estado de sessão sai do processo e vai para Redis ou banco; assim qualquer instância atende qualquer requisição. Cargas pesadas e lentas vão para filas e workers.

### Gargalos típicos
Banco de dados costuma ser o primeiro: use réplicas de leitura, cache e depois sharding (aula 5).

## Exemplo: Nginx como load balancer
```nginx
upstream api {
    least_conn;
    server api1:8000 max_fails=3 fail_timeout=10s;
    server api2:8000 max_fails=3 fail_timeout=10s;
    server api3:8000 backup;
}

server {
    listen 80;
    location / {
        proxy_pass http://api;
        proxy_next_upstream error timeout http_502;
    }
}
```

## Exercício
1. Seu serviço guarda o carrinho em memória local. Descreva o que quebra com 3 instâncias e como corrigir.
2. Calcule: cada instância suporta 500 QPS e o pico é 4.000 QPS. Quantas instâncias com margem de 30% e tolerância a perder 1?

## Checklist
- [ ] Diferencio scale up de scale out
- [ ] Sei por que stateless importa
- [ ] Configuro um load balancer básico
