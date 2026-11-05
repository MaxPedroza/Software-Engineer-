# Aula 4 — Composição vs herança

**Duração:** ~20 min · **Módulo 8**

## Objetivo
Decidir entre herança ("é um") e composição ("tem um") e preferir composição quando possível.

## Teoria
- **Herança** cria acoplamento forte: mudanças na superclasse quebram subclasses (problema da *classe base frágil*) e a hierarquia explode com combinações (`PatoVoadorNadador`...).
- **Composição**: um objeto *contém* outros e delega trabalho a eles. Comportamentos podem ser trocados em tempo de execução.
- Regra prática: **prefira composição à herança**. Use herança só para relação "é um" verdadeira e estável (e que respeite o princípio de Liskov, aula 6).
- Composição + injeção de dependência facilita testes (troque o componente por um *fake*).

## Exemplo em Python
```python
class Repositorio:
    def __init__(self):
        self._dados = []
    def salvar(self, item): self._dados.append(item)

class RepositorioFake(Repositorio):
    pass

class Logger:
    def info(self, msg): print(f"INFO {msg}")

class ServicoTarefas:
    def __init__(self, repo, logger):   # dependências injetadas
        self.repo = repo
        self.logger = logger

    def criar(self, titulo):
        self.repo.salvar({"titulo": titulo})
        self.logger.info(f"tarefa criada: {titulo}")

ServicoTarefas(Repositorio(), Logger()).criar("Estudar POO")
```
`ServicoTarefas` *tem um* repositório e *tem um* logger, em vez de herdar de ambos.

## Exercício
1. Modele `Carro` com `Motor` por composição; troque por `MotorEletrico` sem mudar `Carro`.
2. Explique por que `Pilha(list)` é um mau uso de herança.
3. Refatore uma hierarquia `Relatorio → RelatorioPDF/RelatorioCSV` para usar um objeto `Formatador`.

## Checklist
- [ ] Distingo "é um" de "tem um"
- [ ] Injeto dependências pelo construtor
- [ ] Sei apontar problemas de hierarquias profundas
