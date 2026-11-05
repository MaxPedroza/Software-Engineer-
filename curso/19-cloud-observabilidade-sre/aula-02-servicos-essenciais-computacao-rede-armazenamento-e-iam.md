# Aula 2 — Serviços essenciais: computação, rede, armazenamento e IAM

**Duração:** ~25 min · **Módulo 19**

## Objetivo
Conhecer os blocos básicos de qualquer nuvem e aplicar o princípio do menor privilégio.

## Teoria
- **Computação**: VMs (EC2), containers gerenciados (ECS/EKS/Cloud Run), auto scaling groups.
- **Rede**: **VPC** com sub-redes públicas e privadas, tabelas de rotas, **security groups** (firewall com estado), NAT, load balancer, DNS (Route 53). Banco fica em sub-rede privada.
- **Armazenamento**: **objetos** (S3: barato, durável, ilimitado), **blocos** (EBS: discos de VM), **arquivos** (EFS) e **bancos gerenciados** (RDS, DynamoDB).
- **IAM**: quem (usuário, grupo, **role**) pode fazer o quê (policy) em qual recurso. Regras: **menor privilégio**, MFA, roles temporárias em vez de chaves fixas, nunca usar a conta root no dia a dia.

## Exemplo: política IAM de menor privilégio e security group
```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": ["s3:GetObject", "s3:PutObject"],
    "Resource": "arn:aws:s3:::meu-app-artefatos/uploads/*"
  }]
}
```
```hcl
resource "aws_security_group" "api" {
  name   = "api-sg"
  vpc_id = aws_vpc.main.id

  ingress {
    from_port       = 8000
    to_port         = 8000
    protocol        = "tcp"
    security_groups = [aws_security_group.alb.id]  # só o load balancer
  }
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```

## Exercício
1. Desenhe uma VPC com 2 AZs: ALB em sub-redes públicas, API e banco em privadas.
2. Escreva uma policy que permita à API apenas ler de um prefixo de um bucket. Por que não usar `"Action": "*"`?

## Checklist
- [ ] Conheço computação, rede, storage e IAM
- [ ] Separo sub-redes públicas e privadas
- [ ] Aplico menor privilégio
