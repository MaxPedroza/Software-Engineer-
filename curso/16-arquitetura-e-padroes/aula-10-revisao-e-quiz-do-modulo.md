# Aula 10 — Revisão e quiz do módulo

**Duração:** ~20 min · **Módulo 16**

## Resumo
- **Arquitetura** = decisões difíceis de mudar e trade-offs entre atributos de qualidade (cenários mensuráveis).
- **Criacionais**: Factory, Builder, Singleton (com cautela). **Estruturais**: Adapter, Decorator, Facade, Proxy. **Comportamentais**: Strategy, Observer, Command.
- **Hexagonal**: domínio no centro, portas e adaptadores, dependências para dentro.
- **DDD**: linguagem ubíqua, bounded contexts, entidades, objetos de valor, agregados.
- **Monolito modular** como ponto de partida; microsserviços só com motivo claro.
- **EDA, CQRS e Event Sourcing**: eventos, consistência eventual, idempotência.
- **Documentação**: C4 e ADRs versionados.

## Quiz
1. Por que atributos de qualidade devem ser expressos como cenários mensuráveis?
2. Qual problema o padrão Factory resolve?
3. Qual a diferença entre Adapter e Decorator?
4. Quando Strategy é preferível a `if/elif`?
5. O que são portas e adaptadores na arquitetura hexagonal?
6. O que diz a regra da dependência?
7. O que é um agregado e qual o papel da raiz?
8. Cite duas desvantagens dos microsserviços.
9. Por que consumidores de eventos devem ser idempotentes?
10. Qual a função de um ADR e por que não se edita um ADR aceito?

## Gabarito resumido
1. Permitem verificar objetivamente se a arquitetura atende ao requisito.
2. Desacopla o cliente das classes concretas ao centralizar a criação.
3. Adapter converte interfaces incompatíveis; Decorator adiciona comportamento mantendo a mesma interface.
4. Quando há várias variações de algoritmo que mudam ou crescem (aberto/fechado).
5. Portas são interfaces definidas pelo núcleo; adaptadores as implementam com tecnologias concretas.
6. Dependências de código apontam para o domínio (centro), nunca dele para a infraestrutura.
7. Unidade de consistência; a raiz é o único ponto de acesso e protege as invariantes.
8. Complexidade operacional, latência/falhas de rede, consistência eventual, custo.
9. Brokers podem entregar a mesma mensagem mais de uma vez; processar de novo causaria efeitos duplicados.
10. Registrar contexto e razão de uma decisão; mantém o histórico, então se cria um novo ADR que o substitui.

## Entregável do módulo
Documento de arquitetura (`docs/arquitetura.md`) do sistema de tarefas contendo: atributos de qualidade priorizados, diagramas C4 (Contexto e Contêineres), estrutura hexagonal implementada no código (domínio, casos de uso, adaptadores) e ao menos 3 ADRs justificados.

## Checklist final
- [ ] Atributos de qualidade e trade-offs definidos
- [ ] Padrões de projeto aplicados com justificativa
- [ ] Sistema reorganizado em arquitetura hexagonal
- [ ] Diagramas C4 e ADRs versionados
- [ ] Decisão monolito vs microsserviços documentada
