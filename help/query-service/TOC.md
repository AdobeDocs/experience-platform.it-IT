---
audience: user
user-guide-title: Guida al servizio query di Adobe Experience Platform
breadcrumb-title: Guida di Query Service
user-guide-description: Utilizza il linguaggio SQL standard per eseguire query sui dati nel data lake in Experience Platform.
feature: Queries
source-git-commit: 113e74b3a4783a11bc88dc2d16134b68638604e5
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 18%

---


# Servizio query Adobe Experience Platform {#query}

- [Panoramica di Query Service](home.md)
- [Pacchetto Query Service](packages.md)
- [Guardrail di Query Service](guardrails.md)
- Introduzione {#get-started}
   - [Prerequisiti](get-started/prerequisites.md)
- Data Distiller {#data-distiller}
   - [Panoramica](data-distiller/overview.md)
   - [Utilizzo delle licenze](data-distiller/license-usage.md)
   - Archivio accelerato query {#query-accelerated-store}
      - [Inviare query accelerate](data-distiller/query-accelerated-store/send-accelerated-queries.md)
      - [Guida al modello dati per insights di reporting](data-distiller/query-accelerated-store/reporting-insights-data-model.md)
   - Attributi derivati {#derived-attributes}
      - [Panoramica](data-distiller/derived-attributes/overview.md)
      - [Flusso SQL senza interruzioni](data-distiller/derived-attributes/seamless-sql-flow.md)
      - [Creare attributi derivati basati su decile](data-distiller/derived-attributes/decile-based-derived-attributes.md)
   - Pipeline per funzioni AI/ML {#ml-feature-pipelines}
      - [Panoramica](data-distiller/ml-feature-pipelines/overview.md)
      - [Connetti a Jupyter Notebooks](data-distiller/ml-feature-pipelines/establish-connection.md)
      - [Analisi esplorativa dei dati](data-distiller/ml-feature-pipelines/exploratory-analysis.md)
      - [Funzioni del tecnico per ML](data-distiller/ml-feature-pipelines/feature-engineering.md)
      - [Esportare dati in ambienti ML](data-distiller/ml-feature-pipelines/export-data.md)
      - [Flusso di lavoro end-to-end per l’arricchimento della pipeline dati AI/ML](data-distiller/ml-feature-pipelines/end-to-end-notebook-workflow.md)
- Casi d’uso {#use-cases}
   - [Sfoglia abbandonata](use-cases/abandoned-browse.md)
   - [Analisi dell’attribuzione](use-cases/attribution-analysis.md)
   - [Filtro bot](use-cases/bot-filtering.md)
   - [Creare un rapporto con tendenze degli eventi](use-cases/trended-report-of-events.md)
   - [Analisi del consenso](use-cases/consent-analysis.md)
   - [Valore della durata del cliente](use-cases/customer-lifetime-value.md)
   - [Attributi derivati basati su decile](use-cases/deciles-use-case.md)
   - [Corrispondenza fuzzy](use-cases/fuzzy-match.md)
   - [Elencare le visualizzazioni di pagina di un utente](use-cases/list-visitor-sessions.md)
   - [Elencare i visitatori in base alle loro visualizzazioni di pagina](use-cases/visitors-by-number-of-page-views.md)
   - [Punteggio tendenza](use-cases/propensity-score.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [Restituire e utilizzare le variabili di merchandising dai dati di Analytics](use-cases/merchandising-variables.md)
   - [Visualizzare il rapporto di aggregazione per un visitatore](use-cases/roll-up-report-of-a-visitor.md)
   - [Approfondimenti sull’analisi web e mobile](use-cases/analytics-insights.md)
- Connettere i client a Query Service {#clients}
   - [Panoramica delle connessioni client](clients/overview.md)
   - [Modalità SSL](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [Jupyter Notebook](clients//jupyter-notebook.md)
   - [Looker](clients/looker.md)
   - [Postico](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [Studio](clients/rstudio.md)
   - [Tableau](clients/tableau.md)
- Interfaccia utente di Query Service {#ui}
   - [Panoramica dell’interfaccia utente](ui/overview.md)
   - [Guida utente di Query Editor](ui/user-guide.md)
   - [Modelli di query](ui/query-templates.md)
   - [Query con parametri (limitate)](ui/parameterized-queries.md)
   - [Pianificazioni query](ui/query-schedules.md)
   - [Registri query](ui/query-logs.md)
   - [Monitorare le query pianificate](ui/monitor-queries.md)
   - [Guida alle credenziali](ui/credentials.md)
   - [Genera set di dati di output dai risultati della query](ui/create-datasets.md)
- Endpoint API di Query Service {#api}
   - [Introduzione](api/getting-started.md)
   - [Query](api/queries.md)
   - [Parametri di connessione](api/connection-parameters.md)
   - [Schedules](api/scheduled-queries.md)
   - [Viene eseguito per le query pianificate](api/runs-scheduled-queries.md)
   - [Modelli di query](api/query-templates.md)
   - [Query accelerate](api/accelerated-queries.md)
   - [Sottoscrizioni avvisi](api/alert-subscriptions.md)
- Governance dei dati {#data-governance}
   - [Panoramica](data-governance/overview.md)
   - [Guida al registro di controllo](data-governance/audit-log-guide.md)
   - [Identità nei set di dati dello schema ad hoc](data-governance/ad-hoc-schema-identities.md)
   - [Supporto del controllo degli accessi basato su attributi per schemi ad hoc](./data-governance/ad-hoc-schema-labels.md)
- Best practice {#best-practices}
   - [Esecuzione della query](best-practices/writing-queries.md)
   - [Organizzazione delle risorse dati](./best-practices/organize-data-assets.md)
- Concetti essenziali {#essential-concepts}
   - [Utilizzo delle strutture di dati nidificate](essential-concepts/nested-data-structures.md)
   - [Appiattire le strutture di dati nidificate](essential-concepts/flatten-nested-data.md)
   - [Blocco anonimo](essential-concepts/anonymous-block.md)
   - [Modello in linea](essential-concepts/inline-templates.md)
   - [Caricamento incrementale](essential-concepts/incremental-load.md)
   - [Deduplicazione dei dati](essential-concepts/deduplication.md)
   - [Esempi di set di dati](essential-concepts/dataset-samples.md)
   - [Calcolo delle statistiche del set di dati](essential-concepts/dataset-statistics.md)
- Riferimento SQL {#sql}
   - [Panoramica di SQL](sql/overview.md)
   - [Sintassi SQL](sql/syntax.md)
   - [Funzioni definite da Adobe](sql/adobe-defined-functions.md)
   - [Funzioni SQL Spark](sql/spark-sql-functions.md)
   - [Comandi metadati](sql/metadata.md)
   - [Istruzioni preparate](sql/prepared-statements.md)
- [Domande frequenti](troubleshooting-guide.md)
- [Indirizzo IP inserito nell&#39;elenco Consentiti](ip-address-allowlist.md)
- [Riferimento API](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Note sulla versione della piattaforma](https://www.adobe.com/go/platform-release-notes-it)
