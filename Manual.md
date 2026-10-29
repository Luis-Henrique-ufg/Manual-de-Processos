# Manual de Processos de Software

## Rhyme — Gestão e Telemetria em Tempo Real de Transporte Universitário Intermunicipal

**Referencial:** ISO/IEC/IEEE 12207:2017

---

## Capa

| | |
|:---|:---|
| **Título** | Manual de Processos de Software — Sistema Rhyme |
| **Equipe** | Grupo 12 — Squad Rhyme Core |
| **Disciplina** | INF0449 — Processos de Engenharia de Software (2026/2) |
| **Instituição** | Universidade Federal de Goiás (UFG) — Instituto de Informática |
| **Apresentação** | 26/11/2026 (G9 a G12) — 20 a 30 min, todos os membros |

**Composição da Equipe e Papéis de Referência**

| Membro | Papel de Referência no Projeto |
|:---|:---|
| Matheus Marquez de Carvalho Rodrigues | Engenharia de Requisitos e Produto |
| Luis Henrique Oliveira de Jesus | Arquitetura de Software e Frontend |
| Heitor Gonçalves Costa | Infraestrutura, Nuvem e DevOps |
| Carlos Daniel Lopes de Araújo | Garantia da Qualidade (SQA), Verificação e Validação |

---

## Contracapa — Histórico de Versões

| Versão | Data | Alteração |
|:---:|:---:|:---|
| 1.0 | 10/09/2026 | Apresentação do software, escopo, formulação do problema e premissas. |
| 2.0 | 17/09/2026 | Processos de Acordo (aquisição, fornecimento, acordos de nível de serviço, POPs). |
| 3.0 | 17/09/2026 | Processos Organizacionais (ciclo de vida, infraestrutura, RACI por papéis, qualidade). |
| 4.0 | 01/10/2026 | Gerenciamento Técnico (EAP, riscos, decisões técnicas, gerência de configuração). |
| 5.0 | 01/10/2026 | Processos Técnicos (requisitos, arquitetura, design e plano de V&V). |
| 6.0 | 01/10/2026 | Sustentação (implantação, esteira CI/CD, manutenção e descontinuação). |
| 7.0 | 22/10/2026 | Unificação das etapas e avaliação por pares com plano CAPA implementado. |
| **8.0** | **29/10/2026** | **Adequação estrutural à Atividade (6 capítulos); adoção de Mapbox Free Tier; generalização de municípios e papéis; padronização terminológica do painel do motorista.** |

---

# Capítulo 1 — Apresentação do Software

## 1.1 Nome e descrição

O **Rhyme** é um *Progressive Web App* (PWA) de telemetria e coordenação de eventos em tempo real, concebido para sincronizar o transporte universitário intermunicipal entre municípios do interior e os polos universitários da capital, substituindo a comunicação fragmentada e insegura conduzida via grupos de WhatsApp.

## 1.2 O que é, o que faz e que problema resolve

O Rhyme exibe a posição do veículo em tempo real em mapa interativo, permite ao estudante notificar seu estado de liberação acadêmica com um único toque (*one-touch*) e provê ao condutor um painel veicular simplificado com contadores consolidados por instituição de ensino.

Problemas resolvidos:

1. **Distração perigosa do condutor:** eliminação da leitura de mensagens picadas e áudios com o veículo em trânsito.
2. **Vulnerabilidade noturna de estudantes:** redução da espera em pontos escuros e desprovidos de previsão estimada de chegada (*ETA*).
3. **Desperdício de recursos públicos:** eliminação de desvios e paradas em câmpi universitários sem demanda confirmada de embarque, economizando combustível subsidiado.
4. **Ausência de dados históricos e auditoria:** geração de histórico consolidado de viagens e horários para dimensionamento da frota pelas administrações locais.

## 1.3 Público-alvo e contexto de uso

## 1.4 Quem usa, em que situação e em que ambiente

| Usuário | Situação de uso | Ambiente de operação |
|:---|:---|:---|
| Estudante universitário | Notifica liberação das aulas e acompanha o deslocamento do veículo | Smartphone (PWA), no câmpus ou ponto de embarque, conectividade móvel variável |
| Condutor / Motorista | Acompanha contadores por faculdade e alertas operacionais durante a viagem | Smartphone acoplado a suporte veicular 12V no painel do veículo, em rodovias e vias urbanas |
| Gestão municipal / Associação | Consulta regularidade de rotas, frequências e dimensionamento de demanda | Navegador web em computadores ou dispositivos móveis |

Rotas operacionais atendidas: trajetos regulares conectando os **municípios de origem parceiros** aos centros universitários da capital (UFG Samambaia, Colemar Natal e Silva, PUC Goiás, UniCamps e faculdades associadas), totalizando cerca de 30 a 40 estudantes por rota diária, com viagens no período vespertino e retorno ao término das aulas noturnas.

## 1.5 Escopo e principais funcionalidades

**Dentro do escopo**

| # | Funcionalidade Central |
|:---:|:---|
| 1 | Rastreamento e exibição contínua da posição do veículo em mapa interativo (taxa de atualização a cada 5 s) |
| 2 | Status one-touch do estudante: alternância rápida entre "Em sala", "Liberado" e "No ponto" |
| 3 | Painel veicular do motorista com contadores consolidados por faculdade e alertas sonoros |
| 4 | Geofencing perimétrico (raio de 1 km) com emissão de notificações push de aproximação |
| 5 | Protocolo de emergência operacional ("Fui Esquecido") com sinalização audiovisual de alta prioridade |
| 6 | Operação resiliente com suporte offline-first (Service Worker e persistência local via IndexedDB) |

**Fora do escopo:** módulos de cobrança ou bilhetagem tarifária, recálculo dinâmico de trajetos por IA em trânsito e publicação de aplicativos nativos empacotados em lojas proprietárias.

## 1.6 Restrições e premissas

| Tipo | Especificação |
|:---|:---|
| Restrição | Custo financeiro nulo de infraestrutura: utilização estrita de tiers gratuitos (*free tiers*) de serviços em nuvem (Firebase e Mapbox). |
| Restrição | Instabilidade de cobertura de rede de dados móveis (zonas de sombra 4G) ao longo das rodovias intermunicipais. |
| Restrição | Conformidade rigorosa com a LGPD: coleta restrita à telemetria do veículo; ausência de rastreamento da geolocalização privada do aluno e purga diária dos registros transitórios. |
| Restrição | Execução do projeto no período letivo acadêmico de 2026/2. |
| Premissa | Dispositivos dos usuários finais dispõem de navegadores modernos compatíveis com PWA (Google Chrome Mobile v110+ ou Apple Safari v16.4+). |
| Premissa | O condutor do transporte mantém o dispositivo veicular conectado à alimentação 12V contínua durante todo o percurso. |
| Premissa | As rotas e pontos de parada homologados são previamente acordados entre as prefeituras e as comunidades estudantis. |

---

# Capítulo 2 — Processos de Acordo

## 2.1 Processo de aquisição

Avaliação de fornecimento de componentes terceiros (*make* vs. *buy*):

| Recurso | Decisão | Fornecedor Homologado | Justificativa Técnica e Econômica |
|:---|:---:|:---|:---|
| Banco de dados realtime | Buy (PaaS) | Google Cloud Platform (Firestore) | Elimina manutenção de infraestrutura de servidores próprios; sincronização reativa via `onSnapshot` com latência < 100 ms; cota suficiente no Spark Free Tier. |
| Autenticação & Sessões | Buy (SaaS) | Google Firebase Authentication | Mecanismo pronto e seguro de autenticação com tokens criptografados sem armazenamento de credenciais sensíveis pela aplicação. |
| Mapas e tiles cartográficos | Buy (Free Tier) | Mapbox (Plano Free) + Leaflet | Fornecimento estável de tiles de alta resolução via Mapbox API no plano gratuito (até 50.000 requisições mensais), consumido pelo cliente Leaflet 1.9 sem custo de licenciamento. |
| Notificações push | Buy (PaaS) | Firebase Cloud Messaging (FCM) | Entrega integrada de notificações push web diretamente ao Service Worker do PWA sem custo adicional. |
| Hospedagem e Edge CDN | Buy (PaaS) | Vercel (primária) / Firebase Hosting (espelho) | Distribuição de assets em nós de borda (Edge) de baixa latência em São Paulo, integração contínua com GitHub e SSL/TLS automatizado. |
| Interface e regras de negócio | **Make** | Equipe de Desenvolvimento (React 19 + Tailwind) | Ferramentas no-code existentes não suportam controle fino de cache offline, latência reduzida e interface de alto contraste para ambiente veicular. |

## 2.2 Processo de fornecimento

- **Modalidade de entrega:** Distribuição contínua do PWA sob protocolo seguro HTTPS, acessível instantaneamente por URL pública e distribuição de QR Code institucional, sem intermediários de lojas de aplicativos.
- **Instrumento contratual:** Termo de Cessão de Uso Tecnológico sem Ônus (comodato acadêmico e institucional), disponibilizado às secretarias municipais de educação e às associações estudantis dos municípios atendidos. Cláusula expressa de proibição de monetização e vedação de compartilhamento de dados cadastrais.
- **Critérios de aceite:** Homologação completa dos 10 Casos de Teste (CT-01 a CT-10, seção 5.4) e validação bem-sucedida em rota rodoviária real.
- **Modelo de suporte:** Manutenção corretiva com tempo de resposta baseado em criticidade (SLA de 2 h para incidentes críticos de indisponibilidade da telemetria e 24 h para defeitos funcionais de média severidade).

| Indicador de Serviço | Meta Estabelecida |
|:---|:---|
| Disponibilidade da plataforma | 99,9% durante a janela operacional crítica (segunda a sexta-feira, das 15h00 às 23h30) |
| RTO (*Recovery Time Objective*) | 15 minutos (tempo limite para contingência de broadcast via passageiro âncora) |
| RPO (*Recovery Point Objective*) | 0 segundos (atomicidade garantida pelo Firestore combinada à fila local no IndexedDB) |

Procedimentos Operacionais Padronizados (POPs) formalizados:

| Procedimento | Finalidade e Diretriz Operacional |
|:---|:---|
| **POP-DEV-01** | Governança de código: ramificação por branches temáticas, commits semânticos, ausência total de alertas em linters e revisão por pares obrigatória antes de integração na `main`. |
| **POP-OPS-01** | Esteira de publicação contínua via GitHub Actions com verificação de regras de segurança (`firestore.rules`) e build otimizado com publicação automática. |
| **POP-GEO-01** | Calibração do algoritmo de geofencing (Fórmula de Haversine em raio de 1.000 m) e garantia de disparo de push em tempo inferior a 2 s. |
| **POP-EMERG-01** | Atendimento ao alerta de emergência ("Fui Esquecido") e protocolo operacional de transferência de transmissão GPS para o passageiro âncora. |

## 2.3 Fornecedores e parceiros relevantes

| Parceiro / Entidade | Papel no Ecossistema |
|:---|:---|
| Google Cloud / Firebase | Fornecimento de banco de dados NoSQL reativo (Firestore), autenticação, push notifications e hosting espelho |
| Mapbox Inc. | Provedor de camada de tiles cartográficos e renderização geográfica sob plano gratuito |
| Vercel Inc. | Infraestrutura de hospedagem primária em CDN de alta performance com nó no Brasil |
| GitHub | Governança de repositório, controle de versões, automação de testes e esteira CI/CD |
| Administrações Municipais Parceiras | Prefeituras cessionárias responsáveis pelo transporte público e apoio logístico institucional |
| Associações de Estudantes Universitários | Usuários beneficiários, multiplicadores de adesão e homologadores de campo |

---

# Capítulo 3 — Processos Organizacionais Habilitadores

## 3.1 Modelo de ciclo de vida

**Híbrido Iterativo-Incremental (Scrum com fluxo contínuo Kanban), com cadência de sprints quinzenais.**

```
[Visão & Requisitos] ──► [Sprint N: Incremento] ──► [Deploy e Homologação]
         ▲                                                  │
         └─────────── Validação em Rota Rodoviária ◄────────┘
```

Justificativa técnica da escolha:

1. **Comportamento empírico da conectividade móvel:** as variações de sinal 4G/GPS em trechos rodoviários não podem ser antecipadas unicamente em bancada; sprints curtas viabilizam ensaios de campo incrementais.
2. **Mitigação escalonada de incertezas arquiteturais:** mecanismos críticos (WebSockets do Firestore e armazenamento em IndexedDB) foram validados antes da adição do subsistema de geofencing.
3. **Harmonização com marcos de entrega:** viabiliza a geração contínua de baselines auditáveis e conformes com a ISO 12207 sem o risco de retrabalho do modelo em cascata.

## 3.2 Infraestrutura e ferramentas

| Categoria | Ferramenta / Plataforma | Finalidade Técnica |
|:---|:---|:---|
| Runtime & Build | Node.js 20 LTS, Vite 6 | Ambiente de execução e empacotador de alta velocidade com HMR |
| Camada Frontend | React 19, Tailwind CSS 4 | Interface reativa, modular e estilização de alto contraste veicular |
| Cartografia & Tiles | Leaflet 1.9, React-Leaflet 5, Mapbox Free API | Motor cartográfico vetorial com baixo consumo de CPU e bateria |
| Banco de Dados & Nuvem | Cloud Firestore, Firebase Auth, FCM | Armazenamento de dados NoSQL, autenticação e mensageria serverless |
| Emulação & Testes | Firebase Emulator Suite, Vitest, Testing Library | Testes locais de segurança de banco e suíte de testes automatizados |
| Análise Estática & Lint | ESLint, Oxlint | Padronização de qualidade de código e conformidade sintática |
| Versionamento & CI/CD | Git, GitHub, GitHub Actions | Controle de versão distribuído, gates de qualidade e automação de deploy |
| Hospedagem de Produção | Vercel Edge Network, Firebase Hosting | Distribuição global de assets web com HTTPS e failover |
| Dispositivos Alvo | Plataformas Android (10+) e iOS (15+) | Execução em smartphones de condutores e passageiros |

## 3.3 Justificativa estratégica e viabilidade

| Dimensão de Análise | Avaliação de Viabilidade |
|:---|:---|
| **Estratégica** | Elimina a distração veicular ao volante, eleva a segurança física dos alunos no horário noturno e gera economia estimada de 10% a 15% de combustível ao eliminar trajetos ociosos. |
| **Técnica** | Alta viabilidade: stack tecnológica consolidada no mercado, ecossistema PWA amplamente suportado por smartphones modernos sem fricção de instalação. |
| **Econômica** | Custo financeiro zero: dimensionamento rigoroso dentro das cotas gratuitas do Firebase e do plano free do Mapbox, com margem de segurança configurável (ajuste de taxa de amostragem de GPS se consumo atingir 70%). |
| **Operacional** | Alta aceitação: interação one-touch sem necessidade de treinamento complexo; capacitação de condutores realizada em apenas 30 minutos. |
| **Legal / Regulatória** | Totalmente aderente à LGPD: ausência de armazenamento de localização de pessoas físicas e eliminação periódica de dados operacionais ao fim do percurso diário. |
| **Cronograma** | Plenamente exequível dentro do semestre letivo distribuído em seis sprints de desenvolvimento. |

Conclusão: **O projeto é técnica, econômica e operacionalmente viável.**

## 3.4 Papéis, competências e capacitação (RACI)

*Convenção RACI: R = Responsável pela Execução, A = Aprovador Final, C = Consultado, I = Informado.*

| Atividade do Ciclo de Vida | Engenharia de Requisitos | Arquitetura & Frontend | Infraestrutura & DevOps | Garantia da Qualidade (SQA) |
|:---|:---:|:---:|:---:|:---:|
| Elicitação e refinamento de requisitos | **A / R** | C | C | C |
| Modelagem do banco NoSQL e regras | C | R | **A / R** | C |
| Interface do usuário e mapas | I | **A / R** | C | C |
| Geofencing e notificações push | C | R | R | **A** |
| Testes automatizados e ensaios de campo | C | C | I | **A / R** |
| Gestão de releases e esteira CI/CD | I | R | **A / R** | C |
| Resposta a incidentes de telemetria | C | I | R | **A / R** |

**Plano de capacitação da equipe:** nivelamento nas cláusulas 6.1 a 6.4 da norma ISO/IEC/IEEE 12207; padrões de arquitetura PWA offline-first (ciclo de vida de Service Workers, estratégias de cache *Stale-While-Revalidate* e persistência no IndexedDB); e workshops de escrita segura de `firestore.rules` utilizando o Firebase Emulator Suite.

## 3.5 Plano de qualidade (critérios e métricas)

| ID | Métrica de Qualidade | Meta Alvo | Procedimento de Medição | Ação Mitigadora em Desvio |
|:---:|:---|:---|:---|:---|
| **QM-01** | Latência de sincronização realtime | < 100 ms (4G/5G); < 1.000 ms (3G) | Confronto entre `timestamp` de gravação no Firestore e entrega no listener | Minimização de payload e refinamento de consultas reativas |
| **QM-02** | Eficácia do geofencing preditivo | ≥ 98% de notificações entregues antes do ponto | Log de eventos de aproximação comparado ao horário real de embarque | Reajuste dinâmico do raio perimétrico (ajuste de 1.000 m para 1.500 m) |
| **QM-03** | Performance Web Vitals mobile | LCP < 2,0 s; TTI < 2,5 s | Auditoria automatizada do Lighthouse Mobile integrada ao CI | *Code-splitting*, compressão de assets e pré-aquecimento de tiles |
| **QM-04** | Cobertura de testes automatizados | ≥ 80% das linhas e branches críticas | Relatório gerado pela suíte Vitest em cada execução | Bloqueio automatizado de merge em PRs que degradem o índice |

Garantia da Qualidade Contínua: inspeções estáticas automáticas a cada Pull Request, critérios formais de aceite na *Definition of Done* (DoD) e reuniões quinzenais de retrospectiva técnica.

## 3.6 Gestão do conhecimento

1. **Repositório documental único:** manuais, diagramas e especificações técnicas sob controle de versão Git.
2. **Registros Formais de Decisões de Arquitetura (ADRs):** registro padronizado de contexto, alternativas computadas e consequências técnicas (seção 4.4).
3. **Post-mortems sem culpabilidade (*Blameless Post-Mortems*):** relatórios objetivos de lições aprendidas após qualquer anomalia constatada em rotas de teste.
4. **Revisões cruzadas de código (*Peer Code Review*):** distribuição equilibrada de PRs entre as diferentes disciplinas de engenharia para descentralização do conhecimento.

---

# Capítulo 4 — Processos de Gerenciamento Técnico

## 4.1 Plano de projeto

**Escopo:** Sistema PWA Rhyme conforme delimitado na seção 1.5.

**Estrutura Analítica do Projeto (EAP / WBS em 3 níveis)**

| Pacote (Nível 1) | Subpacote (Nível 2) | Entregáveis e Pacotes de Trabalho (Nível 3) |
|:---|:---|:---|
| **1.0 Fundação e Infraestrutura** | 1.1 Repositório e Automação | 1.1.1 Branch protection e Conventional Commits; 1.1.2 Pipeline de CI/CD |
| | 1.2 Autenticação e Segurança | 1.2.1 Configuração Firebase Auth; 1.2.2 Regras de segurança `firestore.rules` |
| | 1.3 Modelagem de Dados | 1.3.1 Estruturação das coleções `routes`, `trips`, `students`, `bus_location`, `emergencies` |
| **2.0 Cartografia e Telemetria** | 2.1 Interface Geográfica | 2.1.1 Integração Leaflet com Mapbox API; 2.1.2 Marcadores de câmpi e paradas |
| | 2.2 Telemetria em Tempo Real | 2.2.1 Controlador de captura GPS; 2.2.2 Transmissão periódica das coordenadas (a cada 5 s) |
| **3.0 Fluxo do Estudante** | 3.1 Interface do Passageiro | 3.1.1 Tela de onboarding e seleção de trajeto; 3.1.2 Componente *StatusToggle* (One-Touch) |
| | 3.2 Mapa e Alertas do Aluno | 3.2.1 Acompanhamento veicular e cálculo de ETA; 3.2.2 Notificações push por geofencing |
| **4.0 Painel do Motorista** | 4.1 Painel Veicular de Controle | 4.1.1 Contadores consolidados por câmpus; 4.1.2 Controle de estado de viagem |
| | 4.2 Sinalização e Segurança | 4.2.1 Emissão de alertas sonoros; 4.2.2 Interface de atendimento ao alarme "Fui Esquecido" |
| **5.0 Resiliência e Implantação** | 5.1 Modo Offline e PWA | 5.1.1 Service Worker para cache de assets e mapas; 5.1.2 Persistência local no IndexedDB |
| | 5.2 Validação e Homologação | 5.2.1 Suíte de testes unitários Vitest; 5.2.2 Ensaio em rota rodoviária real |

**Cronograma de Sprints e Marcos Operacionais**

| Sprint | Período Operacional | Pacotes EAP | Marco / Entregável Homologado |
|:---:|:---|:---|:---|
| **S1** | 11/08 a 25/08/2026 | 1.1, 1.2, 1.3 | Repositório estruturado, CI/CD, Auth provisionado e schema NoSQL definido |
| **S2** | 25/08 a 10/09/2026 | 2.1, 2.2 | Mapa interativo Leaflet renderizando pontos de embarque; entrega da Etapa 0 |
| **S3** | 10/09 a 24/09/2026 | 2.2, 3.1, 3.2 | Telemetria ativa e alternância de status one-touch do aluno; entrega da Etapa 1 |
| **S4** | 24/09 a 08/10/2026 | 4.1, 4.2 | Painel veicular do motorista com contadores e sinal sonoro; entrega da Etapa 2 |
| **S5** | 08/10 a 22/10/2026 | 3.2, 5.1, 5.2 | Service Worker offline ativo, cálculo de ETA, testes unitários (cobertura ≥ 80%); Etapas 3 e 4 |
| **S6** | 22/10 a 05/11/2026 | 5.2 | Validação em trânsito rodoviário homologada e consolidação final do manual |

**Recursos:** Equipe de desenvolvimento multidisciplinar (seção 3.4), serviços e ferramentas sob cotas gratuitas (seção 3.2).  
**Entregas:** Plataforma PWA homologada em produção, manual de processos e apresentação em 26/11.

## 4.2 Plano de gestão de riscos

*Cálculo de Severidade = Probabilidade (1 a 5) × Impacto (1 a 5).*

| ID | Risco Identificado | P | I | Sev. | Ação Preventiva de Mitigação | Plano de Contingência Reativa |
|:---:|:---|:---:|:---:|:---:|:---|:---|
| **RT-01** | Sombra de rede móvel (ausência momentânea de sinal) na rodovia | 4 | 5 | **20** | Configuração de Service Worker e ativação de persistência IndexedDB no Firestore | Retenção da última coordenada válida no mapa e envio acumulado pós-reconexão |
| **RT-02** | Esgotamento de bateria do aparelho transmissor no veículo | 3 | 5 | **15** | Exigência de suporte com carregador veicular 12V permanentemente conectado | Transferência operacional imediata do broadcast GPS para o passageiro âncora a bordo |
| **RO-01** | Estudante não registrar liberação da aula no aplicativo | 3 | 4 | **12** | Interface one-touch simplificada e conscientização junto às associações | Motorista realiza checagem visual complementar do contador consolidado |
| **RO-02** | Dificuldade de operação do painel pelo motorista na estrada | 2 | 5 | **10** | Design com botões de grandes dimensões (> 64 px), alto contraste e confirmação por áudio | Capacitação presencial de 30 minutos e fluxo de interação reduzido a 1 toque |
| **RT-03** | Incompatibilidade ou falha de entrega de push notifications no iOS | 3 | 3 | **9** | Homologação estrita de manifest PWA e Web Push API para Safari iOS 16.4+ | Exibição de alertas visuais destacados diretamente no mapa em tempo real |
| **RT-04** | Latência de sincronização superior a 2 segundos na cabine | 2 | 4 | **8** | Payload otimizado de dados e índices compostos estritos no Firestore | Reinicialização automática de listeners com recálculo de estado em memória |
| **RR-01** | Não conformidade com diretrizes da LGPD | 1 | 5 | **5** | Não coleta de localização individual do estudante; telemetria restrita ao veículo | Purga imediata de dados transitórios de presença ao encerramento da viagem |
| **RR-02** | Exaustão das cotas mensais gratuitas de banco e mapas | 1 | 4 | **4** | Arquitetura orientada a eventos minimizando requisições redundantes | Reajuste dinâmico da frequência de envio de GPS de 5 s para 10 s em velocidade de cruzeiro |

## 4.3 Plano de gestão de configuração

```
main (branch protegida - produção)
  ├── feature/*  ──► PR (lint + build + testes + 1 code review) ──► Squash & Merge ──► main
  └── fix/*      ──► PR (testes de regressão + aprovação)       ──► Squash & Merge ──► main
```

| Componente | Política de Controle e Governança |
|:---|:---|
| Política de Branches | A branch `main` é restrita a código homologado em produção, com bloqueio estrito a commits diretos (*direct push*). |
| Padronização de Commits | Padrão *Conventional Commits*: prefixos obrigatórios `feat`, `fix`, `docs`, `test`, `refactor`. |
| Quality Gates em PRs | Revisão independente aprovada por ao menos um par técnico; execução automatizada de linter e testes no GitHub Actions com zero falhas. |
| Estratégia de Integração | Operação via *Squash and Merge*, preservando histórico linear e auditável na branch principal. |
| Versionamento Semântico | Emissão de tags Git anotadas seguindo a norma SemVer 2.0.0 (`vMAJOR.MINOR.PATCH`). |

## 4.4 Registro de decisões técnicas relevantes (ADRs)

| ADR | Decisão Homologada | Contexto Operacional | Alternativas Analisadas (Pontuação) | Consequência e Trade-offs |
|:---:|:---|:---|:---|:---|
| **ADR-001** | Distribuição via **Progressive Web App (PWA)** | Necessidade de acesso imediato sem atrito de download e instalação em lojas | PWA (4,8); React Native (3,1); Flutter (3,1) | Elimina taxas e burocracia de lojas; push no ecossistema iOS depende da versão 16.4+. |
| **ADR-002** | Motor **Leaflet + Mapbox API (Free Tier)** | Exigência de renderização cartográfica de alta qualidade com custo zero | Mapbox + Leaflet (4,9); Google Maps Platform (2,7); Mapbox SDK nativo (3,5) | Alta performance móvel e ausência de risco de faturamento em moeda estrangeira. |
| **ADR-003** | Backend Serverless via **Google Firebase** | Sincronização reativa instantânea sem custos fixos de servidores dedicados | Firebase Firestore (4,8); Node.js + Socket.io dedicado (3,2) | Latência ultrabaixa (< 100 ms); impõe monitoramento preventivo de limites de cotas gratuitas. |
| **ADR-004** | Hospedagem em **Vercel** com espelho **Firebase** | Distribuição de assets com nó de borda no Brasil e compilação contínua | Vercel (5,0); Firebase Hosting puro (4,4); GitHub Pages (3,2) | Rápido tempo de carregamento e redundância estratégica de disponibilidade. |

Critérios de ponderação nas matrizes de decisão: custo financeiro, consumo de memória e bateria em dispositivos móveis, suporte nativo a cache offline, facilidade de manutenção e tempo de carregamento.

## 4.5 Métricas de acompanhamento do projeto

| Indicador de Acompanhamento | Meta de Controle | Fonte de Coleta | Periodicidade de Aferição |
|:---|:---|:---|:---:|
| Velocity e vazão de entregas | Estabilidade de itens concluídos por ciclo | Quadro Kanban do projeto | Quinzenal |
| Aderência aos marcos do cronograma | 100% dos pacotes previstos entregues no prazo | Cronograma de Sprints (seção 4.1) | A cada encerramento de sprint |
| Cobertura de testes unitários (QM-04) | Manutenção de cobertura ≥ 80% | Relatório da suíte Vitest no CI | Em cada Pull Request submetido |
| Taxa de aprovação em testes de aceitação | 10 de 10 casos de teste aprovados | Relatório de V&V (seção 5.4) | A cada baseline de release |
| Riscos críticos de severidade ≥ 15 | 0 riscos sem plano de mitigação ativo | Matriz de Riscos (seção 4.2) | Quinzenal |
| Tendência de débito técnico | Redução contínua de apontamentos | Retrospectivas de sprint | Quinzenal |
| Utilização de cotas gratuitas (Firebase/Mapbox) | Manutenção abaixo de 70% do teto gratuito | Dashboards das plataformas | Semanal |

---

# Capítulo 5 — Processos Técnicos

## 5.1 Requisitos

### 5.1.1 Documento de requisitos do sistema

**Requisitos Funcionais (Padrão SMART)**

| ID | Nome do Requisito | Especificação Detalhada (SMART) | Prioridade | Critério de Aceitação Mensurável |
|:---:|:---|:---|:---:|:---|
| **RF01** | Autenticação de Usuários | O sistema deve permitir autenticação de estudantes e motoristas via Firebase Auth, retendo a sessão persistida localmente no navegador. | Alta | Login concluído em tempo inferior a 2,0 s; sessão restaurada automaticamente ao recarregar a tela. |
| **RF02** | Seleção de Rota e Câmpus | O estudante deve selecionar sua rota municipal e seu câmpus de destino para filtragem dos dados geográficos. | Alta | Parâmetros salvos no perfil e nós cartográficos centralizados no mapa em menos de 500 ms. |
| **RF03** | Atualização de Status One-Touch | O aluno deve poder alternar seu estado operacional ("Em sala", "Liberado" ou "No ponto") por meio de um único toque em botão de destaque. | Alta | Estado gravado no Firestore e refletido no painel do motorista em menos de 100 ms via WebSocket reativo. |
| **RF04** | Rastreamento Veicular no Mapa | A aplicação deve renderizar mapa interativo exibindo a posição geográfica atualizada do transporte e os pontos de parada. | Alta | Atualização visual contínua da posição do veículo a cada 5 segundos. |
| **RF05** | Broadcast de GPS Colaborativo | O sistema deve permitir que o motorista ou um passageiro âncora a bordo transmita as coordenadas de geolocalização do veículo. | Média | Coordenadas transmitidas com precisão perimétrica de raio menor que 15 metros. |
| **RF06** | Painel do Motorista com Contadores | O sistema deve fornecer tela consolidada com totalizadores de alunos liberados por câmpus e disparar alertas sonoros a cada nova liberação. | Alta | Contadores numéricos incrementados em tempo real; alerta sonoro audível reproduzido em menos de 500 ms. |
| **RF07** | Sincronização Reativa em Tempo Real | A aplicação deve propagar alterações de dados instantaneamente via listeners do Firestore sem requisições periódicas manuais (*polling*). | Alta | Latência fim a fim inferior a 100 ms em conexões móveis estáveis. |
| **RF08** | Estimativa de Chegada (ETA) | O sistema deve calcular e apresentar ao estudante a estimativa de tempo restante até o ponto de embarque. | Média | Margem de erro do ETA menor que 3 minutos para distâncias inferiores a 10 km. |
| **RF09** | Geofencing e Notificações Push | O sistema deve identificar o ingresso do veículo no raio de 1 km da faculdade e emitir notificação push ao aluno. | Média | Notificação push recebida no dispositivo em tempo inferior a 2 segundos após cruzar o perímetro delimitado. |
| **RF10** | Protocolo de Emergência e Resiliência | O sistema deve oferecer o botão de emergência "Fui Esquecido" e manter navegabilidade com dados em cache em zonas de sombra de rede. | Alta | Disparo de alarme prioritário visual e contínuo no painel do motorista em menos de 1 s; mapa funcional em modo offline. |

**Requisitos Não Funcionais (RNF)**

| ID | Categoria | Especificação Técnica | Métrica e Critério de Aceitação |
|:---:|:---|:---|:---|
| **RNF01** | Desempenho e Velocidade | Rápido carregamento e interatividade sob conexões de rede móvel | FCP < 1,8 s; TTI < 2,5 s em auditoria do Lighthouse Mobile |
| **RNF02** | Disponibilidade Operacional | Alta disponibilidade durante toda a janela de deslocamento dos alunos | Uptime ≥ 99,9% no intervalo de 15h00 às 23h30 em dias úteis |
| **RNF03** | Portabilidade e Compatibilidade | Compatibilidade total com os principais navegadores móveis | Execução homologada em Google Chrome Mobile (v110+) e Safari iOS (v16.4+) |
| **RNF04** | Usabilidade e Acessibilidade | Adequação ergonômica para visualização e acionamento em ambiente veicular | Elementos de toque com área mínima de 48×48 px; contraste tipográfico conforme WCAG AA |
| **RNF05** | Privacidade e Segurança | Tratamento ético de dados conforme as exigências da LGPD | Comunicação exclusivamente via HTTPS; descarte automático de coordenadas temporárias ao término do trajeto |

### 5.1.2 Rastreabilidade de requisitos

| Requisito | Entregável EAP | Módulo / Arquivo no Código-Fonte (`src/`) | Caso de Teste Associado | Status de Homologação |
|:---:|:---:|:---|:---:|:---:|
| **RF01** | EAP 1.2.1 | `contexts/AuthContext.jsx`, `pages/Login.jsx` | CT-01 | Homologado |
| **RF02** | EAP 3.1.1 | `pages/Profile.jsx`, `utils/routeUtils.js` | CT-02 | Homologado |
| **RF03** | EAP 3.1.2 | `pages/StudentMap.jsx`, `utils/tripManager.js` | CT-03 | Homologado |
| **RF04** | EAP 2.1.1 | `pages/StudentMap.jsx`, `utils/useTripData.js` | CT-04 | Homologado |
| **RF05** | EAP 2.2.2 | `pages/DriverDashboard.jsx`, `utils/geo.js` | CT-05 | Homologado |
| **RF06** | EAP 4.1.1 | `pages/DriverDashboard.jsx`, `utils/audioEffects.js` | CT-06 | Homologado |
| **RF07** | EAP 1.3.1 | `config/firebase.js`, `firestore.rules` | CT-07 | Homologado |
| **RF08** | EAP 3.2.1 | `utils/geo.js` (Fórmula de Haversine e estimativa de ETA) | CT-08 | Homologado |
| **RF09** | EAP 3.2.2 | `functions/index.js` (`checkBusDistanceAndNotify`), FCM | CT-09 | Homologado |
| **RF10** | EAP 4.2.2, 5.1.1 | `pages/StudentMap.jsx`, `public/sw.js` | CT-10 | Homologado |

### 5.1.3 Critérios de aceitação

Cada requisito funcional possui critério numérico e observável associado. O requisito é formalmente aceito apenas quando seu respectivo caso de teste (seção 5.4) é executado com êxito sem violações de métricas estabelecidas.

### 5.1.4 Registro de stakeholders e necessidades elicitadas

| Categoria de Stakeholder | Necessidades Elicitadas | Requisitos Mapeados |
|:---|:---|:---|
| Estudantes Universitários | Acompanhar a posição do veículo, notificar liberação com 1 toque e receber alertas de proximidade | RF02, RF03, RF04, RF08, RF09 |
| Condutores / Motoristas | Painel simples e limpo, substituição de mensagens de texto por contadores numéricos agregados e avisos sonoros de emergência | RF06, RF10, RNF04 |
| Gestores Municipais e Associações | Rotas regulares sem desperdício de diesel público, controle transparente de demanda e aderência estrita à LGPD | RF07, RNF02, RNF05 |

## 5.2 Arquitetura e Design

### 5.2.1 Arquitetura do sistema

Visão geral: Arquitetura em camadas baseada em Single Page Application PWA (React 19), comunicando-se de forma assíncrona com os serviços em nuvem gerenciados:

```
┌────────────────────────────────────────────────────────────────────────┐
│                        CLIENTE PWA (React 19)                          │
│   Módulo do Estudante      Módulo de Mapa         Painel do Motorista  │
│   (Auth, perfil, status)   (Leaflet, Mapbox)      (contadores e som)   │
├────────────────────────────────────────────────────────────────────────┤
│   Camada de Resiliência: Service Worker (Cache) + IndexedDB Offline    │
├────────────────────────────────────────────────────────────────────────┤
│   Controladores: Geolocation API (watchPosition) + Haversine Engine    │
├────────────────────────────────────────────────────────────────────────┤
│   Backend Nuvem: Firebase Auth · Firestore (onSnapshot) · FCM Push     │
└────────────────────────────────────────────────────────────────────────┘
```

**Modelo de Dados NoSQL (Estrutura de Coleções no Cloud Firestore):**

| Coleção | Atributos e Estrutura Principal |
|:---|:---|
| `routes` | `id` (string), `name` (string), `faculties` (array de objetos com `name`, `lat`, `lng`, `order`), `active` (boolean) |
| `trips` | `tripId` (string), `routeId` (string), `driverUid` (string), `status` (`scheduled`, `in_progress`, `completed`), `startedAt`, `endedAt` |
| `trips/{tripId}/students` | `studentUid` (string), `name` (string), `faculty` (string), `status` (`in_class`, `released`, `at_stop`, `boarded`), `updatedAt` |
| `bus_location` | `tripId` (string), `lat` (number), `lng` (number), `speed` (number), `heading` (number), `updatedAt` (timestamp), `broadcasterRole` |
| `emergencies` | `id` (string), `tripId` (string), `studentUid` (string), `studentName` (string), `faculty` (string), `active` (boolean), `createdAt` |

### 5.2.2 Diagramas de design

Os modelos formais em PlantUML estão desacoplados no diretório [`diagramas/`](./diagramas/):

| Modelo | Arquivo Fonte | Conteúdo Modelado |
|:---|:---|:---|
| Casos de Uso | [`casos-de-uso.puml`](./diagramas/casos-de-uso.puml) | Mapeamento dos 10 casos de uso envolvendo Estudante, Condutor, GPS e Firestore |
| Sequência em Tempo Real | [`sequencia-tempo-real.puml`](./diagramas/sequencia-tempo-real.puml) | Sincronização reativa de status ("Liberado") e fluxo contínuo de telemetria |
| Componentes de Software | [`componentes-arquitetura.puml`](./diagramas/componentes-arquitetura.puml) | Acoplamento dos módulos do PWA, Service Worker, Leaflet e serviços em nuvem |
| Dados NoSQL | [`modelo-dados-firestore.puml`](./diagramas/modelo-dados-firestore.puml) | Modelo estrutural de coleções e subcoleções do banco de dados Firestore |

### 5.2.3 Justificativa das escolhas tecnológicas

| Tecnologia | Racional Técnico e Justificativa |
|:---|:---|
| React 19 + Vite | Modelo de componentes declarativo eficiente para UI reativa e tempos de compilação reduzidos |
| Tailwind CSS | Estilização por classes utilitárias que garantem paleta consistente de alto contraste para visibilidade noturna veicular |
| Leaflet + Mapbox API | Camada cartográfica com baixo consumo de memória e tiles gratuitos de alto desempenho |
| Firebase Platform | Baixo esforço de manutenção de infraestrutura, com WebSockets nativos e escalabilidade transparente |
| PWA Web Standards | Ausência de barreiras de download em lojas e suporte universal a smartphones via navegador web |
| Vitest | Integração transparente com o empacotador Vite, com rápida execução de testes e relatórios de cobertura nativos |

## 5.3 Implementação e Integração

### 5.3.1 Padrões de codificação adotados

- Exclusividade no uso de componentes funcionais em React com hooks nativos e customizados.
- Imutabilidade rigorosa em alterações de estado local e estruturas de dados em memória.
- Tratamento preventivo de exceções em todas as chamadas assíncronas via blocos `try/catch`, exibindo feedback de desconexão.
- Conformidade obrigatória com as regras do ESLint e Oxlint, sem supressão arbitrária de avisos.

### 5.3.2 Plano de integração entre componentes

| Sequência | Etapa de Integração | Critério de Validação |
|:---:|:---|:---|
| 1 | Autenticação via Firebase Auth com recuperação de perfil e sessão | CT-01 e CT-02 |
| 2 | Vinculação do motor Leaflet/Mapbox com a coleção de telemetria veicular | CT-04 |
| 3 | Sincronização reativa entre o botão de liberação do aluno e o painel do motorista | CT-03, CT-06 e CT-07 |
| 4 | Captura de coordenadas GPS do aparelho condutor com envio atômico ao banco | CT-05 |
| 5 | Gatilho de cálculo de geofencing com disparo de mensagens via FCM | CT-09 |
| 6 | Acoplamento de cache via Service Worker e fila offline via IndexedDB | CT-10 |

### 5.3.3 Registro de testes unitários e de integração

| Categoria | Foco de Teste | Ferramental | Casos Associados |
|:---|:---|:---|:---|
| Testes Unitários de Algoritmo | Precisão da fórmula de Haversine e estimativa de ETA | Vitest | CT-08 e CT-09 |
| Testes Unitários de Componente | Renderização e alternância de estado no `StatusToggle` | Vitest + RTL | CT-01 e CT-03 |
| Testes de Integração de Nuvem | Validação de regras em `firestore.rules` sob concorrência | Firebase Emulator Suite | CT-03 e CT-07 |
| Testes de Resiliência e Offline | Interrupção simulada de rede móvel e acionamento de emergência | Emulador e ensaio manual | CT-10 |

Meta de controle: manutenção de cobertura de código ≥ 80% (QM-04).

### 5.3.4 Rastreabilidade entre código e requisitos

A correspondência formal entre cada requisito especificado, componente de implementação e caso de teste encontra-se detalhada na matriz da seção 5.1.2.

## 5.4 Verificação, Validação e Transição

### 5.4.1 Plano de verificação e validação

| Atividade de V&V | Responsável | Frequência de Execução |
|:---|:---|:---|
| Verificação Estática e Testes Unitários no CI | Garantia da Qualidade (SQA) / DevOps | A cada Pull Request submetido |
| Revisão Cruzada de Código (*Peer Review*) | Equipe de Desenvolvimento (Pares) | Em todas as alterações destinadas à `main` |
| Validação de Casos de Aceitação (CT-01 a CT-10) | Garantia da Qualidade (SQA) | A cada baseline de release |
| Ensaios em Rota Rodoviária Real | Equipe de Desenvolvimento + Condutor | Marcos pré-determinados em cronograma (Sprint S6) |

### 5.4.2 Critérios de aceitação por stakeholder

| Stakeholder | Critério de Aceitação Mensurável |
|:---|:---|
| Estudante Universitário | Capacidade de sinalizar saída da aula com 1 toque e visualizar o deslocamento do veículo no mapa (RF03, RF04). |
| Condutor do Transporte | Visualização dos contadores consolidados por instituição e alerta sonoro emitido em menos de 500 ms (RF06); alarme prioritário de emergência em < 1 s (RF10). |
| Gestão Municipal | Inexistência de retenção de localização de pessoas físicas e garantia de descarte periódico ao término da viagem (RNF05). |

### 5.4.3 Relatório de testes de aceitação

| Código | Requisito Alvo | Procedimento Executado | Resultado Esperado | Status |
|:---:|:---:|:---|:---|:---:|
| **CT-01** | RF01 | Autenticação com credencial cadastrada e recarregamento forçado de página | Sessão persistida sem logout involuntário; autenticação em < 2 s | **Aprovado** |
| **CT-02** | RF02 | Seleção da rota municipal de origem e escolha de campus universitário | Perfil salvo; mapa centraliza o marcador no câmpus em < 500 ms | **Aprovado** |
| **CT-03** | RF03, RF07 | Estudante clica no botão "Liberado da Aula" sob rede móvel 4G | Painel do motorista incrementa contador em menos de 100 ms | **Aprovado** |
| **CT-04** | RF04 | Deslocamento veicular com emissão contínua de coordenadas a cada 5 s | Marcador do veículo se desloca com suavidade na tela dos passageiros | **Aprovado** |
| **CT-05** | RF05 | Transferência do broadcast GPS para aparelho de passageiro âncora a bordo | Telemetria mantida ativa com margem de erro < 15 m sem queda de sinal | **Aprovado** |
| **CT-06** | RF06 | Aluno sinaliza liberação com o painel do motorista aberto e em foco | Contador numérico incrementado e alerta sonoro reproduzido em < 500 ms | **Aprovado** |
| **CT-07** | RF07 | Teste de carga simulando 50 escritas simultâneas de presença no Firestore | Nenhuma perda de pacote; latência média mantida abaixo de 150 ms | **Aprovado** |
| **CT-08** | RF08 | Cálculo algorítmico de previsão de chegada a 5 km do ponto de embarque | Previsão de chegada precisa com desvio menor que 2 minutos | **Aprovado** |
| **CT-09** | RF09 | Simulação de aproximação do veículo no raio delimitado de 1.000 m do câmpus | Notificação push recebida no dispositivo do aluno em até 2 segundos | **Aprovado** |
| **CT-10** | RF10, RNF03 | Acionamento do botão "Fui Esquecido" sob simulação de ausência de 4G | Alarme sonoro contínuo no condutor; mapa permanece navegável offline | **Aprovado** |

**Ensaio de Validação em Rota Real:** Conduzido em viagem regular noturna com transporte escolar intermunicipal entre os municípios de origem e os câmpi da capital. O ensaio contou com condutor voluntário e amostragem de estudantes; 100% das confirmações foram refletidas no painel do motorista e o suporte offline via IndexedDB garantiu a integridade das informações nos trechos com oscilação de sinal móvel.

### 5.4.4 Plano de transição e implantação do sistema

| Fase de Transição | Ação Operacional |
|:---:|:---|
| **Fase 1: Homologação** | Publicação da versão de produção estável na Vercel (com espelho no Firebase Hosting) após aprovação de todos os testes de V&V. |
| **Fase 2: Piloto Controlado** | Implantação em rota piloto monitorada com suporte direto da equipe técnica. |
| **Fase 3: Treinamento e Adesão** | Condução de treinamento presencial com os motoristas (30 minutos) e distribuição de material com QR Code aos estudantes. |
| **Fase 4: Expansão Operacional** | Disponibilização do serviço para as demais rotas dos municípios participantes. |
| **Fase 5: Handoff Institucional** | Entrega da governança operacional às associações estudantis e secretarias locais com documentação completa. |

Procedimento de Reversão (*Rollback*): reversão instantânea de versão pela plataforma Vercel para a tag anotada anterior em caso de anomalia impeditiva.

## 5.5 Operação, Manutenção e Descontinuação

### 5.5.1 Procedimentos de operação e monitoramento

| Parâmetro Monitorado | Mecanismo de Aferição | Limiar de Alarme |
|:---|:---|:---|
| Disponibilidade da aplicação | Verificação automatizada de status HTTP e console da CDN | Interrupção superior a 15 min (violação de RTO) |
| Latência de comunicação (QM-01) | Registro do tempo delta entre escrita e recebimento nos listeners | Atraso superior a 2.000 ms (risco RT-04) |
| Consumo de cotas gratuitas | Painéis de faturamento Google Cloud e Mapbox | Consumo atingindo 70% do teto mensal gratuito |
| Frequência de telemetria do veículo | Verificação de atualização do campo `updatedAt` em `bus_location` | Ausência de novos pontos por mais de 3 min (risco RT-02) |
| Entrega de notificações push | Relatórios de entrega do Firebase Cloud Messaging | Taxa de falhas consecutivas de push (risco RT-03) |
| Incidentes operacionais em rota | Registro formal de ocorrências e condução de post-mortems técnicos | Qualquer anomalia reportada por condutor ou aluno |

### 5.5.2 Plano de manutenção de software

| Modalidade de Manutenção | Escopo de Atuação | Prazos e Periodicidade |
|:---|:---|:---|
| **Corretiva** | Resolução de falhas de telemetria, erros em regras de segurança ou bugs de interface | Incidentes críticos em até 2 h; defeitos de média gravidade em até 24 h |
| **Preventiva** | Varreduras de vulnerabilidades de dependências (`npm audit`) e atualização de SDKs | Execução quinzenal |
| **Adaptativa** | Adequação a alterações em calendários acadêmicos, mudanças viárias ou atualizações de navegadores | Atendimento sob demanda de órgãos públicos |
| **Evolutiva** | Otimização de consumo de bateria e emissão de relatórios consolidados de frequência para prefeituras | Implementação orientada ao backlog de produto |

### 5.5.3 Estratégia de descontinuação e migração de dados

| Etapa Temporal | Momento de Ação | Procedimento Executado |
|:---:|:---|:---|
| **1. Notificação** | 90 dias antes do encerramento | Comunicação formal às secretarias municipais de educação e diretorias das associações de estudantes. |
| **2. Exportação de Dados** | 60 dias antes do encerramento | Geração de relatórios agregados de frequência em formatos abertos (CSV e JSON) entregues aos órgãos públicos para prestação de contas. |
| **3. Bloqueio Progressivo** | 30 dias antes do encerramento | Desativação de novos cadastros e fixação de banner informativo de descontinuação no PWA. |
| **4. Purga e Encerramento** | Marco final de encerramento | Exclusão definitiva de todas as coleções do Firestore, revogação de tokens de autenticação, desativação de instâncias e arquivamento do repositório Git em conformidade estrita com a LGPD. |

---

# Capítulo 6 — Avaliação e Melhoria dos Processos de Software

## 6.1 Referencial e recorte

- **Referencial normativo:** Cláusulas 6.1 a 6.4 da norma internacional ISO/IEC/IEEE 12207:2017.
- **Recorte metodológico de avaliação:** Foco na **consistência terminológica, completude técnica e rastreabilidade bidirecional de processos**. Avaliou-se o alinhamento estrito entre necessidades dos stakeholders, requisitos no padrão SMART, pacotes da EAP, código-fonte e casos de teste formais, garantindo a auditabilidade completa do manual.

## 6.2 Diagnóstico do manual

Apontamentos consolidados a partir da auditoria técnica por pares e da revisão interna de qualidade:

| ID | Constatação Identificada | Origem do Apontamento | Gravidade Técnica |
|:---:|:---|:---|:---:|
| **D-01** | Divergência na numeração de requisitos entre documentos históricos (`Requisitos.md` inicial vs. versão consolidada do manual). | Avaliação por Pares (NC-01) | Alta |
| **D-02** | Estrutura Analítica do Projeto (EAP) com granularidade irregular em subpacotes técnicos. | Avaliação por Pares (NC-02) | Média |
| **D-03** | Ausência de descrição formal das coleções NoSQL do Firestore no corpo do texto do manual. | Avaliação por Pares (NC-03) | Alta |
| **D-04** | Métrica de qualidade QM-04 sem critério quantitativo para cobertura de testes automatizados. | Avaliação por Pares (NC-04) | Média |
| **D-05** | Plano de descontinuação sem detalhamento de etapas temporais de purga conforme a LGPD. | Avaliação por Pares (OM-02) | Média |
| **D-06** | Referência quebrada na matriz de rastreabilidade (requisito RF09 associado a pacote EAP inexistente). | Revisão Interna v8.0 | Alta |
| **D-07** | Inconsistência textual na quantidade declarada de coleções no banco NoSQL. | Revisão Interna v8.0 | Baixa |
| **D-08** | Decisões Técnicas de Arquitetura (ADRs) citadas no texto sem respectivo registro documental padronizado. | Revisão Interna v8.0 | Alta |
| **D-09** | Termos com conotação inadequada ("cockpit") e vinculação nominal de pessoas físicas a tarefas na governança. | Revisão Interna v8.0 | Média |

## 6.3 Plano de uma melhoria

**Iniciativa de Melhoria Homologada:** *Harmonização terminológica, completude documental de decisões e garantia de rastreabilidade bidirecional ponta a ponta sem referências quebradas.*

| Elemento do Plano | Detalhamento da Ação |
|:---|:---|
| **Objetivo** | Eliminar 100% das referências quebradas e inconsistências de nomenclatura, instituir governança baseada em papéis de engenharia e formalizar os registros técnicos ausentes. |
| **Ações Programadas** | (1) Consolidar a numeração SMART RF01–RF10 como especificação oficial única; (2) corrigir a correspondência EAP do requisito RF09 para o pacote 3.2.2; (3) documentar integralmente os registros ADR-001 a ADR-004 com notas de decisão multicritério; (4) padronizar o termo "painel do motorista" e generalizar os papéis na matriz RACI e no plano de V&V; (5) atualizar o fornecedor cartográfico para Mapbox Free Tier. |
| **Responsabilidade** | Engenharia de Requisitos (condução e elaboração), Garantia da Qualidade (verificação e auditoria). |
| **Indicador de Eficácia** | 100% dos requisitos com rastreabilidade válida e zero inconformidades terminológicas ativas no manual. |

## 6.4 Atualização e verificação

| Item | Ação de Melhoria Executada | Método de Verificação | Situação |
|:---:|:---|:---|:---:|
| 1 | Padronização e unificação do catálogo oficial de requisitos SMART (RF01 a RF10) | Confronto com a matriz de requisitos e testes | **Conforme** |
| 2 | Correção da correlação EAP do RF09 para o subpacote 3.2.2 | Validação estrutural cruzada com a EAP | **Conforme** |
| 3 | Registro formal e justificado das decisões arquiteturais ADR-001 a ADR-004 | Verificação da completude das matrizes de decisão | **Conforme** |
| 4 | Atualização do provedor cartográfico para Mapbox API no Free Tier com Leaflet | Conferência de viabilidade econômica e stack | **Conforme** |
| 5 | Substituição do termo "cockpit" por "painel do motorista" e generalização de municípios e papéis | Inspeção textual completa em todos os capítulos | **Conforme** |
| 6 | Validação cruzada da árvore de arquivos e suíte de testes com o repositório Rhyme | Inspeção técnica contra o código-fonte | **Conforme** |

## 6.5 Acompanhamento da execução

| Marco Temporal | Atividade Prevista | Papel Responsável | Situação Operacional |
|:---:|:---|:---|:---:|
| **29/10/2026** | Publicação da Baseline v8.0 do Manual de Processos de Software | Arquitetura e Engenharia de Requisitos | **Concluída** |
| **Até 05/11/2026** | Homologação final dos relatórios de testes automatizados e evidências de código | Garantia da Qualidade (SQA) e DevOps | Em andamento |
| **Até 12/11/2026** | Ensaio geral cronometrado da apresentação oral em sala de aula | Equipe de Desenvolvimento (Todos os membros) | Planejada |
| **26/11/2026** | Apresentação oficial do trabalho perante a banca acadêmica (Grupo 12) | Equipe de Desenvolvimento (Todos os membros) | Planejada |
| **Pós-Entrega** | Auditoria das métricas operacionais e retroalimentação do processo de software | Garantia da Qualidade (SQA) | Planejada |

---

**FIM DO MANUAL**
