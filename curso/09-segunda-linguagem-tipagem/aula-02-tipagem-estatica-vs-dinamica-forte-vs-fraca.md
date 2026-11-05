# Aula 2 — Tipagem estática vs dinâmica, forte vs fraca

**Duração:** ~20 min · **Módulo 9**

## Objetivo
Distinguir os dois eixos de tipagem e entender seus trade-offs.

## Teoria
Eixo 1 — **quando** os tipos são verificados:
- **Estática**: em tempo de compilação (Java, Go, TypeScript). Erros aparecem antes de rodar; melhor autocompletar e refatoração.
- **Dinâmica**: em tempo de execução (Python, JavaScript, Ruby). Mais flexível e rápida de prototipar, mas erros surgem tarde.

Eixo 2 — **quão rígida** é a conversão entre tipos:
- **Forte**: não converte tipos silenciosamente. Python: `"1" + 1` → `TypeError`.
- **Fraca**: converte implicitamente. JavaScript: `"1" + 1` → `"11"`; `"3" * 2` → `6`.

Logo: Python = dinâmica e forte; JavaScript = dinâmica e fraca; TypeScript = estática (sobre JS), mas só checa em compilação, pois apaga os tipos ao gerar JS. Python também aceita *type hints*, verificados por ferramentas como `mypy`.

## Exemplo
```python
def somar(a, b):
    return a + b

somar(1, 2)      # 3
somar("1", 2)    # TypeError só em tempo de execução
```
```typescript
function somar(a: number, b: number): number {
  return a + b;
}

somar(1, 2);
// somar("1", 2); // erro de compilação: string não é number
```

## Exercício
1. Classifique Python, JavaScript, Java, Go e TypeScript nos dois eixos.
2. Preveja o resultado em JS: `[] + {}`, `"5" - 2`, `"5" + 2`; depois teste no Node.
3. Adicione type hints a uma função Python e rode `mypy`.

## Checklist
- [ ] Diferencio estática/dinâmica de forte/fraca
- [ ] Sei dar uma vantagem de cada abordagem
- [ ] Sei que TypeScript verifica tipos só na compilação
