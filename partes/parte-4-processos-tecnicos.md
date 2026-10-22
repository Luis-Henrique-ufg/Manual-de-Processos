# MANUAL DE PROCESSO DE SOFTWARE — SISTEMA RHYME
## Parte 4 — Processos Técnicos
> **Norma de Referência:** ISO/IEC/IEEE 12207:2017 (Cláusula 6.4)  
> **Equipe Executora:** Grupo 12 (Squad Rhyme Core) — INF0449 UFG (2026/2)  
> **Baseline:** 7.0 Oficial Consolidada  
> **Navegação:** [Voltar ao Sumário Geral](../README.md) | [Manual Consolidado](../Manual.md)

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
Os diagramas formais de design e arquitetura do sistema foram desacoplados em arquivos dedicados na pasta [`../diagramas/`](../diagramas/), em conformidade com as melhores práticas de governança e legibilidade:

| Diagrama | Arquivo Fonte Desacoplado | Norma / Propósito | Descrição Técnica do Modelo |
|:---|:---|:---:|:---|
| **Casos de Uso** | [`diagramas/casos-de-uso.puml`](../diagramas/casos-de-uso.puml) | ISO 12207 §6.4.1 | Especificação dos 10 Casos de Uso (UC01 a UC10) envolvendo Estudante, Motorista, GPS e Firestore. |
| **Sequência Realtime** | [`diagramas/sequencia-tempo-real.puml`](../diagramas/sequencia-tempo-real.puml) | ISO 12207 §6.4.3 | Fluxo temporal reativo de alteração de status do aluno ("Liberado") e broadcast contínuo de telemetria GPS. |
| **Componentes PWA** | [`diagramas/componentes-arquitetura.puml`](../diagramas/componentes-arquitetura.puml) | ISO 12207 §6.4.3 | Mapeamento dos módulos do cliente PWA (React 19, Leaflet, Service Worker) e serviços em nuvem (Firebase). |
| **Modelo de Dados NoSQL** | [`diagramas/modelo-dados-firestore.puml`](../diagramas/modelo-dados-firestore.puml) | ISO 12207 §6.4.4 | Modelagem estrutural das coleções do Firestore (`routes`, `trips`, `students`, `bus_location`, `emergencies`). |

> *Nota de Visualização:* Para renderizar os diagramas interativamente no VS Code, instale a extensão **PlantUML** (`jebbs.plantuml`) e utilize o atalho `Alt + D`. Consulte o [Guia de Renderização](../diagramas/README.md) para maiores instruções.

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