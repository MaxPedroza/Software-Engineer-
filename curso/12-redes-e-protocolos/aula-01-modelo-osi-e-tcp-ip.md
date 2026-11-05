# Aula 1 — Modelo OSI e TCP/IP

**Duração:** ~20 min · **Módulo 12**

## Objetivo
Entender a divisão em camadas e o caminho de um dado entre cliente e servidor.

## Teoria
Camadas isolam responsabilidades: cada uma usa a de baixo e oferece serviço à de cima.

| OSI | TCP/IP | Exemplos | Unidade |
|-----|--------|----------|---------|
| 7 Aplicação, 6 Apresentação, 5 Sessão | Aplicação | HTTP, DNS, TLS, SMTP | Mensagem |
| 4 Transporte | Transporte | TCP, UDP | Segmento/datagrama |
| 3 Rede | Internet | IP, ICMP | Pacote |
| 2 Enlace | Enlace | Ethernet, Wi-Fi, MAC | Quadro |
| 1 Física | — | Cabo, rádio | Bits |

### Encapsulamento
Ao enviar, cada camada adiciona seu **cabeçalho**: dados HTTP → segmento TCP (portas) → pacote IP (endereços IP) → quadro Ethernet (endereços MAC). O receptor faz o caminho inverso (desencapsulamento).

- **IP** identifica máquinas entre redes; **MAC** identifica a interface na rede local (via ARP).
- **Porta** identifica o processo/serviço (80 HTTP, 443 HTTPS, 22 SSH, 53 DNS).
- O modelo OSI é de referência didática; a internet real usa TCP/IP.

## Exemplo
```bash
ip addr                # camada 2/3: MAC e IP locais
ip neigh               # tabela ARP
ss -tn                 # conexões TCP (camada 4)
curl -v http://example.com 2>&1 | head -20   # camada 7 sobre TCP
```

## Exercício
1. Em que camada atuam: um switch, um roteador, o TCP, o HTTP, um cabo?
2. Rode `ss -tn` durante um `curl` e identifique IP e porta de origem e destino.
3. Desenhe o encapsulamento de uma requisição HTTP.

## Checklist
- [ ] Nomeio as camadas e exemplos de cada uma
- [ ] Explico encapsulamento
- [ ] Diferencio MAC, IP e porta
