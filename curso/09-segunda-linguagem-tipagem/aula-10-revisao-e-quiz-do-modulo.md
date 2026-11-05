# Aula 10 — Revisão e quiz do módulo

**Duração:** ~25 min · **Módulo 9**

## Resumo
- Aprender várias linguagens amplia repertório; os conceitos se transferem.
- **Tipagem**: estática vs dinâmica (quando checa) e forte vs fraca (conversões).
- **TypeScript**: tipos básicos, inferência, `unknown` em vez de `any`, `strict: true`.
- **Interfaces/types/enums**: tipagem estrutural, uniões discriminadas.
- **Generics**: reutilização com segurança de tipos.
- **Tooling**: módulos ES, npm, `tsconfig`, ESLint, Prettier.
- **Assíncrono**: callbacks → Promises → `async/await`; `Promise.all`.
- **Memória**: stack/heap, GC por alcançabilidade, vazamentos lógicos.
- **Comparação**: escolha pela necessidade, ecossistema e equipe.

## Quiz
1. Qual a diferença entre tipagem estática e dinâmica?
2. `"1" + 1` em Python e em JavaScript: o que acontece e por quê?
3. Por que preferir `unknown` a `any`?
4. Quando usar `interface` e quando usar `type`?
5. O que é tipagem estrutural?
6. O que faz `T extends { id: number }` em um generic?
7. Qual a função do `tsconfig.json`?
8. O que `await` faz e o que `Promise.all` oferece?
9. Como o GC decide o que liberar?
10. Cite uma situação ideal para Go e uma para Python.

## Gabarito resumido
1. Estática checa em compilação; dinâmica checa em execução.
2. Python lança `TypeError` (forte); JS resulta em `"11"` (fraca).
3. `unknown` obriga a checar o tipo antes de usar; `any` desliga a verificação.
4. `interface` para contratos de objetos/classes; `type` para uniões, tuplas e aliases.
5. Compatibilidade depende da forma do valor, não do nome do tipo.
6. Restringe `T` a tipos que tenham a propriedade numérica `id`.
7. Configura o compilador: alvo, módulos, diretórios e rigor (`strict`).
8. `await` pausa a função até a Promise resolver; `Promise.all` roda várias em paralelo.
9. Libera objetos inalcançáveis a partir das raízes.
10. Go: microsserviço/CLI concorrente; Python: análise de dados ou automação.

## Entregável do módulo
Reescreva o núcleo do sistema de tarefas em TypeScript (`strict: true`): interfaces, `Repositorio<T>` genérico, funções assíncronas de persistência, ESLint + Prettier, build para `dist/` com `.d.ts` e instalação local via `npm link`.

## Checklist final
- [ ] Respondi o quiz sem consulta
- [ ] Projeto compila sem erros em modo estrito
- [ ] Nenhum `any` no código
- [ ] Biblioteca publicada localmente com `npm link`
- [ ] README com instruções de uso
