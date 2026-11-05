# Aula 10 — Revisão e quiz do módulo

**Duração:** ~25 min · **Módulo 20**

## Resumo
- **CIA**, menor privilégio, defesa em profundidade e fail closed guiam o design.
- **OWASP Top 10**: Broken Access Control lidera; valide autorização no servidor.
- **Injeção/XSS/CSRF/SSRF**: parametrize, escape, tokens/SameSite, allowlist.
- **Criptografia**: hash (integridade), AES-GCM (sigilo), assinaturas (autenticidade); nunca crie a sua.
- **Senhas**: Argon2id/bcrypt com salt; segredos em cofres, nunca no Git.
- **MFA/passkeys** reduzem fortemente o risco de contas.
- **STRIDE** estrutura o modelo de ameaças.
- **Supply chain**: lockfile, SCA, SBOM, assinatura.
- **DevSecOps**: SAST, DAST, SCA e secret scanning no pipeline; **LGPD** exige minimização e transparência.

## Quiz
1. O que significa a sigla CIA?
2. Por que "fail closed" é preferível?
3. Qual a defesa principal contra SQL Injection?
4. Qual diferença entre XSS e CSRF?
5. Por que SHA-256 puro não serve para armazenar senhas?
6. Qual a vantagem de AES-GCM sobre AES-CBC sem MAC?
7. Por que passkeys resistem a phishing?
8. O que cada letra de STRIDE representa?
9. O que é um SBOM e para que serve?
10. Qual a diferença entre SAST e DAST?

## Gabarito resumido
1. Confidencialidade, Integridade, Disponibilidade.
2. Em caso de erro, o acesso é negado, evitando exposição.
3. Queries parametrizadas.
4. XSS executa script na vítima; CSRF força ações autenticadas sem ela perceber.
5. É rápido demais, facilitando força bruta; falta custo e salt.
6. Fornece autenticação e integridade (AEAD).
7. A credencial é vinculada ao domínio e a chave privada nunca é enviada.
8. Spoofing, Tampering, Repudiation, Information disclosure, DoS, Elevation of privilege.
9. Inventário de componentes; permite localizar CVEs.
10. SAST analisa o código estático; DAST testa a aplicação em execução.

## Entregável do módulo
**Modelo de ameaças** (DFD + tabela STRIDE) e **relatório de correções** do projeto: vulnerabilidade, severidade, correção aplicada, evidência (teste ou varredura) e pipeline com varredura ativa.

## Checklist final
- [ ] Acertei ao menos 8 de 10 no quiz
- [ ] Modelo de ameaças concluído
- [ ] Vulnerabilidades corrigidas e documentadas
- [ ] Varredura de segurança no pipeline
