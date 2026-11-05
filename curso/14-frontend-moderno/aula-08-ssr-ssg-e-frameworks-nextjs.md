# Aula 8 — SSR, SSG e frameworks (Next.js)

**Duração:** ~20 min · **Módulo 14**

## Objetivo
Entender estratégias de renderização e quando usar um framework como o Next.js.

## Teoria
| Estratégia | Quando renderiza | Bom para |
|-----------|------------------|----------|
| **CSR** (client-side) | No navegador | Apps internos, dashboards |
| **SSR** (server-side) | A cada requisição | Conteúdo dinâmico e SEO |
| **SSG** (static) | No build | Blogs, documentação, marketing |
| **ISR** | Estático + revalidação periódica | Catálogos que mudam pouco |

- CSR entrega HTML quase vazio: pior SEO e primeiro conteúdo mais lento (LCP).
- **Hidratação**: o React "ativa" no navegador o HTML vindo do servidor.
- **Next.js** (App Router): roteamento por pastas (`app/tarefas/page.tsx`), layouts, **Server Components** (rodam só no servidor, sem JS no cliente) e **Client Components** (`'use client'`, usam estado e eventos).
- Server Components podem acessar banco/API diretamente; nunca exponha segredos em Client Components.
- Outras opções: Remix, Astro (conteúdo), Nuxt (Vue), SvelteKit.
- Criar projeto: `npx create-next-app@latest`.

## Exemplo
```tsx
// app/tarefas/page.tsx — Server Component (SSR a cada requisição)
type Tarefa = { id: number; titulo: string };

export default async function Tarefas() {
  const resp = await fetch(`${process.env.API_URL}/tarefas`, { cache: 'no-store' });
  const tarefas: Tarefa[] = await resp.json();
  return (
    <main>
      <h1>Tarefas</h1>
      <ul>{tarefas.map(t => <li key={t.id}>{t.titulo}</li>)}</ul>
    </main>
  );
}

// app/tarefas/[id]/page.tsx — dinâmica, revalidada a cada 60 s (ISR)
export const revalidate = 60;
export default async function Detalhe({ params }: { params: Promise<{ id: string }> }) {
  const { id } = await params;
  const t = await (await fetch(`${process.env.API_URL}/tarefas/${id}`)).json();
  return <h1>{t.titulo}</h1>;
}
```

## Exercício
1. Para cada página do sistema (home, lista, detalhe, perfil), escolha CSR, SSR, SSG ou ISR e justifique.
2. Crie um projeto Next.js com a rota `/tarefas` acima.
3. Compare o HTML inicial (Ver código-fonte) de uma SPA Vite e de uma página Next.js.

## Checklist
- [ ] Diferencio CSR, SSR, SSG e ISR
- [ ] Sei o que é hidratação
- [ ] Distingo Server e Client Components
