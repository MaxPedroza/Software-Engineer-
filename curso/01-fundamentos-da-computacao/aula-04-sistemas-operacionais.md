# Aula 4 — Sistemas operacionais

**Duração:** ~15 min · **Módulo 1**

## Objetivo
Entender o papel do SO como intermediário entre programas e hardware.

## Teoria
O **sistema operacional** (Linux, Windows, macOS, Android, iOS) gerencia:
- **Processos e CPU** (escalonamento: quem roda e por quanto tempo)
- **Memória** (alocação, isolamento entre programas, memória virtual)
- **Arquivos** (organização e permissões)
- **Dispositivos** (drivers: teclado, disco, rede, GPU)
- **Segurança** (usuários, permissões, isolamento)

### Kernel e espaço de usuário
O **kernel** é o núcleo do SO, com acesso total ao hardware. Programas rodam em *espaço de usuário* e pedem serviços ao kernel via **chamadas de sistema (syscalls)**, como `open`, `read`, `write`, `fork`.

### Por que engenheiros de software precisam disso?
Servidores quase sempre rodam **Linux**; containers dependem de recursos do kernel Linux; entender SO ajuda a depurar travamentos, vazamentos de memória e problemas de desempenho.

## Exercício
1. Liste os processos em execução (`ps aux` ou `top`) e identifique 3 e seus consumos de memória.
2. Pesquise: qual a diferença entre Linux, Windows e macOS no tratamento de permissões de arquivos?

## Checklist
- [ ] Sei listar as responsabilidades do SO
- [ ] Sei o que é kernel e syscall
- [ ] Sei por que Linux é importante em servidores
