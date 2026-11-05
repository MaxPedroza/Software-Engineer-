# Aula 3 — Padrões de projeto: estruturais

**Duração:** ~20 min · **Módulo 16**

## Objetivo
Usar Adapter, Decorator e Facade para organizar relações entre classes e componentes.

## Teoria
Padrões **estruturais** tratam de como compor classes e objetos em estruturas maiores.
- **Adapter**: converte a interface de uma classe na que o cliente espera (integrar bibliotecas/APIs de terceiros).
- **Decorator**: adiciona comportamento a um objeto dinamicamente, por composição (log, cache, autenticação), sem herança.
- **Facade**: interface simples para um subsistema complexo.
- **Proxy**: representante que controla acesso (cache, lazy loading, permissões).
- **Composite**: trata objetos individuais e grupos de forma uniforme (árvores).
- **Bridge**: separa abstração e implementação para variarem de forma independente.
- Prefira **composição a herança**.

## Exemplo em TypeScript
```ts
interface Pagamento {
  pagar(valor: number): string;
}

// API de terceiro com interface incompatível
class GatewayExterno {
  cobrarCentavos(centavos: number): { ok: boolean; id: string } {
    return { ok: true, id: "tx-123" };
  }
}

// Adapter
class GatewayAdapter implements Pagamento {
  constructor(private gw: GatewayExterno) {}
  pagar(valor: number): string {
    const r = this.gw.cobrarCentavos(Math.round(valor * 100));
    if (!r.ok) throw new Error("pagamento recusado");
    return r.id;
  }
}

// Decorator
class PagamentoComLog implements Pagamento {
  constructor(private interno: Pagamento) {}
  pagar(valor: number): string {
    console.log(`Iniciando pagamento de R$ ${valor}`);
    const id = this.interno.pagar(valor);
    console.log(`Pagamento concluído: ${id}`);
    return id;
  }
}

const pagamento: Pagamento = new PagamentoComLog(new GatewayAdapter(new GatewayExterno()));
pagamento.pagar(49.9);
```

## Exercício
1. Crie um `PagamentoComRetry` (Decorator) que tenta 3 vezes antes de falhar e empilhe com o de log.
2. Escreva uma Facade `CheckoutService` que oculte estoque, pagamento e envio.
3. Em Python, implemente um decorator `@cache_simples` para uma função e relacione ao padrão.

## Checklist
- [ ] Distingo Adapter, Decorator e Facade
- [ ] Prefiro composição a herança
- [ ] Empilho decorators sem alterar o cliente
