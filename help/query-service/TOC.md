---
audience: user
user-guide-title: Guida al servizio query di Adobe Experience Platform
breadcrumb-title: Guida al servizio query
user-guide-description: Utilizza SQL standard per eseguire query sui dati in Platform Data Lake.
feature: Queries
source-git-commit: df894d8b52aff3708aa06e73d4c5ba3e1e501f10
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 16%

---


# Servizio query Adobe Experience Platform {#query}

- [Panoramica del servizio query](home.md)
- [Pacchetto del servizio query](packages.md)
- [Garanzie del servizio query](guardrails.md)
- Distiller dati {#data-distiller}
   - [Utilizzo della licenza](data-distiller/licence-usage.md)
- Introduzione {#get-started}
   - [Prerequisiti](get-started/prerequisites.md)
- Casi d’uso {#use-cases}
   - [Sfoglia abbandonato](use-cases/abandoned-browse.md)
   - [Analisi Delle Attività Con Adobe Target](use-cases/activity-analysis-with-adobe-target.md)
   - [Analisi di attribuzione](use-cases/attribution-analysis.md)
   - [Filtro bot](use-cases/bot-filtering.md)
   - [Informazioni approfondite su web e dispositivi mobili](use-cases/analytics-insights.md)
- API del servizio query {#api}
   - [Introduzione](api/getting-started.md)
   - [Query](api/queries.md)
   - [Parametri di connessione](api/connection-parameters.md)
   - [Query pianificate](api/scheduled-queries.md)
   - [Viene eseguito per query pianificate](api/runs-scheduled-queries.md)
   - [Modelli di query](api/query-templates.md)
- Interfaccia utente del servizio query {#ui}
   - [Panoramica dell’interfaccia utente](ui/overview.md)
   - [Guida utente dell’editor delle query](ui/user-guide.md)
   - [Modelli di query](ui/query-templates.md)
   - [Utilizzo delle credenziali del servizio query](ui/credentials.md)
   - [Generazione di set di dati dai risultati delle query](ui/create-datasets.md)
- Best practice {#best-practices}
   - [Indicazioni generali per l’esecuzione delle query](best-practices/writing-queries.md)
   - [Guida all&#39;organizzazione delle risorse dati](./best-practices/organize-data-assets.md)
   - [Utilizzo delle strutture di dati nidificate](best-practices/nested-data-structures.md)
   - [Strutture dati nidificate appiattite](best-practices/flatten-nested-data.md)
   - [Blocco anonimo](best-practices/anonymous-block.md)
   - [Caricamento incrementale](best-practices/incremental-load.md)
   - [Deduplicazione dati](best-practices/deduplication.md)
- Attributi derivati {#derived-attributes}
   - [Panoramica](derived-attributes/overview.md)
   - [Caso di utilizzo dei decibel](derived-attributes/deciles-use-case.md)
- Query di esempio {#sample-queries}
   - [Query Evento esperienza di esempio](sample-queries/experience-event.md)
   - [Query Adobe Analytics di esempio](sample-queries/adobe-analytics.md)
- Riferimento SQL {#sql}
   - [Panoramica SQL](sql/overview.md)
   - [Sintassi SQL](sql/syntax.md)
   - [Funzioni definite dall&#39;Adobe](sql/adobe-defined-functions.md)
   - [Funzioni SQL di Spark](sql/spark-sql-functions.md)
   - [Comandi metadati](sql/metadata.md)
   - [Dichiarazioni preparate](sql/prepared-statements.md)
   - [Esempi di set di dati](sql/dataset-samples.md)
- Connettere i client al servizio query {#clients}
   - [Panoramica delle connessioni client](clients/overview.md)
   - [Modalità SSL](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [Visualizzatore Db](./clients/dbvisulaizer.md)
   - [Notebook Jupyter](clients//jupyter-notebook.md)
   - [Guardaroba](clients/looker.md)
   - [Postico](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RSudio](clients/rstudio.md)
   - [Tableau](clients/tableau.md)
- Governance dei dati {#data-governance}
   - [Panoramica](data-governance/overview.md)
   - [Guida al registro di controllo](data-governance/audit-log-guide.md)
   - [Identità nei set di dati di schemi ad hoc](data-governance/ad-hoc-schema-identities.md)
   - [Supporto del controllo degli accessi basato su attributi per schemi ad hoc](./data-governance/ad-hoc-schema-labels.md)
- [Guida alla risoluzione dei problemi](troubleshooting-guide.md)
- [Riferimento API](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Note sulla versione di Platform](https://www.adobe.com/go/platform-release-notes-en)