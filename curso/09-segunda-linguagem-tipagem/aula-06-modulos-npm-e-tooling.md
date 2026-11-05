# Aula 6 — Módulos, npm e tooling (tsconfig, linters, formatadores)

**Duração:** ~25 min · **Módulo 9**

## Objetivo
Organizar um projeto TypeScript com módulos, npm e ferramentas de qualidade.

## Teoria
- **Módulos ES**: `export` / `import` separam o código em arquivos.
- **npm**: gerenciador de pacotes. `package.json` descreve o projeto; `package-lock.json` fixa versões; `node_modules/` guarda as dependências (fora do Git).
- `dependencies` (runtime) vs `devDependencies` (build/teste). `scripts` automatizam tarefas.
- **`tsconfig.json`**: configura o compilador (`target`, `module`, `outDir`, `strict`).
- **ESLint**: analisa o código em busca de problemas. **Prettier**: formata automaticamente.
- **`npm link`**: instala localmente um pacote em desenvolvimento, simulando publicação.

## Exemplo
```bash
mkdir tarefas-ts && cd tarefas-ts
npm init -y
npm i -D typescript eslint prettier @types/node
npx tsc --init
```
`tsconfig.json` (trecho):
```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "NodeNext",
    "outDir": "dist",
    "rootDir": "src",
    "strict": true,
    "declaration": true
  }
}
```
`package.json` (trecho):
```json
{
  "main": "dist/index.js",
  "types": "dist/index.d.ts",
  "scripts": {
    "build": "tsc",
    "format": "prettier --write src"
  }
}
```
`src/tarefa.ts` e `src/index.ts`:
```typescript
export interface Tarefa { id: number; titulo: string }
export const criar = (id: number, titulo: string): Tarefa => ({ id, titulo });
```
```typescript
export * from "./tarefa.js";
```
Depois: `npm run build` e, em outro projeto, `npm link tarefas-ts`.

## Exercício
1. Crie o projeto acima e compile com `npm run build`.
2. Adicione o script `lint` rodando ESLint e corrija os avisos.
3. Rode `npm link` e importe a função `criar` em um segundo projeto.

## Checklist
- [ ] Separo código em módulos com `import`/`export`
- [ ] Configuro `tsconfig.json` com `strict`
- [ ] Uso ESLint e Prettier via scripts npm
