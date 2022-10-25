---
keywords: Experience Platform;home;argomenti popolari;connettori sorgente;connettore sorgente;origini;origini dati;origine dati;connessione origine dati
solution: Experience Platform
title: Panoramica dei connettori di origine
topic-legacy: overview
description: Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: cf9390076e027ba746c3bc83df8a18e3751b84a8
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 0%

---

# Panoramica dei connettori sorgente

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archivi basati su cloud, database e molti altri.

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie sorgenti all’interno di Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful che consente di configurare facilmente le connessioni sorgente a vari provider di dati. Queste connessioni di origine consentono di autenticare i sistemi di terze parti, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

Ad Experience Platform, è possibile centralizzare i dati raccolti da fonti diverse e utilizzare le informazioni raccolte per fare di più.

## Tipi di fonti

Le origini in Experience Platform sono raggruppate nelle seguenti categorie:

### Applicazioni di Adobe {#adobe-applications}

Experience Platform consente l’acquisizione di dati da altre applicazioni Adobe, tra cui Adobe Analytics e Adobe Audience Manager. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [Panoramica della sorgente Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
   - [Creare una connessione sorgente Adobe Audience Manager nell’interfaccia utente](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Panoramica dell’origine dati classificazioni di Adobe Analytics](connectors/adobe-applications/classifications.md)
   - [Creare una connessione all’origine dati Adobe Analytics Classifications nell’interfaccia utente](./tutorials/ui/create/adobe-applications/classifications.md)
- [Panoramica dell’origine dati della suite di rapporti di Adobe Analytics](connectors/adobe-applications/analytics.md)
   - [Creare una connessione sorgente Adobe Analytics nell’interfaccia utente](./tutorials/ui/create/adobe-applications/analytics.md)
- [Panoramica della sorgente Adobe Campaign Managed Cloud Services](connectors/adobe-applications/campaign.md)
   - [Creare una connessione sorgente Adobe Campaign Managed Cloud Services nell’interfaccia utente](./tutorials/ui/create/adobe-applications/campaign.md)
- [Panoramica della raccolta dati di Adobe](connectors/adobe-applications/data-collection.md)
   - [Creare una connessione sorgente Attributi del cliente nell&#39;interfaccia utente](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] panoramica di origine](connectors/adobe-applications/marketo/marketo.md)
   - [Crea un [!DNL Marketo Engage] connessione sorgente nell’interfaccia utente](./tutorials/ui/create/adobe-applications/marketo.md)
- [Panoramica della sorgente Adobe Workfront](connectors/adobe-applications/workfront.md)
   - [Creare una connessione sorgente Workfront nell’interfaccia utente](./tutorials/ui/create/adobe-applications/workfront.md)

### Advertising {#advertising}

Experience Platform fornisce il supporto per l’acquisizione di dati da un sistema pubblicitario di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consulta i seguenti documenti correlati:

- [Google Ads](connectors/advertising/ads.md)

### Analytics {#analytics}

Experience Platform fornisce il supporto per l’acquisizione di dati da una piattaforma di analisi di terze parti. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md)

### Archiviazione cloud {#cloud-storage}

Le origini di archiviazione cloud possono importare i tuoi dati in Platform senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come JSON XDM, Parquet XDM o delimitati. Ogni passaggio del processo viene integrato nel flusso di lavoro Origini tramite l’interfaccia utente. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md)
- [[!DNL FTP]](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md)

### Consenso e preferenze {#consent}

Experience Platform fornisce il supporto per l’acquisizione di dati da una piattaforma di gestione del consenso e delle preferenze di terze parti. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md)

### Gestione delle relazioni con i clienti (CRM) {#customer-relationship-management}

I sistemi di gestione delle relazioni con i clienti forniscono dati che possono aiutare a creare relazioni con i clienti, che a loro volta creano fidelizzazione e promuovono la fidelizzazione dei clienti. Experience Platform fornisce il supporto per l’acquisizione di dati CRM da [!DNL Microsoft Dynamics 365] e [!DNL Salesforce]. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce]](connectors/crm/salesforce.md)
- [[!DNL Veeva CRM]](connectors/crm/veeva.md)
- [[!DNL Zoho CRM]](connectors/crm/zoho.md)

### Successo del cliente {#customer-success}

Experience Platform fornisce il supporto per l’acquisizione di dati da un’applicazione di successo per clienti di terze parti. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [[!DNL Oracle Service Cloud]](connectors/customer-success/oracle-service-cloud.md)
- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md)
- [[!DNL Zendesk]](connectors/customer-success/zendesk.md)

### Database {#database}

Experience Platform supporta l’acquisizione di dati da un database di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consulta i seguenti documenti correlati:

- [[!DNL Amazon Redshift]](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage]](connectors/databases/ats.md)
- [[!DNL Couchbase]](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md)
- [[!DNL GreenPlum]](connectors/databases/greenplum.md)
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md)
- [[!DNL MariaDB]](connectors/databases/mariadb.md)
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md)
- [[!DNL MySQL]](connectors/databases/mysql.md)
- [[!DNL Oracle]](connectors/databases/oracle.md)
- [[!DNL Phoenix]](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL]](connectors/databases/postgres.md)
- [[!DNL Snowflake]](connectors/databases/snowflake.md)
- [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md)

### eCommerce {#ecommerce}

Experience Platform supporta l’acquisizione di dati da un sistema eCommerce di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consulta i seguenti documenti correlati:

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### Sistema locale {#local-system}

Experience Platform supporta l’acquisizione di dati dal sistema locale. Per ulteriori informazioni su connettori sorgente specifici, consulta i seguenti documenti correlati:

- [Caricamento file locale](connectors/local-system/local-file-upload.md)

### Automazione del marketing {#marketing-automation}

Experience Platform fornisce il supporto per l’acquisizione di dati da un sistema di automazione marketing di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consulta i seguenti documenti correlati:

- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md)
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md)
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md)
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md)

### Pagamenti {#payments}

Experience Platform fornisce il supporto per l’acquisizione di dati da un sistema di pagamenti di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consulta i seguenti documenti correlati:

- [[!DNL PayPal]](connectors/payments/paypal.md)
- [[!DNL Square]](connectors/payments/square.md)

### Streaming {#streaming}

Experience Platform supporta l’acquisizione di dati da sorgenti in streaming. Per ulteriori informazioni su connettori sorgente specifici, consulta i seguenti documenti correlati:

- [[!DNL HTTP API]](connectors/streaming/http.md)

### Protocolli {#protocols}

Experience Platform fornisce il supporto per l’acquisizione di dati da un sistema di protocolli di terze parti. Per ulteriori informazioni su connettori sorgente specifici, consulta i seguenti documenti correlati:

- [[!DNL Generic OData]](connectors/protocols/odata.md)
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md)

## Controllo degli accessi alle origini durante l’acquisizione dei dati

Le autorizzazioni per le origini nell’acquisizione dei dati possono essere gestite in Adobe Admin Console. Puoi accedere alle autorizzazioni tramite **[!UICONTROL Autorizzazioni]** in un particolare profilo di prodotto. Da **[!UICONTROL Modifica autorizzazioni]** puoi accedere alle autorizzazioni relative alle origini tramite il pannello **[!UICONTROL inserimento dati]** voce di menu. La **[!UICONTROL Visualizza origini]** l&#39;autorizzazione consente l&#39;accesso in sola lettura alle origini disponibili nel **[!UICONTROL Catalogo]** e le origini autenticate nel **[!UICONTROL Sfoglia]** , mentre **[!UICONTROL Gestisci origini]** Le autorizzazioni consentono l&#39;accesso completo alle origini in lettura, creazione, modifica e disattivazione.

La tabella seguente illustra il funzionamento dell’interfaccia utente in base a diverse combinazioni di queste autorizzazioni:

| Livello di autorizzazione | Descrizione |
| ---- | ----|
| **[!UICONTROL Visualizza origini]** On | Concedi l&#39;accesso in sola lettura alle origini in ciascun tipo di origine nella scheda Catalogo, nonché alle schede Sfoglia, Account e Flusso di dati. |
| **[!UICONTROL Gestisci origini]** On | Oltre alle funzioni incluse in **[!UICONTROL Visualizza origini]**, concede l&#39;accesso **[!UICONTROL Origine connessione]** opzione in **[!UICONTROL Catalogo]** e **[!UICONTROL Seleziona dati]** opzione in **[!UICONTROL Sfoglia]**. **[!UICONTROL Gestisci origini]** consente inoltre di abilitare o disabilitare **[!UICONTROL Flussi dati]** e modificarne le pianificazioni. |
| **[!UICONTROL Visualizza origini]** Off e **[!UICONTROL Gestisci origini]** Disattivato | Revoca tutti gli accessi alle sorgenti. |

Per ulteriori informazioni sulle autorizzazioni disponibili concesse tramite Autorizzazioni di Adobe, consulta la sezione [panoramica sul controllo degli accessi](../access-control/home.md).

### Controllo dell&#39;accesso basato su attributi per le origini

Il controllo dell&#39;accesso basato su attributi in Adobe Experience Platform consente agli amministratori di controllare l&#39;accesso a oggetti e/o funzionalità specifici in base agli attributi.

Con il controllo dell&#39;accesso basato sugli attributi, puoi applicare configurazioni di mappatura ai campi a cui disponi delle autorizzazioni. Inoltre, non puoi inserire dati in un set di dati se non hai accesso a tutti i campi del set di dati.

Per ulteriori informazioni sul controllo degli accessi basato su attributi, consulta la sezione [panoramica sul controllo dell&#39;accesso basato sugli attributi](../access-control/abac/overview.md).

## Termini e condizioni {#terms-and-conditions}

Utilizzando una delle fonti etichettate come beta (&quot;Beta&quot;), l&#39;Utente riconosce che la Beta è fornita ***&quot;così com&#39;è&quot; senza garanzia di alcun tipo***.

L&#39;Adobe non ha l&#39;obbligo di mantenere, correggere, aggiornare, modificare, modificare o altrimenti supportare la versione beta. Si consiglia di usare cautela e di non fare affidamento in alcun modo sul corretto funzionamento o sulle prestazioni di tali materiali Beta e/o di accompagnamento. La versione beta è considerata un’informazione riservata di Adobe.

Qualsiasi &quot;Feedback&quot; (informazioni relative alla Beta, compresi, tra l&#39;altro, problemi o difetti riscontrati durante l&#39;utilizzo della Beta, suggerimenti, miglioramenti e raccomandazioni) fornito dall&#39;Utente all&#39;Adobe, è assegnato all&#39;Adobe, inclusi tutti i diritti, il titolo e l&#39;interesse per e per tale Feedback.

Invia un feedback aperto o crea un ticket di supporto per condividere i tuoi suggerimenti o segnalare un bug, cerca un miglioramento della funzione.
