# Aula 1 — Por que aprender mais de uma linguagem

**Duração:** ~15 min · **Módulo 9**

## Objetivo
Entender o valor de conhecer várias linguagens e como transferir conceitos entre elas.

## Teoria
- Conceitos (variáveis, funções, estruturas de dados, OO, concorrência) são **universais**; a sintaxe muda.
- Cada linguagem expõe **ideias diferentes**: tipagem estática, pattern matching, goroutines, ownership. Isso amplia seu repertório de soluções.
- O **mercado** e o **ecossistema** pedem ferramentas distintas: web front-end (JavaScript/TypeScript), dados (Python), sistemas (Go, Rust, C), empresas (Java, C#).
- Aprender a segunda linguagem é bem mais rápido que a primeira, e você passa a escolher a ferramenta pelo problema, não pelo hábito.
- Estratégia: aprenda **sintaxe → idioms → ecossistema → projeto real**.
- Neste módulo usaremos **TypeScript**: JavaScript com tipos estáticos, que compila para JS.

## Exemplo
O mesmo conceito em duas linguagens:
```python
# Python
def dobrar(xs):
    return [x * 2 for x in xs]
```
```typescript
// TypeScript
const dobrar = (xs: number[]): number[] => xs.map((x) => x * 2);

console.log(dobrar([1, 2, 3])); // [2, 4, 6]
```
Mesma ideia; o TypeScript declara os tipos e o compilador os verifica.

## Exercício
1. Liste 3 conceitos do Python que você espera encontrar no TypeScript.
2. Instale Node.js e execute `node -v` e `npx tsc -v`.
3. Escreva em TypeScript uma função que retorna o maior valor de um array de números e compare com a versão em Python.

## Checklist
- [ ] Explico por que aprender outra linguagem ajuda
- [ ] Sei que conceitos se transferem entre linguagens
- [ ] Tenho Node.js e `tsc` instalados
