# Manual de Processos de Software — Sistema Rhyme

[![Norma: ISO/IEC/IEEE 12207:2017](https://img.shields.io/badge/Norma-ISO%2FIEC%2FIEEE_12207%3A2017-0052CC?style=flat-square)](https://www.iso.org/standard/63711.html)
[![Baseline: 8.0](https://img.shields.io/badge/Baseline-8.0_Oficial-10b981?style=flat-square)](./historico-versoes/historico-versoes.md)
[![Instituição: UFG](https://img.shields.io/badge/Instituição-UFG_INF-F59E0B?style=flat-square)](https://inf.ufg.br/)
[![Demo PWA](https://img.shields.io/badge/Demo_PWA-track--22dc6.web.app-2563EB?style=flat-square)](https://track-22dc6.web.app)

Repositório oficial de governança, engenharia de processos e garantia da qualidade do **Sistema Rhyme**, estruturado segundo o padrão internacional **ISO/IEC/IEEE 12207:2017** (*Systems and software engineering — Software life cycle processes*).

Desenvolvido para a disciplina **INF0449 — Processos de Engenharia de Software** do Instituto de Informática (INF) da Universidade Federal de Goiás (UFG).

---

## Visão Geral do Sistema

O **Rhyme** é uma Progressive Web App (PWA) de telemetria veicular e coordenação operacional em tempo real concebida para otimizar o transporte universitário intermunicipal. O sistema substitui listas manuais e grupos informais de mensagens por uma plataforma reativa que conecta estudantes, condutores e gestores municipais.

```
┌────────────────────────┐      Realtime Listeners     ┌────────────────────────┐
│  Estudante (PWA)       │◄───────────────────────────►│  Google Cloud Firestore│
│  - Status One-Touch    │                             │  - trips               │
│  - Mapa e ETA          │                             │  - students            │
└────────────────────────┘                             │  - bus_location        │
                                                       │  - emergencies         │
┌────────────────────────┐      Broadcast a cada 5s    │                        │
│  Painel do Motorista   │────────────────────────────►│                        │
│  - Contadores ao vivo  │                             └───────────┬────────────┘
│  - Alertas sonoros     │                                         │
└────────────────────────┘                                Document Trigger
                                                                   ▼
┌────────────────────────┐      Web Push (raio 1 km)   ┌────────────────────────┐
│  Notificação Push FCM  │◄────────────────────────────┤  Cloud Functions v2    │
└────────────────────────┘                             └────────────────────────┘
```

> [!NOTE]
> A aplicação em produção está disponível publicamente em [track-22dc6.web.app](https://track-22dc6.web.app). Para testar a experiência veicular completa no smartphone, instale o PWA através do navegador móvel via "Adicionar à tela de início".

---

## Estrutura do Repositório

| Caminho | Descrição |
|:---|:---|
| [Manual.md](./Manual.md) | **Documento integral do manual**, estruturado em 6 capítulos normativos conforme as diretrizes acadêmicas. |
| [Manual.docx](./Manual.docx) | Versão diagramada em Microsoft Word com estilos institucionais, pronta para submissão e impressão. |
| [diagramas/](./diagramas/) | Modelos formais de design e arquitetura em sintaxe PlantUML (`.puml`). |
| [historico-versoes/](./historico-versoes/historico-versoes.md) | Tabela auditável de baselines e histórico de evolução das versões (v1.0 à v8.0). |
| [requisitos/](./requisitos/Requisitos.md) | Especificação histórica preliminar de requisitos (v1.0). |

---

## Conteúdo do Manual de Processos

O manual está organizado em conformidade com as cláusulas fundamentais da **ISO/IEC/IEEE 12207:2017**:

### 1. Apresentação do Software
- Descrição da solução, formulação do problema mitigado e impacto operacional.
- Público-alvo (estudantes, condutores e administrações municipais) e contexto rodoviário.
- Escopo delimitado, funcionalidades centrais, premissas e restrições (custo financeiro zero, LGPD e conectividade móvel variável).

### 2. Processos de Acordo (Cláusula 6.1)
- **Aquisição (*Make vs. Buy*):** Adoção de serviços em nuvem gerenciados sob cotas gratuitas (Google Firebase, Mapbox Free Tier e Vercel CDN) com desenvolvimento proprietário da lógica de interface reativa em React 19.
- **Fornecimento:** Termo de Cessão de Uso Tecnológico sem ônus (comodato acadêmico institucional) às prefeituras e associações estudantis.
- **Níveis de Serviço:** SLA de 99,9% na janela operacional crítica (15h00 às 23h30), RTO de 15 minutos e RPO de 0 segundos.
- **Procedimentos Operacionais Padronizados (POPs):** POP-DEV-01 (qualidade de código), POP-OPS-01 (esteira CI/CD), POP-GEO-01 (calibração de geofencing) e POP-EMERG-01 (contingência e emergência).

### 3. Processos Organizacionais Habilitadores (Cláusula 6.2)
- Modelo de ciclo de vida híbrido iterativo-incremental (Scrum/Kanban) com sprints quinzenais.
- Inventário de infraestrutura física, lógica e ferramental técnico.
- Análise de viabilidade estratégica, técnica, econômica, operacional e jurídica.
- Matriz RACI estruturada por papéis formais de engenharia de software e plano de capacitação da equipe.
- Plano de qualidade com indicadores quantitativos (QM-01 a QM-04) e estratégia de gestão do conhecimento.

### 4. Processos de Gerenciamento Técnico (Cláusula 6.3)
- Plano de desenvolvimento do projeto com Estrutura Analítica do Projeto (EAP) em 3 níveis e cronograma de sprints S1–S6.
- Matriz de Gestão de Riscos (*Risk Register*) com avaliação de probabilidade e impacto, planos de mitigação preventiva e contingência reativa.
- Governança de gerência de configuração: fluxo de branches protegidas, commits semânticos, quality gates em Pull Requests e SemVer 2.0.0.
- Registros Formais de Decisões de Arquitetura (ADR-001 a ADR-004) embasados em Matrizes de Decisão Multicritério.
- Métricas objetivas de acompanhamento do progresso e saúde do projeto.

### 5. Processos Técnicos (Cláusula 6.4)
- Documento de Requisitos do Sistema: 10 Requisitos Funcionais no padrão SMART (RF01 a RF10) e 5 Requisitos Não Funcionais (RNF01 a RNF05).
- Matriz bidirecional de rastreabilidade integrando Requisitos ↔ Entregáveis EAP ↔ Código-Fonte (`src/`) ↔ Casos de Teste (V&V).
- Arquitetura de software em camadas, modelo de dados NoSQL do Cloud Firestore e justificativa das tecnologias adotadas.
- Padrões de codificação, esteira de integração e testes automatizados.
- Plano e relatório formal de Verificação e Validação (Casos de Teste CT-01 a CT-10 aprovados e ensaio de validação em rota rodoviária real).
- Procedimentos de operação, observabilidade contínua, modalidades de manutenção e protocolo de descarte e purga LGPD em quatro etapas.

### 6. Avaliação e Melhoria dos Processos de Software
- Diagnóstico formal de conformidade baseado em avaliação por pares (*Peer Review*) e inspeção interna de qualidade.
- Plano de Ação Corretiva e Preventiva (CAPA) com foco na eliminação de referências quebradas, governança por papéis e harmonização terminológica.
- Registro de verificação das ações executadas e acompanhamento temporal até a homologação final.

---

## Modelagem e Diagramas de Design

Os diagramas de arquitetura e design estão versionados no diretório [`diagramas/`](./diagramas/):

| Diagrama | Arquivo Fonte | Cláusula | Descrição |
|:---|:---|:---:|:---|
| **Casos de Uso** | [`casos-de-uso.puml`](./diagramas/casos-de-uso.puml) | ISO 12207 §6.4.1 | 10 casos de uso detalhando interações de Estudantes, Condutores, Telemetria GPS e Firestore. |
| **Sequência em Tempo Real** | [`sequencia-tempo-real.puml`](./diagramas/sequencia-tempo-real.puml) | ISO 12207 §6.4.3 | Fluxo assíncrono de notificação de liberação (*one-touch*) e telemetria contínua do veículo. |
| **Componentes de Software** | [`componentes-arquitetura.puml`](./diagramas/componentes-arquitetura.puml) | ISO 12207 §6.4.3 | Módulos do PWA React 19, Service Worker de cache offline, Leaflet/Mapbox e serviços Firebase. |
| **Modelo de Dados NoSQL** | [`modelo-dados-firestore.puml`](./diagramas/modelo-dados-firestore.puml) | ISO 12207 §6.4.4 | Estrutura de coleções (`routes`, `trips`, `students`, `bus_location`, `emergencies`). |

> [!TIP]
> Consulte o guia detalhado em [diagramas/README.md](./diagramas/README.md) para orientações sobre como renderizar os modelos no VS Code via extensão PlantUML ou online.

---

## Equipe de Engenharia (Grupo 12 — Squad Rhyme Core)

| Integrante | Papel de Referência no Projeto | Contato Institucional |
|:---|:---|:---|
| **Matheus Marquez de Carvalho Rodrigues** | Engenharia de Requisitos e Produto | `matheus.marquez@discente.ufg.br` |
| **Luis Henrique Oliveira de Jesus** | Arquitetura de Software e Frontend | `luis.henrique@discente.ufg.br` |
| **Heitor Gonçalves Costa** | Infraestrutura, Nuvem e DevOps | `heitor.costa@discente.ufg.br` |
| **Carlos Daniel Lopes de Araújo** | Garantia da Qualidade (SQA), Verificação e Validação | `carlos.daniel@discente.ufg.br` |

---

## Geração do Documento Formatado (DOCX)

O repositório inclui utilitário automatizado em Python para conversão do manual em Markdown para formato Word (`.docx`), com aplicação de folhas de estilo institucionais:

```bash
# Instalar dependências necessárias
pip install python-docx

# Executar a compilação do documento
python convert_to_docx.py
```

O arquivo compilado é salvo na raiz como [`Manual.docx`](./Manual.docx).
