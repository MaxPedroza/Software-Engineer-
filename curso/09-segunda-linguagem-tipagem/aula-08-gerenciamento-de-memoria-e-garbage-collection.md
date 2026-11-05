# Aula 8 — Gerenciamento de memória e garbage collection

**Duração:** ~25 min · **Módulo 9**

## Objetivo
Entender como linguagens gerenciam memória e evitar vazamentos.

## Teoria
- **Stack**: variáveis locais e chamadas de função; alocação rápida e liberação automática ao sair do escopo. **Heap**: objetos de vida variável.
- **Manual** (C: `malloc`/`free`): controle total, risco de *leaks* e *use-after-free*.
- **Garbage Collector (GC)**: libera objetos **inalcançáveis** a partir das raízes (variáveis globais e da pilha). Usado por JS (V8), Java, Go, C#.
- **Contagem de referências** (Python/CPython) + coletor de ciclos. **Ownership** (Rust): verificado em compilação, sem GC.
- **GC geracional**: objetos novos morrem cedo, então são coletados com mais frequência.
- Trade-off do GC: produtividade e segurança, ao custo de pausas e uso extra de memória.
- **Vazamentos** em linguagens com GC ocorrem quando referências esquecidas mantêm objetos alcançáveis: caches sem limite, listeners não removidos, timers, globais.

## Exemplo
```typescript
// Vazamento: cache cresce sem limite
const cache = new Map<string, object>();
function obter(chave: string) {
  if (!cache.has(chave)) cache.set(chave, { dados: new Array(1000).fill(0) });
  return cache.get(chave);
}

// Alternativa: WeakMap permite que a chave seja coletada
const meta = new WeakMap<object, string>();
let usuario: object | null = { nome: "Ana" };
meta.set(usuario, "premium");
usuario = null; // entrada elegível para coleta

console.log(process.memoryUsage().heapUsed);
```
Em Python: `import sys; sys.getrefcount(obj)` e o módulo `gc` mostram contagem de referências e ciclos.

## Exercício
1. Execute o laço que chama `obter` com 100 mil chaves e observe `heapUsed`.
2. Limite o cache a 100 entradas (descartando a mais antiga).
3. Explique por que um ciclo `a.ref = b; b.ref = a` é coletado pelo GC, mas não por contagem de referências simples.

## Checklist
- [ ] Diferencio stack e heap
- [ ] Explico alcançabilidade no GC
- [ ] Reconheço causas comuns de vazamento
