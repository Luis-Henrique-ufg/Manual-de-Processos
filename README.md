# Manual de Processo de Software — Sistema Rhyme
> **Governança de Ciclo de Vida segundo a Norma ISO/IEC/IEEE 12207:2017**  
> **Projeto Integrador da Disciplina:** INF0449 — Processos de Engenharia de Software  
> **Instituição:** Instituto de Informática (INF) — Universidade Federal de Goiás (UFG)  
> **Semestre:** 2026/2 | **Baseline Vigente:** 7.0 Oficial Consolidada  
> **Equipe Executora (Grupo 12):** Matheus Marquez, Luis Henrique, Heitor Gonçalves, Carlos Daniel  

---

## 🧭 Visão Geral do Repositório

Este repositório armazena a documentação oficial, padronizada e auditável do **Manual de Processo de Software** da plataforma **Rhyme** (Progressive Web App para gestão e telemetria em tempo real de transporte universitário intermunicipal).

A estrutura deste repositório foi concebida sob o princípio da **modularidade e desacoplamento**:
1. **Manual Unificado Consolidado:** Mantido em [`Manual.md`](./Manual.md) como o documento formal integral pronto para submissão e publicação acadêmica/corporativa.
2. **Módulos Independentes por Parte:** Disponíveis na pasta [`partes/`](./partes/) para navegação focada e manutenção modular em ciclos ágeis.
3. **Diagramas Desacoplados:** Fontes formais PlantUML isolados em [`diagramas/`](./diagramas/) para edição ágil no VS Code e integração contínua.

---

## 📚 Sumário Normativo do Manual (ISO/IEC/IEEE 12207)

Abaixo está o mapa de navegação das seções do manual, com links diretos para cada módulo individual e correspondente capítulo no manual unificado:

| Cláusula ISO 12207 | Módulo do Manual | Arquivo Modular | Tópicos Centrais Contemplados |
|:---|:---|:---:|:---|
| **Metadados** | **Capa e Baselines** | [`Manual.md`](./Manual.md) | Controle oficial de versões (v1.0 a v7.0), dados da equipe e classificação. |
| **Contexto** | **Parte 0 — Apresentação e Visão Geral** | [`partes/parte-0-visao-geral.md`](./partes/parte-0-visao-geral.md) | Ficha da equipe, problema real mitigado (rotas Cromínia e Prof. Jamil ↔ UFG), escopo e não-metas. |
| **Cláusula 6.1** | **Parte 1 — Processos de Acordo** | [`partes/parte-1-processos-acordo.md`](./partes/parte-1-processos-acordo.md) | Make vs. Buy (Firebase, OSM, Vercel), Termo de Cessão, SLA 99,9%, RTO/RPO e POPs 01 a 04. |
| **Cláusula 6.2** | **Parte 2 — Processos Organizacionais** | [`partes/parte-2-organizacional.md`](./partes/parte-2-organizacional.md) | Ciclo Iterativo-Incremental (Scrum/Kanban), Inventário técnico, Matriz RACI, Métricas QM-01 a QM-04 e Gestão do Conhecimento. |
| **Cláusula 6.3** | **Parte 3 — Gerenciamento Técnico** | [`partes/parte-3-gerenciamento.md`](./partes/parte-3-gerenciamento.md) | PDS, EAP em 3 níveis, Cronograma Sprints S1–S6, Risk Register (RT/RO/RR), MDAs e Git Trunk-based. |
| **Cláusula 6.4** | **Parte 4 — Processos Técnicos** | [`partes/parte-4-processos-tecnicos.md`](./partes/parte-4-processos-tecnicos.md) | Requisitos SMART (RF01–RF10, RNF01–RNF05), Matriz Rastreabilidade, C4 Model, CI/CD, V&V (CT-01 a CT-10), UAT e Descontinuação LGPD. |
| **Auditoria** | **Anexo — Avaliação por Pares** | [`partes/anexo-peer-review.md`](./partes/anexo-peer-review.md) | Simulação de Auditoria de Pares, Checklist normativo, Matriz de NCs/OMs, Plano CAPA resolvido e Parecer Final. |

---

## 📐 Diagramas e Modelos de Arquitetura Desacoplados

Os modelos formais de design do software estão disponíveis na pasta [`diagramas/`](./diagramas/):

* 📊 **Casos de Uso:** [`diagramas/casos-de-uso.puml`](./diagramas/casos-de-uso.puml) — 10 casos de uso com Estudante, Motorista, GPS e Firestore.
* ⏱️ **Sequência em Tempo Real:** [`diagramas/sequencia-tempo-real.puml`](./diagramas/sequencia-tempo-real.puml) — Notificações de liberação One-Touch e telemetria contínua.
* 🧩 **Componentes de Arquitetura:** [`diagramas/componentes-arquitetura.puml`](./diagramas/componentes-arquitetura.puml) — Cliente PWA React 19, Leaflet, Service Worker e BaaS.
* 🗄️ **Modelo NoSQL Firestore:** [`diagramas/modelo-dados-firestore.puml`](./diagramas/modelo-dados-firestore.puml) — Estrutura de coleções `routes`, `trips`, `students`, `bus_location` e `emergencies`.

Consulte o arquivo [`diagramas/README.md`](./diagramas/README.md) para instruções detalhadas de renderização no VS Code.

---

## 👥 Constituição da Equipe (Grupo 12)

* **Matheus Marquez de Carvalho Rodrigues** — Requisitos, Produto e Gestão de Backlog
* **Luis Henrique Oliveira de Jesus** — Arquitetura de Software e Engenheiro Frontend
* **Heitor Gonçalves Costa** — Infraestrutura, Nuvem, DevOps e CI/CD
* **Carlos Daniel Lopes de Araújo** — Garantia da Qualidade (SQA), Verificação e Validação

---

## 📂 Organização Física de Pastas

```
Manual-de-Processos/
├── README.md                          # Portal oficial do repositório no GitHub
├── Manual.md                          # Manual de Processo de Software Unificado Completo
├── historico-versoes.md               # Histórico formal de versões e baselines
├── Requisitos.md                      # Especificação complementar de requisitos
├── Atividade.md                       # Diretrizes do Desafio do Manual (INF0449)
├── diagramas/                         # Diagramas PlantUML desacoplados
│   ├── README.md                      # Guia de renderização e documentação dos modelos
│   ├── casos-de-uso.puml              # Diagrama de Casos de Uso UML
│   ├── sequencia-tempo-real.puml      # Diagrama de Sequência em Tempo Real
│   ├── componentes-arquitetura.puml   # Diagrama de Componentes de Arquitetura
│   └── modelo-dados-firestore.puml    # Diagrama Entidade-Relacionamento NoSQL
└── partes/                            # Módulos normativos desacoplados para consulta focada
    ├── parte-0-visao-geral.md         # Parte 0 — Apresentação e Visão Geral
    ├── parte-1-processos-acordo.md    # Parte 1 — Processos de Acordo (§6.1)
    ├── parte-2-organizacional.md      # Parte 2 — Processos Organizacionais (§6.2)
    ├── parte-3-gerenciamento.md       # Parte 3 — Gerenciamento Técnico (§6.3)
    ├── parte-4-processos-tecnicos.md  # Parte 4 — Processos Técnicos (§6.4)
    └── anexo-peer-review.md           # Anexo — Avaliação por Pares & CAPA
```

---

*Manual de Processo de Software — Sistema Rhyme — Universidade Federal de Goiás (UFG).*
