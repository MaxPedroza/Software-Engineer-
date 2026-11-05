# Aula 8 — ORMs e acesso a dados (vantagens e armadilhas)

**Duração:** ~25 min · **Módulo 11**

## Objetivo
Usar um ORM com consciência de seus custos, evitando problemas como o N+1.

## Teoria
Um **ORM** (SQLAlchemy, Django ORM, Prisma, Hibernate) mapeia tabelas para classes.

**Vantagens**: produtividade, menos SQL repetitivo, proteção padrão contra SQL injection (parâmetros), migrações e portabilidade.

**Armadilhas**:
- **N+1 queries**: 1 consulta para a lista + 1 por item para relacionamentos.
- **Lazy loading** inesperado fora de sessão/transação.
- Consultas ineficientes geradas automaticamente; carregar colunas desnecessárias.
- Abstração vazando: sem entender SQL, não se diagnostica lentidão.
- Transações e sessões mal delimitadas.

Boas práticas: use `EXPLAIN`, *eager loading* (`joinedload`/`selectinload`), paginação, índices, e SQL puro para casos complexos. Padrões: **Repository** isola o acesso a dados do domínio.

## Exemplo (SQLAlchemy 2.x)
```python
from sqlalchemy import select, ForeignKey
from sqlalchemy.orm import (DeclarativeBase, Mapped, mapped_column,
                            relationship, selectinload, Session)

class Base(DeclarativeBase): pass

class Projeto(Base):
    __tablename__ = "projetos"
    id: Mapped[int] = mapped_column(primary_key=True)
    nome: Mapped[str]
    tarefas: Mapped[list["Tarefa"]] = relationship(back_populates="projeto")

class Tarefa(Base):
    __tablename__ = "tarefas"
    id: Mapped[int] = mapped_column(primary_key=True)
    titulo: Mapped[str]
    projeto_id: Mapped[int] = mapped_column(ForeignKey("projetos.id"))
    projeto: Mapped[Projeto] = relationship(back_populates="tarefas")

def listar(s: Session):
    # N+1: for p in s.scalars(select(Projeto)): p.tarefas
    stmt = select(Projeto).options(selectinload(Projeto.tarefas))  # 2 queries
    return s.scalars(stmt).all()
```

## Exercício
1. Ative `echo=True` no engine e conte as queries da versão com N+1 e com `selectinload`.
2. Reescreva uma consulta do projeto em SQL puro e compare com o `EXPLAIN`.

## Checklist
- [ ] Sei apontar vantagens e riscos de ORMs
- [ ] Identifico e corrijo N+1
- [ ] Sei quando recorrer a SQL puro
