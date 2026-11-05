# Aula 8 — Segurança da cadeia de suprimentos (dependências, SBOM)

**Duração:** ~20 min · **Módulo 20**

## Objetivo
Reduzir riscos vindos de dependências, build e artefatos de terceiros.

## Teoria
Seu software é, em grande parte, código de terceiros. Ataques comuns:
- **Dependência vulnerável** (ex.: Log4Shell).
- **Typosquatting** e **dependency confusion**: pacotes com nome parecido ou pacote público que substitui um interno.
- **Conta de mantenedor comprometida** ou pacote malicioso publicado.
- **Pipeline/CI comprometido** (ex.: SolarWinds).

### Defesas
- **Lockfiles** (`package-lock.json`, `poetry.lock`) e versões fixas; instalação reprodutível (`npm ci`).
- **SCA** (Software Composition Analysis): Dependabot, `npm audit`, `pip-audit`, OSV-Scanner, Trivy.
- **SBOM** (*Software Bill of Materials*): inventário de componentes em formato CycloneDX ou SPDX.
- **Assinatura e proveniência**: Sigstore/cosign, SLSA.
- Menos dependências; revisar as novas; escopos de registry privados; imagens base mínimas e fixadas por *digest*.
- Segredos do CI com escopo mínimo; revisão obrigatória de alterações em workflows.

## Comandos
```bash
npm ci && npm audit --audit-level=high
pip install pip-audit && pip-audit -r requirements.txt
trivy fs --format cyclonedx --output sbom.json .   # gera SBOM
trivy sbom sbom.json                               # busca CVEs no SBOM
```

```yaml
# .github/dependabot.yml
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule: { interval: "weekly" }
```

## Exercício
1. Gere o SBOM do seu projeto e conte as dependências (diretas e transitivas).
2. Rode o auditor e trate uma vulnerabilidade (atualizar, substituir ou justificar).

## Checklist
- [ ] Uso lockfile e instalação reprodutível
- [ ] Tenho varredura automática de dependências
- [ ] Sei gerar e interpretar um SBOM
