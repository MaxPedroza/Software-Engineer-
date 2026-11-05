# Aula 10 — Revisão e quiz do módulo

**Duração:** ~30 min · **Módulo 12**

## Resumo
- **Camadas**: aplicação, transporte, internet, enlace; dados são encapsulados a cada camada.
- **IP/CIDR/NAT**: prefixo define a rede; NAT traduz IPs privados em públicos.
- **TCP** é confiável (handshake de 3 vias); **UDP** é leve e sem garantias.
- **DNS** resolve nomes via raiz → TLD → autoritativo, com cache por TTL.
- **HTTP/2** multiplexa; **HTTP/3** usa QUIC sobre UDP.
- **TLS** dá confidencialidade, integridade e autenticidade via certificados.
- **WebSocket** (bidirecional) e **SSE** (servidor → cliente) para tempo real.
- **Reverse proxy/LB** distribuem carga e terminam TLS; **CDN** aproxima o conteúdo.

## Quiz
1. O que é encapsulamento?
2. Quantos hosts utilizáveis tem uma rede `/24`?
3. Para que serve o NAT?
4. Quais são os passos do handshake TCP?
5. Qual a diferença entre um registro A e um CNAME?
6. Que problema o HTTP/2 resolve em relação ao HTTP/1.1?
7. Por que o HTTP/3 usa UDP?
8. O que um certificado TLS comprova?
9. Quando usar SSE em vez de WebSocket?
10. Qual a função do cabeçalho `X-Forwarded-For`?

## Gabarito resumido
1. Cada camada adiciona seu cabeçalho aos dados da camada superior.
2. 254.
3. Compartilhar um IP público entre dispositivos com IPs privados.
4. SYN, SYN-ACK, ACK.
5. A aponta para um IP; CNAME é alias para outro nome.
6. Multiplexação de requisições numa só conexão (menos bloqueio e conexões).
7. QUIC evita o bloqueio de TCP e reduz o tempo de handshake.
8. Que a chave pública pertence ao domínio, atestado por uma CA confiável.
9. Quando o fluxo é só servidor → cliente e se quer reconexão automática sobre HTTP.
10. Informar o IP original do cliente após passar por proxies.

## Entregável do módulo
Relatório de captura de tráfego (pcap + texto) explicando uma requisição HTTPS de ponta a ponta: DNS, TCP, TLS e HTTP. Inclua o Nginx como reverse proxy com HTTPS local na frente da aplicação.

## Checklist final
- [ ] Quiz respondido sem consulta
- [ ] Nginx com HTTPS local funcionando
- [ ] Captura analisada no Wireshark
- [ ] Relatório escrito
