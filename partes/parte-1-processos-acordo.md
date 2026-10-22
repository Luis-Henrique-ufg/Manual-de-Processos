# MANUAL DE PROCESSO DE SOFTWARE — SISTEMA RHYME
## Parte 1 — Processos de Acordo
> **Norma de Referência:** ISO/IEC/IEEE 12207:2017 (Cláusula 6.1)  
> **Equipe Executora:** Grupo 12 (Squad Rhyme Core) — INF0449 UFG (2026/2)  
> **Baseline:** 7.0 Oficial Consolidada  
> **Navegação:** [Voltar ao Sumário Geral](../README.md) | [Manual Consolidado](../Manual.md)

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