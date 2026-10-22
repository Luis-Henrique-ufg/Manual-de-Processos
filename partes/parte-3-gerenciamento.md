# MANUAL DE PROCESSO DE SOFTWARE — SISTEMA RHYME
## Parte 3 — Processos de Gerenciamento Técnico
> **Norma de Referência:** ISO/IEC/IEEE 12207:2017 (Cláusula 6.3)  
> **Equipe Executora:** Grupo 12 (Squad Rhyme Core) — INF0449 UFG (2026/2)  
> **Baseline:** 7.0 Oficial Consolidada  
> **Navegação:** [Voltar ao Sumário Geral](../README.md) | [Manual Consolidado](../Manual.md)

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