# Aula 8 — Resiliência: retry, timeout, circuit breaker e backpressure

**Duração:** ~25 min · **Módulo 17**

## Objetivo
Proteger o sistema contra falhas parciais e falhas em cascata.

## Teoria
- **Timeout**: toda chamada remota precisa de um; sem ele, threads ficam presas.
- **Retry com backoff exponencial e jitter**: só em erros transitórios e operações **idempotentes**. Sem limite, vira *retry storm*.
- **Circuit breaker**: estados *fechado* → (muitas falhas) → *aberto* (falha rápido) → *meio-aberto* (testa) → fechado.
- **Bulkhead**: isola recursos (pools) por dependência.
- **Backpressure**: sinalizar ao produtor para desacelerar — filas limitadas, rejeição (HTTP 429/503), *load shedding*.
- **Degradação graciosa** e fallbacks (dado em cache, recomendação padrão).
- **Chaos engineering**: injetar falhas de propósito para validar.

## Exemplo em Python
```python
import random, time

def retry(fn, tentativas=4, base=0.2):
    for i in range(tentativas):
        try:
            return fn()
        except TimeoutError:
            if i == tentativas - 1:
                raise
            time.sleep(base * 2 ** i * random.uniform(0.5, 1.5))

class CircuitBreaker:
    def __init__(self, limite=3, espera=10):
        self.falhas, self.limite, self.espera, self.aberto_em = 0, limite, espera, None

    def chamar(self, fn):
        if self.aberto_em and time.time() - self.aberto_em < self.espera:
            raise RuntimeError("circuito aberto")
        try:
            r = fn()
            self.falhas, self.aberto_em = 0, None
            return r
        except Exception:
            self.falhas += 1
            if self.falhas >= self.limite:
                self.aberto_em = time.time()
            raise
```

## Exercício
1. Crie uma função que falha 70% das vezes e meça a taxa de sucesso com e sem `retry`.
2. Use `queue.Queue(maxsize=100)` e rejeite com erro quando cheia; explique o efeito de backpressure.

## Checklist
- [ ] Defino timeouts em toda chamada remota
- [ ] Uso retry com backoff e jitter
- [ ] Sei descrever o circuit breaker e backpressure
