# Aula 9 — CDN e ferramentas de diagnóstico (curl, dig, traceroute, Wireshark)

**Duração:** ~25 min · **Módulo 12**

## Objetivo
Entender CDNs e diagnosticar problemas de rede com as ferramentas certas.

## Teoria
**CDN** (Cloudflare, Fastly, CloudFront): rede de servidores de borda (*edge*) que guarda cópias de conteúdo perto do usuário. Reduz latência e carga na origem, absorve picos e ataques DDoS. Controle por `Cache-Control` (`max-age`, `s-maxage`, `no-store`) e invalidação (*purge*). Cabeçalhos úteis: `Age`, `X-Cache`, `CF-Cache-Status` (HIT/MISS).

### Diagnóstico: de baixo para cima
| Pergunta | Ferramenta |
|----------|-----------|
| Host responde? | `ping` |
| Por onde o pacote passa? | `traceroute` / `mtr` |
| O nome resolve? | `dig` |
| A porta está aberta? | `nc -vz host 443`, `ss -tlnp` |
| O HTTP/TLS está correto? | `curl -v`, `openssl s_client` |
| O que trafega de fato? | `tcpdump`, **Wireshark** |

## Exemplo
```bash
ping -c 3 example.com
traceroute example.com
dig example.com +short
nc -vz example.com 443
curl -sI https://example.com | grep -iE 'cache|age|server'
curl -w 'dns:%{time_namelookup} tcp:%{time_connect} tls:%{time_appconnect} ttfb:%{time_starttransfer} total:%{time_total}\n' \
     -o /dev/null -s https://example.com
sudo tcpdump -i any -n -w captura.pcap 'port 443'   # abra no Wireshark
```
No Wireshark, filtros úteis: `dns`, `tcp.flags.syn==1`, `tls.handshake`, `http`, `ip.addr==1.2.3.4`.

## Exercício
1. Meça dns/tcp/tls/ttfb de um site e identifique a etapa mais lenta.
2. Capture uma requisição a `example.com` e localize o DNS, o handshake TCP e o `ClientHello` do TLS.
3. Verifique se um site usa CDN pelos cabeçalhos.

## Checklist
- [ ] Explico o que a CDN faz e como o cache é controlado
- [ ] Uso curl, dig, traceroute para diagnosticar
- [ ] Sei filtrar capturas no Wireshark
