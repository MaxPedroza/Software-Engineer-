# Aula 2 — CSS: layout, Flexbox e Grid

**Duração:** ~20 min · **Módulo 14**

## Objetivo
Dominar o modelo de caixa e montar layouts com Flexbox e Grid.

## Teoria
- **Box model**: content + padding + border + margin. Use `box-sizing: border-box` para que `width` inclua padding e borda.
- **Cascata e especificidade**: inline > id > classe/atributo > elemento. Prefira classes simples (ex.: BEM) e evite `!important`.
- **Variáveis CSS**: `--cor: #0a7;` e `var(--cor)`.
- **Flexbox**: layout **unidimensional** (linha ou coluna). Propriedades: `display:flex`, `flex-direction`, `justify-content` (eixo principal), `align-items` (eixo cruzado), `gap`, `flex: 1`.
- **Grid**: layout **bidimensional** (linhas e colunas). `grid-template-columns`, `gap`, `fr`, `repeat()`, `minmax()`, `grid-template-areas`.
- Regra prática: Flexbox para componentes (barra, cartão); Grid para a estrutura da página.

## Exemplo
```css
:root { --cor: #0a7; --espaco: 1rem; }
*, *::before, *::after { box-sizing: border-box; }

.barra {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: var(--espaco);
}

.pagina {
  display: grid;
  grid-template-columns: 240px 1fr;
  grid-template-areas:
    "topo topo"
    "menu conteudo";
  min-height: 100vh;
}
.topo { grid-area: topo; background: var(--cor); }
.menu { grid-area: menu; }
.conteudo { grid-area: conteudo; }

.cartoes {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
  gap: var(--espaco);
}
```

## Exercício
1. Monte uma barra de navegação com logo à esquerda e links à direita usando Flexbox.
2. Crie uma grade de cartões de tarefas que se ajuste sozinha ao tamanho da tela.
3. Centralize um elemento na tela com Grid (`place-items: center`).

## Checklist
- [ ] Entendo o box model e `border-box`
- [ ] Sei quando usar Flexbox e quando usar Grid
- [ ] Uso variáveis CSS
