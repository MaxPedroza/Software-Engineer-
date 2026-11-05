# Trilhas de Especialização (opcionais)

Após o núcleo (módulos 1–24), escolha uma ou mais trilhas de 3–4 módulos. Cada módulo tem ~10 aulas e um projeto prático que estende o sistema do curso.

**Pré-requisito geral:** módulos 1–20 do núcleo (o projeto final, módulo 24, é recomendado).

---

## 1. Frontend Avançado
**Pré-requisitos:** módulos 3, 9, 14, 15.

### T1.1 — Design Systems e Componentização
- Tokens de design
- Biblioteca de componentes
- Storybook
- Theming e dark mode
- Acessibilidade em componentes
- Versionamento e publicação (npm)
- Documentação
- Composição e padrões (compound, headless)
- CSS moderno (container queries, layers)
- Governança do design system

### T1.2 — Performance Web
- Core Web Vitals
- Profiling com DevTools
- Code splitting
- Lazy loading
- Otimização de imagens e fontes
- Cache e Service Workers
- SSR/SSG/ISR e streaming
- Orçamento de performance
- Monitoramento real (RUM)
- Lighthouse CI

### T1.3 — State Management e Arquitetura
- Estado local vs global
- Redux Toolkit
- Zustand/Jotai
- React Query/SWR
- Máquinas de estado (XState)
- Atualizações otimistas
- Formulários complexos
- Micro-frontends
- Monorepo (Turborepo/Nx)
- Organização de pastas e escalabilidade

### T1.4 — Testes Visuais e E2E
- Testes de componentes
- Testing Library
- Playwright
- Regressão visual (Chromatic/Percy)
- Testes de acessibilidade (axe)
- Mocks de API (MSW)
- Testes em CI
- Testes instáveis (flakiness)
- Cobertura útil
- Testes de performance

**Recursos:** web.dev, MDN, *Refactoring UI*, documentação do React, Storybook docs.

---

## 2. Backend Avançado
**Pré-requisitos:** módulos 9, 10, 11, 12, 13, 15.

### T2.1 — Microsserviços
- Monólito vs microsserviços
- Domain-Driven Design
- Bounded contexts
- Comunicação síncrona e assíncrona
- API Gateway
- Service discovery
- Saga e transações distribuídas
- Resiliência (retry, circuit breaker)
- Contratos entre serviços
- Observabilidade distribuída

### T2.2 — Event Sourcing, CQRS e Mensageria
- Eventos de domínio
- Event sourcing
- CQRS
- Kafka e RabbitMQ
- Entrega at-least-once
- Idempotência
- Outbox pattern
- Evolução de schemas de eventos
- Projeções e read models
- Reprocessamento e DLQ

### T2.3 — Alta Performance e Escalabilidade
- Profiling
- Cache em camadas
- Pooling de conexões
- Particionamento e sharding
- Replicação
- Concorrência e async
- Rate limiting
- Filas e backpressure
- Testes de carga
- Otimização de queries

### T2.4 — Java, Go ou .NET em Produção
- Ecossistema e tooling
- Concorrência (goroutines/threads/async)
- Frameworks (Spring, Gin, ASP.NET)
- Injeção de dependência
- Testes
- Memória e coleta de lixo (GC)
- Profilers
- Build e empacotamento
- gRPC
- Boas práticas idiomáticas

**Recursos:** *Designing Data-Intensive Applications*, *Building Microservices*, *Domain-Driven Design*, microservices.io.

---

## 3. Cloud & DevOps
**Pré-requisitos:** módulos 2, 12, 16, 17, 18, 19.

### T3.1 — Kubernetes Avançado
- Arquitetura do cluster
- Deployments e StatefulSets
- Helm e Kustomize
- Ingress e service mesh
- HPA/VPA
- Políticas de rede
- RBAC
- Operators e CRDs
- GitOps (Argo CD/Flux)
- Troubleshooting

### T3.2 — Infraestrutura como Código com Terraform
- HCL e providers
- State remoto e locking
- Módulos
- Workspaces e ambientes
- Variáveis e outputs
- Testes de IaC
- Políticas (OPA/Sentinel)
- Drift
- Pipelines de IaC
- Boas práticas e custos

### T3.3 — Plataformas Internas e SRE
- Platform engineering
- Golden paths
- Backstage
- SLI/SLO/error budget
- Gestão de incidentes
- Postmortems
- Chaos engineering
- Capacity planning
- FinOps
- Runbooks e on-call

### T3.4 — Certificações e Arquiteturas Cloud
- Well-Architected Framework
- Redes (VPC)
- IAM
- Armazenamento e bancos gerenciados
- Serverless
- Alta disponibilidade e DR
- Segurança na nuvem
- Custos
- Simulados
- Plano de estudos (AWS/Azure/GCP, CKA)

**Recursos:** documentação da CNCF/Kubernetes, *Site Reliability Engineering* (Google), *The Phoenix Project*, Terraform Learn, labs dos provedores.

---

## 4. Dados & IA
**Pré-requisitos:** módulos 3, 4, 10, 11 (álgebra linear e probabilidade do módulo 4 são essenciais).

### T4.1 — Engenharia de Dados
- Data warehouse e lakehouse
- Modelagem dimensional
- ETL vs ELT
- Airflow/Dagster
- Spark
- dbt
- Streaming (Kafka)
- Qualidade de dados
- Governança e catálogo
- Formatos (Parquet, Delta)

### T4.2 — Machine Learning Básico
- Pandas e NumPy
- Regressão e classificação
- Treino/validação/teste
- Métricas
- Overfitting e regularização
- Árvores e ensembles
- Feature engineering
- Clustering
- scikit-learn
- Visualização de dados

### T4.3 — MLOps
- Ciclo de vida de ML
- Versionamento de dados e modelos
- Experimentos (MLflow)
- Pipelines
- Feature stores
- Deploy de modelos (API, batch)
- Monitoramento e drift
- CI/CD para ML
- Reprodutibilidade
- Custos e governança

### T4.4 — LLMs e Aplicações de IA
- Fundamentos de LLM e tokens
- Prompt engineering
- Embeddings
- Busca vetorial
- RAG
- Function calling e agentes
- Avaliação e guardrails
- Fine-tuning vs RAG
- Custos e latência
- IA responsável e privacidade

**Recursos:** *Hands-On Machine Learning* (Géron), *Designing Machine Learning Systems* (Huyen), fast.ai, Kaggle, documentação do scikit-learn e dos provedores de LLM.

---

## 5. Mobile
**Pré-requisitos:** módulos 3, 8, 9, 13, 14.

### T5.1 — Android Nativo (Kotlin)
- Kotlin essencial
- Ciclo de vida
- Jetpack Compose
- Navegação
- ViewModel e estado
- Room
- Retrofit e coroutines
- Injeção (Hilt)
- Permissões e sensores
- Testes

### T5.2 — iOS Nativo (Swift)
- Swift essencial
- SwiftUI
- Ciclo de vida
- Navegação
- Combine e async/await
- Core Data/SwiftData
- Redes
- Notificações
- Arquitetura (MVVM)
- Testes

### T5.3 — Multiplataforma (React Native/Flutter)
- Comparação das abordagens
- Componentes e layout
- Navegação
- Estado
- Acesso a APIs nativas
- Armazenamento local
- Offline-first
- Animações
- Testes
- Performance

### T5.4 — Publicação em Lojas
- Contas de desenvolvedor
- Assinatura e builds
- CI/CD mobile (Fastlane)
- Diretrizes das lojas
- Privacidade e permissões
- Testes beta (TestFlight/Play Console)
- Metadados e ASO
- Analytics e crashes
- Atualizações
- Monetização

**Recursos:** developer.android.com, developer.apple.com, docs.flutter.dev, reactnative.dev, diretrizes de design (Material, HIG).

---

## 6. Segurança Ofensiva e Defensiva
**Pré-requisitos:** módulos 2, 12, 13, 19 (Segurança), noções de Linux e redes.

### T6.1 — Fundamentos de Pentest
- Metodologia (PTES/OWASP)
- Reconhecimento
- Varredura (nmap)
- Enumeração
- Exploração
- Burp Suite
- Escalada de privilégios
- Pós-exploração
- Relatórios
- Ética e legislação

### T6.2 — Segurança de Aplicações (AppSec)
- OWASP Top 10
- Injeção
- Autenticação e sessão
- Controle de acesso
- XSS e CSRF
- SSRF
- Criptografia aplicada
- SAST/DAST/SCA
- Threat modeling
- Secure SDLC

### T6.3 — Defesa e Resposta a Incidentes
- Logs e SIEM
- Detecção e alertas
- Hardening
- Gestão de vulnerabilidades
- Ciclo de resposta (NIST)
- Forense básica
- Contenção e recuperação
- Inteligência de ameaças
- Playbooks
- Comunicação e LGPD

**Recursos:** OWASP (Top 10, Cheat Sheets, WebGoat), PortSwigger Web Security Academy, Hack The Box, TryHackMe, NIST SP 800-61.
**Aviso:** pratique apenas em ambientes autorizados.

---

## 7. Jogos
**Pré-requisitos:** módulos 3, 4 (álgebra linear), 5, 6, 8.

### T7.1 — Engines e Game Loop
- Game loop e delta time
- Unity ou Godot
- Cenas e entidades
- ECS
- Input
- Sprites e animação
- Áudio
- UI e menus
- Gerenciamento de recursos
- Build e publicação

### T7.2 — Física e Matemática de Jogos
- Vetores e matrizes
- Transformações
- Colisões (AABB, SAT)
- Corpos rígidos
- Integração numérica
- Câmera
- Pathfinding (A*)
- Steering behaviors
- Geração procedural
- Otimização espacial (quadtree)

### T7.3 — Gráficos e Renderização
- Pipeline gráfico
- Shaders (GLSL/HLSL)
- Iluminação
- Texturas e materiais
- Câmeras e projeção
- Sombras
- Partículas
- Pós-processamento
- Otimização (draw calls, LOD)
- Introdução a Vulkan/WebGL

**Recursos:** *Game Programming Patterns* (Nystrom), *Real-Time Rendering*, docs do Godot/Unity, Learn OpenGL, game jams no itch.io.
