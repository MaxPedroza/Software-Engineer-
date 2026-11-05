# Aula 4 — Interfaces, types e enums

**Duração:** ~25 min · **Módulo 9**

## Objetivo
Modelar a forma dos dados com `interface`, `type` e `enum`.

## Teoria
- **`interface`**: descreve a forma de objetos; pode ser estendida (`extends`) e implementada por classes.
- **`type`** (alias): nomeia qualquer tipo — uniões, interseções, tuplas, funções.
- Regra prática: `interface` para contratos de objetos/classes; `type` para uniões e composições.
- **Tipagem estrutural**: compatibilidade depende da forma, não do nome (duck typing checado).
- Propriedades `?` (opcionais) e `readonly` (imutáveis).
- **`enum`**: conjunto nomeado de constantes. Muitas equipes preferem uniões de literais (`"a" | "b"`) por gerarem menos código JS.
- **Uniões discriminadas**: campo comum (`tipo`) permite *narrowing* seguro.

## Exemplo
```typescript
enum Prioridade { Baixa = 1, Media, Alta }

interface Tarefa {
  readonly id: number;
  titulo: string;
  prioridade: Prioridade;
  descricao?: string;
}

interface Repositorio {
  salvar(t: Tarefa): void;
}

class RepoMemoria implements Repositorio {
  private itens: Tarefa[] = [];
  salvar(t: Tarefa): void { this.itens.push(t); }
}

type Resultado =
  | { tipo: "ok"; valor: Tarefa }
  | { tipo: "erro"; mensagem: string };

function mostrar(r: Resultado): string {
  return r.tipo === "ok" ? r.valor.titulo : `Erro: ${r.mensagem}`;
}

new RepoMemoria().salvar({ id: 1, titulo: "Estudar TS", prioridade: Prioridade.Alta });
```

## Exercício
1. Crie a interface `Usuario` com `id`, `nome` e `email?` e uma função que recebe um `Usuario`.
2. Converta o `enum Prioridade` em união de literais e compare.
3. Modele `Pagamento` como união discriminada (`pix` | `cartao`) com campos distintos.

## Checklist
- [ ] Sei quando usar `interface` e `type`
- [ ] Uso `readonly` e propriedades opcionais
- [ ] Modelo uniões discriminadas
