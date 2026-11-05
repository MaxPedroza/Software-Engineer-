# Aula 9 — Armazenamento de arquivos e objetos (S3), backups e retenção

**Duração:** ~25 min · **Módulo 11**

## Objetivo
Guardar arquivos em object storage e planejar backups com retenção e restauração testada.

## Teoria
- **Object storage** (Amazon S3, GCS, MinIO): objetos identificados por chave em **buckets**, acessados via HTTP. Escala quase infinita, durabilidade altíssima, mas sem edição parcial nem sistema de arquivos real.
- Não guarde arquivos grandes no banco: guarde no S3 e salve só a **chave/URL** no banco.
- **URLs pré-assinadas** permitem upload/download direto com prazo de expiração, sem expor credenciais.
- Recursos: versionamento, *lifecycle* (mover para classes frias, expirar), criptografia em repouso, buckets privados por padrão.

### Backups
- **Regra 3-2-1**: 3 cópias, 2 mídias diferentes, 1 fora do local.
- Defina **RPO** (quanto dado se aceita perder) e **RTO** (quanto tempo para voltar).
- Tipos: completo, incremental, e *point-in-time recovery* (WAL).
- **Retenção**: ex. diários por 7 dias, semanais por 4 semanas, mensais por 12 meses (respeitando LGPD).
- Backup que nunca foi restaurado **não é backup**.

## Exemplo (MinIO/S3 com boto3)
```python
import boto3
s3 = boto3.client("s3", endpoint_url="http://localhost:9000",
                  aws_access_key_id="minio", aws_secret_access_key="minio12345")
s3.upload_file("relatorio.pdf", "anexos", "tarefa-1/relatorio.pdf")
url = s3.generate_presigned_url("get_object",
        Params={"Bucket": "anexos", "Key": "tarefa-1/relatorio.pdf"}, ExpiresIn=300)
print(url)
```
```bash
pg_dump -Fc tarefas > backup-$(date +%F).dump
pg_restore -d tarefas_teste backup-2026-01-01.dump
```

## Exercício
1. Suba o MinIO, envie um arquivo e gere uma URL válida por 5 minutos.
2. Escreva uma política de backup (RPO, RTO, retenção) para o projeto e teste uma restauração.

## Checklist
- [ ] Sei por que arquivos vão para object storage
- [ ] Conheço RPO, RTO e a regra 3-2-1
- [ ] Já testei uma restauração
