# Aula 8 — RAG, embeddings e bancos vetoriais

**Duração:** ~25 min · **Módulo 22**

## Objetivo
Construir um pipeline RAG simples para responder com base em documentos próprios.

## Teoria
- **Embedding**: vetor numérico que representa o significado de um texto; textos semelhantes ficam **próximos**.
- **Similaridade**: cosseno (mais usada), produto interno, distância euclidiana.
- **Banco vetorial**: armazena vetores e faz busca por vizinhos mais próximos (ANN): pgvector, Chroma, Qdrant, FAISS, Pinecone.
- **RAG** (*Retrieval-Augmented Generation*): recuperar trechos relevantes e incluí-los no prompt para reduzir alucinações e usar dados atualizados/privados.

### Pipeline
1. **Ingestão**: carregar, limpar e dividir em *chunks* (ex.: 500 tokens, com sobreposição).
2. **Indexação**: gerar embeddings e guardar com metadados (fonte, página).
3. **Recuperação**: embedding da pergunta → top-k chunks.
4. **Geração**: prompt com os trechos + instrução "responda só com base no contexto; se não houver, diga que não sabe"; cite as fontes.
5. **Avaliação**: perguntas de teste, acerto da recuperação (recall@k), fidelidade da resposta.

Cuidados: controle de acesso por documento, injeção de prompt em documentos, chunking ruim.

## Exemplo mínimo
```python
import numpy as np
from openai import OpenAI

client = OpenAI()
docs = ["Reembolsos levam até 7 dias úteis.", "O suporte atende de 9h às 18h.",
        "Senhas são trocadas em Configurações > Segurança."]

def embed(textos):
    r = client.embeddings.create(model="text-embedding-3-small", input=textos)
    return np.array([d.embedding for d in r.data])

E = embed(docs)

def buscar(pergunta, k=2):
    q = embed([pergunta])[0]
    sims = E @ q / (np.linalg.norm(E, axis=1) * np.linalg.norm(q))
    return [docs[i] for i in sims.argsort()[::-1][:k]]

def responder(pergunta):
    contexto = "\n".join(buscar(pergunta))
    prompt = (f"Responda só com base no contexto. Se não souber, diga 'não sei'.\n"
              f"Contexto:\n{contexto}\n\nPergunta: {pergunta}")
    r = client.chat.completions.create(model="gpt-4o-mini", temperature=0,
        messages=[{"role": "user", "content": prompt}])
    return r.choices[0].message.content

print(responder("Quanto tempo demora o reembolso?"))
```

## Exercício
1. Indexe a documentação do seu projeto e crie 10 perguntas de teste com a resposta esperada.
2. Varie o tamanho do chunk e o `k`; meça o acerto da recuperação.

## Checklist
- [ ] Explico embeddings e similaridade
- [ ] Implemento recuperação + geração
- [ ] Avalio com perguntas de teste
