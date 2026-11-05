# Aula 5 — Processos e threads

**Duração:** ~20 min · **Módulo 1**

## Objetivo
Diferenciar processos e threads e entender o básico de concorrência.

## Teoria
- **Programa**: arquivo com instruções (passivo). **Processo**: programa em execução, com memória própria, PID e recursos.
- **Thread**: unidade de execução dentro de um processo. Threads do mesmo processo **compartilham memória**.

| | Processo | Thread |
|--|----------|--------|
| Memória | Isolada | Compartilhada |
| Criação | Mais pesada | Mais leve |
| Comunicação | IPC (pipes, sockets) | Variáveis compartilhadas |
| Falha | Isolada | Pode derrubar o processo |

### Concorrência vs paralelismo
- **Concorrência**: lidar com várias tarefas ao mesmo tempo (alternando).
- **Paralelismo**: executar várias tarefas literalmente ao mesmo tempo (múltiplos núcleos).

### Problemas clássicos
- **Race condition**: resultado depende da ordem de execução das threads.
- **Deadlock**: duas threads esperando uma a outra indefinidamente.
- Soluções: locks/mutex, filas, imutabilidade, evitar estado compartilhado.

## Exemplo em Python
```python
import threading

contador = 0
lock = threading.Lock()

def incrementar():
    global contador
    for _ in range(100_000):
        with lock:
            contador += 1

ts = [threading.Thread(target=incrementar) for _ in range(4)]
[t.start() for t in ts]; [t.join() for t in ts]
print(contador)  # 400000 (sem o lock, pode variar)
```

## Exercício
1. Remova o `lock` e rode várias vezes. O resultado muda? Por quê?
2. Explique com suas palavras a diferença entre concorrência e paralelismo.

## Checklist
- [ ] Diferencio processo de thread
- [ ] Sei o que é race condition e deadlock
- [ ] Sei por que locks existem
