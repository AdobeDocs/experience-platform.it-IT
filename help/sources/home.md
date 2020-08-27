---
keywords: Experience Platform;home;popular topics;source connectors;source connector;sources;data sources;data source;data source connection
solution: Experience Platform
title: Panoramica dei connettori sorgente Adobe Experience Platform
topic: overview
description: Adobe Experience Platform consente l'acquisizione di dati da origini esterne, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Piattaforma. È possibile acquisire dati da origini diverse, come applicazioni  Adobe, storage basato su cloud, database e molti altri.
translation-type: tm+mt
source-git-commit: c8e53a25c5b22e8d840658fe26ff47875947a6d0
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---


# Panoramica sui connettori sorgente

Adobe Experience Platform consente l&#39;acquisizione di dati da origini esterne, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] i servizi. È possibile acquisire dati da origini diverse, come applicazioni  Adobe, storage basato su cloud, database e molti altri.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di configurare con facilità le connessioni di origine a vari provider di dati. Queste connessioni di origine consentono di autenticare i sistemi di terze parti, impostare i tempi di caricamento e gestire il throughput di assimilazione dei dati.

Con [!DNL Experience Platform], è possibile centralizzare i dati raccolti da fonti diverse e utilizzare le informazioni acquisite per fare di più.

## Tipi di fonti

Le origini [!DNL Experience Platform] sono raggruppate nelle seguenti categorie:

###  applicazioni Adobe

[!DNL Experience Platform] consente il trasferimento di dati da altre applicazioni  Adobe, inclusi  Adobe Analytics, Adobe Audience Manager e [!DNL Experience Platform Launch]. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [Panoramica del connettore Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
- [Creare un connettore sorgente Adobe Audience Manager nell’interfaccia utente](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Panoramica del connettore dati di classificazione Adobe Analytics](connectors/adobe-applications/classifications.md)
- [Creare un connettore  origine dati di classificazione Adobe Analytics nell&#39;interfaccia utente](./tutorials/ui/create/adobe-applications/classifications.md)
- [Panoramica del connettore dati Adobe Analytics](connectors/adobe-applications/analytics.md)
- [Creare un connettore sorgente Adobe Analytics  nell’interfaccia utente](./tutorials/ui/create/adobe-applications/analytics.md)
- [Creare un connettore di origine Attributi del cliente nell&#39;interfaccia utente](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Pubblicità

[!DNL Experience Platform] fornisce il supporto per l&#39;acquisizione di dati da un sistema pubblicitario di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consultate i seguenti documenti correlati:

- [Connettore [!DNL Google AdWords]](connectors/advertising/ads.md)

### Archiviazione cloud

Le origini di archiviazione cloud possono importare i tuoi dati [!DNL Platform] senza bisogno di scaricare, formattare o caricare. I dati ingeriti possono essere formattati come JSON XDM, parquet XDM o delimitati. Ogni fase del processo è integrata nel flusso di lavoro Origini tramite l&#39;interfaccia utente. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [[!DNL Azure Data Lake Storage Gen2] connettore](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob] connettore](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis] connettore](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3] connettore](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS] connettore](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs] connettore](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage] connettore](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL FTP and SFTP] connettore](connectors/cloud-storage/ftp-sftp.md)
- [[!DNL Google Cloud Storage] connettore](connectors/cloud-storage/google-cloud-storage.md)

### Gestione delle relazioni con i clienti (CRM)

I sistemi CRM forniscono dati che possono aiutare a creare relazioni con i clienti, creando a loro volta fidelizzazione e promuovendo la fidelizzazione dei clienti. [!DNL Experience Platform] fornisce supporto per l&#39;acquisizione di dati CRM da [!DNL Microsoft Dynamics 365] e [!DNL Salesforce]. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [[!DNL Microsoft Dynamics] connettore](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] connettore](connectors/crm/salesforce.md)

### Successo cliente

[!DNL Experience Platform] fornisce supporto per l’acquisizione di dati da un’applicazione di successo cliente di terze parti. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [[!DNL Salesforce Service Cloud] connettore](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow] connettore](connectors/customer-success/servicenow.md)

### Database

[!DNL Experience Platform] fornisce il supporto per l&#39;acquisizione di dati da un database di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consultate i seguenti documenti correlati:

- [[!DNL Amazon Redshift] connettore](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights] connettore](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights] connettore](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer] connettore](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics] connettore](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage] connettore](connectors/databases/ats.md)
- [[!DNL Couchbase] connettore](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery] connettore](connectors/databases/bigquery.md)
- [[!DNL GreenPlum] connettore](connectors/databases/greenplum.md)
- [[!DNL HP Vertica] connettore](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2] connettore](connectors/databases/ibm-db2.md)
- [[!DNL Microsoft SQL Server] connettore](connectors/databases/sql-server.md)
- [[!DNL MySQL] connettore](connectors/databases/mysql.md)
- [[!DNL Oracle] connettore](connectors/databases/oracle.md)
- [[!DNL Phoenix] connettore](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL] connettore](connectors/databases/postgres.md)

### Marketing Automation

[!DNL Experience Platform] fornisce il supporto per l&#39;acquisizione di dati da un sistema di automazione marketing di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consultate i seguenti documenti correlati:

- [[!DNL HubSpot] connettore](connectors/marketing-automation/hubspot.md)

### Pagamenti

[!DNL Experience Platform] fornisce supporto per l&#39;acquisizione di dati da un sistema di pagamenti di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consultate i seguenti documenti correlati:

- [[!DNL PayPal] connettore](connectors/payments/paypal.md)

### Protocolli

[!DNL Experience Platform] fornisce il supporto per l&#39;acquisizione di dati da un sistema di protocolli di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consultate i seguenti documenti correlati:

- [[!DNL Generic OData] connettore](connectors/protocols/odata.md)

## Controllo degli accessi per le origini nell&#39;assimilazione dei dati

Le autorizzazioni per le origini nell&#39;assimilazione dei dati possono essere gestite all&#39;interno dell&#39;Adobe Admin Console. Puoi accedere alle autorizzazioni tramite la *[!UICONTROL Permissions]* scheda in un particolare profilo di prodotto. Dal **[!UICONTROL Edit Permissions]** pannello potete accedere alle autorizzazioni relative alle origini tramite la voce di *[!UICONTROL data ingestion]* menu. L&#39; **[!UICONTROL View Sources]** autorizzazione consente l&#39;accesso in sola lettura alle origini disponibili nella *[!UICONTROL Catalog]* scheda e alle origini autenticate nella *[!UICONTROL Browse]* scheda, mentre l&#39; **[!UICONTROL Manage Sources]** autorizzazione consente l&#39;accesso completo alle origini di lettura, creazione, modifica e disattivazione.

La tabella seguente illustra il comportamento dell’interfaccia utente in base alle diverse combinazioni di queste autorizzazioni:

| Livello di autorizzazione | Descrizione |
| ---- | ----|
| **[!UICONTROL View Sources]** Attivato | Concedere l&#39;accesso in sola lettura alle origini in ciascun tipo di origine nella scheda *Catalogo* , nonché alle schede *Sfoglia*, *Account* e *DataFlow* . |
| **[!UICONTROL Manage Sources]** Attivato | Oltre alle funzioni incluse in **[!UICONTROL View Sources]**, concede l&#39;accesso all&#39; *[!UICONTROL Connect Source]* opzione in *[!UICONTROL Catalog]* e all&#39; *[!UICONTROL Select Data]* opzione in *[!UICONTROL Browse]*. **[!UICONTROL Manage Sources]** consente inoltre di abilitare o disabilitare *[!UICONTROL DataFlows]* e modificare le relative pianificazioni. |
| **[!UICONTROL View Sources]** Disattivato e **[!UICONTROL Manage Sources]** disattivato | Revoca tutti gli accessi alle origini. |

Per ulteriori informazioni sulle autorizzazioni disponibili concesse tramite il Admin Console di , comprese quelle quattro origini, consultate la panoramica [del controllo di](../access-control/home.md)accesso.

## Termini e condizioni {#terms-and-conditions}

Utilizzando una delle fonti etichettate come beta (&quot;Beta&quot;), l&#39;Utente dichiara che la Beta è fornita ***&quot;così come è&quot; senza garanzia di alcun tipo***.

 Adobe non ha l&#39;obbligo di mantenere, correggere, aggiornare, modificare, modificare o in altro modo supportare la versione beta. Si consiglia di usare cautela e di non fare affidamento in alcun modo sul corretto funzionamento o sulle prestazioni di tali sostanze Beta e/o materiali di accompagnamento. La versione beta è considerata un&#39;informazione confidenziale  Adobe.

Eventuali &quot;Feedback&quot; (informazioni relative alla versione beta che includono, tra l&#39;altro, problemi o difetti riscontrati durante l&#39;utilizzo della versione beta, suggerimenti, miglioramenti e raccomandazioni) forniti dall&#39;Utente  Adobe sono assegnati al Adobe  compresi tutti i diritti, il titolo e l&#39;interesse per e a tale Feedback.

Invia un feedback aperto o crea un ticket di supporto per condividere i tuoi suggerimenti o segnalare un bug, per ottenere un miglioramento della funzione.
