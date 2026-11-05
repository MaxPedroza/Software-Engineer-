# Aula 9 — Gestão de produto, priorização e MVP

**Duração:** ~25 min · **Módulo 21**

## Objetivo
Priorizar o que construir e validar hipóteses com um MVP.

## Teoria
- **Produto** resolve um problema de um usuário gerando valor para o negócio; **output ≠ outcome** (entregar funcionalidades não é gerar resultado).
- **MVP** (Produto Mínimo Viável): a menor versão que permite **aprender** com usuários reais — não é um produto ruim, é um experimento.
- **Descoberta contínua**: hipótese → experimento → métrica → decisão (persistir, pivotar, parar).
- Métricas: ativação, retenção, NPS, conversão; métrica *North Star*.

### Técnicas de priorização
- **MoSCoW**: Must, Should, Could, Won't.
- **RICE** = (Alcance × Impacto × Confiança) / Esforço.
- **Valor × Esforço** (matriz 2×2), **Kano**, **custo do atraso**.

## Exemplo: RICE
```python
itens = {
    "Filtro por status": dict(r=800, i=2, c=0.9, e=2),
    "Notificações":      dict(r=500, i=3, c=0.7, e=5),
    "Tema escuro":       dict(r=300, i=1, c=1.0, e=1),
}
rice = {k: v["r"] * v["i"] * v["c"] / v["e"] for k, v in itens.items()}
for nome, score in sorted(rice.items(), key=lambda x: -x[1]):
    print(f"{score:7.1f}  {nome}")
```

## Template: hipótese de MVP
```text
Acreditamos que [funcionalidade]
para [persona] resolverá [problema].
Saberemos que acertamos quando [métrica] atingir [meta] em [prazo].
Experimento: [versão mínima] · Aprendizado esperado: ...
```

## Roadmap Agora/Próximo/Depois
Organize por objetivos, não datas: **Agora** (em execução), **Próximo** (definido), **Depois** (ideias).

## Exercício
1. Pontue 6 itens do seu backlog com RICE e ordene.
2. Defina o MVP da nova funcionalidade com a hipótese acima.

## Checklist
- [ ] Diferencio output e outcome
- [ ] Aplico RICE ou MoSCoW
- [ ] Defini MVP com métrica de sucesso
