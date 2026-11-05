# Aula 3 — Design responsivo e fundamentos de UX/UI

**Duração:** ~20 min · **Módulo 14**

## Objetivo
Criar interfaces que se adaptam a qualquer tela e aplicar princípios básicos de UX/UI.

## Teoria
- **Mobile-first**: escreva o CSS base para telas pequenas e amplie com `min-width`.
- **Meta viewport** obrigatória: `<meta name="viewport" content="width=device-width, initial-scale=1">`.
- **Media queries** definem breakpoints (ex.: 640px, 1024px). Prefira unidades relativas: `rem`, `%`, `vw`, `clamp()`.
- **Imagens responsivas**: `max-width: 100%`, `srcset` e `loading="lazy"`.
- **UX** (experiência) vs **UI** (aparência): UX trata de fluxo, clareza e esforço do usuário; UI trata de cores, tipografia e componentes.
- **Princípios**:
  - Hierarquia visual (tamanho, peso, contraste).
  - Consistência (mesmos padrões para mesmas ações).
  - Feedback (estados de carregamento, erro e sucesso).
  - Alvos de toque com pelo menos 44×44 px.
  - Heurísticas de Nielsen: visibilidade do estado, prevenção de erros, reconhecer em vez de lembrar.

## Exemplo
```css
body { font-family: system-ui, sans-serif; font-size: clamp(1rem, 1vw + 0.9rem, 1.2rem); }

.lista { display: grid; gap: 1rem; padding: 1rem; }

@media (min-width: 640px) {
  .lista { grid-template-columns: repeat(2, 1fr); }
}
@media (min-width: 1024px) {
  .lista { grid-template-columns: repeat(3, 1fr); max-width: 1200px; margin-inline: auto; }
}

button { min-height: 44px; padding: 0 1.25rem; }
button:focus-visible { outline: 3px solid #05f; outline-offset: 2px; }

@media (prefers-color-scheme: dark) {
  body { background: #111; color: #eee; }
}
```

## Exercício
1. Transforme a página de tarefas em mobile-first com 1, 2 e 3 colunas conforme a largura.
2. Teste no DevTools em modo dispositivo (320px, 768px, 1280px).
3. Liste 3 problemas de UX de um app que você usa, citando a heurística violada.

## Checklist
- [ ] Escrevo CSS mobile-first
- [ ] Uso media queries e unidades relativas
- [ ] Sei diferenciar UX de UI
