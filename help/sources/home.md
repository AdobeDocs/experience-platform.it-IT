---
keywords: Experience Platform;home;argomenti popolari;connettori sorgente;connettori sorgente;origini;origini dati;origine dati;connessione origine dati
solution: Experience Platform
title: Panoramica dei connettori di origine
topic-legacy: overview
description: Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
translation-type: tm+mt
source-git-commit: af5564a07577a0123e1a45043d5479f6ad45d73e
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 0%

---

# Panoramica dei connettori sorgente

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archivi basati su cloud, database e molti altri.

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie sorgenti all’interno di Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful che consente di configurare facilmente le connessioni sorgente a vari provider di dati. Queste connessioni di origine consentono di autenticare i sistemi di terze parti, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

Ad Experience Platform, è possibile centralizzare i dati raccolti da fonti diverse e utilizzare le informazioni raccolte per fare di più.

## Tipi di fonti

Le origini in Experience Platform sono raggruppate nelle seguenti categorie:

### Applicazioni di Adobe

Experience Platform consente l’acquisizione di dati da altre applicazioni Adobe, tra cui Adobe Analytics, Adobe Audience Manager e [!DNL Experience Platform Launch]. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [Panoramica del connettore Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
- [Creare una connessione sorgente Adobe Audience Manager nell’interfaccia utente](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Panoramica del connettore dati classificazioni di Adobe Analytics](connectors/adobe-applications/classifications.md)
- [Creare una connessione all’origine dati Adobe Analytics Classifications nell’interfaccia utente](./tutorials/ui/create/adobe-applications/classifications.md)
- [Panoramica del connettore dati Adobe Analytics](connectors/adobe-applications/analytics.md)
- [Creare una connessione sorgente Adobe Analytics nell’interfaccia utente](./tutorials/ui/create/adobe-applications/analytics.md)
- [Creare una connessione sorgente Attributi del cliente nell&#39;interfaccia utente](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] panoramica del connettore](connectors/adobe-applications/marketo/marketo.md)
- [Creare una connessione  [!DNL Marketo Engage] sorgente nell’interfaccia utente](./tutorials/ui/create/adobe-applications/marketo.md)

### Pubblicità

Experience Platform fornisce il supporto per l’acquisizione di dati da un sistema pubblicitario di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consulta i seguenti documenti correlati:

- [[!DNL Google AdWords]](connectors/advertising/ads.md) connettore

### Archiviazione cloud

Le origini di archiviazione cloud possono importare i tuoi dati in Platform senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come JSON XDM, Parquet XDM o delimitati. Ogni passaggio del processo viene integrato nel flusso di lavoro Origini tramite l’interfaccia utente. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [[!DNL Azure Data Lake Storage Gen2] connettore](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob] connettore](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis] connettore](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3] connettore](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS] connettore](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs] connettore](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage] connettore](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL FTP] connettore](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage] connettore](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub] connettore](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage] connettore](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP] connettore](connectors/cloud-storage/sftp.md)

### Gestione delle relazioni con i clienti (CRM)

I sistemi di gestione delle relazioni con i clienti forniscono dati che possono aiutare a creare relazioni con i clienti, che a loro volta creano fidelizzazione e promuovono la fidelizzazione dei clienti. Experience Platform fornisce il supporto per l’acquisizione di dati CRM da [!DNL Microsoft Dynamics 365] e [!DNL Salesforce]. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [[!DNL Microsoft Dynamics] connettore](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] connettore](connectors/crm/salesforce.md)

### Successo del cliente

Experience Platform fornisce il supporto per l’acquisizione di dati da un’applicazione di successo per clienti di terze parti. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [[!DNL Salesforce Service Cloud] connettore](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow] connettore](connectors/customer-success/servicenow.md)

### Database

Experience Platform supporta l’acquisizione di dati da un database di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consulta i seguenti documenti correlati:

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

### eCommerce

Experience Platform supporta l’acquisizione di dati da un sistema eCommerce di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consulta i seguenti documenti correlati:

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### Automazione del marketing

Experience Platform fornisce il supporto per l’acquisizione di dati da un sistema di automazione marketing di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consulta i seguenti documenti correlati:

- [[!DNL HubSpot] connettore](connectors/marketing-automation/hubspot.md)

### Pagamenti

Experience Platform fornisce il supporto per l’acquisizione di dati da un sistema di pagamenti di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consulta i seguenti documenti correlati:

- [[!DNL PayPal] connettore](connectors/payments/paypal.md)

### Protocolli

Experience Platform fornisce il supporto per l’acquisizione di dati da un sistema di protocolli di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consulta i seguenti documenti correlati:

- [[!DNL Generic OData] connettore](connectors/protocols/odata.md)

## Controllo degli accessi alle origini durante l’acquisizione dei dati

Le autorizzazioni per le origini nell’acquisizione dei dati possono essere gestite in Adobe Admin Console. Puoi accedere alle autorizzazioni tramite la scheda **[!UICONTROL Permissions]** in un particolare profilo di prodotto. Dal pannello **[!UICONTROL Edit Permissions]** puoi accedere alle autorizzazioni relative alle origini tramite la voce di menu **[!UICONTROL data ingestion]** . L&#39;autorizzazione **[!UICONTROL View Sources]** consente l&#39;accesso in sola lettura alle origini disponibili nella scheda **[!UICONTROL Catalog]** e alle origini autenticate nella scheda **[!UICONTROL Browse]**, mentre l&#39;autorizzazione **[!UICONTROL Manage Sources]** consente l&#39;accesso completo per leggere, creare, modificare e disabilitare le origini.

La tabella seguente illustra il funzionamento dell’interfaccia utente in base a diverse combinazioni di queste autorizzazioni:

| Livello di autorizzazione | Descrizione |
| ---- | ----|
| **[!UICONTROL View Sources]** On | Concedi l&#39;accesso in sola lettura alle origini in ciascun tipo di origine nella scheda Catalogo, nonché alle schede Sfoglia, Account e Flusso di dati. |
| **[!UICONTROL Manage Sources]** On | Oltre alle funzioni incluse in **[!UICONTROL View Sources]**, consente l&#39;accesso all&#39;opzione **[!UICONTROL Connect Source]** in **[!UICONTROL Catalog]** e all&#39;opzione **[!UICONTROL Select Data]** in **[!UICONTROL Browse]**. **[!UICONTROL Manage Sources]** consente inoltre di abilitare o disabilitare  **[!UICONTROL DataFlows]** e modificare le relative pianificazioni. |
| **[!UICONTROL View Sources]** Disattivato e  **[!UICONTROL Manage Sources]** disattivato | Revoca tutti gli accessi alle sorgenti. |

Per ulteriori informazioni sulle autorizzazioni disponibili concesse tramite l&#39;Admin Console, incluse quelle quattro origini, consulta la [panoramica sul controllo degli accessi](../access-control/home.md).

## Termini e condizioni {#terms-and-conditions}

Utilizzando una delle fonti etichettate come beta (&quot;Beta&quot;), l&#39;Utente riconosce che la Beta viene fornita ***&quot;così com&#39;è&quot; senza garanzia di alcun tipo***.

L&#39;Adobe non ha l&#39;obbligo di mantenere, correggere, aggiornare, modificare, modificare o altrimenti supportare la versione beta. Si consiglia di usare cautela e di non fare affidamento in alcun modo sul corretto funzionamento o sulle prestazioni di tali materiali Beta e/o di accompagnamento. La versione beta è considerata un’informazione riservata di Adobe.

Qualsiasi &quot;Feedback&quot; (informazioni relative alla Beta, compresi, tra l&#39;altro, problemi o difetti riscontrati durante l&#39;utilizzo della Beta, suggerimenti, miglioramenti e raccomandazioni) fornito dall&#39;Utente all&#39;Adobe, è assegnato all&#39;Adobe, inclusi tutti i diritti, il titolo e l&#39;interesse per e per tale Feedback.

Invia un feedback aperto o crea un ticket di supporto per condividere i tuoi suggerimenti o segnalare un bug, cerca un miglioramento della funzione.
