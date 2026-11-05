# Aula 7 — Roteamento e consumo de APIs

**Duração:** ~25 min · **Módulo 14**

## Objetivo
Criar navegação entre páginas em uma SPA e consumir a API de tarefas do Módulo 13.

## Teoria
- **SPA** (Single Page Application): uma página HTML; o roteador troca componentes sem recarregar. Biblioteca comum: **React Router** (`npm i react-router-dom`).
- Conceitos: `BrowserRouter`, `Routes`/`Route`, `Link`, `useParams`, `useNavigate`, rotas aninhadas e rota `*` para 404.
- **Consumo de API**: centralize chamadas em um módulo (`api.ts`), com URL base em variável de ambiente (`import.meta.env.VITE_API_URL`).
- Trate sempre os três estados: **carregando, erro, sucesso**.
- **CORS**: o backend precisa autorizar a origem do frontend.
- **Autenticação**: envie o token no cabeçalho `Authorization: Bearer ...`. Prefira cookies `HttpOnly` quando possível; evite guardar tokens sensíveis em `localStorage` (risco de XSS).
- Rotas protegidas: redirecione para `/login` se não houver sessão.

## Exemplo
```tsx
// api.ts
const BASE = import.meta.env.VITE_API_URL ?? 'http://localhost:8000';

export async function http<T>(caminho: string, init?: RequestInit): Promise<T> {
  const resp = await fetch(`${BASE}${caminho}`, {
    headers: { 'Content-Type': 'application/json' },
    ...init,
  });
  if (!resp.ok) throw new Error(`Erro ${resp.status}`);
  return resp.json();
}

// App.tsx
import { BrowserRouter, Routes, Route, Link, useParams } from 'react-router-dom';
import { useFetch } from './useFetch';

type Tarefa = { id: number; titulo: string; descricao?: string };

function Detalhe() {
  const { id } = useParams();
  const { dados, erro, carregando } = useFetch<Tarefa>(`${import.meta.env.VITE_API_URL}/tarefas/${id}`);
  if (carregando) return <p>Carregando...</p>;
  if (erro || !dados) return <p role="alert">Erro: {erro}</p>;
  return <article><h2>{dados.titulo}</h2><p>{dados.descricao}</p></article>;
}

export default function App() {
  return (
    <BrowserRouter>
      <nav><Link to="/">Início</Link></nav>
      <Routes>
        <Route path="/" element={<h1>Tarefas</h1>} />
        <Route path="/tarefas/:id" element={<Detalhe />} />
        <Route path="*" element={<p>Página não encontrada</p>} />
      </Routes>
    </BrowserRouter>
  );
}
```

## Exercício
1. Crie as rotas `/`, `/tarefas/:id` e `/nova`, com navegação por `Link`.
2. Implemente criar e excluir tarefas via `POST` e `DELETE` na API do Módulo 13.
3. Habilite CORS no backend e teste a integração.

## Checklist
- [ ] Configuro rotas e parâmetros
- [ ] Centralizo as chamadas HTTP
- [ ] Trato carregando, erro e sucesso
