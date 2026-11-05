# Aula 7 — Feature flags e gerenciamento de configuração

**Duração:** ~20 min · **Módulo 18**

## Objetivo
Separar deploy de release com feature flags e gerenciar configuração com segurança.

## Teoria
- **Feature flag**: condição em runtime que liga/desliga um comportamento sem novo deploy.
- Tipos: **release** (esconde recurso incompleto; permite *trunk-based development*), **experimento** (A/B), **operacional** (kill switch), **permissão**.
- **Rollout gradual** por percentual de usuários, usando hash do ID para resultado estável.
- Flags geram dívida: **remova** as antigas e dê dono e data de expiração.
- **Config (12-factor)**: configuração no ambiente, não no código; mesma imagem em todos os ambientes.
- **Segredos**: em gerenciador (Vault, AWS Secrets Manager, Kubernetes Secrets com criptografia), nunca no Git; rotacione.
- Valide a configuração na inicialização (falhe rápido).

## Exemplo
```python
import hashlib, os

FLAGS = {
    "novo_checkout": {"ativo": True, "percentual": 20},
    "modo_manutencao": {"ativo": False, "percentual": 100},
}

def habilitada(flag: str, user_id: str) -> bool:
    cfg = FLAGS.get(flag)
    if not cfg or not cfg["ativo"]:
        return False
    bucket = int(hashlib.sha256(f"{flag}:{user_id}".encode()).hexdigest(), 16) % 100
    return bucket < cfg["percentual"]

class Config:
    database_url = os.environ["DATABASE_URL"]       # falha se ausente
    log_level = os.getenv("LOG_LEVEL", "INFO")

if habilitada("novo_checkout", "user-42"):
    print("novo fluxo")
else:
    print("fluxo antigo")
```
ConfigMap/Secret no Kubernetes:
```yaml
apiVersion: v1
kind: ConfigMap
metadata: { name: api-config }
data:
  LOG_LEVEL: "INFO"
```

## Exercício
1. Verifique que ≈20% de 10.000 IDs ficam com a flag ligada e que o resultado é estável entre execuções.
2. Liste 3 flags do seu projeto, com tipo, dono e data de remoção.

## Checklist
- [ ] Diferencio deploy de release
- [ ] Implemento rollout por percentual
- [ ] Mantenho segredos fora do Git
