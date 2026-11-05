# Aula 9 — Performance web (Core Web Vitals) e PWA

**Duração:** ~20 min · **Módulo 14**

## Objetivo
Medir e melhorar a performance e transformar o app em um PWA básico.

## Teoria
- **Core Web Vitals** (metas "bom"):
  - **LCP** (Largest Contentful Paint) ≤ 2,5 s — carregamento do maior elemento.
  - **INP** (Interaction to Next Paint) ≤ 200 ms — responsividade.
  - **CLS** (Cumulative Layout Shift) ≤ 0,1 — estabilidade visual.
- Ferramentas: **Lighthouse**, PageSpeed Insights, aba Performance do DevTools, biblioteca `web-vitals`.
- **Técnicas**:
  - Reduzir JS: *code splitting* e `React.lazy`, tree shaking.
  - Imagens em WebP/AVIF, com `width`/`height` (evita CLS) e `loading="lazy"`.
  - Cache HTTP e CDN; compressão gzip/brotli.
  - Fontes com `font-display: swap`.
  - Evitar tarefas longas na thread principal.
- **PWA**: site instalável e com suporte offline. Requer HTTPS, **manifest** e **Service Worker** (intercepta requisições e usa cache).

## Exemplo
```tsx
import { lazy, Suspense } from 'react';
const Grafico = lazy(() => import('./Grafico'));

export function Relatorio() {
  return (
    <Suspense fallback={<p>Carregando gráfico...</p>}>
      <Grafico />
    </Suspense>
  );
}
```
```json
// public/manifest.webmanifest
{
  "name": "Gerenciador de Tarefas",
  "short_name": "Tarefas",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#0a7",
  "icons": [{ "src": "/icon-512.png", "sizes": "512x512", "type": "image/png" }]
}
```
```js
// public/sw.js — cache-first para arquivos estáticos
const CACHE = 'tarefas-v1';
self.addEventListener('install', e =>
  e.waitUntil(caches.open(CACHE).then(c => c.addAll(['/', '/index.html']))));
self.addEventListener('fetch', e =>
  e.respondWith(caches.match(e.request).then(r => r || fetch(e.request))));
// registro: navigator.serviceWorker.register('/sw.js')
```

## Exercício
1. Rode o Lighthouse no app e anote LCP, INP/TBT e CLS.
2. Aplique duas otimizações (ex.: lazy loading e imagens com dimensões) e compare.
3. Adicione manifest e service worker e verifique a opção "Instalar" no navegador.

## Checklist
- [ ] Conheço LCP, INP e CLS
- [ ] Aplico code splitting e otimização de imagens
- [ ] Sei os requisitos de um PWA
