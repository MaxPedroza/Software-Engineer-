# Aula 1 — Lógica proposicional e álgebra booleana

**Duração:** ~25 min · **Módulo 4**

## Objetivo
Entender proposições, conectivos lógicos e as leis da álgebra booleana.

## Teoria
- **Proposição**: afirmação que é verdadeira (V/1) ou falsa (F/0). "2 > 1" é proposição; "feche a porta" não é.
- Conectivos:

| Conectivo | Símbolo | Python | Significado |
|-----------|---------|--------|-------------|
| Negação | ¬p | `not p` | inverte |
| Conjunção | p ∧ q | `p and q` | verdadeira se ambas V |
| Disjunção | p ∨ q | `p or q` | verdadeira se ao menos uma V |
| Ou exclusivo | p ⊕ q | `p != q` | verdadeira se diferentes |
| Implicação | p → q | `(not p) or q` | falsa só se p=V e q=F |
| Bicondicional | p ↔ q | `p == q` | verdadeira se iguais |

- **Leis de De Morgan**: ¬(p ∧ q) ≡ ¬p ∨ ¬q e ¬(p ∨ q) ≡ ¬p ∧ ¬q.
- Outras leis: comutativa, associativa, distributiva (p ∧ (q ∨ r) ≡ (p ∧ q) ∨ (p ∧ r)), dupla negação, identidade (p ∧ V ≡ p), absorção (p ∨ (p ∧ q) ≡ p).
- **Tautologia**: sempre V (p ∨ ¬p). **Contradição**: sempre F (p ∧ ¬p).
- Em hardware, `AND`, `OR`, `NOT` são portas lógicas — a base da CPU (Módulo 1).

## Exemplo em Python
```python
def implica(p: bool, q: bool) -> bool:
    return (not p) or q

p, q = True, False
print(not (p and q) == ((not p) or (not q)))   # De Morgan → True
print(implica(True, False), implica(False, False))  # False True

# Aplicação: regra de acesso
def pode_acessar(logado: bool, admin: bool, bloqueado: bool) -> bool:
    return logado and (admin or not bloqueado)
```

## Exercício
1. Traduza para símbolos: "Se chover e eu não tiver guarda-chuva, então me molho".
2. Prove com Python, para todos os valores de p, q, que `not (p or q) == (not p and not q)`.
3. Escreva a negação de `idade >= 18 and tem_documento` aplicando De Morgan.

## Checklist
- [ ] Conheço os conectivos e seus equivalentes em Python
- [ ] Aplico as leis de De Morgan
- [ ] Reconheço tautologias e contradições
