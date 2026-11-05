# Aula 10 — Revisão e quiz do módulo

**Duração:** ~25 min · **Módulo 8**

## Resumo
- **Paradigmas**: imperativo, POO, funcional e declarativo; escolha conforme o problema.
- **POO**: classes, objetos e encapsulamento mantêm o estado válido.
- **Herança/polimorfismo/abstração**: interfaces comuns, comportamentos distintos.
- **Composição** costuma vencer herança: menos acoplamento, mais testabilidade.
- **Funcional**: funções puras, imutabilidade, `map`/`filter`/`reduce`.
- **SOLID**: SRP, OCP, LSP, ISP, DIP.
- **Clean Code**: nomes que revelam intenção, funções pequenas, comentários do porquê.
- **Refatoração** com testes; **erros** com exceções específicas e contratos.

## Quiz
1. Cite dois paradigmas e um caso de uso de cada.
2. Para que serve o encapsulamento?
3. O que é polimorfismo?
4. Quando preferir composição a herança?
5. O que define uma função pura?
6. O que diz o princípio Aberto/Fechado?
7. Por que `Quadrado(Retangulo)` pode violar Liskov?
8. Qual a diferença entre comentar "o quê" e "o porquê"?
9. O que é um code smell e o que é refatorar?
10. Qual a diferença entre pré-condição e invariante?

## Gabarito resumido
1. Ex.: POO para entidades de domínio; funcional para transformar dados.
2. Proteger o estado interno e expor uma interface mínima.
3. Mesma interface, comportamentos diferentes conforme o tipo concreto.
4. Quando a relação é "tem um" ou o comportamento precisa ser trocável.
5. Mesma entrada → mesma saída, sem efeitos colaterais.
6. Estender comportamento sem modificar o código existente.
7. Alterar largura/altura em conjunto quebra o contrato esperado de `Retangulo`.
8. O "quê" deve estar no código; o comentário explica a razão da decisão.
9. Smell: sinal de design ruim; refatorar: melhorar a estrutura sem mudar o comportamento.
10. Pré-condição: exigida do chamador antes da chamada; invariante: vale sempre para o objeto.

## Entregável do módulo
Refatore a CLI de tarefas em classes (`Tarefa`, `RepositorioTarefas`, `ServicoTarefas`, `CLI`) aplicando SOLID, com exceções de domínio e testes. Inclua um documento explicando cada decisão de design.

## Checklist final
- [ ] Respondi o quiz sem consulta
- [ ] CLI refatorada com responsabilidades separadas
- [ ] Dependências injetadas via abstrações
- [ ] Testes passando após a refatoração
- [ ] Decisões de design documentadas
