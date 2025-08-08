---
keywords: Experience Platform;home;argomenti popolari;connettori di origine;connettore di origine;origini;origini dati;origine dati;connessione origine dati;;home;popular topic;source connectors;source connector;sources;data source connection
solution: Experience Platform
title: Panoramica dei connettori Source
description: Adobe Experience Platform consente di acquisire dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: cad2cafdf39c718c3ba971eaa4e7f2318bd5f517
workflow-type: tm+mt
source-wordcount: '1644'
ht-degree: 12%

---

# Panoramica dei connettori Source

Adobe Experience Platform consente di acquisire dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archivi basati su cloud, database e molte altre.

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da diverse origini in Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful che consentono di impostare facilmente le connessioni sorgente a vari provider di dati. Queste connessioni di origine ti consentono di autenticare i sistemi di terze parti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

Con Experience Platform, puoi centralizzare i dati raccolti da origini diverse e utilizzare le informazioni acquisite per fare di più.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

>[!BEGINSHADEBOX]

## Sorgenti create da Adobe e dai partner {#adobe-and-partner-built-sources}

Alcuni dei connettori nel catalogo origini di Experience Platform sono generati e gestiti da Adobe, mentre altri sono generati e gestiti da società partner utilizzando [Origini SDK](/help/sources/sources-sdk/overview.md). Una nota nella parte superiore della pagina della documentazione per ciascun connettore creato dal partner richiama se un’origine viene creata e gestita dal partner. Ad esempio, il [connettore Amazon S3](/help/sources/connectors/cloud-storage/s3.md) è creato da Adobe, mentre il [connettore RainFocus](/help/sources/connectors/analytics/rainfocus.md) è creato e gestito dal team RainFocus.

Per i connettori creati e gestiti dal partner, ciò significa che potrebbe essere necessario risolvere i problemi con il connettore dal team partner (metodo di contatto fornito nella nota nella pagina della documentazione). Per i problemi relativi ai connettori creati e gestiti da Adobe, contatta il rappresentante Adobe o l’Assistenza clienti.

>[!ENDSHADEBOX]

## Catalogo origini

Leggere le sezioni seguenti per un elenco di tutte le origini disponibili nel catalogo delle origini.

### Applicazioni di Adobe {#adobe-applications}

Experience Platform consente di acquisire i dati da altre applicazioni Adobe, tra cui Adobe Analytics e Adobe Audience Manager. Per ulteriori informazioni, leggere i seguenti documenti correlati:

- [Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
   - [Creare una connessione sorgente Adobe Audience Manager nell’interfaccia utente](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Dati classificazioni Adobe Analytics](connectors/adobe-applications/classifications.md)
   - [Creare una connessione origine dati per le classificazioni di Adobe Analytics nell’interfaccia utente](./tutorials/ui/create/adobe-applications/classifications.md)
- [Dati suite di rapporti Adobe Analytics](connectors/adobe-applications/analytics.md)
   - [Creare una connessione sorgente Adobe Analytics nell’interfaccia utente](./tutorials/ui/create/adobe-applications/analytics.md)
- [Adobe Campaign Managed Cloud Services](connectors/adobe-applications/campaign.md)
   - [Creare una connessione sorgente Adobe Campaign Managed Cloud Services nell’interfaccia utente](./tutorials/ui/create/adobe-applications/campaign.md)
- [Adobe Commerce](connectors/adobe-applications/commerce.md)
- [Raccolta dati di Adobe](connectors/adobe-applications/data-collection.md)
   - [Creare una connessione sorgente Attributi del cliente nell’interfaccia utente](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage]](connectors/adobe-applications/marketo/marketo.md)
   - [Crea una connessione di origine  [!DNL Marketo Engage]  nell&#39;interfaccia utente](./tutorials/ui/create/adobe-applications/marketo.md)
   - [Crea una connessione di origine e un flusso di dati  [!DNL Marketo Engage]  per i dati attività personalizzati](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)

### Origini aziendali avanzate {#advanced-enterprise-sources}

Le seguenti origini sono disponibili solo per [clienti Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

| Origine | Categoria | Tipo di acquisizione | Cloud |
| --- | --- | --- | --- |
| [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md) | Archiviazione cloud | Streaming | Azure, AWS |
| [[!DNL Amazon Redshift]](connectors/databases/redshift.md) | Database | Batch | Azure, AWS |
| [[!DNL Azure Databricks]](connectors/databases/databricks.md) | Database | Batch | Azure |
| [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md) | Archiviazione cloud | Streaming | Azure, AWS |
| [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md) | Database | Batch | Azure |
| [[!DNL Google BigQuery]](connectors/databases/bigquery.md) | Database | Batch | Azure, AWS |
| [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md) | Archiviazione cloud | Streaming | Azure |
| [[!DNL Snowflake]](connectors/databases/snowflake-streaming.md) | Database | Streaming | Azure, AWS |
| [[!DNL Snowflake]](connectors/databases/snowflake.md) | Database | Batch | Azure, AWS |

{style="table-layout:auto"}

### Advertising {#advertising}

Per acquisire i dati pubblicitari in Experience Platform, puoi utilizzare le seguenti origini.

| Origine | Tipo di acquisizione | Cloud |
| --- | --- | --- |
| [Google Ads](connectors/advertising/ads.md) | Batch | Azure |

{style="table-layout:auto"}

### Analytics {#analytics}

Per acquisire i dati analitici in Experience Platform, puoi utilizzare le seguenti origini.

| Origine | Tipo di acquisizione | Cloud |
| --- | --- | --- |
| [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) | Batch | Azure |
| [[!DNL Pendo]](connectors/analytics/pendo-webhook.md) | Streaming | Azure |
| [[!DNL RainFocus]](connectors/analytics/rainfocus.md) | Streaming | Azure |

{style="table-layout:auto"}

### Archiviazione cloud {#cloud-storage}

Le origini di archiviazione cloud possono inserire i tuoi dati in Experience Platform senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come XDM JSON, XDM Parquet o delimitati. Ogni passaggio del processo viene integrato nel flusso di lavoro Origini tramite l’interfaccia utente di. Per ulteriori informazioni, consulta i seguenti documenti correlati:

Per acquisire i dati dall’archiviazione cloud in Experience Platform, puoi utilizzare le seguenti origini.

| Origine | Tipo di acquisizione | Cloud |
| --- | --- | --- |
| [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md) | Batch | Azure |
| [[!DNL Azure Blob]](connectors/cloud-storage/blob.md) | Batch | Azure |
| [[!DNL Amazon S3]](connectors/cloud-storage/s3.md) | Batch | Azure, AWS |
| [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md) | Batch | Azure |
| [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md) | Batch | Azure |
| [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md) | Batch | Azure, AWS |
| [[!DNL FTP]](connectors/cloud-storage/ftp.md) | Batch | Azure |
| [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md) | Batch | Azure |
| [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md) | Batch | Azure |
| [[!DNL SFTP]](connectors/cloud-storage/sftp.md) | Batch | Azure |

{style="table-layout:auto"}

### Consenso e preferenze {#consent}

Per acquisire i dati su consenso e preferenze in Experience Platform, puoi utilizzare le seguenti origini.

| Origine | Tipo di acquisizione | Cloud |
| --- | --- | --- |
| [[!DNL Didomi]](../sources/connectors/consent-and-preferences/didomi.md) | Streaming | Azure |
| [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md) | Batch | Azure |

{style="table-layout:auto"}

### Gestione delle relazioni con i clienti (CRM) {#customer-relationship-management}

I sistemi di gestione delle relazioni con i clienti forniscono dati che possono aiutare a costruire relazioni con i clienti, creando a sua volta fedeltà e incentivandone la fidelizzazione. Experience Platform fornisce supporto per l&#39;acquisizione di dati CRM da [!DNL Microsoft Dynamics 365] e [!DNL Salesforce]. Per ulteriori informazioni, consulta i seguenti documenti correlati:

Per acquisire i dati CRM in Experience Platform puoi utilizzare le seguenti origini.

| Origine | Tipo di acquisizione | Cloud |
| --- | --- | --- |
| [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md) | Batch | Azure |
| [[!DNL Salesforce]](connectors/crm/salesforce.md) | Batch | Azure, AWS |
| [[!DNL SugarCRM]](connectors/crm/sugarcrm.md) | Batch | Azure |
| [[!DNL Veeva CRM]](connectors/crm/veeva.md) | Batch | Azure |

{style="table-layout:auto"}

### Customer Success {#customer-success}

Puoi utilizzare le seguenti origini per acquisire i dati di successo dei clienti in Experience Platform.

| Origine | Tipo di acquisizione | Cloud |
| --- | --- | --- |
| [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md) | Batch | Azure |
| [[!DNL ServiceNow]](connectors/customer-success/servicenow.md) | Batch | Azure |
| [[!DNL Zendesk]](connectors/customer-success/zendesk.md) | Batch | Azure |

{style="table-layout:auto"}

### Database {#database}

Experience Platform fornisce supporto per l’acquisizione di dati da un database di terze parti. Per ulteriori informazioni su connettori di origine specifici, consulta i seguenti documenti correlati:

Per acquisire i dati dal database ad Experience Platform, puoi utilizzare le seguenti origini.

| Origine | Tipo di acquisizione | Cloud |
| --- | --- | --- |
| [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md) | Batch | Azure |
| [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md) | Batch | Azure |
| [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md) | Batch | Azure |
| [[!DNL Azure Table Storage]](connectors/databases/ats.md) | Batch | Azure |
| [[!DNL GreenPlum]](connectors/databases/greenplum.md) | Batch | Azure |
| [[!DNL HP Vertica]](connectors/databases/hp-vertica.md) | Batch | Azure |
| [[!DNL IBM DB2]](connectors/databases/ibm-db2.md) | Batch | Azure |
| [[!DNL MariaDB]](connectors/databases/mariadb.md) | Batch | Azure |
| [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md) | Batch | Azure |
| [[!DNL MySQL]](connectors/databases/mysql.md) | Batch | Azure, AWS |
| [[!DNL Oracle]](connectors/databases/oracle.md) | Batch | Azure, AWS |
| [[!DNL PostgreSQL]](connectors/databases/postgres.md) | Batch | Azure, AWS |
| [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md) | Batch | Azure |

{style="table-layout:auto"}

### Partner di dati e identità {#data-partner}

Puoi utilizzare le seguenti origini per acquisire dati e dati dei partner di identità in Experience Platform.

| Origine | Tipo di acquisizione | Cloud |
| --- | --- | --- |
| [[!DNL Acxiom Data Ingestion]](connectors/data-partners/acxiom-data-ingestion.md) | Batch | Azure |
| [[!DNL Acxiom Prospecting Data Import]](connectors/data-partners/acxiom-prospecting-data-import.md) | Batch | Azure |
| [[!DNL Algolia User Profiles]](connectors/data-partners/algolia-user-profiles.md) | Batch | Azure |
| [[!DNL Bombora Intent]](connectors/data-partners/bombora.md) | Batch | Azure |
| [[!DNL Demandbase Intent]](connectors/data-partners/demandbase.md) | Batch | Azure |
| [[!DNL Merkury Enterprise Identity Resolution]](connectors/data-partners/merkury.md) | Batch | Azure |

{style="table-layout:auto"}

### e-commerce {#ecommerce}

Per acquisire i dati di e-commerce in Experience Platform, puoi utilizzare le seguenti origini.

| Origine | Tipo di acquisizione | Cloud |
| --- | --- | --- |
| [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md) | Batch | Azure |
| [[!DNL Shopify]](connectors/ecommerce/shopify.md) | Batch | Azure |
| [[!DNL Shopify]](connectors/ecommerce/shopify-streaming.md) | Streaming | Azure |

{style="table-layout:auto"}

### Sistema locale {#local-system}

Per acquisire i dati dal sistema locale ad Experience Platform, puoi utilizzare le seguenti origini.

| Origine | Tipo di acquisizione | Cloud |
| --- | --- | --- |
| [Caricamento file locale](connectors/local-system/local-file-upload.md) | Batch | Azure |

{style="table-layout:auto"}

### Marketing Automation {#marketing-automation}

Per acquisire i dati di automazione marketing in Experience Platform, puoi utilizzare le seguenti origini.

| Origine | Tipo di acquisizione | Cloud |
| --- | --- | --- |
| [[!DNL Braze]](connectors/marketing-automation/braze.md) | Streaming | Azure |
| [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md) | Streaming | Azure |
| [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md) | Streaming | Azure |
| [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md) | Batch | Azure |
| [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md) | Batch | Azure |
| [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md) | Batch | Azure |
| [[!DNL Oracle NetSuite]](connectors/marketing-automation/oracle-netsuite.md) | Batch | Azure |
| [[!DNL PathFactory]](connectors/marketing-automation/pathfactory.md) | Batch | Azure |
| [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md) | Batch | Azure, AWS |

{style="table-layout:auto"}

### Pagamenti {#payments}

Per acquisire i dati dei pagamenti in Experience Platform, puoi utilizzare le seguenti origini.

| Origine | Tipo di acquisizione | Cloud |
| --- | --- | --- |
| [[!DNL Square]](connectors/payments/square.md) | Batch | Azure |
| [[!DNL Stripe]](connectors/payments/stripe.md) | Batch | Azure |

{style="table-layout:auto"}

### Streaming {#streaming}

Per inviare dati ad Experience Platform, puoi utilizzare le seguenti origini.

| Origine | Tipo di acquisizione | Supporto cloud |
| --- | --- | --- |
| [[!DNL HTTP API]](connectors/streaming/http.md) | Streaming | Azure, AWS |

{style="table-layout:auto"}

### Protocolli {#protocols}

Per acquisire i dati del protocollo in Experience Platform, puoi utilizzare le seguenti origini.

| Origine | Tipo di acquisizione | Supporto cloud |
| --- | --- | --- |
| [[!DNL Generic OData]](connectors/protocols/odata.md) | Batch | Azure |
| [[!DNL Generic REST API]](connectors/protocols/generic-rest.md) | Batch | Azure |

{style="table-layout:auto"}

## Controllo degli accessi per le origini nell’acquisizione dei dati

Le autorizzazioni per le origini nell’acquisizione dei dati possono essere gestite all’interno di Adobe Admin Console. Puoi accedere alle autorizzazioni tramite la scheda **[!UICONTROL Autorizzazioni]** in un particolare profilo di prodotto. Dal pannello **[!UICONTROL Modifica autorizzazioni]**, puoi accedere alle autorizzazioni relative alle origini tramite la voce di menu **[!UICONTROL Acquisizione dati]**. L&#39;autorizzazione **[!UICONTROL Visualizza origini]** consente l&#39;accesso in sola lettura alle origini disponibili nella scheda **[!UICONTROL Catalogo]** e alle origini autenticate nella scheda **[!UICONTROL Sfoglia]**, mentre l&#39;autorizzazione **[!UICONTROL Gestisci origini]** consente l&#39;accesso completo alle origini di lettura, creazione, modifica e disabilitazione.

La tabella seguente illustra il comportamento dell’interfaccia utente in base a diverse combinazioni di queste autorizzazioni:

| Livello di autorizzazione | Descrizione |
| ---- | ----|
| **[!UICONTROL Visualizza origini]** su | Concedi l’accesso in sola lettura alle origini in ciascun tipo di origine nella scheda Catalogo, nonché nelle schede Sfoglia, Account e Flusso di dati. |
| **[!UICONTROL Gestisci origini]** su | Oltre alle funzioni incluse in **[!UICONTROL Visualizza origini]**, consente l&#39;accesso all&#39;opzione **[!UICONTROL Connetti Source]** in **[!UICONTROL Catalogo]** e all&#39;opzione **[!UICONTROL Seleziona dati]** in **[!UICONTROL Sfoglia]**. **[!UICONTROL Gestisci origini]** consente inoltre di abilitare o disabilitare **[!UICONTROL Flussi dati]** e di modificarne le pianificazioni. |
| **[!UICONTROL Visualizza origini]** disattivato e **[!UICONTROL Gestisci origini]** disattivato | Revoca l&#39;accesso alle origini. |

Per ulteriori informazioni sulle autorizzazioni disponibili concesse tramite le autorizzazioni Adobe, leggere la [panoramica sul controllo degli accessi](../access-control/home.md).

### Controllo degli accessi basato su attributi

Il controllo dell’accesso basato su attributi in Adobe Experience Platform consente agli amministratori di controllare l’accesso a oggetti e/o funzionalità specifici in base agli attributi.

Con il controllo degli accessi basato su attributi, puoi applicare configurazioni di mappatura ai campi per i quali disponi delle autorizzazioni di. Inoltre, non puoi acquisire dati in un set di dati se non hai accesso a tutti i campi del set di dati.

#### Supporto per il controllo degli accessi basato su attributi nelle origini

>[!TIP]
>
>Il controllo degli accessi basato su attributi funziona come segue: **i ruoli** vengono creati per categorizzare i tipi di utenti che interagiscono con l&#39;istanza Experience Platform. **Le etichette** sono applicate a **ruoli** per designare l&#39;accesso di quel determinato ruolo. **Le etichette** sono applicate anche a risorse come campi e segmenti dello schema. Per consentire a un utente di accedere a determinati campi e segmenti dello schema, è necessario aggiungerli a *un ruolo con la stessa etichetta assegnata alla risorsa su cui è stata eseguita la query*. Per ulteriori informazioni, leggere la [guida end-to-end per il controllo degli accessi basato su attributi](../access-control/abac/end-to-end-guide.md).

- Applica le etichette ai campi dello schema per definire l’accesso a specifici campi dello schema nella tua organizzazione. Una volta stabilito l’accesso a campi dello schema specifici, gli utenti potranno creare mappature solo per i campi a cui hanno accesso.
- Gli utenti che non dispongono dei ruoli appropriati non potranno creare o aggiornare flussi di dati con mappature che coinvolgono campi schema inaccessibili. Inoltre, gli utenti non autorizzati non possono aggiornare, eliminare, abilitare o disabilitare flussi di dati esistenti con campi schema inaccessibili.
- Inoltre, un flusso di dati deve avere esattamente lo stesso ID schema e la stessa versione nella mappatura, nel set di dati di destinazione e nella connessione di destinazione.

Per ulteriori informazioni sul controllo degli accessi basato su attributi, leggere la [panoramica sul controllo degli accessi basato su attributi](../access-control/abac/overview.md).

## Termini e condizioni {#terms-and-conditions}

Utilizzando una delle origini etichettate come beta (&quot;Beta&quot;), l&#39;utente riconosce che il Beta è fornito ***&quot;così com&#39;è&quot; senza alcuna garanzia***.

Adobe non ha alcun obbligo di mantenere, correggere, aggiornare, modificare, modificare o supportare in altro modo Beta. Si consiglia di utilizzare il materiale informativo e di non fare affidamento in alcun modo sul corretto funzionamento o sulle prestazioni di tale Beta e/o dei materiali di accompagnamento. Beta è considerata un&#39;informazione riservata di Adobe.

Qualsiasi &quot;Feedback&quot; (informazioni relative a Beta, compresi, a titolo esemplificativo e non esaustivo, problemi o difetti riscontrati durante l’utilizzo di Beta, suggerimenti, miglioramenti e raccomandazioni) fornito dall’Utente a Adobe viene assegnato ad Adobe, inclusi tutti i diritti, i titoli e gli interessi relativi a tale Feedback.

Invia un feedback aperto o crea un ticket di supporto per condividere i suggerimenti o segnalare un bug, cercare un miglioramento delle funzioni.
