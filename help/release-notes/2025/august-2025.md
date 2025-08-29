---
title: Note sulla versione di Adobe Experience Platform di agosto 2025
description: Note sulla versione di Adobe Experience Platform di agosto 2025.
exl-id: d93e98f3-d165-4710-ad1d-2ad3857cd0f8
source-git-commit: 35c3933f5debbba04c885f6000b908e292613395
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 85%

---

# Note sulla versione di Adobe Experience Platform

>[!TIP]
>
>Per le note sulla versione di altre applicazioni Adobe Experience Platform, consulta la seguente documentazione:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/it/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/it/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composizione di pubblico federato](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/it/docs/real-time-cdp-collaboration/using/latest)

**Data di rilascio: 19 agosto 2025**


Nuove funzioni e aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Avvisi](#alerts)
- [Servizio catalogo](#catalog-service)
- [Destinazioni](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Sandbox](#sandboxes)
- [Servizio di segmentazione](#segmentation-service)
- [Origini](#sources)

## Avvisi {#alerts}

Experience Platform consente di iscriverti agli avvisi basati su eventi per varie attività di Experience Platform. Puoi iscriverti a diverse regole di avviso tramite la scheda [!UICONTROL Avvisi] nell’interfaccia utente di Experience Platform e scegliere di ricevere messaggi di avviso nell’interfaccia stessa o tramite notifiche e-mail.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Avvisi sulla capacità della velocità effettiva di streaming | Tre nuovi avvisi consentono agli utenti di iscriversi e configurare gli avvisi per gestire e monitorare in modo proattivo le prestazioni della capacità di velocità effettiva di streaming. I nuovi avvisi includono quando la velocità effettiva di streaming ha raggiunto l’80%, il 90% o supera i limiti della capacità. Per ulteriori informazioni, consulta la guida sulle [regole sugli avvisi della capacità](../../observability/alerts/rules.md#capacity). |

Per ulteriori informazioni sugli avvisi, consulta la [[!DNL Observability Insights] panoramica](../../observability/home.md).

## Servizio catalogo {#catalog-service}

Il servizio catalogo è il sistema di registrazione per la posizione e la derivazione dei dati in Adobe Experience Platform. Tutti i dati acquisiti in Experience Platform vengono memorizzati nel data lake come file e directory. Il servizio catalogo, invece, contiene i metadati e le descrizioni di tali file e directory a scopo di ricerca e monitoraggio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Conservazione dei dati per profilo cliente in tempo reale | Puoi **solo** aggiornare il periodo di conservazione dei dati per il profilo cliente in tempo reale una volta ogni 30 giorni. |

Per ulteriori informazioni sul Servizio catalogo, consulta la [panoramica sul servizio catalogo](../../catalog/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

>[!IMPORTANT]
>
>**Estensione pianificazione dell’esportazione dei set di dati**
>
>Se nell’organizzazione sono presenti flussi di dati di esportazione del set di dati creati prima di novembre 2024, questi flussi di dati cesseranno di funzionare il **1° settembre 2025**. Se è necessario che i flussi di dati continuino a esportare dati dopo il 1° settembre 2025, è necessario estendere le pianificazioni per ogni destinazione in cui i set di dati vengono esportati, seguendo i passaggi descritti in [questa guida](../../destinations/ui/dataset-expiration-update.md).

>[!IMPORTANT]
>
>**Aggiornamento dell’elenco IP consentiti necessario per le destinazioni basate su API**
>
>A causa degli aggiornamenti al motore di esportazione delle destinazioni di streaming, le organizzazioni che utilizzano l’[elenco IP consentiti](../../destinations/catalog/streaming/ip-address-allow-list.md) per le destinazioni basate su API devono aggiungere i seguenti indirizzi IP ai propri elenchi consentiti **prima del 15 settembre 2025**:
>
>**Indirizzi IP obbligatori:**
>
>```
>3.209.222.108
>3.211.230.204
>35.169.227.49
>66.117.18.133
>66.117.18.134
>66.117.18.135
>```
>
>**Questa modifica si applica ai seguenti tipi di destinazione:**
>
>- [Destinazioni di esportazione del pubblico in streaming](../../destinations/destination-types.md#streaming-destinations) ([Pubblico in tempo reale Pega CDH](/help/destinations/catalog/personalization/pega-v2.md), integrazioni basate su API con [Salesforce Marketing Cloud](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) e [Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md))
>- Destinazioni pubbliche o private generate tramite [Destination SDK](../../destinations/destination-sdk/getting-started.md)
>
>**Azione richiesta:** se hai utilizzato Adobe per inserire eventuali indirizzi IP nell’elenco consentiti verso destinazioni di streaming basate su API, dovrai aggiungere tali indirizzi al tuo elenco consentiti, così da garantire flussi di dati ininterrotti verso le destinazioni basate su API.

**Nuove destinazioni**

| Destinazione | Descrizione |
| --- | --- |
| Destinazione [[!DNL Acxiom Real ID Audience Connection]](../../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) | Utilizza la destinazione [!DNL Acxiom Real ID Audience Connection] per migliorare i tipi di pubblico con la tecnologia [!DNL Acxiom's] [Real ID](https://www.acxiom.com/real-id/real-id/) e attivare i tipi di pubblico su più piattaforme, ad esempio [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] e altro ancora. |

**Destinazioni aggiornate**

| Destinazione | Descrizione |
| --- | --- |
| Aggiornamento interno di [[!DNL Microsoft Bing]](../../destinations/catalog/advertising/bing.md) | A partire dall’11 agosto 2025, per un breve periodo di tempo, potresti aver visto due schede **[!DNL Microsoft Bing]** una accanto all’altra nel catalogo delle destinazioni. Questo è dovuto a un aggiornamento interno del servizio destinazioni. Il connettore della destinazione **[!DNL Microsoft Bing]** esistente è stato ridenominato in **[!UICONTROL Microsoft Bing (obsoleto)]** ed è ora disponibile una nuova scheda denominata **[!UICONTROL Microsoft Bing]**. <br> Aggiornamento completato. La scheda obsoleta è stata rimossa dal catalogo di destinazione. Utilizza la connessione **[!UICONTROL Microsoft Bing]** nel catalogo per i nuovi flussi di dati di attivazione. Se sono presenti flussi di dati attivi nella destinazione **[!UICONTROL (obsoleto) Microsoft Bing]**, questi verranno aggiornati automaticamente, pertanto non è richiesta alcuna azione da parte dell&#39;utente. <br><br>Se stai creando flussi di dati tramite [API Flow Service ](https://developer.adobe.com/experience-platform-apis/references/destinations/), è necessario aggiornare l’[!DNL flow spec ID] e l’[!DNL connection spec ID] ai seguenti valori:<ul><li>Flow spec ID: `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>Connection spec ID: `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> In seguito a questo aggiornamento, potresti riscontrare un **calo nel numero di profili attivati** nei flussi di dati verso [!DNL Microsoft Bing]. Questo calo è causato dall’introduzione del **requisito di mappatura ECID** per tutte le attivazioni su questa piattaforma di destinazione. |
| Dettagli di scadenza dell&#39;autenticazione per [[!DNL LinkedIn]](../../destinations/catalog/social/linkedin.md) e [tipi di pubblico collegati](../../destinations/catalog/social/linkedin-b2b.md) corrispondenti alle destinazioni | Le informazioni sulla scadenza dell&#39;autenticazione per le destinazioni [!DNL LinkedIn] sono ora visibili direttamente nell&#39;interfaccia di Experience Platform, per consentirti di vedere quando scadrà l&#39;autenticazione e rinnovarla prima che causi interruzioni dei flussi di dati. Puoi monitorare le date di scadenza del token dalla colonna **[!UICONTROL Data di scadenza account]** nelle schede **[[!UICONTROL Account]](../../destinations/ui/destinations-workspace.md#accounts)** o **[[!UICONTROL Sfoglia]](../../destinations/ui/destinations-workspace.md#browse)**. |

**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Funzionalità avanzate di ricerca, filtro e assegnazione di tag per le destinazioni | Migliora il flusso di lavoro di gestione della destinazione con funzionalità di ricerca, filtro e assegnazione tag avanzate nelle schede [Sfoglia](../../destinations/ui/destinations-workspace.md#browse) e [Account](../../destinations/ui/destinations-workspace.md#accounts). <br> È ora possibile cercare flussi di dati e account specifici per nome, filtrare in base a vari criteri tra cui piattaforma di destinazione, stato e date e creare tag personalizzati per organizzare le destinazioni. L’ordinamento a colonne è disponibile anche per campi chiave come l’ultimo runtime del flusso di dati, facilitando l’identificazione e la gestione delle connessioni di destinazione. <br> ![Dimostrazione animata della ricerca di un flusso di dati di destinazione nella scheda Sfoglia](../../destinations/assets/ui/workspace/search.gif) |

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Schemi basati su modelli | Semplifica la modellazione dei dati con schemi basati su modelli. Ora puoi creare gli schemi più facilmente con esempi e indicazioni completi. Questa funzione è attualmente disponibile per i titolari di licenze per l’orchestrazione delle campagne e verrà estesa in disponibilità generale alla clientela Data Distiller, rendendo la modellazione dei dati più accessibile ed efficiente. |

Per ulteriori informazioni, consulta la [panoramica su XDM](../../xdm/home.md).

<!--
## Real-Time Customer Profile {#profile}

Real-Time Customer Profile provides a unified, actionable view of each customer by consolidating data from all channels into a single profile.

**New or updated features**

| Feature | Description |
| --- | --- |
| Enhanced lookup functionality in the Entities API | The Entities API now supports the following: <ul><li>Person (Profile)</li><li>Experience Events</li><li>Account</li><li>Opportunity</li></ul> This update simplifies API usage and helps ensure optimal performance and reliability. If you previously used lookups for other entity types—including join tables and custom Multi-Entity types—now is a great opportunity to review your API usage and take advantage of the improved experience. For more information, read the [Real-Time CDB B2B Edition architecture upgrade guide](../../rtcdp/b2b-architecture-upgrade.md). |

For more information on Real-Time Customer Profile, read the [Profile overview](../../profile/home.md).

-->

## Sandbox {#sandboxes}

Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono provvedere a sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Deduplica degli oggetti di dipendenza nel flusso di lavoro di importazione | Ora gli strumenti sandbox riutilizzano sempre gli oggetti esistenti se vengono rilevati oggetti con lo stesso nome, per evitarne la proliferazione. Questa modifica si applica ai seguenti oggetti: <ul><li>Schema</li><li>Gruppo di campi</li><li>Pubblico</li><li>`decisioning_ranking`</li><li>`decisioning_rules`</li></ul> Per ulteriori informazioni, consulta la [guida agli oggetti supportati per gli strumenti sandbox](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |
| Supporto intero della sandbox per la condivisione di pacchetti tra organizzazioni | Gli strumenti sandbox ora supportano il tipo **Sandbox intera** nella condivisione dei pacchetti tra organizzazioni. Ora puoi condividere sia l’intera sandbox che i pacchetti con più oggetti tra le organizzazioni. Per ulteriori informazioni, consulta la [guida agli oggetti supportati per gli strumenti sandbox](../../sandboxes/ui/sharing-packages-across-orgs.md). |

Per ulteriori informazioni sulle origini, consulta la [panoramica sulle origini](../../sandboxes/home.md).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I tipi di pubblico possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo brand.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Stime del pubblico | Le stime del pubblico ora vengono generate automaticamente nel Generatore di segmenti. Questo valore viene aggiornato ogni volta che modifichi il pubblico e riflette sempre le regole del pubblico più recenti. Inoltre, la stima verrà ora visualizzata come un **intervallo**, basato sull’intervallo di affidabilità dei dati di campionamento. |

Per ulteriori informazioni, consulta la [[!DNL Segmentation Service] panoramica](../../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Autenticazione avanzata per [!DNL Azure Blob Storage] | Ora puoi utilizzare l’autenticazione basata sull’entità principale del servizio per connettere l’origine [!DNL Azure Blob Storage] a Experience Platform. Utilizza l’autenticazione basata sull’entità principale del servizio per una maggiore sicurezza, per agevolare la rotazione delle credenziali e per un controllo degli accessi più granulare per il tuo account. Per ulteriori informazioni, consulta la [[!DNL Azure Blob Storage] panoramica](../../sources/connectors/cloud-storage/blob.md). |

Per ulteriori informazioni, consulta la [panoramica sulle origini](../../sources/home.md).

<!--
| [!DNL Marketo] source documentation updates | Get complete visibility into how your [!DNL Marketo] data is transformed when it enters Experience Platform. All field mappings now include detailed explanations of data transformations, so you can understand exactly how your `PersonID` becomes `leadID` and `eventType` becomes `activityType`. |
| [!BADGE Beta]{type=Informative} Support for [!DNL Azure Private Links] in the UI | You can now use [!DNL Azure Private Links] for a select group of sources in the UI. Use this feature to create a private endpoint that which your source can connect to. With private endpoints, you can set up connections and dataflows that bypass the public internet, giving you enhanced security and network isolation for your sensitive data. Support for [!DNL Azure Private Links] is available to the following following sources: <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li></ul> For more information, read the guide on [[!DNL Azure Private Links]](../../sources/tutorials/ui/private-link.md). |

| Enhanced [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md) destination  | The enhanced [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md) destination is an upgraded version of the existing [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md) connector. This new connector brings profile sync capabilities in addition to the existing audience sync capabilities from the legacy connector, providing a tighter integration with [!DNL Marketo Engage]. <br> The [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md) connector will be deprecated in **March 2026**. To ensure a smooth transition to the new **[[!UICONTROL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md)** destination, review the following key points and required actions: <ul><li>All users of the existing **[!UICONTROL (Legacy) (V2) Marketo Engage]** must migrate to the new **[!UICONTROL Marketo Engage]** destination by March 2026.</li><li> **Existing dataflows will not be migrated automatically.** You must [set up a new connection](../../destinations/ui/connect-destination.md) to the new **[!UICONTROL Marketo Engage]** destination and activate your audiences there.</li></ul>|
-->
