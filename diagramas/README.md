# Catálogo de Diagramas de Arquitetura e Design — Sistema Rhyme

[![Norma: ISO/IEC/IEEE 12207:2017](https://img.shields.io/badge/Norma-ISO%2FIEC%2FIEEE_12207%3A2017-0052CC?style=flat-square)](https://www.iso.org/standard/63711.html)
[![Formato: PlantUML](https://img.shields.io/badge/Formato-PlantUML-orange?style=flat-square)](https://plantuml.com/)

Este diretório reúne os modelos formais estruturais e comportamentais do **Sistema Rhyme**, desenvolvidos em conformidade com as cláusulas **6.4.3 (Design de Arquitetura)** e **6.4.4 (Design de Software)** da norma **ISO/IEC/IEEE 12207:2017**.

Todos os diagramas são mantidos desacoplados em arquivos-fonte `.puml`, permitindo controle de versão granulado, edição simplificada e compilação em esteiras de integração contínua.

---

## Modelos Arquiteturais Disponíveis

| Arquivo Fonte | Tipo de Modelo | Cláusula ISO | Descrição Técnica |
|:---|:---|:---:|:---|
| [casos-de-uso.puml](./casos-de-uso.puml) | Diagrama de Casos de Uso UML | §6.4.1 | Especificação dos 10 Casos de Uso (UC01 a UC10) envolvendo Estudantes, Condutores, Telemetria GPS e Cloud Firestore. |
| [sequencia-tempo-real.puml](./sequencia-tempo-real.puml) | Diagrama de Sequência UML | §6.4.3 | Fluxo temporal reativo de notificação de status acadêmico ("Liberado") e broadcast contínuo de coordenadas do veículo. |
| [componentes-arquitetura.puml](./componentes-arquitetura.puml) | Diagrama de Componentes UML | §6.4.3 | Arquitetura do cliente PWA (React 19, Leaflet, Mapbox API, Service Worker de cache) e integração serverless com o Google Firebase. |
| [modelo-dados-firestore.puml](./modelo-dados-firestore.puml) | Modelo Entidade-Relacionamento NoSQL | §6.4.4 | Estrutura de coleções e subcoleções do Cloud Firestore (`routes`, `trips`, `students`, `bus_location`, `emergencies`). |

---

## Como Visualizar e Renderizar os Diagramas

### Opção 1: Visual Studio Code (Recomendada)

1. Instale a extensão oficial [PlantUML](https://marketplace.visualstudio.com/items?itemName=jebbs.plantuml) (`jebbs.plantuml`).
2. Caso não possua o Graphviz e o Java instalados localmente, configure o servidor público do PlantUML no arquivo `settings.json` do VS Code:
   ```json
   "plantuml.server": "https://www.plantuml.com/plantuml"
   ```
3. Abra qualquer arquivo `.puml` e pressione o atalho **`Alt + D`** (ou `Option + D` no macOS) para visualizar o diagrama renderizado em tempo real.

> [!TIP]
> Pelo menu contextual no VS Code (`Ctrl + Shift + P` > *PlantUML: Export Current Diagram*), é possível exportar o diagrama diretamente para formatos vetoriais (`SVG`) ou imagem (`PNG`).

### Opção 2: Servidor Online PlantUML

Caso prefira visualizar sem extensões locais:
1. Abra o arquivo `.puml` desejado e copie todo o seu conteúdo.
2. Acesse o [PlantUML Online Server](https://www.plantuml.com/plantuml/uml/).
3. Cole o código no editor online para obter a renderização gráfica instantânea.

---

> [!NOTE]
> Os diagramas deste catálogo são referenciados no **Capítulo 5 (Processos Técnicos)** do [Manual de Processos de Software](../Manual.md).
