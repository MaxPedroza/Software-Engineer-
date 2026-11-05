# Aula 10 — Revisão e quiz do módulo

**Duração:** ~25 min · **Módulo 22**

## Resumo
- **LLMs** preveem o próximo token; geram texto plausível, com janela de contexto e custo por token.
- **Assistentes** (inline, chat, agente) dependem de bom contexto; você é responsável pelo resultado.
- **Prompts** eficazes: contexto, tarefa, restrições, exemplos, formato e critérios de aceite.
- **Revisão crítica**: dependências inexistentes, segurança, casos-limite, testes que realmente falham.
- **Testes, docs e refatoração**: passos pequenos, com testes de caracterização.
- **Agentes**: LLM + ferramentas em laço; menor privilégio, sandbox, humano no circuito.
- **Integração**: valide saída, trate erros e custo; chave no servidor; streaming para latência.
- **RAG**: embeddings + busca vetorial + prompt com contexto e citações.
- **Riscos**: alucinação, prompt injection, vazamento, licenças, ética e LGPD.

## Quiz
1. O que é um token e por que importa?
2. O que a `temperature` controla?
3. Cite dois elementos de um bom prompt de código.
4. Por que devemos verificar se os pacotes sugeridos pela IA existem?
5. Por que escrever testes de caracterização antes de refatorar com IA?
6. O que caracteriza um agente de código?
7. Por que validar a saída JSON de um LLM com um schema?
8. Para que serve o RAG?
9. Como se reduz o risco de prompt injection?
10. Que cuidados tomar com dados pessoais ao usar APIs de LLM?

## Gabarito resumido
1. Unidade de texto processada; define custo e limite de contexto.
2. A aleatoriedade/variedade da geração.
3. Ex.: contexto/stack, restrições, exemplos, formato de saída, critérios de aceite.
4. Podem ser alucinações ou pacotes maliciosos registrados com nomes inventados.
5. Garantem que o comportamento foi preservado a cada passo.
6. LLM em laço com ferramentas, agindo e observando resultados.
7. A saída pode vir malformada ou incorreta; o schema evita falhas e usos inseguros.
8. Fundamentar respostas em documentos recuperados, reduzindo alucinações e usando dados próprios.
9. Separar dados de instruções, menor privilégio, allowlist de ações, filtros e confirmação humana.
10. Minimizar/mascarar, base legal e transparência (LGPD), contratos e retenção adequados.

## Entregável do módulo
**Funcionalidade com IA** no sistema (ex.: resumo e sugestão de tarefas) com guardrails, **testes de avaliação** (≥ 10 casos, incluindo injeção) e **documento de riscos**.

## Checklist final
- [ ] Acertei ao menos 8 de 10 no quiz
- [ ] Recurso com LLM funcionando com guardrails
- [ ] Testes de avaliação automatizados
- [ ] Documento de riscos concluído
