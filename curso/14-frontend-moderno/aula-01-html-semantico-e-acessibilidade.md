# Aula 1 — HTML semântico e acessibilidade

**Duração:** ~20 min · **Módulo 14**

## Objetivo
Estruturar páginas com HTML semântico e aplicar boas práticas básicas de acessibilidade (a11y).

## Teoria
- **HTML semântico** usa tags que descrevem o significado do conteúdo: `header`, `nav`, `main`, `section`, `article`, `aside`, `footer`, `button`, `label`.
- Leitores de tela e buscadores dependem dessa estrutura. Uma `div` com `onclick` não é focável nem anunciada como botão.
- **Regras de ouro**:
  - Um único `h1` por página; hierarquia de títulos sem pular níveis.
  - Toda imagem informativa tem `alt`; decorativa usa `alt=""`.
  - Todo campo de formulário tem `label` associado.
  - Navegação completa por teclado (Tab, Enter, Espaço) e foco visível.
  - Contraste mínimo WCAG AA: 4,5:1 para texto normal.
- **ARIA** só quando o HTML nativo não basta (`aria-live`, `aria-label`). Primeira regra: prefira o elemento nativo.

## Exemplo
```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Minhas tarefas</title>
</head>
<body>
  <a href="#conteudo">Pular para o conteúdo</a>
  <header><nav aria-label="Principal"><a href="/">Início</a></nav></header>
  <main id="conteudo">
    <h1>Minhas tarefas</h1>
    <form>
      <label for="titulo">Nova tarefa</label>
      <input id="titulo" name="titulo" required>
      <button type="submit">Adicionar</button>
    </form>
    <p role="status" aria-live="polite">0 tarefas pendentes</p>
  </main>
  <footer><small>Curso de Engenharia de Software</small></footer>
</body>
</html>
```

## Exercício
1. Reescreva um trecho feito só com `div`s usando tags semânticas.
2. Navegue pela página só com o teclado e corrija o que não receber foco.
3. Rode o Lighthouse (aba Accessibility) e corrija dois problemas apontados.

## Checklist
- [ ] Uso tags semânticas em vez de `div` para tudo
- [ ] Associo `label` a cada campo
- [ ] Sei verificar contraste e navegação por teclado
