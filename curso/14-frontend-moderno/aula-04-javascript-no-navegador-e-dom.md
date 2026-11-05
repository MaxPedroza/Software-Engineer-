# Aula 4 — JavaScript no navegador e DOM

**Duração:** ~20 min · **Módulo 14**

## Objetivo
Manipular a página com JavaScript, tratar eventos e usar `fetch` de forma assíncrona.

## Teoria
- **DOM** (Document Object Model): árvore de objetos que representa o HTML. O JS lê e altera essa árvore.
- Seleção: `document.querySelector`, `querySelectorAll`. Alteração: `textContent`, `classList`, `append`, `remove`.
- **Eventos**: `addEventListener('click', fn)`. **Delegação de eventos**: um único listener no pai trata os filhos via `event.target`.
- Prefira `textContent` a `innerHTML` com dados externos (evita **XSS**).
- **Assíncrono**: `fetch` retorna uma Promise; use `async/await` e trate erros com `try/catch`. `fetch` não rejeita em HTTP 4xx/5xx; verifique `response.ok`.
- `localStorage` guarda strings (use `JSON.stringify/parse`).
- Use `<script type="module">` para ES Modules (`import`/`export`).

## Exemplo
```html
<ul id="lista"></ul>
<script type="module">
  const lista = document.querySelector('#lista');

  async function carregar() {
    try {
      const resp = await fetch('https://jsonplaceholder.typicode.com/todos?_limit=5');
      if (!resp.ok) throw new Error(`HTTP ${resp.status}`);
      const tarefas = await resp.json();
      for (const t of tarefas) {
        const li = document.createElement('li');
        li.textContent = t.title;
        li.dataset.id = t.id;
        li.classList.toggle('feita', t.completed);
        lista.append(li);
      }
    } catch (erro) {
      lista.textContent = `Falha ao carregar: ${erro.message}`;
    }
  }

  lista.addEventListener('click', (e) => {
    const li = e.target.closest('li');
    if (li) li.classList.toggle('feita');
  });

  carregar();
</script>
```

## Exercício
1. Adicione um formulário que insere novas tarefas na lista sem recarregar a página.
2. Persista as tarefas no `localStorage` e recarregue-as ao abrir.
3. Mostre mensagem de "Carregando..." durante o `fetch`.

## Checklist
- [ ] Seleciono e altero elementos do DOM
- [ ] Uso delegação de eventos
- [ ] Trato erros em `fetch` com `response.ok`
