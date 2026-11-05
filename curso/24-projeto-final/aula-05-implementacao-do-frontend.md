# Aula 5 — Implementação do frontend

**Duração:** ~40 min · **Módulo 24 — Etapa 5**

## Objetivo
Construir uma interface acessível e responsiva que consome a API.

## Passo a passo
1. **Wireframes** das 3–5 telas principais (papel ou Figma) a partir das jornadas.
2. **Setup** (React/Vite ou similar), roteamento, cliente HTTP central com tratamento de erro e token.
3. **Componentes reutilizáveis** (botão, input, lista, modal) e estado (Context/Zustand/React Query).
4. **Telas**: login/cadastro, listagem com paginação, criação/edição, estados de *loading*, vazio e erro.
5. **Acessibilidade**: HTML semântico, labels, foco visível, contraste ≥ 4,5:1, navegação por teclado.
6. **Responsividade** mobile-first e **performance** (code splitting, imagens otimizadas).
7. **Variável de ambiente** para a URL da API (`VITE_API_URL`).

### Cliente HTTP
```ts
export async function api<T>(path: string, init: RequestInit = {}): Promise<T> {
  const res = await fetch(`${import.meta.env.VITE_API_URL}${path}`, {
    ...init,
    headers: { 'Content-Type': 'application/json', Authorization: `Bearer ${getToken()}`, ...init.headers },
  });
  if (!res.ok) throw await res.json();
  return res.json();
}
```

## Entregáveis
- Aplicação frontend integrada à API, com build de produção
- Wireframes em `docs/ux/`
- Relatório do Lighthouse salvo em `docs/`

## Critérios de aceite
- [ ] Todas as jornadas Must funcionam ponta a ponta
- [ ] Estados de loading, vazio e erro tratados
- [ ] Lighthouse: Acessibilidade ≥ 90 e Performance ≥ 80
- [ ] Funciona em 360 px e em desktop
