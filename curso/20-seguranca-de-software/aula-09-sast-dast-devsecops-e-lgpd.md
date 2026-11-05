# Aula 9 — SAST, DAST, DevSecOps e LGPD/privacidade

**Duração:** ~25 min · **Módulo 20**

## Objetivo
Automatizar verificações de segurança no pipeline e respeitar a privacidade de dados.

## Teoria
### Ferramentas de varredura
- **SAST**: analisa o código-fonte sem executar (CodeQL, Semgrep, Bandit). Rápido, mas gera falsos positivos.
- **DAST**: ataca a aplicação em execução (OWASP ZAP). Encontra problemas de configuração e runtime.
- **SCA**: dependências. **Secret scanning**: segredos. **IaC/Container scan**: Trivy, Checkov.
- **DevSecOps** = *shift left*: segurança em cada commit, não só no fim.

### LGPD (Lei 13.709/2018)
- **Dado pessoal** identifica alguém; **dado sensível** (saúde, biometria, religião…) exige mais cuidado.
- Princípios: finalidade, necessidade (**minimização**), transparência, segurança, prevenção.
- Bases legais: consentimento, obrigação legal, execução de contrato, legítimo interesse etc.
- Direitos do titular: acesso, correção, anonimização, portabilidade, eliminação.
- Incidentes: comunicar à ANPD e aos titulares. Prática: *privacy by design*, pseudonimização, criptografia, retenção limitada.

## Pipeline
```yaml
name: seguranca
on: [pull_request]
jobs:
  scan:
    runs-on: ubuntu-latest
    permissions: { contents: read, security-events: write }
    steps:
      - uses: actions/checkout@v4
      - uses: github/codeql-action/init@v3
        with: { languages: python }
      - uses: github/codeql-action/analyze@v3
      - run: pip install pip-audit bandit && pip-audit -r requirements.txt && bandit -r src
```

## Exercício
1. Adicione o workflow ao projeto e corrija um achado.
2. Liste os dados pessoais do seu sistema, a finalidade de cada um e o prazo de retenção; remova o que for desnecessário.

## Checklist
- [ ] Distingo SAST, DAST e SCA
- [ ] Pipeline roda varredura a cada PR
- [ ] Apliquei minimização de dados (LGPD)
