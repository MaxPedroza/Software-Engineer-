# Aula 5 — React: componentes, props e estado

**Duração:** ~25 min · **Módulo 14**

## Objetivo
Construir interfaces declarativas com componentes React, props e estado local.

## Teoria
- **React** é uma biblioteca para UI declarativa: você descreve *como a tela deve ser* para um estado, e o React atualiza o DOM.
- **Componente**: função que recebe **props** (somente leitura) e retorna **JSX**.
- **Estado** (`useState`): dado que muda ao longo do tempo e dispara nova renderização. Nunca altere o estado diretamente; crie um novo valor (imutabilidade).
- **Listas** exigem `key` estável e única (use o id, não o índice).
- **Elevar o estado** (lifting state up): o estado fica no ancestral comum e desce via props; filhos avisam via callbacks.
- Fluxo de dados é **unidirecional** (pai → filho).
- Criar projeto: `npm create vite@latest tarefas -- --template react-ts`.

## Exemplo
```tsx
import { useState } from 'react';

type Tarefa = { id: number; titulo: string; feita: boolean };

function Item({ tarefa, onAlternar }: { tarefa: Tarefa; onAlternar: (id: number) => void }) {
  return (
    <li>
      <label>
        <input type="checkbox" checked={tarefa.feita} onChange={() => onAlternar(tarefa.id)} />
        {tarefa.titulo}
      </label>
    </li>
  );
}

export default function App() {
  const [tarefas, setTarefas] = useState<Tarefa[]>([]);
  const [titulo, setTitulo] = useState('');

  function adicionar(e: React.FormEvent) {
    e.preventDefault();
    if (!titulo.trim()) return;
    setTarefas([...tarefas, { id: Date.now(), titulo, feita: false }]);
    setTitulo('');
  }

  function alternar(id: number) {
    setTarefas(tarefas.map(t => (t.id === id ? { ...t, feita: !t.feita } : t)));
  }

  return (
    <main>
      <h1>Tarefas</h1>
      <form onSubmit={adicionar}>
        <input value={titulo} onChange={e => setTitulo(e.target.value)} aria-label="Nova tarefa" />
        <button>Adicionar</button>
      </form>
      <ul>{tarefas.map(t => <Item key={t.id} tarefa={t} onAlternar={alternar} />)}</ul>
    </main>
  );
}
```

## Exercício
1. Adicione um botão para remover tarefas (use `filter`).
2. Mostre um contador de tarefas pendentes derivado do estado (sem criar outro estado).
3. Extraia o formulário para um componente `NovaTarefa` com a prop `onAdicionar`.

## Checklist
- [ ] Crio componentes e passo props tipadas
- [ ] Atualizo estado de forma imutável
- [ ] Uso `key` corretamente em listas
