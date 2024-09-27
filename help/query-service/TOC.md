---
audience: user
user-guide-title: Guida al servizio query di Adobe Experience Platform
breadcrumb-title: Guida di Query Service
user-guide-description: Utilizza il linguaggio SQL standard per eseguire query sui dati nel data lake in Experience Platform.
feature: Queries
role: User,Developer
source-git-commit: 67d4bcbf2a055d4427218ba7d98355f09d860a8c
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 22%

---


# Servizio query Adobe Experience Platform {#query}

- [Panoramica di Query Service](home.md)
- [Pacchetto Query Service](packaging.md)
- [Guardrail di Query Service](guardrails.md)
- Introduzione {#get-started}
   - [Prerequisiti](get-started/prerequisites.md)
- Data Distiller {#data-distiller}
   - [Panoramica](data-distiller/overview.md)
   - [Utilizzo delle licenze](data-distiller/license-usage.md)
   - Set di dati derivati {#derived-datasets}
      - [Panoramica](data-distiller/derived-datasets/overview.md)
      - [Creare set di dati derivati con SQL](data-distiller/derived-datasets/create-derived-datasets-with-sql.md)
      - [Creare set di dati derivati basati su decile](data-distiller/derived-datasets/decile-based-derived-attributes.md)
   - SQL Insights per il reporting esteso dell&#39;app {#sql-insights}
      - [Panoramica](data-distiller/sql-insights/overview.md)
      - [Modalità query pro](data-distiller/sql-insights/query-pro-mode.md)
      - [Inviare query accelerate](data-distiller/sql-insights/send-accelerated-queries.md)
      - [Guida al modello dati per insights di reporting](data-distiller/sql-insights/reporting-insights-data-model.md)
   - Pipeline di funzionalità IA/ML {#ml-feature-pipelines}
      - [Panoramica](data-distiller/ml-feature-pipelines/overview.md)
      - [Connetti a Jupyter Notebooks](data-distiller/ml-feature-pipelines/establish-connection.md)
      - [Analisi esplorativa dei dati](data-distiller/ml-feature-pipelines/exploratory-analysis.md)
      - [Funzioni del tecnico per ML](data-distiller/ml-feature-pipelines/feature-engineering.md)
      - [Esportare dati in ambienti ML](data-distiller/ml-feature-pipelines/export-data.md)
      - [Flusso di lavoro end-to-end per l’arricchimento della pipeline dati AI/ML](data-distiller/ml-feature-pipelines/end-to-end-notebook-workflow.md)
- Pubblico di Data Distiller {#data-distiller-audiences}
   - [Creare tipi di pubblico esterni tramite SQL](data-distiller-audiences/overview.md)
- Esempi {#use-cases}
   - [Panoramica](use-cases/overview.md)
   - [Sfoglia abbandonata](use-cases/abandoned-browse.md)
   - [Analisi dell’attribuzione](use-cases/attribution-analysis.md)
   - [Filtro bot](use-cases/bot-filtering.md)
   - [Creare un rapporto con tendenze degli eventi](use-cases/trended-report-of-events.md)
   - [Analisi del consenso](use-cases/consent-analysis.md)
   - [Valore del ciclo di vita del cliente](use-cases/customer-lifetime-value.md)
   - [Esplorazione dei dati](./use-cases/data-exploration.md)
   - [Set di dati derivati basati su decile](use-cases/deciles-use-case.md)
   - [Corrispondenza parziale](use-cases/fuzzy-match.md)
   - [Elencare le visualizzazioni di pagina di un utente](use-cases/list-visitor-sessions.md)
   - [Elencare i visitatori in base alle loro visualizzazioni di pagina](use-cases/visitors-by-number-of-page-views.md)
   - [Punteggio di propensione](use-cases/propensity-score.md)
   - [Recuperare record simili con funzioni di ordine superiore](use-cases/retrieve-similar-records.md)
   - [Restituire e utilizzare le variabili di merchandising dai dati di Analytics](use-cases/merchandising-variables.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [Visualizzare il rapporto di aggregazione per un visitatore](use-cases/roll-up-report-of-a-visitor.md)
   - [Approfondimenti sull’analisi web e mobile](use-cases/analytics-insights.md)
- Concetti chiave {#key-concepts}
   - [Utilizzo delle strutture di dati nidificate](key-concepts/nested-data-structures.md)
   - [Appiattire le strutture di dati nidificate](key-concepts/flatten-nested-data.md)
   - [Blocco anonimo](key-concepts/anonymous-block.md)
   - [Modello in linea](key-concepts/inline-templates.md)
   - [Caricamento incrementale](key-concepts/incremental-load.md)
   - [Deduplicazione dei dati](key-concepts/deduplication.md)
   - [Esempi di set di dati](key-concepts/dataset-samples.md)
   - [Calcolo delle statistiche del set di dati](key-concepts/dataset-statistics.md)
- Ipercubi Data Distiller {#hypercubes}
   - [Analisi dei big data efficiente con ipercubi](hypercubes/overview.md)
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
   - [Query con parametri](ui/parameterized-queries.md)
   - [Pianificazioni query](ui/query-schedules.md)
   - [Registri query](ui/query-logs.md)
   - [Monitorare le query pianificate](ui/monitor-queries.md)
   - [Guida alle credenziali](ui/credentials.md)
   - [Genera set di dati di output dai risultati della query](ui/create-datasets.md)
- Endpoint API servizio query {#api}
   - [Introduzione](api/getting-started.md)
   - [Query](api/queries.md)
   - [Parametri di connessione](api/connection-parameters.md)
   - [Pianificazioni](api/scheduled-queries.md)
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
- Riferimento SQL {#sql}
   - [Panoramica di SQL](sql/overview.md)
   - [Sintassi SQL](sql/syntax.md)
   - [Funzioni definite da Adobe](sql/adobe-defined-functions.md)
   - [Funzioni di ordine superiore](sql/higher-order-functions.md)
   - [Funzioni SQL Spark](sql/spark-sql-functions.md)
   - [Comandi metadati](sql/metadata.md)
   - [Istruzioni preparate](sql/prepared-statements.md)
- [Domande frequenti](troubleshooting-guide.md)
- [Indirizzo IP inserisco nell&#39;elenco Consentiti](ip-address-allowlist.md)
- [Riferimento API](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Note sulla versione della piattaforma](https://experienceleague.adobe.com/it/docs/experience-platform/release-notes/latest)
