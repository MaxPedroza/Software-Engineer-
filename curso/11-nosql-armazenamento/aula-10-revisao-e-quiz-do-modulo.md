# Aula 10 — Revisão e quiz do módulo

**Duração:** ~30 min · **Módulo 11**

## Resumo
- NoSQL resolve limites específicos do relacional: escala, flexibilidade e padrões de acesso especiais.
- **Documento** (MongoDB): agregados flexíveis; **chave-valor** (Redis): cache com TTL e cache-aside.
- **Colunar/séries**: analytics e métricas; **grafo**: relacionamentos profundos; **busca**: índice invertido.
- **CAP**: na partição, escolha entre consistência e disponibilidade; consistência eventual e quórum.
- **ORMs** aumentam produtividade, mas exigem atenção a N+1.
- **S3** para arquivos; backups seguem 3-2-1, RPO/RTO e restauração testada.

## Quiz
1. Cite dois limites do modelo relacional que motivaram o NoSQL.
2. Quando embutir documentos em vez de referenciar no MongoDB?
3. O que é cache-aside?
4. Para que serve o TTL no Redis?
5. Por que bancos colunares são bons para analytics?
6. Qual consulta é mais natural em um grafo que em SQL?
7. O que é um índice invertido?
8. O que o CAP diz sobre partições de rede?
9. O que é o problema N+1 e como corrigi-lo?
10. O que significam RPO e RTO?

## Gabarito resumido
1. Escala horizontal de escrita e esquema rígido/impedância objeto-relacional.
2. Dados lidos juntos, de tamanho limitado e sem compartilhamento.
3. Ler do cache; em miss, ler do banco, gravar no cache e devolver.
4. Expirar chaves automaticamente, limitando dados velhos e memória.
5. Leem só as colunas necessárias e comprimem bem.
6. Caminhos de múltiplos saltos (amigos de amigos, menor caminho).
7. Mapa termo → documentos que o contêm.
8. Na partição, é preciso sacrificar consistência ou disponibilidade.
9. Uma query extra por item; use eager loading/join.
10. RPO: perda de dados tolerada; RTO: tempo máximo para restaurar.

## Entregável do módulo
Documento de decisão (ADR) justificando cada tecnologia de armazenamento escolhida (PostgreSQL, Redis para cache, índice de busca, S3 para anexos), com contexto, alternativas, decisão e consequências. Inclua o cache Redis e a busca full-text nas tarefas.

## Checklist final
- [ ] Respondi o quiz sem consultar o material
- [ ] Cache Redis funcionando no projeto
- [ ] Busca full-text implementada
- [ ] ADR escrito e revisado
