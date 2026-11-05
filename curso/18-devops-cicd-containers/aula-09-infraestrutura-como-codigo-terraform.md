# Aula 9 — Infraestrutura como Código (Terraform)

**Duração:** ~25 min · **Módulo 18**

## Objetivo
Provisionar infraestrutura de forma declarativa, versionada e repetível com Terraform.

## Teoria
- **IaC**: infraestrutura descrita em arquivos versionados, revisados em PR e aplicados por pipeline. Evita "snowflakes" e *drift*.
- **Terraform** (HCL): **providers** (AWS, GCP, Azure...), **resources**, **variables**, **outputs**, **modules**.
- **State**: arquivo que mapeia código → recursos reais. Use **backend remoto** com lock; nunca commite o state (contém segredos).
- Fluxo: `init` → `fmt`/`validate` → `plan` (revisar) → `apply`. `destroy` remove.
- Declarativo e idempotente: aplicar de novo sem mudanças não altera nada.
- Segredos via variáveis `sensitive`, não no código.

## Exemplo: `main.tf` (bucket S3 na AWS)
```hcl
terraform {
  required_version = ">= 1.6"
  required_providers {
    aws = { source = "hashicorp/aws", version = "~> 5.0" }
  }
}

variable "ambiente" {
  type    = string
  default = "dev"
}

provider "aws" {
  region = "sa-east-1"
}

resource "aws_s3_bucket" "artefatos" {
  bucket = "meu-app-artefatos-${var.ambiente}"
  tags   = { Ambiente = var.ambiente }
}

resource "aws_s3_bucket_versioning" "artefatos" {
  bucket = aws_s3_bucket.artefatos.id
  versioning_configuration { status = "Enabled" }
}

output "bucket_arn" {
  value = aws_s3_bucket.artefatos.arn
}
```
```bash
terraform init
terraform plan -var ambiente=staging -out plano.tfplan
terraform apply plano.tfplan
```
No CI, rode `terraform plan` no PR e `apply` só após o merge.

## Exercício
1. Escreva um módulo/recurso (ex.: provider `docker` ou `local_file`, sem custo) e rode plan/apply/destroy.
2. Altere uma variável, rode `plan` e explique o que será criado/alterado/destruído.

## Checklist
- [ ] Sei o fluxo init/plan/apply
- [ ] Entendo state e backend remoto
- [ ] Não commito state nem segredos
