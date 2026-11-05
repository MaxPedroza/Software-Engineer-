# Aula 4 — Criptografia: hash, simétrica, assimétrica e assinaturas

**Duração:** ~25 min · **Módulo 20**

## Objetivo
Escolher a primitiva criptográfica correta para cada necessidade.

## Teoria
| Primitiva | Uso | Exemplos |
|-----------|-----|----------|
| Hash | Integridade, impressão digital (sem chave, irreversível) | SHA-256, SHA-3 |
| Simétrica | Cifrar dados com a mesma chave | AES-GCM, ChaCha20-Poly1305 |
| Assimétrica | Troca de chaves, cifrar com chave pública | RSA-OAEP, ECDH, X25519 |
| Assinatura | Autenticidade + integridade | Ed25519, ECDSA, RSA-PSS |

- **Regra de ouro:** nunca invente seu próprio algoritmo; use bibliotecas consagradas.
- MD5 e SHA-1 estão quebrados para segurança. Use cifras **autenticadas** (AEAD) como AES-GCM.
- Nunca reutilize o *nonce* com a mesma chave.
- **TLS** combina tudo: assimétrica para negociar, simétrica para o tráfego, certificados assinados.

## Exemplos (Python, biblioteca `cryptography`)
```python
import hashlib, os
from cryptography.hazmat.primitives.ciphers.aead import AESGCM
from cryptography.hazmat.primitives.asymmetric.ed25519 import Ed25519PrivateKey

print(hashlib.sha256(b"ola").hexdigest())

# Simétrica autenticada
chave = AESGCM.generate_key(bit_length=256)
nonce = os.urandom(12)
cifrado = AESGCM(chave).encrypt(nonce, b"segredo", b"contexto")
assert AESGCM(chave).decrypt(nonce, cifrado, b"contexto") == b"segredo"

# Assinatura
priv = Ed25519PrivateKey.generate()
sig = priv.sign(b"mensagem")
priv.public_key().verify(sig, b"mensagem")  # lança exceção se inválida
```

## Exercício
1. Calcule o SHA-256 de um arquivo, altere 1 byte e compare os hashes.
2. Altere o `cifrado` em 1 byte e tente decifrar. O que acontece e por quê?

## Checklist
- [ ] Diferencio hash, cifra e assinatura
- [ ] Uso AEAD e nonces únicos
- [ ] Não implemento criptografia própria
