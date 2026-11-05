# Aula 3 — Engenharia de prompts para desenvolvimento

**Duração:** ~25 min · **Módulo 22**

## Objetivo
Escrever prompts claros, estruturados e verificáveis para tarefas de código.

## Teoria
Um bom prompt contém:
1. **Papel/contexto** (stack, versão, convenções).
2. **Tarefa** específica e delimitada.
3. **Restrições** (o que não fazer, bibliotecas permitidas, estilo).
4. **Exemplos** (*few-shot*) de entrada/saída.
5. **Formato de saída** (código só, JSON, diff).
6. **Critérios de aceite** (testes que devem passar).

### Técnicas
- **Few-shot**: mostre 2–3 exemplos do padrão desejado.
- **Passo a passo / planejar antes**: peça um plano, valide, depois implemente.
- **Iteração**: refine com o erro real (stack trace, saída de teste).
- **Separar instruções de dados** com delimitadores (reduz *prompt injection*).
- Peça para **listar suposições** e dúvidas antes de codar.

## Prompt ruim vs. bom
```text
Ruim:  "faz uma função de desconto"

Bom:
Contexto: Python 3.12, sem dependências externas, type hints.
Tarefa: implemente `aplicar_desconto(preco: Decimal, cupom: str) -> Decimal`.
Regras: "PROMO10" = 10%; "FRETE" = 0%; cupom inválido levanta ValueError;
        o resultado nunca é negativo; arredonde para 2 casas (ROUND_HALF_UP).
Saída: apenas o código da função e 5 testes pytest, incluindo casos-limite.
Antes de codar, liste suposições que você fez.
```

## Exemplo: saída estruturada
```text
Classifique o comentário em: bug | sugestão | elogio.
Responda somente JSON: {"categoria": "...", "confianca": 0-1}
Exemplos:
"O botão não funciona" -> {"categoria":"bug","confianca":0.95}
"Seria legal ter tema escuro" -> {"categoria":"sugestão","confianca":0.9}
Comentário: """{texto_do_usuario}"""
```

## Exercício
1. Reescreva 3 prompts vagos seus usando o checklist de 6 itens e compare os resultados.
2. Crie um prompt reutilizável (template) para "gerar testes de uma função".

## Checklist
- [ ] Incluo contexto, restrições e formato
- [ ] Uso exemplos e critérios de aceite
- [ ] Itero com erros reais
