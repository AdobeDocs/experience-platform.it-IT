---
audience: user
user-guide-title: Guida al servizio query di Adobe Experience Platform
breadcrumb-title: Guida di Query Service
user-guide-description: Utilizza il linguaggio SQL standard per eseguire query sui dati nel data lake in Experience Platform.
feature: Queries
source-git-commit: a43947f87337e235eb059db6f497999bc4ede74d
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 16%

---


# Servizio query Adobe Experience Platform {#query}

- [Panoramica del servizio query](home.md)
- [Pacchetto del servizio query](packages.md)
- [Garanzie del servizio query](guardrails.md)
- Introduzione {#get-started}
   - [Prerequisiti](get-started/prerequisites.md)
- Distiller dati {#data-distiller}
   - [Panoramica](data-distiller/overview.md)
   - [Utilizzo delle licenze](data-distiller/license-usage.md)
   - Archivio accelerato query {#query-accelerated-store}
      - [Invia query accelerate](data-distiller/query-accelerated-store/send-accelerated-queries.md)
      - [Guida al modello di dati per approfondimenti sui rapporti](data-distiller/query-accelerated-store/reporting-insights-data-model.md)
   - Attributi derivati {#derived-attributes}
      - [Panoramica](data-distiller/derived-attributes/overview.md)
      - [Creare attributi derivati basati su decile](data-distiller/derived-attributes/decile-based-derived-attributes.md)
- Casi d’uso {#use-cases}
   - [Sfoglia abbandonato](use-cases/abandoned-browse.md)
   - [Analisi delle attività con Adobe Target](use-cases/activity-analysis-with-adobe-target.md)
   - [Analisi di attribuzione](use-cases/attribution-analysis.md)
   - [Filtro bot](use-cases/bot-filtering.md)
   - [Creare un rapporto con tendenze degli eventi](use-cases/trended-report-of-events.md)
   - [Attributi derivati basati su decile](use-cases/deciles-use-case.md)
   - [Elencare le visualizzazioni di pagina di un utente](use-cases/list-visitor-sessions.md)
   - [Elencare i visitatori in base alle loro visualizzazioni di pagina](use-cases/visitors-by-number-of-page-views.md)
   - [Punteggio tendenza](use-cases/propensity-score.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [Restituire e utilizzare le variabili merchandising dai dati di analytics](use-cases/merchandising-variables.md)
   - [Visualizzare il rapporto introduttivo per un visitatore](use-cases/roll-up-report-of-a-visitor.md)
   - [Informazioni approfondite su web e dispositivi mobili](use-cases/analytics-insights.md)
- Connettere i client al servizio query {#clients}
   - [Panoramica delle connessioni client](clients/overview.md)
   - [Modalità SSL](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [Notebook Jupyter](clients//jupyter-notebook.md)
   - [Guardaroba](clients/looker.md)
   - [Postico](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RSudio](clients/rstudio.md)
   - [Tableau](clients/tableau.md)
- Interfaccia utente del servizio query {#ui}
   - [Panoramica dell’interfaccia utente](ui/overview.md)
   - [Guida utente dell’editor delle query](ui/user-guide.md)
   - [Modelli di query](ui/query-templates.md)
   - [Pianificazioni query](ui/query-schedules.md)
   - [Monitoraggio delle query pianificate](ui/monitor-queries.md)
   - [Guida alle credenziali](ui/credentials.md)
   - [Genera set di dati di output dai risultati della query](ui/create-datasets.md)
- Endpoint API del servizio query {#api}
   - [Introduzione](api/getting-started.md)
   - [Query](api/queries.md)
   - [Parametri di connessione](api/connection-parameters.md)
   - [Pianificazioni](api/scheduled-queries.md)
   - [Viene eseguito per query pianificate](api/runs-scheduled-queries.md)
   - [Modelli di query](api/query-templates.md)
   - [Query accelerate](api/accelerated-queries.md)
   - [Abbonamenti agli avvisi](api/alert-subscriptions.md)
- Governance dei dati {#data-governance}
   - [Panoramica](data-governance/overview.md)
   - [Guida al registro di controllo](data-governance/audit-log-guide.md)
   - [Identità nei set di dati di schemi ad hoc](data-governance/ad-hoc-schema-identities.md)
   - [Supporto del controllo degli accessi basato su attributi per schemi ad hoc](./data-governance/ad-hoc-schema-labels.md)
- Best practice {#best-practices}
   - [Esecuzione della query](best-practices/writing-queries.md)
   - [Organizzazione delle risorse dati](./best-practices/organize-data-assets.md)
- Concetti essenziali {#essential-concepts}
   - [Utilizzo delle strutture di dati nidificate](essential-concepts/nested-data-structures.md)
   - [Strutture dati nidificate appiattite](essential-concepts/flatten-nested-data.md)
   - [Blocco anonimo](essential-concepts/anonymous-block.md)
   - [Caricamento incrementale](essential-concepts/incremental-load.md)
   - [Deduplicazione dati](essential-concepts/deduplication.md)
   - [Esempi di set di dati](essential-concepts/dataset-samples.md)
- Riferimento SQL {#sql}
   - [Panoramica SQL](sql/overview.md)
   - [Sintassi SQL](sql/syntax.md)
   - [Funzioni definite dall&#39;Adobe](sql/adobe-defined-functions.md)
   - [Funzioni SQL di Spark](sql/spark-sql-functions.md)
   - [Comandi metadati](sql/metadata.md)
   - [Dichiarazioni preparate](sql/prepared-statements.md)
- [Domande frequenti](troubleshooting-guide.md)
- [Riferimento API](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Note sulla versione di Platform](https://www.adobe.com/go/platform-release-notes-en)
