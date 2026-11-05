# Aula 1 — Princípios de segurança

**Duração:** ~20 min · **Módulo 20**

## Objetivo
Aplicar os princípios fundamentais de segurança ao projetar sistemas.

## Teoria
### Tríade CIA
- **Confidencialidade**: só quem deve acessa a informação (criptografia, controle de acesso).
- **Integridade**: dados não são alterados indevidamente (hashes, assinaturas, validações).
- **Disponibilidade**: o sistema responde quando necessário (redundância, rate limit, backups).

### Princípios de design
- **Menor privilégio**: cada usuário/serviço recebe só as permissões necessárias.
- **Defesa em profundidade**: várias camadas (rede, aplicação, dados); a falha de uma não expõe tudo.
- **Falhar de forma segura** (*fail closed*): na dúvida, negar.
- **Segurança por padrão** e **mínima superfície de ataque**.
- **Nunca confie em entrada do usuário**: valide, sanitize, escape.
- **Segregação de funções** e **auditoria** (logs de quem fez o quê).

### Segurança não é obscuridade
O sistema deve ser seguro mesmo que o atacante conheça o design; apenas chaves são secretas (princípio de Kerckhoffs).

## Exemplo: fail closed com menor privilégio
```python
PERMISSOES = {"admin": {"ler", "escrever", "apagar"}, "leitor": {"ler"}}

def autorizado(papel: str, acao: str) -> bool:
    return acao in PERMISSOES.get(papel, set())  # papel desconhecido => nega

def apagar_pedido(usuario, pedido_id):
    if not autorizado(usuario.papel, "apagar"):
        raise PermissionError("negado")
    ...
```

## Exercício
1. Classifique em C, I ou A: (a) vazamento de CPFs; (b) alteração de saldo; (c) ataque DDoS.
2. Liste 3 permissões excessivas comuns em um sistema (ex.: usuário de banco com DROP) e como reduzi-las.

## Checklist
- [ ] Explico CIA com exemplos
- [ ] Aplico menor privilégio e fail closed
- [ ] Entendo defesa em profundidade
