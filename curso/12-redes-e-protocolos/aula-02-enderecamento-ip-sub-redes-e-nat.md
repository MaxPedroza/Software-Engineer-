# Aula 2 — Endereçamento IP, sub-redes e NAT

**Duração:** ~25 min · **Módulo 12**

## Objetivo
Ler notação CIDR, calcular sub-redes e entender NAT.

## Teoria
- **IPv4**: 32 bits (ex.: `192.168.1.10`). **IPv6**: 128 bits (`2001:db8::1`).
- **CIDR**: `192.168.1.0/24` — 24 bits de rede, 8 de host → 2⁸ = 256 endereços (254 utilizáveis: o primeiro é a rede, o último o broadcast).
- **Máscara**: `/24` = `255.255.255.0`.
- **Faixas privadas** (RFC 1918): `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`. `127.0.0.0/8` é loopback.
- **Gateway**: roteador que leva pacotes para fora da sub-rede.
- **NAT**: o roteador troca o IP privado de origem pelo IP público, mantendo uma tabela (IP:porta) para devolver as respostas. Economiza IPv4, mas dificulta conexões de entrada (exige *port forwarding*).
- **DHCP** distribui IPs automaticamente.

### Dividindo sub-redes
`10.0.0.0/24` em duas: `10.0.0.0/25` (hosts .1–.126) e `10.0.0.128/25` (.129–.254). Cada bit a mais no prefixo divide o bloco ao meio.

## Exemplo
```python
import ipaddress
rede = ipaddress.ip_network("192.168.10.0/24")
print(rede.netmask, rede.num_addresses)         # 255.255.255.0 256
print(list(rede.subnets(new_prefix=26)))         # 4 sub-redes
print(ipaddress.ip_address("192.168.10.77") in rede)  # True
```
```bash
ip route          # rota padrão (gateway)
curl ifconfig.me  # IP público visto de fora (após NAT)
```

## Exercício
1. Quantos hosts utilizáveis tem `/27`? E `/20`?
2. Divida `172.16.0.0/16` em 4 sub-redes iguais e liste os blocos.
3. Compare seu IP local com o IP público e explique a diferença.

## Checklist
- [ ] Leio notação CIDR
- [ ] Calculo sub-redes e hosts
- [ ] Explico NAT e IPs privados
