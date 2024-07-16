---
keywords: Experience Platform;home;argomenti popolari;connettori di origine;connettore di origine;origini;origini dati;origine dati;connessione origine dati
solution: Experience Platform
title: Panoramica dei connettori Source
description: Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 22f3b76c02e641d2f4c0dd7c0e5cc93038782836
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 2%

---

# Panoramica dei connettori Source

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archivi basati su cloud, database e molte altre.

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da diverse origini in Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful che consentono di impostare facilmente le connessioni sorgente a vari provider di dati. Queste connessioni di origine ti consentono di autenticare i sistemi di terze parti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

Ad Experience Platform, puoi centralizzare i dati raccolti da fonti diverse e utilizzare le informazioni acquisite per fare di più.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Sorgenti create da Adobi e da partner {#adobe-and-partner-built-sources}

Alcuni dei connettori nel catalogo di origini Experience Platform sono generati e gestiti da Adobe, mentre altri sono generati e gestiti da società partner tramite [Sources SDK](/help/sources/sources-sdk/overview.md). Una nota nella parte superiore della pagina della documentazione per ciascun connettore creato dal partner richiama se un’origine viene creata e gestita dal partner. Il [connettore Amazon S3](/help/sources/connectors/cloud-storage/s3.md), ad esempio, viene creato da Adobe, mentre il [connettore RainFocus](/help/sources/connectors/analytics/rainfocus.md) viene creato e gestito dal team RainFocus.

Per i connettori creati e gestiti dal partner, ciò significa che potrebbe essere necessario risolvere i problemi con il connettore dal team partner (metodo di contatto fornito nella nota nella pagina della documentazione). Per i problemi relativi ai connettori creati e gestiti da Adobe, contatta il rappresentante dell’Adobe o l’Assistenza clienti.

## Tipi di origini

Le origini in Experience Platform sono raggruppate nelle seguenti categorie:

### Applicazioni di Adobe {#adobe-applications}

Experience Platform consente di acquisire i dati da altre applicazioni Adobe, tra cui Adobe Analytics e Adobe Audience Manager. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [Panoramica origine Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
   - [Creare una connessione sorgente Adobe Audience Manager nell’interfaccia utente](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Panoramica sull’origine dati delle classificazioni di Adobe Analytics](connectors/adobe-applications/classifications.md)
   - [Creare una connessione origine dati per le classificazioni di Adobe Analytics nell’interfaccia utente](./tutorials/ui/create/adobe-applications/classifications.md)
- [Panoramica dell’origine dati della suite di rapporti di Adobe Analytics](connectors/adobe-applications/analytics.md)
   - [Creare una connessione sorgente Adobe Analytics nell’interfaccia utente](./tutorials/ui/create/adobe-applications/analytics.md)
- [Panoramica origine Adobe Campaign Managed Cloud Services](connectors/adobe-applications/campaign.md)
   - [Creare una connessione sorgente Adobe Campaign Managed Cloud Services nell’interfaccia utente](./tutorials/ui/create/adobe-applications/campaign.md)
- [Panoramica sull’origine di Adobe Commerce](connectors/adobe-applications/commerce.md)
- [Panoramica sull’origine di Adobe Data Collection](connectors/adobe-applications/data-collection.md)
   - [Creare una connessione sorgente Attributi del cliente nell’interfaccia utente](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [Panoramica dell&#39;origine [!DNL Marketo Engage]](connectors/adobe-applications/marketo/marketo.md)
   - [Crea una connessione di origine  [!DNL Marketo Engage]  nell&#39;interfaccia utente](./tutorials/ui/create/adobe-applications/marketo.md)
   - [Crea una connessione di origine e un flusso di dati  [!DNL Marketo Engage]  per i dati attività personalizzati](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)

### Advertising {#advertising}

Experience Platform fornisce supporto per l’acquisizione di dati da un sistema pubblicitario di terze parti. Per ulteriori informazioni su connettori di origine specifici, consulta i seguenti documenti correlati:

- [Google Ads](connectors/advertising/ads.md) [!BADGE Batch]{type=Informative}

### Analytics {#analytics}

Experience Platform fornisce supporto per l’acquisizione di dati da una piattaforma di analisi di terze parti. Per ulteriori informazioni, leggere i seguenti documenti correlati:

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) [!BADGE Batch]{type=Informative}
- [[!DNL Pendo]](connectors/analytics/pendo-webhook.md) [!BADGE Streaming]{type=Positive}
- [[!DNL RainFocus]](connectors/analytics/rainfocus.md) [!BADGE Streaming]{type=Positive}

### Archiviazione cloud {#cloud-storage}

Le origini di archiviazione cloud possono inserire i tuoi dati in Platform senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come XDM JSON, XDM Parquet o delimitati. Ogni passaggio del processo viene integrato nel flusso di lavoro Origini tramite l’interfaccia utente di. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md) [!BADGE Batch]{type=Informative}
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md) [!BADGE Batch]{type=Informative}
- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md) [!BADGE Batch]{type=Informative}
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md) [!BADGE Batch]{type=Informative}
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md) [!BADGE Batch]{type=Informative}
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md) [!BADGE Batch]{type=Informative}
- [[!DNL FTP]](connectors/cloud-storage/ftp.md) [!BADGE Batch]{type=Informative}
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md) [!BADGE Batch]{type=Informative}
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md) [!BADGE Batch]{type=Informative}
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md) [!BADGE Batch]{type=Informative}

### Consenso e preferenze {#consent}

Experience Platform fornisce supporto per l’acquisizione dei dati da una piattaforma di gestione delle preferenze e del consenso di terze parti. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md) [!BADGE Batch]{type=Informative}

### Gestione delle relazioni con i clienti (CRM) {#customer-relationship-management}

I sistemi di gestione delle relazioni con i clienti forniscono dati che possono aiutare a costruire relazioni con i clienti, creando a sua volta fedeltà e incentivandone la fidelizzazione. Experience Platform fornisce supporto per l&#39;acquisizione di dati CRM da [!DNL Microsoft Dynamics 365] e [!DNL Salesforce]. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md) [!BADGE Batch]{type=Informative}
- [[!DNL Salesforce]](connectors/crm/salesforce.md) [!BADGE Batch]{type=Informative}
- [[!DNL SugarCRM]](connectors/crm/sugarcrm.md) [!BADGE Batch]{type=Informative}
- [[!DNL Veeva CRM]](connectors/crm/veeva.md) [!BADGE Batch]{type=Informative}
- [[!DNL Zoho CRM]](connectors/crm/zoho.md) [!BADGE Batch]{type=Informative}

### Customer Success {#customer-success}

Experience Platform fornisce supporto per l’acquisizione di dati da un’applicazione di successo per un cliente di terze parti. Per ulteriori informazioni, consulta i seguenti documenti correlati:

- [[!DNL Oracle Service Cloud]](connectors/customer-success/oracle-service-cloud.md) [!BADGE Batch]{type=Informative}
- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md) [!BADGE Batch]{type=Informative}
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md) [!BADGE Batch]{type=Informative}
- [[!DNL Zendesk]](connectors/customer-success/zendesk.md) [!BADGE Batch]{type=Informative}

### Database {#database}

Experience Platform fornisce supporto per l’acquisizione di dati da un database di terze parti. Per ulteriori informazioni su connettori di origine specifici, consulta i seguenti documenti correlati:

- [[!DNL Amazon Redshift]](connectors/databases/redshift.md) [!BADGE Batch]{type=Informative}
- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md) [!BADGE Batch]{type=Informative}
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md) [!BADGE Batch]{type=Informative}
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md) [!BADGE Batch]{type=Informative}
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md) [!BADGE Batch]{type=Informative}
- [[!DNL Azure Table Storage]](connectors/databases/ats.md) [!BADGE Batch]{type=Informative}
- [[!DNL Couchbase]](connectors/databases/couchbase.md) [!BADGE Batch]{type=Informative}
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md) [!BADGE Batch]{type=Informative}
- [[!DNL GreenPlum]](connectors/databases/greenplum.md) [!BADGE Batch]{type=Informative}
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md) [!BADGE Batch]{type=Informative}
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md) [!BADGE Batch]{type=Informative}
- [[!DNL MariaDB]](connectors/databases/mariadb.md) [!BADGE Batch]{type=Informative}
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md) [!BADGE Batch]{type=Informative}
- [[!DNL MySQL]](connectors/databases/mysql.md) [!BADGE Batch]{type=Informative}
- [[!DNL Oracle]](connectors/databases/oracle.md) [!BADGE Batch]{type=Informative}
- [[!DNL Phoenix]](connectors/databases/phoenix.md) [!BADGE Batch]{type=Informative}
- [[!DNL PostgreSQL]](connectors/databases/postgres.md) [!BADGE Batch]{type=Informative}
- [[!DNL Snowflake]](connectors/databases/snowflake-streaming.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Snowflake]](connectors/databases/snowflake.md) [!BADGE Batch]{type=Informative}
- [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md) [!BADGE Batch]{type=Informative}

### Partner di dati e identità {#data-partner}

Experience Platform fornisce supporto per l’acquisizione di dati da un database di terze parti. Per ulteriori informazioni su connettori di origine specifici, consulta i seguenti documenti correlati:

- [[!DNL Acxiom Data Ingestion]](connectors/data-partners/acxiom-data-ingestion.md) [!BADGE Batch]{type=Informative}
- [[!DNL Acxiom Prospecting Data Import]](connectors/data-partners/acxiom-prospecting-data-import.md) [!BADGE Batch]{type=Informative}
- [[!DNL Merkury Enterprise Identity Resolution]](connectors/data-partners/merkury.md) [!BADGE Batch]{type=Informative}

### eCommerce {#ecommerce}

Experience Platform fornisce supporto per l’acquisizione di dati da un sistema eCommerce di terze parti. Per ulteriori informazioni su connettori di origine specifici, consulta i seguenti documenti correlati:

- [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md) [!BADGE Batch]{type=Informative}
- [[!DNL Shopify]](connectors/ecommerce/shopify.md) [!BADGE Batch]{type=Informative}
- [[!DNL Shopify]](connectors/ecommerce/shopify-streaming.md) [!BADGE Streaming]{type=Positive}

### Sistema locale {#local-system}

Experience Platform fornisce supporto per l’acquisizione di dati dal sistema locale. Per ulteriori informazioni su connettori di origine specifici, consulta i seguenti documenti correlati:

- [Caricamento di file locali](connectors/local-system/local-file-upload.md)

### Marketing Automation {#marketing-automation}

Experience Platform fornisce supporto per l’acquisizione di dati da un sistema di automazione del marketing di terze parti. Per ulteriori informazioni su connettori di origine specifici, consulta i seguenti documenti correlati:

- [[!DNL Braze]](connectors/marketing-automation/braze.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md) [!BADGE Streaming]{type=Positive}
- [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md) [!BADGE Streaming]{type=Positive}
- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md) [!BADGE Batch]{type=Informative}
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md) [!BADGE Batch]{type=Informative}
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md) [!BADGE Batch]{type=Informative}
- [[!DNL Oracle NetSuite]](connectors/marketing-automation/oracle-netsuite.md) [!BADGE Batch]{type=Informative}
- [[!DNL PathFactory]](connectors/marketing-automation/pathfactory.md) [!BADGE Batch]{type=Informative}
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md) [!BADGE Batch]{type=Informative}
<!-- 
- [[!DNL Oracle Responsys]](connectors/marketing-automation/oracle-responsys.md)
-->

### Pagamenti {#payments}

Experience Platform fornisce supporto per l’acquisizione di dati da un sistema di pagamenti di terze parti. Per ulteriori informazioni su connettori di origine specifici, consulta i seguenti documenti correlati:

- [[!DNL PayPal]](connectors/payments/paypal.md) [!BADGE Batch]{type=Informative}
- [[!DNL Square]](connectors/payments/square.md) [!BADGE Batch]{type=Informative}
- [[!DNL Stripe]](connectors/payments/stripe.md) [!BADGE Batch]{type=Informative}

### Streaming {#streaming}

Experience Platform fornisce supporto per l’acquisizione di dati da origini di streaming. Per ulteriori informazioni su connettori di origine specifici, consulta i seguenti documenti correlati:

- [[!DNL HTTP API]](connectors/streaming/http.md) [!BADGE Streaming]{type=Positive}

### Protocolli {#protocols}

Experience Platform supporta l’acquisizione di dati da un sistema di protocolli di terze parti. Per ulteriori informazioni su connettori di origine specifici, consulta i seguenti documenti correlati:

- [[!DNL Generic OData]](connectors/protocols/odata.md) [!BADGE Batch]{type=Informative}
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md) [!BADGE Batch]{type=Informative}

## Controllo degli accessi per le origini nell’acquisizione dei dati

Le autorizzazioni per le origini nell’acquisizione dei dati possono essere gestite all’interno di Adobe Admin Console. Puoi accedere alle autorizzazioni tramite la scheda **[!UICONTROL Autorizzazioni]** in un particolare profilo di prodotto. Dal pannello **[!UICONTROL Modifica autorizzazioni]**, puoi accedere alle autorizzazioni relative alle origini tramite la voce di menu **[!UICONTROL Acquisizione dati]**. L&#39;autorizzazione **[!UICONTROL Visualizza origini]** consente l&#39;accesso in sola lettura alle origini disponibili nella scheda **[!UICONTROL Catalogo]** e alle origini autenticate nella scheda **[!UICONTROL Sfoglia]**, mentre l&#39;autorizzazione **[!UICONTROL Gestisci origini]** consente l&#39;accesso completo alle origini di lettura, creazione, modifica e disabilitazione.

La tabella seguente illustra il comportamento dell’interfaccia utente in base a diverse combinazioni di queste autorizzazioni:

| Livello di autorizzazione | Descrizione |
| ---- | ----|
| **[!UICONTROL Visualizza origini]** su | Concedi l’accesso in sola lettura alle origini in ciascun tipo di origine nella scheda Catalogo, nonché nelle schede Sfoglia, Account e Flusso di dati. |
| **[!UICONTROL Gestisci origini]** su | Oltre alle funzioni incluse in **[!UICONTROL Visualizza origini]**, consente l&#39;accesso all&#39;opzione **[!UICONTROL Connetti Source]** in **[!UICONTROL Catalogo]** e all&#39;opzione **[!UICONTROL Seleziona dati]** in **[!UICONTROL Sfoglia]**. **[!UICONTROL Gestisci origini]** consente inoltre di abilitare o disabilitare **[!UICONTROL Flussi dati]** e di modificarne le pianificazioni. |
| **[!UICONTROL Visualizza origini]** disattivato e **[!UICONTROL Gestisci origini]** disattivato | Revoca l&#39;accesso alle origini. |

Per ulteriori informazioni sulle autorizzazioni disponibili concesse tramite Autorizzazioni Adobe, leggere la [panoramica sul controllo degli accessi](../access-control/home.md).

### Controllo degli accessi basato su attributi

Il controllo dell’accesso basato su attributi in Adobe Experience Platform consente agli amministratori di controllare l’accesso a oggetti e/o funzionalità specifici in base agli attributi.

Con il controllo degli accessi basato su attributi, puoi applicare configurazioni di mappatura ai campi per i quali disponi delle autorizzazioni di. Inoltre, non puoi acquisire dati in un set di dati se non hai accesso a tutti i campi del set di dati.

#### Supporto per il controllo degli accessi basato su attributi nelle origini

>[!TIP]
>
>Il controllo degli accessi basato su attributi funziona come segue: **i ruoli** vengono creati per categorizzare i tipi di utenti che interagiscono con l&#39;istanza Platform. **Le etichette** sono applicate a **ruoli** per designare l&#39;accesso di quel determinato ruolo. **Le etichette** sono applicate anche a risorse come campi e segmenti dello schema. Per consentire a un utente di accedere a determinati campi e segmenti dello schema, è necessario aggiungerli a *un ruolo con la stessa etichetta assegnata alla risorsa su cui è stata eseguita la query*. Per ulteriori informazioni, leggere la [guida end-to-end per il controllo degli accessi basato su attributi](../access-control/abac/end-to-end-guide.md).

- Applica le etichette ai campi dello schema per definire l’accesso a specifici campi dello schema nella tua organizzazione. Una volta stabilito l’accesso a campi dello schema specifici, gli utenti potranno creare mappature solo per i campi a cui hanno accesso.
- Gli utenti che non dispongono dei ruoli appropriati non potranno creare o aggiornare flussi di dati con mappature che coinvolgono campi schema inaccessibili. Inoltre, gli utenti non autorizzati non possono aggiornare, eliminare, abilitare o disabilitare flussi di dati esistenti con campi schema inaccessibili.
- Inoltre, un flusso di dati deve avere esattamente lo stesso ID schema e la stessa versione nella mappatura, nel set di dati di destinazione e nella connessione di destinazione.

Per ulteriori informazioni sul controllo degli accessi basato su attributi, leggere la [panoramica sul controllo degli accessi basato su attributi](../access-control/abac/overview.md).

## Termini e condizioni {#terms-and-conditions}

Utilizzando una delle origini etichettate come beta (&quot;Beta&quot;), l&#39;utente riconosce che il Beta è fornito ***&quot;così com&#39;è&quot; senza alcuna garanzia***.

Adobe non ha alcun obbligo di mantenere, correggere, aggiornare, modificare, modificare o supportare in altro modo la Beta. Si consiglia di utilizzare il materiale informativo e di non fare affidamento in alcun modo sul corretto funzionamento o sulle prestazioni di tale Beta e/o dei materiali di accompagnamento. La Beta è considerata un&#39;informazione riservata di Adobe.

Qualsiasi &quot;Feedback&quot; (informazioni relative a Beta, inclusi ma non limitati a problemi o difetti riscontrati durante l’utilizzo di Beta, suggerimenti, miglioramenti e raccomandazioni) fornito dall’Utente a Adobe viene assegnato a Adobe, inclusi tutti i diritti, il titolo, l’interesse e il feedback.

Invia un feedback aperto o crea un ticket di supporto per condividere i suggerimenti o segnalare un bug, cercare un miglioramento delle funzioni.
