# Aula 9 — Como a internet funciona (visão geral)

**Duração:** ~20 min · **Módulo 1**

## Objetivo
Entender o caminho de uma requisição entre seu navegador e um servidor.

## Teoria
- **Cliente** (navegador/app) pede; **servidor** responde.
- **Endereço IP**: identifica um dispositivo na rede (IPv4: `192.168.0.1`; IPv6 mais longo).
- **DNS**: "lista telefônica" que traduz `exemplo.com` em um IP.
- **Pacotes**: os dados são divididos em pacotes que viajam por vários roteadores e são remontados no destino.
- **Protocolos**: regras de comunicação. **TCP/IP** (entrega confiável), **HTTP/HTTPS** (web), **TLS** (criptografia).
- **Portas**: identificam serviços na máquina (80 = HTTP, 443 = HTTPS, 22 = SSH).

### O que acontece ao abrir `https://exemplo.com`
1. O navegador consulta o **DNS** e obtém o IP.
2. Abre uma conexão **TCP** com o servidor (porta 443).
3. Faz o **handshake TLS** (autentica e cria chave de criptografia).
4. Envia uma requisição **HTTP** (`GET /`).
5. O servidor processa (talvez consulta banco de dados) e responde com HTML/JSON.
6. O navegador renderiza e pede recursos extras (CSS, JS, imagens).

## Prática
```bash
nslookup exemplo.com          # ou: dig exemplo.com
curl -v https://example.com   # veja DNS, TLS e cabeçalhos HTTP
ping -c 3 example.com
```

## Exercício
Rode `curl -v https://example.com` e identifique: o IP conectado, a versão do TLS, o método HTTP e o código de status da resposta.

## Checklist
- [ ] Explico o papel de DNS, IP, TCP e HTTP
- [ ] Descrevo o caminho de uma requisição de ponta a ponta
- [ ] Sei usar curl para inspecionar uma requisição
