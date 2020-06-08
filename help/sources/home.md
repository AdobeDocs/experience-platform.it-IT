---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica sui connettori sorgente della piattaforma Adobe Experience
topic: overview
translation-type: tm+mt
source-git-commit: f181d544e93f0924bf4c239fad93d78c974afdc0
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---


# Panoramica sui connettori sorgente

Adobe Experience Platform consente di acquisire dati da origini esterne, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi della piattaforma. È possibile acquisire dati da origini diverse come applicazioni Adobe, archiviazione basata su cloud, database e molti altri.

Experience Platform fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di configurare con facilità le connessioni di origine a vari provider di dati. Queste connessioni di origine consentono di autenticare i sistemi di terze parti, impostare i tempi di caricamento e gestire il throughput di assimilazione dei dati.

Con Experience Platform, puoi centralizzare i dati raccolti da fonti diverse e utilizzare le informazioni acquisite per fare di più.

## Tipi di fonti

Le origini in Experience Platform sono raggruppate nelle seguenti categorie:

### Applicazioni Adobe

Experience Platform consente di acquisire dati da altre applicazioni Adobe, tra cui Adobe Analytics, Adobe Audience Manager e Experience Platform Launch. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [Panoramica del connettore Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
- [Creare un connettore sorgente Adobe Audience Manager nell’interfaccia utente](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Panoramica del connettore dati di Adobe Analytics](connectors/adobe-applications/analytics.md)
- [Creare un connettore sorgente Adobe Analytics nell’interfaccia utente](./tutorials/ui/create/adobe-applications/analytics.md)
- [Creare un connettore di origine Attributi del cliente nell&#39;interfaccia utente](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Pubblicità

Experience Platform supporta l’acquisizione di dati da un sistema pubblicitario di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consultate i seguenti documenti correlati:

- [Connettore Google AdWords](connectors/advertising/ads.md)

### Archiviazione cloud

Le origini di archiviazione cloud possono portare i tuoi dati in Platform senza bisogno di scaricare, formattare o caricare. I dati ingeriti possono essere formattati come JSON XDM, parquet XDM o delimitati. Ogni fase del processo è integrata nel flusso di lavoro Origini tramite l&#39;interfaccia utente. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [Connettore Azure Data Lake Storage Gen2](connectors/cloud-storage/adls-gen2.md)
- [Connettore Azure Blob e Amazon S3](connectors/cloud-storage/blob-s3.md)
- [Connettore Amazon Kinesis](connectors/cloud-storage/kinesis.md)
- [Connettore Azure Event Hubs](connectors/cloud-storage/eventhub.md)
- [Connettore archiviazione file Azure](connectors/cloud-storage/azure-file-storage.md)
- [Connettore FTP e SFTP](connectors/cloud-storage/ftp-sftp.md)
- [Connettore di archiviazione Google Cloud](connectors/cloud-storage/google-cloud-storage.md)
- [Connettore HDFS](connectors/cloud-storage/hdfs.md)

### Gestione delle relazioni con i clienti (CRM)

I sistemi CRM forniscono dati che possono aiutare a creare relazioni con i clienti, creando a loro volta fidelizzazione e promuovendo la fidelizzazione dei clienti. Experience Platform supporta l&#39;acquisizione di dati CRM da Microsoft Dynamics 365 e Salesforce. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [Connettore Microsoft Dynamics](connectors/crm/ms-dynamics.md)
- [Connettore Salesforce](connectors/crm/salesforce.md)

### Successo cliente

Experience Platform supporta l’acquisizione di dati da un’applicazione di successo cliente di terze parti. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [Connettore Salesforce Service Cloud](connectors/customer-success/salesforce-service-cloud.md)
- [Connettore ServiceNow](connectors/customer-success/servicenow.md)

### Database

Experience Platform supporta l’acquisizione di dati da un database di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consultate i seguenti documenti correlati:

- [Connettore Amazon Redshift](connectors/databases/redshift.md)
- [Apache Hive sul connettore Azure HDInsights](connectors/databases/hive.md)
- [Apache Spark sul connettore Azure HDInsights](connectors/databases/spark.md)
- [Connettore Azure Data Explorer](connectors/databases/data-explorer.md)
- [Connettore Azure Synapse Analytics](connectors/databases/synapse-analytics.md)
- [Connettore archiviazione tabella Azure](connectors/databases/ats.md)
- [Connettore CouchBase](connectors/databases/couchbase.md)
- [Connettore Google BigQuery](connectors/databases/bigquery.md)
- [Connettore GreenPlum](connectors/databases/greenplum.md)
- [Connettore HP Vertica](connectors/databases/hp-vertica.md)
- [Connettore IBM DB2](connectors/databases/ibm-db2.md)
- [Connettore MariaDB](connectors/databases/mariadb.md)
- [Connettore di Microsoft SQL Server](connectors/databases/sql-server.md)
- [Connettore MySQL](connectors/databases/mysql.md)
- [Connettore Oracle](connectors/databases/oracle.md)
- [Connettore Phoenix](connectors/databases/phoenix.md)
- [Connettore PostgreSQL](connectors/databases/postgres.md)

### Marketing Automation

Experience Platform supporta l’acquisizione di dati da un sistema di automazione marketing di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consultate i seguenti documenti correlati:

- [Connettore HubSpot](connectors/marketing-automation/hubspot.md)

### Pagamenti

Experience Platform supporta l’acquisizione di dati da un sistema di pagamenti di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consultate i seguenti documenti correlati:

- [Connettore PayPal](connectors/payments/paypal.md)

### Protocolli

Experience Platform supporta l’acquisizione di dati da un sistema di protocolli di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consultate i seguenti documenti correlati:

- [Connettore OData generico](connectors/protocols/odata.md)

## Controllo degli accessi per le origini nell&#39;assimilazione dei dati

Le autorizzazioni per le origini nell&#39;assimilazione dei dati possono essere gestite all&#39;interno di Adobe Admin Console. Potete accedere alle autorizzazioni tramite la scheda *Autorizzazioni* in un particolare profilo di prodotto. Dal pannello **Modifica autorizzazioni** , potete accedere alle autorizzazioni relative alle origini tramite la voce del menu di inserimento dei *dati* . L&#39;autorizzazione **Visualizza origini** consente l&#39;accesso in sola lettura alle origini disponibili nella scheda *Catalogo* e alle origini autenticate nella scheda *Sfoglia* , mentre l&#39;autorizzazione **Gestisci origini** consente l&#39;accesso completo alle origini di lettura, creazione, modifica e disattivazione.

La tabella seguente illustra il comportamento dell’interfaccia utente in base alle diverse combinazioni di queste autorizzazioni:

| Livello di autorizzazione | Descrizione |
| ---- | ----|
| **Visualizza origini** su | Concedere l&#39;accesso in sola lettura alle origini in ciascun tipo di origine nella scheda *Catalogo* , nonché alle schede *Sfoglia*, *Account* e *DataFlow* . |
| **Gestisci origini** su | Oltre alle funzioni incluse in **Visualizza origini**, concede l&#39;accesso all&#39;opzione Origine ** Connect in *Catalogo* e all&#39;opzione *Seleziona dati* in *Sfoglia*. **Manage Sources** (Gestisci origini) consente inoltre di abilitare o disabilitare *DataFlows* e di modificarne le pianificazioni. |
| **Visualizza origini** disattivate e **gestisci origini** disattivate | Revoca tutti gli accessi alle origini. |

Per ulteriori informazioni sulle autorizzazioni disponibili concesse tramite Admin Console, comprese quelle quattro origini, vedi la panoramica [del controllo](../access-control/home.md)degli accessi.
