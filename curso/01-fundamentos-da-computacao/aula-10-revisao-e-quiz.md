# Aula 10 — Revisão e quiz do módulo

**Duração:** ~20 min · **Módulo 1**

## Resumo
- Engenharia de software = construir, entregar e manter sistemas (não só codar).
- Dados são bits; texto usa Unicode/UTF-8; decimais têm imprecisão.
- CPU executa, RAM guarda o que está em uso, disco persiste; cache reduz latência.
- O SO gerencia processos, memória, arquivos e dispositivos.
- Threads compartilham memória (cuidado com race conditions).
- Compilar vs interpretar vs bytecode/JIT: trade-offs de velocidade e portabilidade.
- Um processo tem code, data, heap e stack.
- Uma requisição web envolve DNS → TCP → TLS → HTTP.

## Quiz (responda sem consultar)
1. Quantos valores distintos um byte pode representar?
2. Converta `0xFF` para decimal e `13` para binário.
3. Por que `0.1 + 0.2` não dá exatamente `0.3`?
4. Qual a diferença entre RAM e SSD? Cite uma característica de cada.
5. O que é uma syscall?
6. Cite duas diferenças entre processo e thread.
7. O que é uma race condition e como evitá-la?
8. Python é compilado ou interpretado? Explique a nuance do bytecode.
9. Qual a diferença entre stack e heap?
10. Cite os passos principais quando você acessa `https://exemplo.com`.

## Gabarito resumido
1. 256 · 2. 255 e `1101` · 3. Ponto flutuante binário (IEEE 754) · 4. RAM volátil/rápida; SSD persistente/mais lento · 5. Pedido de serviço do programa ao kernel · 6. Memória isolada vs compartilhada; criação mais pesada vs leve · 7. Resultado depende da ordem das threads; locks/filas/imutabilidade · 8. Compila para bytecode e a VM interpreta · 9. Stack: chamadas/locais, automática; heap: dinâmica · 10. DNS → TCP → TLS → HTTP → resposta → renderização

## Entregável do módulo
Documento (1–2 páginas) **"Do código ao processador"** com um diagrama próprio e a descrição do **projeto contínuo** que você vai construir.

## Checklist final
- [ ] Acertei 8 ou mais questões
- [ ] Entreguei o documento
- [ ] Pronto para o Módulo 2
