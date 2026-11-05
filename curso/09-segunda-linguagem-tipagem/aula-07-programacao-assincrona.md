# Aula 7 — Programação assíncrona (callbacks, Promises, async/await)

**Duração:** ~30 min · **Módulo 9**

## Objetivo
Lidar com operações demoradas (I/O, rede) sem bloquear o programa.

## Teoria
- JavaScript/Node roda em **uma thread** com **event loop**: operações de I/O são delegadas e retornam depois, sem travar o resto.
- **Callbacks**: função chamada ao final. Aninhar vários gera o "callback hell".
- **Promise**: objeto que representa um valor futuro; estados *pending*, *fulfilled*, *rejected*. Encadeia com `.then`/`.catch`.
- **async/await**: açúcar sintático sobre Promises; código assíncrono com cara de síncrono. Erros tratados com `try/catch`.
- `Promise.all` executa em paralelo e falha se uma falhar; `Promise.allSettled` espera todas.
- Tipo de retorno: `Promise<T>`. Esquecer o `await` é um erro comum.

## Exemplo
```typescript
const esperar = (ms: number): Promise<void> =>
  new Promise((resolve) => setTimeout(resolve, ms));

async function buscarTarefa(id: number): Promise<{ id: number; titulo: string }> {
  await esperar(100);
  if (id <= 0) throw new Error("id inválido");
  return { id, titulo: `Tarefa ${id}` };
}

async function main(): Promise<void> {
  try {
    const t = await buscarTarefa(1);
    console.log(t.titulo);

    // paralelo: ~100 ms em vez de ~300 ms
    const todas = await Promise.all([1, 2, 3].map(buscarTarefa));
    console.log(todas.length);

    await buscarTarefa(0);
  } catch (e) {
    console.error("Falhou:", (e as Error).message);
  }
}

main();
```

## Exercício
1. Reescreva uma função com callback aninhado usando Promises e depois `async/await`.
2. Meça o tempo de 3 chamadas sequenciais vs `Promise.all`.
3. Use `Promise.allSettled` e mostre quais chamadas falharam.

## Checklist
- [ ] Explico event loop em uma frase
- [ ] Uso `async/await` com `try/catch`
- [ ] Sei paralelizar com `Promise.all`
