# Diagramas Estruturais e Comportamentais — Sistema Rhyme

Este diretório contém os modelos formais de design e arquitetura de software desenvolvidos em sintaxe **PlantUML**, em conformidade com as cláusulas **6.4.3 (Design de Arquitetura)** e **6.4.4 (Design de Software)** da norma **ISO/IEC/IEEE 12207:2017**.

---

## 📐 Catálogo de Diagramas

| Arquivo | Tipo de Diagrama | Norma / Propósito | Descrição Técnica |
|:---|:---|:---:|:---|
| [casos-de-uso.puml](./casos-de-uso.puml) | UML Casos de Uso | ISO 12207 §6.4.1 | Especificação dos 10 Casos de Uso (UC01 a UC10) envolvendo Estudante, Motorista, GPS e Firestore. |
| [sequencia-tempo-real.puml](./sequencia-tempo-real.puml) | UML Sequência | ISO 12207 §6.4.3 | Fluxo temporal reativo de alteração de status do aluno ("Liberado") e broadcast contínuo de telemetria GPS. |
| [componentes-arquitetura.puml](./componentes-arquitetura.puml) | UML Componentes | ISO 12207 §6.4.3 | Mapeamento dos módulos do cliente PWA (React 19, Leaflet, Service Worker) e serviços em nuvem (Firebase). |
| [modelo-dados-firestore.puml](./modelo-dados-firestore.puml) | Entidade-Relacionamento NoSQL | ISO 12207 §6.4.4 | Modelagem estrutural das coleções do Firestore (`routes`, `trips`, `students`, `bus_location`, `emergencies`). |

---

## 🛠️ Como Visualizar e Renderizar os Diagramas

### Opção 1: Visual Studio Code (Recomendada)
1. Instale a extensão oficial **PlantUML** (`jebbs.plantuml`) no VS Code.
2. Certifique-se de possuir o Java e Graphviz instalados, ou configure o servidor público do PlantUML em suas configurações:
   ```json
   "plantuml.server": "https://www.plantuml.com/plantuml"
   ```
3. Abra qualquer arquivo `.puml` e pressione `Alt + D` para visualizar o diagrama interativo renderizado em tempo real.

### Opção 2: PlantUML Server Online
Copie o conteúdo de qualquer arquivo deste diretório e cole diretamente no [PlantUML Online Server](https://www.plantuml.com/plantuml/uml/).

---

*Diretório integrante do Manual de Processo de Software — Grupo 12 — INF0449 (UFG 2026/2).*
