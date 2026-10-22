# MANUAL DE PROCESSO DE SOFTWARE — SISTEMA RHYME
## Anexo — Relatório de Avaliação por Pares (Peer Review)
> **Norma de Referência:** ISO/IEC/IEEE 12207:2017 (Auditoria Independente & CAPA)  
> **Equipe Executora:** Grupo 12 (Squad Rhyme Core) — INF0449 UFG (2026/2)  
> **Baseline:** 7.0 Oficial Consolidada  
> **Navegação:** [Voltar ao Sumário Geral](../README.md) | [Manual Consolidado](../Manual.md)

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