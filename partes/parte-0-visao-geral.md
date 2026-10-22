# MANUAL DE PROCESSO DE SOFTWARE — SISTEMA RHYME
## Parte 0 — Apresentação do Software e Visão Geral
> **Norma de Referência:** ISO/IEC/IEEE 12207:2017 (Contexto e Escopo)  
> **Equipe Executora:** Grupo 12 (Squad Rhyme Core) — INF0449 UFG (2026/2)  
> **Baseline:** 7.0 Oficial Consolidada  
> **Navegação:** [Voltar ao Sumário Geral](../README.md) | [Manual Consolidado](../Manual.md)

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