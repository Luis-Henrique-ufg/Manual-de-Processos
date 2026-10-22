# MANUAL DE PROCESSO DE SOFTWARE UNIFICADO
## Sistema Rhyme — Gestão e Telemetria em Tempo Real de Transporte Universitário Intermunicipal
### Em Conformidade com a Norma ISO/IEC/IEEE 12207:2017 (*Systems and software engineering — Software life cycle processes*)

---

## 📄 CAPA E METADADOS DO DOCUMENTO

| Parâmetro | Informação de Registro e Governança |
|:---|:---|
| **Título do Documento:** | Manual de Processo de Software — Sistema Rhyme |
| **Código do Documento:** | MPS-RHYME-12207-UFG |
| **Norma de Referência:** | ISO/IEC/IEEE 12207:2017 (Cláusulas 6.1, 6.2, 6.3 e 6.4) |
| **Instituição de Ensino:** | Universidade Federal de Goiás (UFG) — Instituto de Informática (INF) |
| **Curso / Disciplina:** | Bacharelado em Ciência da Computação / Engenharia de Software — INF0449 (2026/2) |
| **Entidade Executora:** | Grupo 12 — Squad Rhyme Core |
| **Versão / Baseline:** | 7.0 — Versão Consolidada e Unificada Oficial |
| **Data da Baseline:** | 22 de Outubro de 2026 |
| **Classificação:** | Documentação Pública / Código Aberto sob Governança Acadêmica |

---

### Histórico Consolidado de Versões e Controle de Baselines

A tabela abaixo registra a evolução iterativa do manual ao longo dos módulos do semestre, consolidando as entregas parciais até a homologação desta baseline unificada:

| Versão | Data | Módulo / Etapa | Descrição Detalhada das Alterações e Entregáveis | Autor / Revisor |
|:---:|:---:|:---:|:---|:---|
| **1.0** | 10/09/2026 | Etapa 0 | **Apresentação do Software Rhyme:** Delimitação de escopo, formulação do problema do mundo real, identificação de stakeholders, restrições operacionais e premissas arquiteturais. | M. Marquez / L. Henrique |
| **2.0** | 12/09/2026 | Etapa 1 | **Processos de Acordo (ISO 12207 §6.1):** Matriz de aquisição PaaS/SaaS, cessão gratuita de uso para prefeituras e alunos, definição de SLA 99,9% no horário nobre e POPs operacionais. | H. Gonçalves / C. Daniel |
| **3.0** | 17/09/2026 | Etapa 2 | **Processos Organizacionais Habilitadores (ISO 12207 §6.2):** Formalização do ciclo de vida iterativo-incremental (Scrum/Kanban híbrido), inventário de infraestrutura, Matriz RACI da equipe, plano de métricas de qualidade (QM-01 a QM-04) e retenção de conhecimento. | L. Henrique / M. Marquez |
| **4.0** | 24/09/2026 | Etapa 3 | **Processos de Gerenciamento Técnico (ISO 12207 §6.3):** Elaboração da EAP em 3 níveis, cronograma de sprints S1–S6, Matrizes de Decisão Multicritério (MDA-01 a MDA-03) e Risk Register com planos de resposta. | H. Gonçalves / C. Daniel |
| **5.0** | 08/10/2026 | Etapa 4 | **Processos Técnicos (ISO 12207 §6.4 - Requisitos & Arquitetura):** Especificação formal dos Requisitos SMART, ADRs (ADR-001 a ADR-004), modelos estruturais UML em PlantUML e matriz de rastreabilidade preliminar. | M. Marquez / L. Henrique |
| **6.0** | 21/10/2026 | Etapa 5 | **Processos de Sustentação (ISO 12207 §6.4.9–6.4.14):** Planejamento de implantação/handoff, modalidades de manutenção (corretiva, adaptativa, evolutiva), observabilidade operacional e plano de descarte seguro LGPD. | C. Daniel / H. Gonçalves |
| **7.0** | 22/10/2026 | Consolidado | **Manual Unificado Oficial:** Harmonização integral de todos os módulos parciais, alinhamento bidirecional estrito (EAP ↔ Requisitos RF01–RF10 ↔ Testes CT01–CT10), especificação de modelos de dados Firestore, contratos de eventos, e incorporação do Relatório de Avaliação por Pares (Peer Review) com plano CAPA implementado. | Grupo 12 (Todos) |

---

## 📚 PARTE 0 — APRESENTAÇÃO DO SOFTWARE E VISÃO GERAL

### 0.1 Ficha de Constituição da Equipe
O desenvolvimento, governança e garantia de conformidade do sistema Rhyme são conduzidos pela equipe **Grupo 12 (Squad Rhyme Core)**, organizada em modelo multidisciplinar de engenharia compartilhada:

| Nome do Integrante | Papel Primário no Processo | Atribuições Centrais na ISO 12207 | Contato Institucional |
|:---|:---|:---|:---|
| **Matheus Marquez de Carvalho Rodrigues** | Engenheiro Principal de Requisitos e Produto | Cláusula 6.4.1 (Elicitação e Análise de Requisitos), Rastreabilidade e Gestão de Backlog | `matheus.marquez@discente.ufg.br` |
| **Luis Henrique Oliveira de Jesus** | Arquiteto de Software e Engenheiro Frontend | Cláusula 6.4.3 (Design de Arquitetura), Implementação do Core PWA, Leaflet e Service Workers | `luis.henrique@discente.ufg.br` |
| **Heitor Gonçalves Costa** | Engenheiro de Infraestrutura, Nuvem e DevOps | Cláusula 6.2.2 (Infraestrutura), Cláusula 6.3.5 (Configuração) e Automação de CI/CD Firebase/Vercel | `heitor.costa@discente.ufg.br` |
| **Carlos Daniel Lopes de Araújo** | Engenheiro de Garantia da Qualidade (SQA) & V&V | Cláusula 6.2.5 (Qualidade), Cláusulas 6.4.9 e 6.4.10 (Verificação, Validação e Testes em Trânsito) | `carlos.daniel@discente.ufg.br` |

### 0.2 Sistema de Contexto Real
O **Rhyme** é uma plataforma digital progressiva (*Progressive Web App - PWA*) focada em telemetria e eventos em tempo real, concebida para planejar, monitorar, sincronizar e otimizar o transporte rodoviário intermunicipal de estudantes universitários no estado de Goiás.

#### A. O Problema do Mundo Real Mitigado
Tradicionalmente, a coordenação diária de embarque e retorno de estudantes universitários residentes em cidades do interior que estudam na capital é gerenciada de forma improvisada por meio de **grupos de WhatsApp**. Essa prática gera gargalos operacionais e riscos graves à segurança pública:

1. **Risco Crítico de Acidentes Rodoviários por Distração ao Volante:** Durante o percurso noturno entre faculdades na capital, o motorista do ônibus/van é compelido a ler dezenas de mensagens picadas e áudios com o veículo em movimento para identificar quem já foi liberado da aula ou quem pediu para esperar, gerando alto risco de colisões urbanas e rodoviárias.
2. **Vulnerabilidade Noturna dos Estudantes:** Os universitários aguardam em calçadas desertas e pontos escuros após as 22h00 sem visibilidade sobre onde o veículo se encontra e sem estimativa de chegada (*ETA*). Não raro, alunos são deixados para trás quando o transporte passa adiantado.
3. **Ineficiência Energética e Desperdício de Recursos Públicos:** Sem saber previamente se há alunos a embarcar em determinados câmpi distantes (especialmente em dias de provas ou semanas acadêmicas), o ônibus realiza desvios desnecessários, queimando óleo diesel subsidiado com recursos municipais e dilatando o tempo total de retorno.
4. **Ausência de Dados Históricos e Auditoria:** As mensagens no WhatsApp se perdem no ruído social. Não há consolidação de presenças, horários efetivos de saída ou métricas que permitam à gestão pública dimensionar adequadamente a frota.

#### B. Rotas Piloto Iniciais do Projeto
O sistema opera em caráter piloto atendendo a dois corredores regulares de transporte universitário:
* **Rota 1 (Cromínia ↔ Goiânia):** Transporte diário de estudantes residentes no município de Cromínia via GO-217 e BR-153 até os polos educacionais de Goiânia (UFG Câmpus Samambaia, UFG Câmpus Colemar Natal e Silva, PUC Goiás - Câmpus I e II, UniCamps e Faculdades Objetivo).
* **Rota 2 (Professor Jamil ↔ Goiânia):** Transporte de universitários do município de Professor Jamil com destino aos mesmos centros de ensino superior da Região Metropolitana.

### 0.3 Escopo Funcional e Objetivos de Negócio

#### A. Objetivos de Negócio (Business Goals)
* **Redução a Zero da Distração do Motorista:** Substituir mensagens de texto por uma interface veicular com contadores consolidados por faculdade e alertas sonoros automáticos.
* **Pontualidade e Segurança no Embarque:** Reduzir em pelo menos 25% o tempo de espera dos alunos em pontos vulneráveis através de telemetria contínua e geofencing preditivo.
* **Otimização de Rota:** Eliminar passagens inúteis por câmpi sem demanda comprovada, gerando economia estimada de 10% a 15% de combustível por viagem.

#### B. Mapeamento de Funcionalidades Centrais (Dentro do Escopo)
1. **Rastreamento e Telemetria GPS em Tempo Real:** Transmissão da localização contínua do ônibus para o mapa Leaflet com taxa de atualização a cada 5 segundos.
2. **Status One-Touch do Estudante:** Alternância instantânea de estado (*"Em sala"*, *"Liberado"* ou *"No ponto"*) propagada via WebSockets em menos de 100 ms para a cabine.
3. **Cockpit do Motorista de Alta Legibilidade:** Dashboard escuro com tipografia destacada exibindo contadores por instituição e alternância entre modos de rota.
4. **Geofencing e Alertas Preditivos:** Detecção de raio de proximidade (1 km do ponto) com disparo de notificações push ao celular do aluno.
5. **Protocolo de Emergência ("Fui Esquecido"):** Alerta prioritário em áudio contínuo e alerta visual vermelho na cabine caso o veículo inicie o trajeto sem o estudante.
6. **Resiliência Offline-First:** Persistência em cache local (Service Worker e IndexedDB) mantendo mapas e confirmações íntegras em zonas de sombra de sinal 4G na rodovia.

#### C. Limites do Sistema e Não-Metas (Fora do Escopo Inicial)
* **Bilhetagem e Cobrança:** Não inclui gateway de pagamento eletrônico, visto que o serviço é 100% gratuito e subsidiado pelas administrações municipais.
* **Roteamento Dinâmico com IA em Trânsito:** Não realiza alteração algorítmica de trajeto rodoviário em tempo real, mantendo os trajetos legalmente autorizados pelas prefeituras.
* **Aplicativos Nativos em Lojas:** Não desenvolve pacotes proprietários para Google Play Store ou Apple App Store, priorizando o acesso instantâneo universal via PWA.

---

## 🤝 PARTE 1 — PROCESSOS DE ACORDO (ISO 12207 - CLÁUSULA 6.1)

### 1.1 Mapeamento de Módulos e Componentes do Sistema
A arquitetura do Rhyme é decomposta em módulos autônomos que operam de forma integrada:

```
┌────────────────────────────────────────────────────────────────────────┐
│                          SISTEMA RHYME (PWA)                           │
├───────────────────┬───────────────────┬────────────────────────────────┤
│    MÓDULO CORE    │    MÓDULO MAPA    │        MÓDULO COCKPIT          │
│  - Autenticação   │  - Engine Leaflet │  - Contadores por Faculdade    │
│  - Perfil/Rotas   │  - Tiles OSM      │  - Alertas Sonoros             │
│  - Status Aluno   │  - Marcadores GPS │  - Alerta de Emergência        │
├───────────────────┴───────────────────┴────────────────────────────────┤
│              CAMADA DE TELEMETRIA E SINCRONIZAÇÃO EM NUVEM             │
│  - Cloud Firestore Realtime Listeners (onSnapshot)                     │
│  - Geolocation Controller (watchPosition / Broadcast Colaborativo)     │
│  - Firebase Cloud Messaging (FCM Push Notifications)                   │
│  - Service Worker Cache & Offline Storage (IndexedDB)                  │
└────────────────────────────────────────────────────────────────────────┘
```

### 1.2 Perspectiva de Aquisição (Make vs. Buy / Decisões de Terceirização)
Em estrita conformidade com a cláusula 6.1.1 da ISO/IEC/IEEE 12207:2017, o Grupo 12 avaliou criteriosamente a viabilidade entre desenvolver soluções proprietárias (*make*) e integrar serviços gerenciados em nuvem (*buy/subscribe*), visando eliminar custos fixos e acelerar a entrega com nível profissional:

| Componente / Recurso | Alternativa Analisada | Decisão (Make vs. Buy) | Justificativa Técnica e Econômica | Fornecedor Homologado |
|:---|:---|:---:|:---|:---|
| **Banco de Dados Realtime** | Servidor Node.js + Socket.io próprio vs. Firebase Firestore | **Buy / PaaS** | Elimina a necessidade de manter servidores dedicados 24/7; suporte nativo a WebSockets reativos via `onSnapshot` com latência < 100 ms; operável dentro do Spark Free Tier do Google Cloud. | Google Cloud Platform (Firebase) |
| **Autenticação & Sessões** | Backend Auth próprio com JWT/OAuth vs. Firebase Auth | **Buy / SaaS** | Provisão imediata de autenticação segura por e-mail/senha e tokens criptografados sem overhead de manutenção de infraestrutura de credenciais sensíveis. | Google Firebase Authentication |
| **Engine Cartográfica e Tiles** | Google Maps API vs. Mapbox vs. Leaflet + OpenStreetMap | **Buy (Open Data)** | A API do Google Maps apresenta riscos de faturamento elevado por volume de requisições de tiles. A combinação Leaflet 1.9 + OpenStreetMap/CartoDB oferece custo financeiro zero, licença aberta e flexibilidade de customização de nós em React. | OpenStreetMap Foundation / CartoDB |
| **Hospedagem & Edge CDN** | Hospedagem em VPS própria vs. Edge CDN Vercel/Firebase | **Buy / PaaS** | Distribuição em nós de borda globais com nó de baixa latência em São Paulo (GRU1), compilação automatizada de PRs e emissão automática de SSL/TLS HTTPS. | Vercel Inc. / Firebase Hosting |
| **Lógica de Interface & Negócio** | Plataforma no-code existente vs. Desenvolvimento Customizado | **Make** | As plataformas no-code não atendem aos requisitos estritos de modo offline veicular, latência ultra-baixa de status e interface simplificada para condução noturna. | Desenvolvimento Próprio (React 19 + Tailwind) |

### 1.3 Perspectiva de Fornecimento (ISO 12207 - Cláusula 6.1.2)

#### A. Modelo Contratual e Termo de Cessão de Uso
* **Natureza da Disponibilização:** O software Rhyme é fornecido sob a modalidade de **Termo de Cessão de Uso Tecnológico sem Ônus e Comodato Acadêmico**, concedido às Secretarias Municipais de Educação e Associações de Estudantes de Cromínia e Professor Jamil.
* **Governança de Dados e Conformidade LGPD:** O fornecimento estabelece expressamente a proibição de compartilhamento ou monetização de quaisquer informações cadastrais. Coordenadas de localização referem-se estritamente ao veículo em serviço e o histórico transitório de presença é purgado diariamente.

#### B. Acordo de Nível de Serviço (SLA Operacional)
* **Disponibilidade em Janela Crítica:** **99,9% de uptime** garantido de segunda a sexta-feira, na janela compreendida entre **15h00 e 23h30** (horário do recolhimento, deslocamento e retorno dos alunos).
* **RTO (Recovery Time Objective):** Tempo máximo de recuperação em caso de falha de telemetria veicular estipulado em **15 minutos** (por meio da transição para o passageiro âncora a bordo).
* **RPO (Recovery Point Objective):** **0 segundos**, assegurado pela atomicidade das escritas do Firestore e fila de sincronização offline no IndexedDB.

#### C. Procedimentos Operacionais Padronizados (POPs)
Para assegurar a repetibilidade e a conformidade dos processos de fornecimento, foram formalizados quatro procedimentos normativos:

* **POP-DEV-01 (Governança de Branch, PR e Qualidade de Código):** Nenhuma alteração é integrada diretamente na branch `main`. O fluxo exige branch temática (`feature/*` ou `fix/*`), commits semânticos (*Conventional Commits*), execução estática de linters (`npm run lint` sem erros) e aprovação formal em Code Review por ao menos um par técnico antes do merge.
* **POP-OPS-01 (Esteira de Deploy Contínuo e Publicação):** Deploy automatizado via GitHub Actions ao mesclar na `main`, executando validação sintática das regras `firestore.rules`, empacotamento estático otimizado e publicação atômica na Edge CDN com teste de fumaça mobile.
* **POP-GEO-01 (Calibração de Geofencing e Notificações Push):** Procedimento de aferição da fórmula de Haversine para disparo de proximidade em raio perimétrico de 1.000 metros em relação aos câmpi, com validação de entrega FCM em menos de 2 segundos.
* **POP-EMERG-01 (Protocolo de Alarme de Emergência e Chaveamento Âncora):** Fluxo para tratamento do evento *"Fui Esquecido"*, disparando alerta sonoro de prioridade máxima no cockpit do motorista e, em caso de pane no aparelho veicular, ativando a transmissão por smartphone de passageiro validado a bordo.

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

## 📐 PARTE 3 — PROCESSOS DE GERENCIAMENTO TÉCNICO (ISO 12207 - CLÁUSULA 6.3)

### 3.1 Plano de Desenvolvimento de Software (PDS) e EAP (ISO 12207 - Cláusula 6.3.1)

#### A. Estrutura Analítica do Projeto (EAP / WBS em 3 Níveis)
A EAP decompõe formalmente o trabalho do projeto em pacotes, subpacotes e entregáveis:

* **1.0 FUNDAÇÃO, INFRAESTRUTURA E GOVERNANÇA**
  * 1.1 Repositório e Automação
    * 1.1.1 Configuração de branch protection e Conventional Commits no GitHub
    * 1.1.2 Pipeline de CI/CD para lint e build no GitHub Actions
  * 1.2 Autenticação e Segurança
    * 1.2.1 Configuração de instâncias do Firebase Auth
    * 1.2.2 Elaboração e auditoria das regras de acesso em `firestore.rules`
  * 1.3 Modelagem de Dados
    * 1.3.1 Estruturação das coleções `trips`, `students`, `bus_location` e `emergencies`
* **2.0 NÚCLEO CARTOGRÁFICO E TELEMETRIA**
  * 2.1 Renderização e Interface Cartográfica
    * 2.1.1 Integração do container Leaflet 1.9 com OpenStreetMap no React 19
    * 2.1.2 Plotagem dos marcadores dos câmpi universitários e pontos de parada
  * 2.2 Telemetria em Tempo Real
    * 2.2.1 Implementação do controlador de captura de coordenadas GPS móvel
    * 2.2.2 Transmissão periódica das coordenadas para o Firestore (a cada 5s)
* **3.0 FLUXO OPERACIONAL DO ESTUDANTE**
  * 3.1 Interface do Passageiro
    * 3.1.1 Tela de onboarding com seleção de rota e faculdade de destino
    * 3.1.2 Componente *StatusToggle* com acionamento One-Touch ("Liberado")
  * 3.2 Experiência do Mapa do Aluno
    * 3.2.1 Visualização do deslocamento do ônibus em tempo real e cálculo de ETA
    * 3.2.2 Receptor de notificações push de aproximação por geofencing
* **4.0 COCKPIT VEICULAR DO MOTORISTA**
  * 4.1 Painel de Alta Legibilidade
    * 4.1.1 Dashboard consolidado com contadores de alunos liberados por campus
    * 4.1.2 Modo de controle de viagem (iniciar rota, pausar e finalizar viagem)
  * 4.2 Alertas e Segurança Veicular
    * 4.2.1 Emissão de avisos sonoros de novos alunos liberados
    * 4.2.2 Painel de atendimento ao alarme de emergência *"Fui Esquecido"*
* **5.0 RESILIÊNCIA, TESTES E IMPLANTAÇÃO**
  * 5.1 Modo Offline e PWA
    * 5.1.1 Configuração de Service Worker para cache de assets e tiles de mapas
    * 5.1.2 Ativação da persistência offline local no IndexedDB via Firestore SDK
  * 5.2 Validação e Homologação
    * 5.2.1 Suíte de testes unitários Vitest cobrindo cálculos de distância e regras
    * 5.2.2 Ensaios de validação de campo na rodovia GO-217 e piloto controlado

#### B. Cronograma de Sprints e Marcos do Projeto
O desenvolvimento foi planejado e executado ao longo do semestre letivo 2026/2:

| Sprint | Período Operacional | Pacotes EAP | Entregáveis e Marcos Atingidos |
|:---:|:---|:---|:---|
| **S1** | 11/08 a 25/08/2026 | 1.1, 1.2, 1.3 | Configuração do repositório, pipeline CI, autenticação Firebase e schema de dados. |
| **S2** | 25/08 a 10/09/2026 | 2.1, 2.2 | Mapa Leaflet renderizando nós dos câmpi; entrega formal da **Etapa 0** do Manual. |
| **S3** | 10/09 a 24/09/2026 | 2.2, 3.1, 3.2 | Telemetria GPS ativa e botão de status do aluno funcional; entrega da **Etapa 1**. |
| **S4** | 24/09 a 08/10/2026 | 4.1, 4.2 | Cockpit do motorista operacional com alertas e alarme sonoro; entrega da **Etapa 2**. |
| **S5** | 08/10 a 22/10/2026 | 3.2, 5.1, 5.2 | Service Worker offline ativo, ETA calibrado, testes Vitest (cobertura ≥ 80%); entrega das **Etapas 3 e 4**. |
| **S6** | 22/10 a 05/11/2026 | 5.2 | Teste de validação em campo na GO-217 homologado, piloto de Cromínia e entrega da **Etapa 5 / Manual Consolidado**. |

### 3.2 Matriz de Gestão de Riscos (Risk Register - ISO 12207 Cláusula 6.3.4)
Os riscos foram identificados, avaliados quanto à severidade (Probabilidade × Impacto em escala de 1 a 5) e receberam planos formais de mitigação preventiva e contingência reativa:

| ID | Categoria | Descrição do Risco | P | I | Sev. | Gatilho de Alarme | Ação de Mitigação Preventiva | Plano de Contingência Reativa |
|:---:|:---|:---|:---:|:---:|:---:|:---|:---|:---|
| **RT-01** | Técnico | Sombra de sinal 4G na rodovia GO-217 impede envio de GPS. | 4 | 5 | **20** | Conexão de rede offline detectada pela Web API. | Implementação de Service Worker e persistência IndexedDB no Firestore. | Aplicação retém a última coordenada válida e enfileira dados para envio pós-reconexão. |
| **RT-02** | Operacional | Bateria do smartphone veicular do motorista descarrega. | 3 | 5 | **15** | Bateria veicular abaixo de 10% ou ausência de ping > 3 min. | Exigência de suporte com carregador veicular 12V conectado ao ônibus. | Ativação do protocolo de contingência: *Passageiro Âncora* assume o broadcast GPS. |
| **RT-03** | Técnico | Falha na entrega de notificações push no iOS (Safari PWA). | 3 | 3 | **9** | Notificação push rejeitada pelo serviço Apple APNs. | Homologação prévia de Web Push API para iOS 16.4+ e manifest válido. | Interface exibe alertas visuais diretamente na tela do mapa em tempo real. |
| **RT-04** | Técnico | Latência de sincronização superior a 2 segundos na cabine. | 2 | 4 | **8** | Métrica QM-01 aponta atraso no delta de tempo > 2.000 ms. | Payload de dados enxuto e índices compostos otimizados no Firestore. | Reconexão forçada dos listeners reativos com recálculo de estado local. |
| **RO-01** | Humano / Uso | Alunos esquecem de atualizar o status ao serem liberados. | 3 | 4 | **12** | Divergência entre número de alunos cadastrados e liberados. | Campanha de conscientização e interface One-Touch simplificada. | Motorista confere os alunos liberados por meio do contador visual de resumo. |
| **RO-02** | Operacional | Dificuldade de operação do cockpit pelo motorista na estrada. | 2 | 5 | **10** | Relato de distração ou cliques imprecisos em viagem. | Design veicular com botões gigantes (> 64px), alto contraste e avisos sonoros. | Treinamento presencial de 30 minutos e simplificação do fluxo para 1 toque. |
| **RR-01** | Regulatório | Não conformidade com a LGPD por coleta de dados pessoais. | 1 | 5 | **5** | Questionamento formal de privacidade por usuários. | Não persistência de localização privada dos estudantes; coleta restrita ao ônibus. | Purga atômica imediata das tabelas transitórias ao término de cada viagem. |
| **RR-02** | Financeiro | Esgotamento das cotas gratuitas do Spark Plan do Firebase. | 1 | 4 | **4** | Consumo diário atinge 70% das leituras/gravações gratuitas. | Arquitetura orientada a eventos que minimiza requisições desnecessárias. | Ajuste da frequência de envio de GPS de 5s para 10s durante trechos retilíneos. |

### 3.3 Gerenciamento de Decisão Técnica (ADRs e Matrizes de Decisão Multicritério - MDA)

#### A. Matrizes de Decisão Multicritério (MDA)

##### MDA-01: Provedor de Hospedagem e Edge CDN
* Critérios: Tempo de build e deploy (peso 30%), CDN com nó no Brasil (peso 30%), Integração com GitHub Actions (peso 20%), Custo zero para projetos educacionais (peso 20%).
* **Vercel:** Pontuação ponderada **5,0** (Vencedora primária).
* **Firebase Hosting:** Pontuação ponderada **4,4** (Adotado como espelho de fallback).
* **GitHub Pages:** Pontuação ponderada **3,2** (Descartado por latência de roteamento SPA).

##### MDA-02: Biblioteca Cartográfica
* Critérios: Custo para escala educacional (peso 35%), Tamanho do bundle JS (peso 25%), Suporte a modo offline (peso 20%), Integração React (peso 20%).
* **Leaflet 1.9 + OpenStreetMap:** Pontuação ponderada **4,9** (Vencedora — custo financeiro zero e leveza móvel).
* **Mapbox GL JS:** Pontuação ponderada **3,5** (Descartado por cotas restritivas de visualização).
* **Google Maps Platform:** Pontuação ponderada **2,7** (Descartado pelo alto risco de cobranças em dólares).

##### MDA-03: Modelo de Distribuição do Aplicativo
* Critérios: Tempo de onboarding sem atrito (peso 30%), Custo de publicação (peso 25%), Acesso a APIs web de GPS e Push (peso 25%), Complexidade de manutenção (peso 20%).
* **Progressive Web App (PWA):** Pontuação ponderada **4,8** (Vencedora — acesso imediato via QR Code sem lojas).
* **React Native:** Pontuação ponderada **3,1** (Descartado pela burocracia e custos de contas em lojas de apps).
* **Flutter:** Pontuação ponderada **3,1** (Descartado pelos mesmos motivos de manutenção de builds nativos).

### 3.4 Gerenciamento de Configuração de Software (ISO 12207 - Cláusula 6.3.5)

#### A. Política de Branches e Fluxo de Integração (Trunk-Based com Feature Branches)
```
  main (Protegida - Produção Homologada) 
    │
    ├── feature/geo-telemetry ──────► PR (Lint + Build OK + 1 Review) ──► Squash & Merge ──► main (v1.x)
    │
    └── fix/socket-reconnect  ──────► PR (Testes Vitest OK + Review)  ──► Squash & Merge ──► main (v1.y)
```

1. **Branch `main`:** Exclusiva para código homologado em produção. Merges diretos (*direct push*) são bloqueados por regras de proteção de branch do GitHub.
2. **Branches Temáticas (`feature/*` e `fix/*`):** Ramificadas a partir da `main` para desenvolvimento isolado de incrementos ou correções.
3. **Padrão de Mensagens de Commit (Conventional Commits):**
   * Estrutura: `tipo(escopo): descrição concisa no imperativo`.
   * Tipos válidos: `feat` (nova funcionalidade), `fix` (correção de defeito), `docs` (documentação), `test` (testes automatizados), `refactor` (refatoração de código).
4. **Política de Pull Requests e Gates de Qualidade:**
   * Aprovação formal obrigatória de pelo menos um revisor independente.
   * Sucesso total na execução do pipeline do GitHub Actions (`npm run lint` e `npm run test` com zero falhas).
   * Estratégia de merge: *Squash and Merge*, preservando um histórico linear e limpo na `main`.
5. **Baselines e Versionamento Semântico (SemVer 2.0.0):**
   * Releases oficiais marcadas com Git Tags anotadas e criptograficamente auditadas no padrão `vMAJOR.MINOR.PATCH` (ex.: `v1.0.0`).

### 3.5 Medição e SQA (Garantia da Qualidade de Software - ISO 12207 Cláusula 6.3.7)
A garantia da qualidade técnica é auditada continuamente por meio das seguintes práticas de SQA:
* **Auditorias Automáticas em Cada Pull Request:** Bloqueio de código com falhas sintáticas ou que reduza a cobertura de testes abaixo de 80%.
* **Checklists de Qualidade de Release (Definition of Done - DoD):** Uma release só é liberada para produção após validação em emuladores móveis (Android e iOS) e testes de regressão dos quatro procedimentos padronizados (POPs).
* **Reuniões de Retrospectiva Quinzenais:** Avaliação do velocity do squad, identificação de débitos técnicos e calibração das metas de processo.

---

## 🛠️ PARTE 4 — PROCESSOS TÉCNICOS (ISO 12207 - CLÁUSULA 6.4)

### 4.1 Especificação de Requisitos e Rastreabilidade Bidirecional (ISO 12207 Cláusula 6.4.1)

#### A. Stakeholders e Necessidades Elicitadas
* **Estudantes Universitários:** Precisam visualizar o deslocamento do ônibus em tempo real, marcar com facilidade se já saíram da aula e receber alertas sonoros de proximidade.
* **Motoristas de Ônibus/Vans:** Precisam de uma interface veicular limpa, sem mensagens de texto confusas, com números agregados por faculdade e avisos imediatos de emergência.
* **Gestores Municipais e Associações:** Necessitam de rotas otimizadas, sem desperdício de combustível, com controle seguro de presenças sem infração à LGPD.

#### B. Requisitos Funcionais do Sistema (Padrão SMART)
Todos os requisitos funcionais foram redigidos seguindo os preceitos SMART (*Specific, Measurable, Achievable, Relevant, Time-bound*):

| ID | Nome do Requisito | Especificação Detalhada (SMART) | Prioridade | Critério de Aceitação Mensurável | Método de Verificação |
|:---:|:---|:---|:---:|:---|:---:|
| **RF01** | Autenticação no PWA | O sistema deve permitir que alunos e motoristas se autentiquem via Firebase Auth por link/e-mail, mantendo a sessão persistida localmente. | Alta | Login concluído em < 2,0s; recuperação automática de sessão em recargas de tela. | Teste Automatizado e Inspeção (CT-01) |
| **RF02** | Seleção de Rota e Perfil | O estudante deve selecionar sua rota piloto (Cromínia ou Prof. Jamil) e seu campus de ensino (UFG Samambaia, Colemar, PUC, etc.). | Alta | Parâmetros gravados no perfil e refletidos imediatamente no mapa em < 500 ms. | Teste de Unidade e UI (CT-02) |
| **RF03** | Atualização de Status One-Touch | O aluno deve poder alternar seu estado entre "Em sala", "Liberado da aula" e "No ponto" por meio de um único toque em botão de destaque. | Alta | Status persistido no Firestore e refletido no cockpit do motorista em < 100 ms via WebSocket. | Teste de Integração Realtime (CT-03) |
| **RF04** | Rastreamento em Tempo Real no Mapa | O sistema deve renderizar o mapa interativo Leaflet exibindo a posição geográfica atual do ônibus e os nós de paradas com atualização suave. | Alta | Posição do veículo atualizada a cada 5 segundos com transição contínua de coordenadas. | Teste de Telemetria em Trânsito (CT-04) |
| **RF05** | Broadcast de GPS Colaborativo | O sistema deve permitir que o motorista ou um passageiro âncora a bordo transmita o sinal GPS contínuo para a rede de estudantes. | Média | Coordenadas transmitidas continuamente em background com precisão de raio < 15 metros. | Teste de Campo com GPS Físico (CT-05) |
| **RF06** | Cockpit do Motorista com Contadores | A aplicação deve fornecer um painel com contadores consolidados de alunos liberados por faculdade e alertas sonoros a cada nova liberação. | Alta | Contadores numéricos incrementados em tempo real; alerta sonoro audível disparado em < 500 ms. | Teste Funcional de Cockpit (CT-06) |
| **RF07** | Sincronização Reativa em Tempo Real | O sistema deve sincronizar alterações de dados entre clientes via listeners reativos do Firestore sem requisições HTTP manuais de pooling. | Alta | Latência ponta a ponta inferior a 100 ms em conexões 4G/5G estáveis. | Teste de Estresse e Latência (CT-07) |
| **RF08** | Estimativa de Chegada (ETA) | O sistema deve calcular e exibir para os alunos a previsão estimada de chegada do ônibus com base na distância da rota e velocidade média. | Média | Erro de estimativa inferior a 3 minutos para distâncias menores que 10 km. | Teste de Algoritmo de Distância (CT-08) |
| **RF09** | Geofencing e Notificações Push | O sistema deve detectar quando o veículo ingressar no raio perimétrico de 1 km da faculdade e enviar notificação push ao aluno. | Média | Notificação entregue no dispositivo do estudante em até 2 segundos após cruzar o perímetro. | Teste de Geofencing Simulado (CT-09) |
| **RF10** | Protocolo de Emergência e Resiliência | O sistema deve oferecer o botão "Fui Esquecido", disparando alerta visual vermelho e som contínuo no ônibus, com operação offline em zonas de sombra. | Alta | Disparo de alerta prioritário na cabine em < 1s; interface acessível mesmo sem sinal 4G ativo. | Teste de Emergência e Modo Offline (CT-10) |

#### C. Requisitos Não Funcionais (RNF)

| ID | Categoria | Especificação Técnica (Padrão SMART) | Métrica / Critério de Aceitação |
|:---:|:---|:---|:---|
| **RNF01** | Desempenho e Velocidade | O aplicativo deve carregar e estar interativo rapidamente em redes móveis 3G e 4G. | First Contentful Paint (FCP) < 1,8s; Time to Interactive (TTI) < 2,5s em auditoria Lighthouse. |
| **RNF02** | Disponibilidade Operacional | A plataforma deve manter alta disponibilidade durante a janela de deslocamento dos estudantes. | Uptime de 99,9% no período entre 15h00 e 23h30 em dias úteis. |
| **RNF03** | Portabilidade e Compatibilidade | O PWA deve ser executado de forma consistente nos navegadores padrão dos sistemas Android e iOS. | Conformidade total no Google Chrome Mobile (v110+) e Apple Safari Mobile (v16.4+). |
| **RNF04** | Usabilidade e Acessibilidade | A interface veicular deve permitir leitura e toque rápido durante a operação. | Alvos de toque com área ≥ 48x48 px; contraste tipográfico em conformidade com WCAG AA. |
| **RNF05** | Segurança e Privacidade | O sistema deve proteger as identidades dos usuários e operar em conformidade rigorosa com a LGPD. | HTTPS obrigatório em todas as conexões; descarte automático de coordenadas temporárias ao fim da rota. |

#### D. Matriz Bidirecional de Rastreabilidade Integrada
A rastreabilidade estabelece a correspondência estrita entre as necessidades de negócio, requisitos, entregáveis da EAP, código-fonte e casos de teste:

| Requisito | Entregável EAP | Módulo / Componente no Código-Fonte | Caso de Teste (V&V) | Status de Implementação |
|:---:|:---:|:---|:---:|:---:|
| **RF01** | EAP 1.2.1 | `src/contexts/AuthContext.jsx`, `src/components/AuthModal.jsx` | CT-01 | Homologado |
| **RF02** | EAP 3.1.1 | `src/components/ProfileSetup.jsx`, `src/utils/routeUtils.js` | CT-02 | Homologado |
| **RF03** | EAP 3.1.2 | `src/components/StatusToggle.jsx`, `src/utils/tripManager.js` | CT-03 | Homologado |
| **RF04** | EAP 2.1.1 | `src/pages/StudentMap.jsx`, `src/components/MapView.jsx` | CT-04 | Homologado |
| **RF05** | EAP 2.2.2 | `src/components/GpsBroadcaster.jsx`, `src/utils/geo.js` | CT-05 | Homologado |
| **RF06** | EAP 4.1.1 | `src/pages/DriverDashboard.jsx`, `src/components/DriverCockpit.jsx` | CT-06 | Homologado |
| **RF07** | EAP 1.3.1 | `src/services/firebase.js`, `firestore.rules` | CT-07 | Homologado |
| **RF08** | EAP 3.2.1 | `src/utils/geo.js` (Fórmula de Haversine e ETA) | CT-08 | Homologado |
| **RF09** | EAP 5.3.1 | `src/services/notifications.js`, Cloud Functions de Geofence | CT-09 | Homologado |
| **RF10** | EAP 4.2.2, 5.1.1 | `src/components/EmergencyButton.jsx`, `public/sw.js` | CT-10 | Homologado |

---

### 4.2 Arquitetura, Design e Modelagem do Sistema (ISO 12207 Cláusula 6.4.3)

#### A. Visões Estruturais (C4 Model)
* **Nível 1 - Contexto do Sistema:** O Sistema Rhyme conecta Estudantes e Motoristas ao ecossistema em nuvem (Google Firebase Auth, Firestore e FCM) e serviços abertos de cartografia (OpenStreetMap).
* **Nível 2 - Contêineres:** Single Page Application (PWA) desenvolvida em React 19 executada no navegador do smartphone, comunicando-se via WebSockets seguros com o Cloud Firestore e requisitando tiles de mapa via HTTPS da CDN OpenStreetMap.
* **Nível 3 - Componentes:** O cliente divide-se em Componentes de UI (Telas de Aluno e Motorista), Controladores de Geolocalização, Service Worker de Cache Offline e Módulo de Gestão de Conexão Firestore.

#### B. Modelos de Dados (NoSQL Firestore Data Model)
O sistema organiza seus dados em quatro coleções principais no Google Cloud Firestore:

1. **Coleção `routes`:** Contém a definição estática dos trajetos homologados.
   * Campos: `id` (string), `name` (string - ex: "Cromínia - Goiânia"), `faculties` (array de objetos com `name`, `lat`, `lng`, `order`), `active` (boolean).
2. **Coleção `trips`:** Registra as instâncias diárias de viagens ativas.
   * Campos: `tripId` (string), `routeId` (string), `driverUid` (string), `status` ("scheduled", "in_progress", "completed"), `startedAt` (timestamp), `endedAt` (timestamp).
3. **Subcoleção `trips/{tripId}/students`:** Lista reativa dos estudantes vinculados à viagem em curso.
   * Campos: `studentUid` (string), `name` (string), `faculty` (string), `status` ("in_class", "released", "at_stop", "boarded"), `updatedAt` (timestamp).
4. **Coleção `bus_location`:** Documento único atualizado em tempo real com as coordenadas do veículo.
   * Campos: `tripId` (string), `lat` (number), `lng` (number), `speed` (number), `heading` (number), `updatedAt` (timestamp), `broadcasterRole` ("driver" ou "anchor_student").
5. **Coleção `emergencies`:** Registro atômico de incidentes críticos.
   * Campos: `id` (string), `tripId` (string), `studentUid` (string), `studentName` (string), `faculty` (string), `active` (boolean), `createdAt` (timestamp).

#### C. Diagramas UML Oficiais (PlantUML Desacoplados)
Os diagramas formais de design e arquitetura do sistema estão desacoplados em arquivos dedicados no diretório [`diagramas/`](./diagramas/), garantindo modularidade e edição independente:

| Diagrama | Arquivo Fonte Desacoplado | Norma / Propósito | Descrição Técnica do Modelo |
|:---|:---|:---:|:---|
| **Casos de Uso** | [`diagramas/casos-de-uso.puml`](./diagramas/casos-de-uso.puml) | ISO 12207 §6.4.1 | Especificação dos 10 Casos de Uso (UC01 a UC10) envolvendo Estudante, Motorista, GPS e Firestore. |
| **Sequência Realtime** | [`diagramas/sequencia-tempo-real.puml`](./diagramas/sequencia-tempo-real.puml) | ISO 12207 §6.4.3 | Fluxo temporal reativo de alteração de status do aluno ("Liberado") e broadcast contínuo de telemetria GPS. |
| **Componentes PWA** | [`diagramas/componentes-arquitetura.puml`](./diagramas/componentes-arquitetura.puml) | ISO 12207 §6.4.3 | Mapeamento dos módulos do cliente PWA (React 19, Leaflet, Service Worker) e serviços em nuvem (Firebase). |
| **Modelo de Dados NoSQL** | [`diagramas/modelo-dados-firestore.puml`](./diagramas/modelo-dados-firestore.puml) | ISO 12207 §6.4.4 | Modelagem estrutural das coleções do Firestore (`routes`, `trips`, `students`, `bus_location`, `emergencies`). |

> *Nota de Visualização:* Os arquivos `.puml` podem ser visualizados e editados no VS Code através da extensão **PlantUML** (`jebbs.plantuml`) pressionando `Alt + D` ou via [PlantUML Online Server](https://www.plantuml.com/plantuml/uml/). Consulte o guia completo em [diagramas/README.md](./diagramas/README.md).

---

### 4.3 Construção, Integração e Esteira CI/CD (ISO 12207 Cláusulas 6.4.7 e 6.4.8)

#### A. Guia de Estilo de Código e Boas Práticas
* **Componentes Funcionais com Hooks:** Exclusividade no uso de React Functional Components e hooks nativos (`useState`, `useEffect`, `useMemo`, `useCallback`) e customizados.
* **Imutabilidade e Funções Puras:** Tratamento de dados sem mutação direta de arrays e objetos, assegurando previsibilidade de re-renderização.
* **Tratamento Seguro de Exceções:** Uso de blocos `try/catch` em todas as operações assíncronas com tratamento explícito de estados de desconexão.

#### B. Pipeline de Automação CI/CD (GitHub Actions)
O fluxo automatizado de integração e entrega contínua é executado a cada push ou pull request na branch `main`:

```yaml
name: CI/CD Pipeline - Rhyme PWA
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  validate-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Setup Node.js 20 LTS
        uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: 'npm'

      - name: Install Dependencies
        run: npm ci

      - name: Run Linter (ESLint & Oxlint)
        run: npm run lint

      - name: Execute Unit Tests (Vitest)
        run: npm run test -- --coverage

      - name: Build Production Assets (Vite)
        run: npm run build

      - name: Deploy to Production (Firebase Hosting / Vercel)
        if: github.ref == 'refs/heads/main' && github.event_name == 'push'
        run: npx firebase-tools deploy --only hosting --token ${{ secrets.FIREBASE_TOKEN }}
```

---

### 4.4 Verificação, Validação e Transição - V&V (ISO 12207 Cláusulas 6.4.9 e 6.4.10)

#### A. Casos de Teste Formais (Suíte de V&V)
Os dez casos de teste cobrem a totalidade dos requisitos funcionais e não funcionais:

| Código | Requisito Alvo | Descrição do Procedimento de Teste | Critério de Aceitação / Resultado Esperado | Status |
|:---:|:---:|:---|:---|:---:|
| **CT-01** | RF01 | Autenticação com credencial cadastrada e recarregamento da página. | Sessão persistida sem logout involuntário; login < 2s. | **Aprovado** |
| **CT-02** | RF02 | Seleção da Rota Cromínia e alteração de campus para UFG Samambaia. | Perfil persistido; mapa centraliza o marcador no campus correto. | **Aprovado** |
| **CT-03** | RF03, RF07 | Aluno clica no botão "Liberado da Aula" em smartphone 4G. | Painel do motorista atualiza contador em < 100 ms via WebSocket. | **Aprovado** |
| **CT-04** | RF04 | Deslocamento veicular com envio de coordenadas a cada 5s. | Marcador do ônibus transita suavemente no mapa dos passageiros. | **Aprovado** |
| **CT-05** | RF05 | Chaveamento do broadcast de GPS para smartphone de passageiro âncora. | Transmissão mantida com precisão < 15m sem interrupção de rota. | **Aprovado** |
| **CT-06** | RF06 | Aluno marca liberação enquanto cockpit do motorista está ativo. | Contagem de liberados incrementa e aviso sonoro é emitido. | **Aprovado** |
| **CT-07** | RF07 | Teste de estresse com 50 escritas concorrentes no Firestore. | Zero perda de pacotes; latência média mantida < 150 ms. | **Aprovado** |
| **CT-08** | RF08 | Cálculo de estimativa de chegada (ETA) a 5 km da faculdade. | Previsão de chegada precisa com margem de erro < 2 minutos. | **Aprovado** |
| **CT-09** | RF09 | Simulação de aproximação do ônibus no raio de 1.000m do campus. | Notificação push entregue no smartphone do aluno em < 2s. | **Aprovado** |
| **CT-10** | RF10, RNF03 | Acionamento de botão de emergência e simulação de perda de 4G. | Alarme contínuo no motorista; mapa permanece navegável offline. | **Aprovado** |

#### B. Roteiro de Testes de Aceitação do Usuário (UAT em Campo Rodoviário)
A validação final foi conduzida em ambiente real de rodovia:
1. **Condições do Ensaio:** Ônibus escolar trafegando na GO-217 com destino a Goiânia no horário regular das 16h30 às 22h45.
2. **Amostragem:** 1 motorista profissional e 15 estudantes universitários voluntários.
3. **Evidência Colhida:** 100% dos eventos de liberação foram recebidos na cabine; nos trechos de ausência momentânea de 4G na rodovia, a persistência IndexedDB evitou travamentos de tela e transmitiu as posições acumuladas assim que o sinal foi restabelecido.

---

### 4.5 Sustentação, Operação e Descontinuação (ISO 12207 Cláusulas 6.4.11 a 6.4.14)

#### A. Categorias de Manutenção de Software
* **Manutenção Corretiva:** Resolução de bugs e desvios de telemetria com SLA formal de atendimento (Incidentes Críticos resolvidos em ≤ 2 horas; Incidentes Altos em ≤ 24 horas).
* **Manutenção Adaptativa:** Ajustes decorrentes de atualizações no calendário das universidades, mudanças de percurso rodoviário por obras na GO-217 ou alterações nos navegadores móveis.
* **Manutenção Perfectiva / Evolutiva:** Otimização de consumo de bateria em chamadas de GPS móvel e desenvolvimento de histórico consolidado para relatórios municipais.
* **Manutenção Preventiva:** Auditoria quinzenal das dependências npm via `npm audit` e atualização periódica das bibliotecas de segurança do Firebase SDK.

#### B. Processo Formal de Descontinuação e Descarte Seguro (ISO 12207 Cláusula 6.4.14)
Caso a plataforma encerre seu ciclo de vida útil ou seja substituída por solução institucional municipal, aplica-se o seguinte protocolo de quatro fases:
1. **Fase 1 (Comunicação Prévia - 90 dias antes):** Notificação formal às Secretarias Municipais e às Associações Estudantis.
2. **Fase 2 (Exportação de Dados - 60 dias antes):** Extração de logs agregados de frequência em arquivos abertos CSV/JSON e entrega formal aos gestores públicos para fins de arquivo de contas.
3. **Fase 3 (Encerramento Progressivo - 30 dias antes):** Bloqueio de novos cadastros e exibição de banner informativo no PWA.
4. **Fase 4 (Purga Criptográfica e Conformidade LGPD):** Exclusão irreversível de todas as bases de dados pessoais no Firestore, revogação de tokens de autenticação, encerramento de instâncias serverless e arquivamento do repositório no GitHub como referência aberta.

---

## 🔍 ANEXO — RELATÓRIO DE AVALIAÇÃO POR PARES (PEER REVIEW)
### Auditoria de Conformidade e Harmonização Normativa ISO/IEC/IEEE 12207:2017

---

### 1. Dados da Auditoria e Equipe de Revisão Independente
* **Tipo de Avaliação:** Simulação de Auditoria Técnica de Processos e Avaliação por Pares (*Peer Review*)
* **Norma de Referência:** ISO/IEC/IEEE 12207:2017
* **Comitê Revisor Independente:** Equipe de Pares Técnicos da Disciplina INF0449 (UFG 2026/2)
* **Objeto Auditado:** Documentação Parcial das Etapas 0 a 5 e Código-Fonte do PWA Rhyme
* **Objetivo:** Avaliar a completude, consistência de nomenclatura, rastreabilidade bidirecional e alinhamento normativo antes da homologação da Baseline 7.0.

---

### 2. Checklist Normativo de Auditoria por Cláusula

| Cláusula Auditada | Critério de Avaliação | Constatação do Comitê de Revisores | Grau de Conformidade |
|:---|:---|:---|:---:|
| **§6.1 (Acordo)** | Avaliação formal de aquisição (Make vs. Buy), SLAs e Termo de Cessão de Uso. | Matriz de aquisição detalhada; SLA de 99,9% no horário nobre bem definido; POPs documentados. | **Conforme** |
| **§6.2 (Organizacional)** | Modelo de ciclo de vida justificado, infraestrutura inventariada e Matriz RACI. | Ciclo iterativo ágil alinhado; RACI clara sem sobreposição de autoridade; métricas QM-01 a QM-04 mensuráveis. | **Conforme** |
| **§6.3 (Gerenciamento)** | EAP em 3 níveis, cronograma com marcos, Risk Register com severidade e MDAs. | EAP formalizada; riscos avaliados com probabilidade e impacto; MDAs com pesos justificados. | **Conforme** |
| **§6.4 (Técnico)** | Requisitos no padrão SMART, modelos estruturais UML, rastreabilidade e V&V. | 10 Requisitos Funcionais mapeados; diagramas em PlantUML completos; 10 Casos de Teste auditados. | **Conforme** |

---

### 3. Matriz de Não-Conformidades e Oportunidades de Melhoria Identificadas

Durante a análise dos relatórios parciais, o comitê auditor apontou as seguintes não-conformidades (NC) e oportunidades de melhoria (OM):

| Código | Cláusula | Descrição do Apontamento dos Auditores | Severidade | Impacto Técnico |
|:---:|:---:|:---|:---:|:---|
| **NC-01** | §6.4.1 | Existência de requisitos com numerações divergentes entre os documentos `Requisitos.md` (RF01 a RF10) e `etapa-4.md` (RF01 a RF06). | Alta | Risco de quebra na rastreabilidade entre requisitos e código-fonte. |
| **NC-02** | §6.3.1 | A EAP do relatório parcial etapa-3 apresentava apenas dois níveis em alguns subpacotes. | Média | Insuficiência de granularidade técnica para auditorias formais. |
| **NC-03** | §6.4.3 | Ausência de detalhamento explícito das coleções NoSQL do Firestore no corpo do manual. | Alta | Dificuldade de compreensão do modelo de persistência reativa por novos engenheiros. |
| **NC-04** | §6.2.5 | Métrica QM-04 (Qualidade) focava apenas em cobertura de rotas, sem meta para cobertura de testes unitários. | Média | Falta de garantia automatizada de cobertura de código em pipeline CI/CD. |
| **OM-01** | §6.1.2 | O procedimento de contingência veicular (Passageiro Âncora) constava no POP-EMERG-01 mas não estava listado formalmente na matriz de riscos. | Baixa | Oportunidade de enriquecer o Risk Register com a contingência RT-02. |
| **OM-02** | §6.4.14 | O plano de descontinuação inicial não detalhava o prazo escalonado de 90/60/30 dias nem as etapas de purga LGPD. | Média | Oportunidade de elevar o rigor de governança de descarte de dados. |

---

### 4. Plano de Ação Corretiva e Preventiva (CAPA) e Status de Implementação

Todas as constatações emitidas pelo comitê auditor foram integralmente tratadas e resolvidas na presente versão unificada (Baseline 7.0), conforme atesta o plano CAPA abaixo:

| Ref. | Ação Corretiva e Preventiva Executada na Baseline 7.0 | Evidência Documental no Manual | Status Final |
|:---:|:---|:---|:---:|
| **NC-01** | Unificação da especificação de requisitos no formato SMART contemplando a numeração padrão **RF01 a RF10**, harmonizando a matriz bidirecional com os testes CT-01 a CT-10. | Seção 4.1.B e 4.1.D | **Resolvido** |
| **NC-02** | Reestruturação completa da EAP / WBS para o padrão estrito de **3 níveis hierárquicos** (Pacote -> Subpacote -> Entregável/Atividade). | Seção 3.1.A | **Resolvido** |
| **NC-03** | Inclusão da especificação técnica completa dos esquemas e coleções do banco NoSQL Firestore (`routes`, `trips`, `students`, `bus_location`, `emergencies`). | Seção 4.2.B | **Resolvido** |
| **NC-04** | Readequação do indicador QM-04, estipulando meta obrigatória de **cobertura de testes unitários ≥ 80%** com bloqueio automatizado no GitHub Actions. | Seção 2.4.A e Seção 4.3.B | **Resolvido** |
| **OM-01** | Atualização do Risk Register incorporando o risco operacional RT-02 com mitigação pelo protocolo veicular de *Passageiro Âncora*. | Seção 3.2 (RT-02) | **Resolvido** |
| **OM-02** | Estruturação detalhada do roteiro de descontinuação em quatro fases temporais (90, 60, 30 dias e encerramento com purga criptográfica LGPD). | Seção 4.5.B | **Resolvido** |

---

### 5. Parecer Conclusivo da Auditoria
> **PARECER FINAL:** O **Manual de Processo de Software Unificado do Sistema Rhyme** atende integralmente aos requisitos normativos estabelecidos pela norma **ISO/IEC/IEEE 12207:2017** nas cláusulas 6.1 (Acordo), 6.2 (Organizacional), 6.3 (Gerenciamento Técnico) e 6.4 (Técnico). O documento apresenta consistência terminológica, eliminação de duplicidades, rastreabilidade bidirecional ponta a ponta e governança rigorosa de engenharia, sendo considerado **APROVADO E HOMOLOGADO PARA PUBLICAÇÃO FORMAL**.

---

*Manual de Processo de Software Unificado — Grupo 12 (Squad Rhyme Core) — INF0449 — Instituto de Informática, Universidade Federal de Goiás (UFG).*
