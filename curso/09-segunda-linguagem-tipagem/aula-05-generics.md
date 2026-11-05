# Aula 5 — Generics

**Duração:** ~25 min · **Módulo 9**

## Objetivo
Escrever funções e classes reutilizáveis que preservam informação de tipo.

## Teoria
- **Generics** parametrizam tipos: `T` funciona como uma "variável de tipo".
- Evitam duplicação e o uso de `any`: a função aceita qualquer tipo e **mantém** a relação entre entrada e saída.
- **Restrições**: `T extends { id: number }` exige certa forma.
- Podem ser usados em funções, interfaces, tipos e classes.
- **Valores padrão**: `<T = string>`.
- Utilitários nativos baseados em generics: `Partial<T>`, `Readonly<T>`, `Pick<T, K>`, `Record<K, V>`, `Promise<T>`, `Array<T>`.

## Exemplo
```typescript
function primeiro<T>(xs: T[]): T | undefined {
  return xs[0];
}
const n = primeiro([1, 2, 3]);      // number | undefined
const s = primeiro(["a", "b"]);     // string | undefined

interface Entidade { id: number }

class Repositorio<T extends Entidade> {
  private itens = new Map<number, T>();

  salvar(item: T): void {
    this.itens.set(item.id, item);
  }
  buscar(id: number): T | undefined {
    return this.itens.get(id);
  }
}

interface Tarefa extends Entidade { titulo: string }

const repo = new Repositorio<Tarefa>();
repo.salvar({ id: 1, titulo: "Aprender generics" });
console.log(repo.buscar(1)?.titulo);

const edicao: Partial<Tarefa> = { titulo: "Novo título" };
```
`new Repositorio<string>()` é erro: `string` não atende à restrição `Entidade`.

## Exercício
1. Implemente `ultimo<T>(xs: T[]): T | undefined`.
2. Escreva `agrupar<T, K extends string>(xs: T[], chave: (x: T) => K): Record<K, T[]>`.
3. Implemente uma `Pilha<T>` com `empilhar`, `desempilhar` e `topo`.

## Checklist
- [ ] Entendo `<T>` e restrições com `extends`
- [ ] Uso generics em vez de `any`
- [ ] Conheço `Partial`, `Pick` e `Record`
