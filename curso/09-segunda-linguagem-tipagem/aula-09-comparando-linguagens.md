# Aula 9 — Comparando linguagens (Python, TypeScript, Java, Go) e quando usar cada uma

**Duração:** ~25 min · **Módulo 9**

## Objetivo
Comparar linguagens por critérios técnicos e escolher a mais adequada a cada contexto.

## Teoria
| | Python | TypeScript | Java | Go |
|---|---|---|---|---|
| Tipagem | dinâmica, forte (hints opcionais) | estática (sobre JS) | estática, forte | estática, forte |
| Execução | interpretada | transpila para JS (Node/browser) | JVM (bytecode + JIT) | compilada nativa |
| Memória | GC + ref. counting | GC (V8) | GC (JVM) | GC |
| Concorrência | threads limitadas pelo GIL, asyncio | event loop, async/await | threads, virtual threads | goroutines + channels |
| Forte em | dados, IA, scripts, automação | web front/back | sistemas corporativos, Android | APIs, cloud, CLIs, infra |

Critérios para escolher: **problema**, **desempenho**, **ecossistema/bibliotecas**, **equipe**, **manutenção** e **contratação**. Não existe melhor linguagem absoluta.

## Exemplo
O mesmo "olá" concorrente, em estilos distintos:
```python
import asyncio
async def main():
    await asyncio.gather(asyncio.sleep(0.1), asyncio.sleep(0.1))
asyncio.run(main())
```
```typescript
await Promise.all([new Promise(r => setTimeout(r, 100)), new Promise(r => setTimeout(r, 100))]);
```
```go
var wg sync.WaitGroup
for i := 0; i < 2; i++ {
    wg.Add(1)
    go func() { defer wg.Done(); time.Sleep(100 * time.Millisecond) }()
}
wg.Wait()
```
Escolhas típicas: pipeline de ML → Python; app web full-stack → TypeScript; banco/ERP legado → Java; microsserviço de alto throughput → Go.

## Exercício
1. Escolha uma linguagem para: bot de Discord, app mobile Android, ferramenta de linha de comando distribuída em binário único, análise de planilhas. Justifique.
2. Implemente FizzBuzz em duas linguagens e compare tamanho e clareza.
3. Pesquise o que é o GIL e como ele afeta programas CPU-bound em Python.

## Checklist
- [ ] Comparo tipagem, execução e concorrência das quatro linguagens
- [ ] Escolho linguagem com critérios, não por moda
- [ ] Sei que ecossistema e equipe pesam na decisão
