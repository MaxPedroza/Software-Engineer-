# Aula 1 — Fundamentos de cloud (IaaS, PaaS, SaaS) e modelo de responsabilidade

**Duração:** ~20 min · **Módulo 19**

## Objetivo
Distinguir os modelos de serviço em nuvem e saber quem é responsável por quê.

## Teoria
- **Cloud**: recursos sob demanda, pagos por uso, com elasticidade e autoatendimento via API.
- **IaaS** (EC2, Compute Engine): você gerencia VM, SO e acima. **PaaS** (App Service, Cloud Run, Heroku): você gerencia só código e dados. **SaaS** (Gmail, GitHub): você apenas usa.
- Modelos de implantação: pública, privada, híbrida, multicloud.
- **Regiões** e **zonas de disponibilidade (AZs)**: distribua em ≥2 AZs para alta disponibilidade; várias regiões para recuperação de desastres e latência.

### Modelo de responsabilidade compartilhada
| Camada | IaaS | PaaS | SaaS |
|--------|------|------|------|
| Dados, identidades, configuração | Você | Você | Você (parcial) |
| Aplicação | Você | Você | Provedor |
| SO e runtime | Você | Provedor | Provedor |
| Hardware, datacenter, rede física | Provedor | Provedor | Provedor |

O provedor é responsável pela segurança **da** nuvem; você, pela segurança **na** nuvem (ex.: bucket público por engano é culpa sua).

## Exemplo: criar recursos via API/CLI
```bash
aws configure                       # credenciais de um usuário/role restrito
aws ec2 describe-regions --query "Regions[].RegionName" --output text
aws s3 mb s3://meu-app-exemplo-12345 --region sa-east-1
aws s3api put-public-access-block --bucket meu-app-exemplo-12345 \
  --public-access-block-configuration BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true
```

## Exercício
1. Classifique em IaaS/PaaS/SaaS: PostgreSQL em VM, RDS, Cloud Run, Slack, Kubernetes gerenciado (justifique).
2. Liste 3 itens de segurança que continuam sendo sua responsabilidade num PaaS.

## Checklist
- [ ] Diferencio IaaS, PaaS e SaaS
- [ ] Explico regiões e AZs
- [ ] Conheço o modelo de responsabilidade compartilhada
