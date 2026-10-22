# MANUAL DE PROCESSO DE SOFTWARE — SISTEMA RHYME
## Parte 2 — Processos Organizacionais Habilitadores
> **Norma de Referência:** ISO/IEC/IEEE 12207:2017 (Cláusula 6.2)  
> **Equipe Executora:** Grupo 12 (Squad Rhyme Core) — INF0449 UFG (2026/2)  
> **Baseline:** 7.0 Oficial Consolidada  
> **Navegação:** [Voltar ao Sumário Geral](../README.md) | [Manual Consolidado](../Manual.md)

---

## 🏛️ PARTE 2 — PROCESSOS ORGANIZACIONAIS HABILITADORES DE PROJETO (ISO 12207 - CLÁUSULA 6.2)

### 2.1 Modelo de Ciclo de Vida (ISO 12207 - Cláusula 6.2.1)
A equipe Grupo 12 adotou formalmente o **Modelo de Ciclo de Vida Híbrido Iterativo-Incremental**, estruturado com princípios de métodos ágeis (Scrum com fluxo contínuo Kanban) e cadência de sprints quinzenais:

```
┌────────────────────────────────────────────────────────────────────────┐
│                   CICLO DE VIDA ITERATIVO-INCREMENTAL                  │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │
                                    ▼
       [Visão / Requisitos] ──► [Sprint N: Incremento] ──► [Deploy Piloto]
                ▲                                                │
                │                                                ▼
                └─────────── Validação em Campo (GO-217) ────────┘
```

#### Justificativa da Escolha do Modelo:
1. **Natureza Empírica do Ambiente Operacional:** O comportamento da recepção 4G/GPS nas rodovias estaduais (GO-217 e BR-153) apresenta particularidades que não podem ser previstas exclusivamente em bancada. O modelo iterativo permite testar cada funcionalidade em condições reais de rodovia a cada duas semanas.
2. **Mitigação Progressiva de Riscos Técnicos:** Riscos complexos (como a concorrência de WebSockets no Firestore e o cache offline de Service Workers) foram testados em incrementos isolados antes da inclusão de regras avançadas de geofencing.
3. **Harmonização com as Entregas Normativas:** O modelo viabilizou a entrega cumulativa das baselines da ISO 12207 sem retrabalhos cascatas.

### 2.2 Infraestrutura e Ferramental (ISO 12207 - Cláusula 6.2.2)
O inventário abaixo cataloga todos os ativos físicos, lógicos e plataformas de suporte homologados:

| Categoria | Tecnologia / Ferramenta | Versão | Finalidade no Ciclo de Vida do Software |
|:---|:---|:---:|:---|
| **Linguagem & Runtime** | Node.js / ECMAScript | 20 LTS / ES2024 | Execução do ambiente de compilação, scripts e ferramentas de build. |
| **Framework Frontend** | React | 19.x | Componentização declarativa reativa e gestão de estado em tempo real. |
| **Build Tool / Bundler** | Vite | 6.x | Servidor de desenvolvimento ultrarrápido com Hot Module Replacement (HMR). |
| **Estilização & Design** | Tailwind CSS & PostCSS | 4.x | Sistema de tokens utilitários de alto contraste e legibilidade veicular. |
| **Motor Cartográfico** | Leaflet & React-Leaflet | 1.9 / 5.x | Renderização vetorial de mapas com baixo consumo de CPU e bateria móvel. |
| **Base Cartográfica** | OpenStreetMap / CartoDB | CDN Pública | Tiles cartográficos abertos sem custos de licenciamento por visualização. |
| **Banco NoSQL Realtime** | Google Cloud Firestore | NoSQL Realtime | Persistência de documentos e sincronização de eventos com listeners nativos. |
| **Ambiente de Teste Local** | Firebase Emulator Suite | 13.x | Execução local de regras de banco de dados e funções sem consumo de nuvem. |
| **Framework de Testes** | Vitest & React Testing Library | 2.x / 16.x | Execução de testes unitários automatizados e testes de componentes. |
| **Qualidade & Linters** | ESLint & Oxlint | Última estável | Análise estática de código e imposição de padrões de qualidade de código. |
| **Controle de Versão** | Git & GitHub | 2.4x / Cloud | Versionamento distribuído, controle de branches e auditoria de commits. |
| **Pipeline de CI/CD** | GitHub Actions | Workflows v4 | Automação de linters, testes unitários, build e deploy contínuo em produção. |
| **Hospedagem & CDN** | Vercel & Firebase Hosting | Edge CDN | Distribuição global de assets PWA com provisionamento automático HTTPS. |
| **Dispositivos Veiculares** | Smartphones Android e iOS | Android 10+ / iOS 15+ | Telefones veiculares dos motoristas acoplados a suporte 12V no painel do ônibus. |

### 2.3 Recursos Humanos, Matriz RACI e Plano de Capacitação (ISO 12207 - Cláusula 6.2.4)

#### A. Matriz RACI do Projeto
A matriz formaliza a distribuição de papéis e responsabilidades operacionais entre as disciplinas de engenharia do squad:
*(**R** = Responsible / Responsável pela Execução, **A** = Accountable / Aprovador Final, **C** = Consulted / Consultado, **I** = Informed / Informado)*

| Macroatividade do Ciclo de Vida | Requisitos & Produto (Matheus) | Arquitetura & Frontend (Luis) | Infraestrutura & Nuvem (Heitor) | SQA & Testes de Campo (Carlos) |
|:---|:---:|:---:|:---:|:---:|
| **1. Elicitação e Refinamento de Requisitos** | **A / R** | C | C | C |
| **2. Modelagem do Banco NoSQL e Regras** | C | R | **A / R** | C |
| **3. Desenvolvimento da UI e Mapas Leaflet** | I | **A / R** | C | C |
| **4. Implementação de Geofencing e Push** | C | R | R | **A** |
| **5. Testes Unitários e Testes de Campo (GO-217)** | C | C | I | **A / R** |
| **6. Governança de Releases e Deploy CI/CD** | I | R | **A / R** | C |
| **7. Resposta a Incidentes de Telemetria / GPS** | C | I | R | **A / R** |

#### B. Plano de Capacitação Técnica da Equipe
Para assegurar a aderência às melhores práticas de engenharia de software e normas ISO, foram executadas trilhas de capacitação interna:
* **Capacitação em ISO/IEC/IEEE 12207:** Nivelamento sobre os processos das cláusulas 6.1 a 6.4 e seus requisitos de rastreabilidade e auditoria.
* **Treinamento em PWA Offline-First:** Estudo aprofundado dos ciclos de vida de Service Workers, estratégias de cache *Stale-While-Revalidate* e persistência em IndexedDB.
* **Segurança no Firebase:** Oficina prática de escrita e validação sintática de `firestore.rules` utilizando o Firebase Emulator Suite.

### 2.4 Gestão da Qualidade e do Conhecimento (ISO 12207 - Cláusulas 6.2.5 e 6.2.6)

#### A. Métricas Organizacionais de Qualidade
A conformidade do produto e dos processos é monitorada por quatro métricas objetivas:

| Indicador | Parâmetro Mensurado | Meta / Alvo Tolerado | Método de Aferição | Ação Corretiva em Caso de Desvio |
|:---|:---|:---:|:---|:---|
| **QM-01** | Latência de Sincronização Realtime | **< 100 ms** (4G/5G)<br>**< 1.000 ms** (3G) | Confronto entre `timestamp` de gravação no Firestore e recebimento no listener. | Redução do payload de dados e otimização das consultas reativas. |
| **QM-02** | Eficácia do Geofencing Preditivo | **≥ 98%** de entregas antes da chegada ao ponto | Log de eventos de alerta confrontado com o timestamp de embarque efetivo. | Reajuste da margem de raio perimétrico (ajuste dinâmico de 1.000m para 1.500m). |
| **QM-03** | Performance Web Vitals Mobile | **LCP < 2,0s**<br>**TTI < 2,5s** | Relatórios de auditoria automatizada do Google Lighthouse Mobile via CI. | Aplicação de *code-splitting* em rotas e pré-carregamento de tiles essenciais. |
| **QM-04** | Cobertura de Testes Automatizados | **≥ 80%** de linhas e branches críticas | Relatórios de cobertura gerados pelo Vitest na suíte de testes unitários. | Bloqueio automatizado de Pull Requests que reduzam a cobertura percentual. |

#### B. Estratégia de Gestão e Retenção do Conhecimento
1. **Documentação Viva em Repositório Único:** Todos os manuais, guias e especificações são mantidos em Markdown na pasta `docs/` sob controle de versão Git, prevenindo a perda de histórico.
2. **Registros Formais de Decisões de Arquitetura (ADRs):** Toda decisão técnica estrutural é justificada formalmente com registro de contexto, alternativas e consequências.
3. **Post-Mortems de Incidentes sem Culpabilidade (*Blameless*):** Incidentes em viagens reais resultam em análise de causa raiz com implementação de melhorias preventivas imediatas.

---