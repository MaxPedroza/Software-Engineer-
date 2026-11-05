# Aula 10 — Revisão e quiz do módulo

**Duração:** ~30 min · **Módulo 13**

## Resumo
- O backend concentra regras de negócio, persistência e segurança; é *stateless* para escalar.
- **REST**: recursos no plural, métodos e status corretos, idempotência.
- **Validação** na borda (Pydantic), modelos de saída e erros padronizados (RFC 9457).
- **Autenticação**: hash argon2/bcrypt, sessões e cookies seguros. **Autorização**: RBAC/dono, JWT com expiração; OAuth2 delega acesso e OIDC traz identidade.
- **Paginação por cursor**, filtros, versionamento e `Idempotency-Key`.
- **OpenAPI** documenta o contrato (`/docs`).
- **GraphQL** e **gRPC** são alternativas ao REST para casos específicos.
- **Jobs e filas** tiram trabalho lento da requisição; **webhooks** exigem assinatura HMAC.

## Quiz
1. Por que o backend precisa validar mesmo que o frontend valide?
2. Qual status usar ao criar um recurso? E ao remover sem retorno de corpo?
3. Qual a diferença entre 401 e 403?
4. Por que não usar SHA-256 simples para senhas?
5. O que um JWT contém e ele é criptografado?
6. Qual a diferença entre OAuth2 e OIDC?
7. Vantagem da paginação por cursor sobre offset?
8. Para que serve o `Idempotency-Key`?
9. O que é gerado automaticamente pelo FastAPI para documentação?
10. Por que verificar a assinatura HMAC num webhook?

## Gabarito resumido
1. O cliente pode ser contornado; o servidor é a fronteira confiável.
2. 201 (com `Location`); 204.
3. 401: não autenticado; 403: autenticado, sem permissão.
4. É rápido demais, facilitando força bruta; use argon2/bcrypt com salt.
5. Claims (`sub`, `exp`...); é apenas assinado, não criptografado.
6. OAuth2 delega acesso a recursos; OIDC adiciona autenticação/identidade.
7. Desempenho estável e resultados consistentes com inserções.
8. Evitar efeitos duplicados em retentativas de POST.
9. OpenAPI (`/openapi.json`), Swagger UI (`/docs`) e ReDoc (`/redoc`).
10. Garantir que a chamada vem de quem detém o segredo e não foi adulterada.

## Entregável do módulo
API de tarefas publicada localmente (uvicorn atrás do Nginx) com: login, autorização por usuário (JWT), paginação, validação, documentação OpenAPI e uma coleção de requisições (Postman/Insomnia/`.http`) cobrindo os fluxos principais e erros.

## Checklist final
- [ ] Quiz respondido sem consulta
- [ ] Login e autorização por usuário funcionando
- [ ] `/docs` completo, com erros documentados
- [ ] Coleção de requisições exportada
