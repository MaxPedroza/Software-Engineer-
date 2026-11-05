# Aula 1 — Como funcionam os LLMs (visão prática)

**Duração:** ~20 min · **Módulo 22**

## Objetivo
Entender o suficiente sobre LLMs para usá-los com critério.

## Teoria
- **LLM** (*Large Language Model*): rede neural (arquitetura **Transformer**) treinada para prever o **próximo token** dado o contexto.
- **Token**: pedaço de texto (palavra, sílaba, símbolo). Custo e limites são medidos em tokens.
- **Janela de contexto**: máximo de tokens (entrada + saída) que o modelo considera de uma vez. O que não está no contexto, o modelo "não sabe".
- **Treinamento**: pré-treino em grande volume de texto/código → ajuste fino (*instruction tuning*) → alinhamento (RLHF e afins).
- **Geração**: o modelo produz uma distribuição de probabilidades e amostra o próximo token.
  - `temperature`: baixa = mais determinístico; alta = mais variado.
  - `top_p`: limita a amostragem aos tokens mais prováveis.
- **Não é um banco de dados nem um verificador**: produz texto **plausível**, não necessariamente verdadeiro (alucinações). Conhecimento tem data de corte.
- Capacidades úteis: gerar/explicar código, resumir, transformar formatos, classificar. Fraquezas: aritmética exata, fatos recentes, raciocínio longo sem verificação.

## Exemplo: contando tokens
```python
import tiktoken  # pip install tiktoken

enc = tiktoken.get_encoding("cl100k_base")
texto = "Engenharia de software é divertida!"
tokens = enc.encode(texto)
print(len(texto), "caracteres ->", len(tokens), "tokens")
print([enc.decode([t]) for t in tokens])
```
Cada fornecedor usa tokenizadores distintos; a contagem é aproximada para outros modelos.

## Exercício
1. Conte os tokens de um mesmo texto em português e em inglês. Qual usa mais?
2. Estime o custo de 1.000 chamadas com 2.000 tokens de entrada e 500 de saída, usando o preço atual do fornecedor.
3. Explique por que um LLM pode "inventar" uma função inexistente de uma biblioteca.

## Checklist
- [ ] Explico token, contexto e temperatura
- [ ] Sei que LLM prevê texto plausível
- [ ] Conheço as limitações básicas
