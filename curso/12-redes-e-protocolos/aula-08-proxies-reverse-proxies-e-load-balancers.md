# Aula 8 — Proxies, reverse proxies e load balancers

**Duração:** ~25 min · **Módulo 12**

## Objetivo
Configurar um Nginx como reverse proxy e entender balanceamento de carga.

## Teoria
- **Forward proxy**: fica na frente dos *clientes* (filtragem, anonimato, cache corporativo).
- **Reverse proxy**: fica na frente dos *servidores*; o cliente só conhece o proxy. Funções: terminação TLS, roteamento por host/caminho, compressão, cache, rate limiting, ocultar a topologia.
- **Load balancer**: distribui requisições entre várias instâncias. Camada 4 (TCP) ou 7 (HTTP). Algoritmos: *round-robin*, *least connections*, *ip hash* (afinidade).
- **Health checks** retiram instâncias com falha da rotação.
- Cabeçalhos como `X-Forwarded-For` e `X-Forwarded-Proto` preservam o IP e o protocolo originais.

## Exemplo (nginx.conf)
```nginx
upstream api {
    least_conn;
    server 127.0.0.1:8001;
    server 127.0.0.1:8002;
}

server {
    listen 443 ssl;
    server_name localhost;
    ssl_certificate     /etc/nginx/certs/local.crt;
    ssl_certificate_key /etc/nginx/certs/local.key;

    location /api/ {
        proxy_pass http://api/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}

server {
    listen 80;
    return 301 https://$host$request_uri;
}
```
```bash
nginx -t && nginx -s reload
curl -k https://localhost/api/saude
```

## Exercício
1. Suba duas instâncias da API (portas 8001 e 8002) e o Nginx; verifique o balanceamento exibindo o ID da instância.
2. Derrube uma instância e observe o comportamento.
3. Quando preferir balanceamento L4 a L7?

## Checklist
- [ ] Diferencio forward e reverse proxy
- [ ] Configuro `proxy_pass` e cabeçalhos `X-Forwarded-*`
- [ ] Conheço algoritmos de balanceamento
