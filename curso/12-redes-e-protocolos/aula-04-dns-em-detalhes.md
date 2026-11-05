# Aula 4 — DNS em detalhes

**Duração:** ~25 min · **Módulo 12**

## Objetivo
Entender a resolução de nomes, os tipos de registro e o cache com TTL.

## Teoria
O **DNS** traduz nomes em dados (normalmente IPs), como uma agenda distribuída e hierárquica.

### Resolução
1. A aplicação consulta o **resolvedor recursivo** (ISP, 1.1.1.1, 8.8.8.8), que verifica o cache.
2. Sem cache: pergunta a um **servidor raiz** (`.`) → servidor do **TLD** (`.com`) → **servidor autoritativo** do domínio.
3. A resposta volta e é guardada no cache pelo tempo do **TTL**.

### Registros comuns
| Tipo | Função |
|------|--------|
| A / AAAA | Nome → IPv4 / IPv6 |
| CNAME | Alias para outro nome |
| MX | Servidores de e-mail |
| TXT | Texto (SPF, DKIM, verificação de domínio) |
| NS | Servidores autoritativos |
| PTR | IP → nome (reverso) |

Propagação lenta de mudanças vem dos TTLs altos em caches. Antes de migrar um serviço, reduza o TTL. DNS comum é sem criptografia; existem DoH/DoT.

## Exemplo
```bash
dig example.com A +noall +answer
dig example.com MX +short
dig @1.1.1.1 example.com AAAA
dig +trace example.com        # mostra raiz → TLD → autoritativo
dig -x 8.8.8.8 +short         # PTR
dig example.com NS +short
```
Saída típica de `+answer`: `example.com. 3600 IN A 93.184.216.34` (3600 = TTL em segundos).

## Exercício
1. Use `dig +trace` e liste os servidores que responderam em cada nível.
2. Rode `dig` duas vezes no mesmo nome e observe o TTL decrescer (cache).
3. Descubra os servidores MX de um domínio de sua escolha.
4. Teste local: adicione `127.0.0.1 app.local` em `/etc/hosts` e `curl app.local`.

## Checklist
- [ ] Descrevo a cadeia de resolução
- [ ] Conheço A, CNAME, MX, TXT, NS
- [ ] Uso `dig` e entendo TTL
