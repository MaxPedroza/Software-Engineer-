# Aula 3 — TCP vs UDP

**Duração:** ~20 min · **Módulo 12**

## Objetivo
Escolher entre TCP e UDP e entender o handshake e o controle de fluxo.

## Teoria
| | TCP | UDP |
|--|-----|-----|
| Conexão | Orientado a conexão | Sem conexão |
| Entrega | Confiável, em ordem, com retransmissão | Melhor esforço, pode perder/duplicar/reordenar |
| Controle | Fluxo e congestionamento | Nenhum |
| Overhead | Maior (cabeçalho 20+ bytes) | Menor (8 bytes) |
| Usos | HTTP/1-2, SSH, bancos, e-mail | DNS, VoIP, jogos, streaming, QUIC/HTTP-3 |

### Handshake de 3 vias (TCP)
1. Cliente → `SYN`
2. Servidor → `SYN-ACK`
3. Cliente → `ACK`

O encerramento usa `FIN`/`ACK`. Perdas são detectadas por falta de ACK e geram retransmissão; a **janela deslizante** limita dados em trânsito. Isso custa latência (RTT), por isso o HTTP/3 usa UDP (QUIC) e implementa confiabilidade por conta própria.

## Exemplo
```python
# Servidor TCP mínimo
import socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.bind(("127.0.0.1", 9000)); s.listen()
c, _ = s.accept(); print(c.recv(1024)); c.sendall(b"ok")
```
```python
# Cliente UDP (não precisa de conexão; sem garantia de entrega)
import socket
u = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
u.sendto(b"ping", ("127.0.0.1", 9001))
```
```bash
nc -l 9000            # servidor TCP
nc -u -l 9001         # servidor UDP
sudo tcpdump -i lo -n 'tcp port 9000'   # observe SYN, SYN-ACK, ACK
```

## Exercício
1. Rode o servidor TCP e conecte com `nc 127.0.0.1 9000`; capture o handshake com `tcpdump`.
2. Envie datagramas UDP para uma porta sem ninguém ouvindo. O que acontece?
3. Por que DNS usa UDP na maioria das consultas?

## Checklist
- [ ] Diferencio TCP e UDP
- [ ] Descrevo o handshake de 3 vias
- [ ] Sei escolher o protocolo por caso de uso
