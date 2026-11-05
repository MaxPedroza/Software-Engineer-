# Aula 6 — TLS/HTTPS e certificados

**Duração:** ~25 min · **Módulo 12**

## Objetivo
Entender como o TLS garante confidencialidade, integridade e autenticação, e gerar um certificado local.

## Teoria
HTTPS = HTTP sobre **TLS**. Garante:
- **Confidencialidade** (criptografia simétrica da sessão);
- **Integridade** (detecta adulteração);
- **Autenticidade** do servidor (certificado).

### Handshake (TLS 1.3, simplificado)
1. `ClientHello`: versões, cifras, chave pública efêmera (ECDHE) e SNI (nome do host).
2. `ServerHello` + certificado + assinatura.
3. O cliente valida o certificado; ambos derivam a **chave de sessão** e passam a usar criptografia simétrica (AES-GCM/ChaCha20).

### Certificados e cadeia de confiança
O certificado X.509 liga um nome de domínio a uma chave pública, assinado por uma **CA**. O cliente valida a cadeia (servidor → intermediária → raiz presente no sistema), a validade e se o nome confere (SAN). **Let's Encrypt** emite gratuitamente via ACME. Para desenvolvimento use certificado autoassinado ou **mkcert**. Nunca versione a chave privada.

## Exemplo
```bash
# Certificado autoassinado para desenvolvimento
openssl req -x509 -newkey rsa:2048 -nodes -days 365 \
  -keyout local.key -out local.crt -subj "/CN=localhost" \
  -addext "subjectAltName=DNS:localhost"

# Inspecionar o certificado de um site
openssl s_client -connect example.com:443 -servername example.com </dev/null \
  | openssl x509 -noout -subject -issuer -dates

curl -v https://example.com 2>&1 | grep -E 'TLS|subject|issuer'
curl --cacert local.crt https://localhost:8443
```

## Exercício
1. Gere um certificado local e consulte-o com `openssl x509 -in local.crt -text -noout`.
2. Acesse-o com `curl` sem `--cacert`. Qual o erro e por quê?
3. Descubra emissor e validade do certificado de um site.

## Checklist
- [ ] Explico as 3 garantias do TLS
- [ ] Entendo a cadeia de certificados
- [ ] Gero e inspeciono certificados com openssl
