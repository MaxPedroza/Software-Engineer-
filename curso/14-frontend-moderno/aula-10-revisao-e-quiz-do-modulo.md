# Aula 10 — Revisão e quiz do módulo

**Duração:** ~20 min · **Módulo 14**

## Resumo
- **HTML semântico** e a11y: tags corretas, `label`, `alt`, teclado, contraste.
- **CSS**: box model, Flexbox (1D), Grid (2D), variáveis, mobile-first e media queries.
- **JS/DOM**: eventos, delegação, `fetch` com `response.ok`, `textContent` contra XSS.
- **React**: componentes, props, estado imutável, `key`, hooks e `useEffect` com limpeza.
- **SPA**: roteamento, camada de API, estados de carregando/erro/sucesso.
- **SSR/SSG/ISR** e Next.js; **performance**: LCP, INP, CLS, code splitting; **PWA**.

## Quiz
1. Por que usar `<button>` em vez de `<div onclick>`?
2. Qual a diferença entre Flexbox e Grid?
3. O que significa `box-sizing: border-box`?
4. O que é abordagem mobile-first?
5. `fetch` rejeita a Promise em um HTTP 404? Explique.
6. Por que props não devem ser alteradas pelo componente filho?
7. Para que serve a função de retorno de um `useEffect`?
8. Por que usar `key` estável em listas?
9. Cite uma vantagem do SSR sobre o CSR.
10. O que mede o CLS e como reduzi-lo?

## Gabarito resumido
1. O botão nativo é focável, aciona com Enter/Espaço e é anunciado por leitores de tela.
2. Flexbox é unidimensional; Grid é bidimensional.
3. `width`/`height` incluem padding e borda.
4. CSS base para telas pequenas, ampliado com `min-width`.
5. Não; só rejeita em falha de rede. Verifique `response.ok`.
6. O fluxo é unidirecional; mudanças vão pelo pai via callbacks.
7. Limpeza (cancelar fetch, remover listeners, timers).
8. Permite ao React identificar itens e preservar estado/DOM corretamente.
9. Melhor SEO e primeiro conteúdo mais rápido (LCP).
10. Estabilidade visual; defina `width`/`height` em imagens e reserve espaço para conteúdo dinâmico.

## Entregável do módulo
Aplicação React responsiva e acessível que consome a API do Módulo 13 (listar, criar, editar, excluir tarefas), com rotas, estados de carregamento/erro e nota ≥ 90 no Lighthouse em Performance e Acessibilidade. Publique o código no repositório do projeto.

## Checklist final
- [ ] Interface semântica e navegável por teclado
- [ ] Layout responsivo com Flexbox/Grid
- [ ] Componentes React com hooks e roteamento
- [ ] Integração com a API do Módulo 13
- [ ] Lighthouse ≥ 90 nas categorias principais
