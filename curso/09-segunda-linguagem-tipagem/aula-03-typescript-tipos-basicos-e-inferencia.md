# Aula 3 — TypeScript: tipos básicos e inferência

**Duração:** ~25 min · **Módulo 9**

## Objetivo
Usar os tipos primitivos do TypeScript e aproveitar a inferência de tipos.

## Teoria
- Tipos primitivos: `string`, `number`, `boolean`, `bigint`, `null`, `undefined`.
- Coleções: `number[]` ou `Array<number>`; **tuplas** `[string, number]`.
- `any` desliga a verificação (evite); prefira **`unknown`**, que exige checagem antes do uso.
- `void` (função sem retorno) e `never` (nunca retorna, ex.: lança erro).
- **Inferência**: o compilador deduz o tipo da inicialização; anote apenas quando necessário (parâmetros, retornos públicos).
- **União** `string | number` e **literais** `"ativo" | "inativo"`; *narrowing* com `typeof`.
- Ative `"strict": true` no `tsconfig.json`; ele inclui `strictNullChecks`.

## Exemplo
```typescript
let nome = "Ana";          // inferido: string
let idade: number = 30;
const tags: string[] = ["ts", "js"];
const par: [string, number] = ["x", 1];

type Status = "pendente" | "feita";
let s: Status = "pendente";
// s = "outra"; // erro

function formatar(id: string | number): string {
  if (typeof id === "number") {
    return id.toFixed(0).padStart(4, "0");
  }
  return id.toUpperCase();
}

function parse(entrada: unknown): number {
  if (typeof entrada !== "string") throw new Error("esperava string");
  return Number(entrada);
}

console.log(formatar(7), formatar("ab")); // 0007 AB
```

## Exercício
1. Declare variáveis de cada tipo primitivo e deixe o TS inferir; passe o mouse no editor para ver os tipos.
2. Escreva `primeiro(xs: number[])` que devolve `number | undefined` e trate o caso `undefined` no chamador.
3. Troque um `any` por `unknown` e adicione a checagem necessária.

## Checklist
- [ ] Uso tipos primitivos, arrays, tuplas e uniões
- [ ] Evito `any` e conheço `unknown`
- [ ] Uso `strict: true`
