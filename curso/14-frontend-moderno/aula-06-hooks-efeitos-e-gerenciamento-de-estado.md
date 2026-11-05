# Aula 6 — Hooks, efeitos e gerenciamento de estado

**Duração:** ~25 min · **Módulo 14**

## Objetivo
Usar os principais hooks e escolher uma estratégia de gerenciamento de estado.

## Teoria
- **Hooks** só podem ser chamados no topo de componentes ou de outros hooks (nunca em `if`/loops).
- `useState`: estado local. `useReducer`: estado com transições complexas.
- `useEffect(fn, deps)`: sincroniza com o mundo externo (fetch, timers, eventos). Retorne uma função de **limpeza**. A lista de dependências deve conter tudo que o efeito usa.
- `useMemo`/`useCallback`: otimizações; use só quando houver problema medido.
- `useRef`: valor mutável que não causa re-render (ex.: referência a elemento do DOM).
- **Custom hooks**: funções `useAlgo` que reutilizam lógica com estado.
- **Onde guardar estado**:
  1. Local (`useState`) por padrão.
  2. Elevado ao ancestral comum.
  3. **Context** para dados globais pouco mutáveis (tema, usuário).
  4. Bibliotecas (Zustand, Redux Toolkit) para estado global complexo.
  5. **Dados do servidor**: TanStack Query (cache, revalidação) em vez de copiar para estado.

## Exemplo
```tsx
import { useEffect, useReducer, useState } from 'react';

type Acao = { tipo: 'incrementar' } | { tipo: 'zerar' };
function reducer(estado: number, acao: Acao) {
  switch (acao.tipo) {
    case 'incrementar': return estado + 1;
    case 'zerar': return 0;
  }
}

export function useFetch<T>(url: string) {
  const [dados, setDados] = useState<T | null>(null);
  const [erro, setErro] = useState<string | null>(null);
  const [carregando, setCarregando] = useState(true);

  useEffect(() => {
    const controle = new AbortController();
    setCarregando(true);
    fetch(url, { signal: controle.signal })
      .then(r => { if (!r.ok) throw new Error(`HTTP ${r.status}`); return r.json(); })
      .then(setDados)
      .catch(e => { if (e.name !== 'AbortError') setErro(e.message); })
      .finally(() => setCarregando(false));
    return () => controle.abort();
  }, [url]);

  return { dados, erro, carregando };
}

export function Contador() {
  const [n, dispatch] = useReducer(reducer, 0);
  return <button onClick={() => dispatch({ tipo: 'incrementar' })}>Cliques: {n}</button>;
}
```

## Exercício
1. Use `useFetch` para listar tarefas e exiba estados de carregando e erro.
2. Crie um hook `useLocalStorage(chave, inicial)`.
3. Crie um `ThemeContext` com alternância claro/escuro.

## Checklist
- [ ] Sei as regras dos hooks
- [ ] Escrevo `useEffect` com dependências e limpeza
- [ ] Escolho o lugar certo para cada tipo de estado
