---
title: Note sulla versione di Adobe Experience Platform di agosto 2025
description: Note sulla versione di Adobe Experience Platform di agosto 2025.
exl-id: d93e98f3-d165-4710-ad1d-2ad3857cd0f8
source-git-commit: 6672ed3fd4ee4f48952dcf5ffb6561de026fe55b
workflow-type: tm+mt
source-wordcount: '1448'
ht-degree: 39%

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

**Data di rilascio: mercoledì 19 agosto 2025**


Nuove funzioni e aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Avvisi](#alerts)
- [Servizio catalogo](#catalog-service)
- [Destinazioni](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Profilo cliente in tempo reale](#profile)
- [Sandbox](#sandboxes)
- [Servizio di segmentazione](#segmentation-service)
- [Origini](#sources)

## Avvisi {#alerts}

Experience Platform consente di iscriverti agli avvisi basati su eventi per varie attività di Experience Platform. Puoi iscriverti a diverse regole di avviso tramite la scheda [!UICONTROL Avvisi] nell’interfaccia utente di Experience Platform e scegliere di ricevere messaggi di avviso nell’interfaccia stessa o tramite notifiche e-mail.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Avvisi sulla capacità di throughput in streaming | Tre nuovi avvisi consentono agli utenti di abbonarsi e configurare gli avvisi per gestire e monitorare in modo proattivo le prestazioni della capacità di velocità effettiva in streaming. I nuovi avvisi includono quando la velocità effettiva dello streaming ha raggiunto l’80%, il 90% o supera i limiti di capacità. Per ulteriori informazioni, leggere la [guida alle regole per gli avvisi sulla capacità](../../observability/alerts/rules.md#capacity). |

Per ulteriori informazioni sugli avvisi, consulta la [[!DNL Observability Insights] panoramica](../../observability/home.md).

## Servizio catalogo {#catalog-service}

Il servizio catalogo è il sistema di registrazione per la posizione e la derivazione dei dati in Adobe Experience Platform. Tutti i dati acquisiti in Experience Platform vengono memorizzati nel data lake come file e directory. Il servizio catalogo, invece, contiene i metadati e le descrizioni di tali file e directory a scopo di ricerca e monitoraggio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Conservazione dei dati per Real-Time Customer Profile | Puoi **solo** aggiornare il periodo di conservazione dei dati per Real-Time Customer Profile una volta ogni 30 giorni. |

Per ulteriori informazioni su Catalog Service, leggere la [Panoramica di Catalog Service](../../catalog/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l&#39;attivazione diretta dei dati da Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

>[!IMPORTANT]
>
>**Estensione pianificazione esportazione set di dati**
>
>Se nell&#39;organizzazione sono presenti flussi di dati di esportazione del set di dati creati prima di novembre 2024, questi flussi di dati cesseranno di funzionare il **1 settembre 2025**. Se i flussi di dati sono necessari per continuare a esportare dati dopo il 1° settembre 2025, è necessario estendere le pianificazioni per ogni destinazione in cui si esportano i set di dati, seguendo i passaggi descritti in [questa guida](../../destinations/ui/dataset-expiration-update.md).

>[!IMPORTANT]
>
>**È necessario aggiornare il inserisco nell&#39;elenco Consentiti IP per le destinazioni basate su API**
>
>A causa degli aggiornamenti al motore di esportazione delle destinazioni di streaming, le organizzazioni che utilizzano [inserisce nell&#39;elenco Consentiti di IP](../../destinations/catalog/streaming/ip-address-allow-list.md) per le destinazioni basate su API devono aggiungere i seguenti indirizzi IP ai propri inserisce nell&#39;elenco Consentiti di **prima del 15 settembre 2025**:
>
>**Indirizzi IP richiesti:**
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
>**Azione richiesta:** Se hai lavorato con Adobe per inserire nell&#39;elenco Consentiti qualsiasi indirizzo IP a destinazioni di streaming basate su API, devi aggiungere gli indirizzi IP di cui sopra al tuo inserisco nell&#39;elenco Consentiti di per garantire flussi di dati ininterrotti alle destinazioni basate su API.

**Nuove destinazioni**

| Destinazione | Descrizione |
| --- | --- |
| [[!DNL Acxiom Real ID Audience Connection]](../../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) destinazione | Utilizza la destinazione [!DNL Acxiom Real ID Audience Connection] per migliorare i tipi di pubblico con la tecnologia [!DNL Acxiom's] [Real ID](https://www.acxiom.com/real-id/real-id/) e attivare i tipi di pubblico su più piattaforme, ad esempio [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] e altro ancora. |

**Destinazioni aggiornate**

| Destinazione | Descrizione |
| --- | --- |
| Aggiornamento interno di [[!DNL Microsoft Bing]](../../destinations/catalog/advertising/bing.md) | A partire dal martedì 11 agosto 2025 nel catalogo delle destinazioni, puoi visualizzare due schede **[!DNL Microsoft Bing]** affiancate. Questo è dovuto a un aggiornamento interno del servizio destinazioni. Il connettore di destinazione **[!DNL Microsoft Bing]** esistente è stato rinominato in **[!UICONTROL (obsoleto) Microsoft Bing]** ed è ora disponibile una nuova scheda con il nome **[!UICONTROL Microsoft Bing]**. Utilizza la nuova connessione **[!UICONTROL Microsoft Bing]** nel catalogo per i nuovi flussi di dati di attivazione. Se sono presenti flussi di dati attivi nella destinazione **[!UICONTROL (obsoleto) Microsoft Bing]**, questi verranno aggiornati automaticamente, pertanto non è richiesta alcuna azione da parte dell&#39;utente. <br><br>Se stai creando flussi di dati tramite [API Flow Service ](https://developer.adobe.com/experience-platform-apis/references/destinations/), è necessario aggiornare l’[!DNL flow spec ID] e l’[!DNL connection spec ID] ai seguenti valori:<ul><li>Flow spec ID: `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>Connection spec ID: `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> In seguito a questo aggiornamento, potrebbe verificarsi un calo di **del numero di profili attivati** nei flussi di dati a [!DNL Microsoft Bing]. Questo calo è causato dall&#39;introduzione del **requisito di mappatura ECID** per tutte le attivazioni su questa piattaforma di destinazione. |


**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Funzionalità avanzate di ricerca, filtro e assegnazione di tag per le destinazioni | Migliora il flusso di lavoro di gestione della destinazione con funzionalità avanzate di ricerca, filtro e assegnazione di tag nelle schede [Sfoglia](../../destinations/ui/destinations-workspace.md#browse) e [Account](../../destinations/ui/destinations-workspace.md#accounts). <br> È ora possibile cercare flussi di dati e account specifici per nome, filtrare in base a vari criteri tra cui piattaforma di destinazione, stato e date e creare tag personalizzati per organizzare le destinazioni. L’ordinamento a colonne è disponibile anche per campi chiave come l’ultimo runtime del flusso di dati, facilitando l’identificazione e la gestione delle connessioni di destinazione. <br> ![Dimostrazione animata della ricerca di un flusso di dati di destinazione nella scheda Sfoglia](../../destinations/assets/ui/workspace/search.gif) |

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Schemi basati su modelli | Semplifica la modellazione dei dati con schemi basati su modelli. Ora puoi creare gli schemi più facilmente con esempi e indicazioni completi. Questa funzione è attualmente disponibile per i titolari di licenze di Campaign Orchestration e verrà estesa ai clienti Data Distiller in GA, rendendo la modellazione dei dati più accessibile ed efficiente. |

Per ulteriori informazioni, leggere la [panoramica XDM](../../xdm/home.md).

## Profilo cliente in tempo reale {#profile}

Real-Time Customer Profile fornisce una visualizzazione unificata e actionable di ogni cliente, consolidando i dati di tutti i canali in un unico profilo.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Funzionalità di ricerca migliorata nell’API delle entità | L’API Entità ora supporta quanto segue: <ul><li>Persona (profilo)</li><li>Eventi esperienza</li><li>Account</li><li>Opportunità</li></ul> Questo aggiornamento semplifica l’utilizzo delle API e garantisce prestazioni e affidabilità ottimali. Se in precedenza utilizzavi ricerche per altri tipi di entità, tra cui tabelle di join e tipi di più entità personalizzati, ora puoi rivedere l’utilizzo delle API e sfruttare l’esperienza migliorata. Per ulteriori informazioni, leggere la [Guida all&#39;aggiornamento dell&#39;architettura di Real-Time CDB B2B edition](../../rtcdp/b2b-architecture-upgrade.md). |

Per ulteriori informazioni su Real-Time Customer Profile, leggere la [Panoramica profilo](../../profile/home.md).

## Sandbox {#sandboxes}

Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono provvedere a sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Deduplicazione degli oggetti di dipendenza nel flusso di lavoro di importazione | Ora gli strumenti sandbox riutilizzano sempre gli oggetti esistenti se vengono rilevati oggetti con lo stesso nome, per evitare la proliferazione degli oggetti. Questa modifica si applica ai seguenti oggetti: <ul><li>Schema</li><li>Gruppo di campi</li><li>Pubblico</li><li>`decisioning_ranking`</li><li>`decisioning_rules`</li></ul> Per ulteriori informazioni, consulta la [guida agli oggetti supportati per gli strumenti sandbox](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |
| Supporto completo della sandbox per la condivisione di pacchetti tra organizzazioni | Gli strumenti sandbox ora supportano il tipo **Intero sandbox** nella condivisione dei pacchetti tra organizzazioni. Ora puoi condividere tra le organizzazioni sia l’intero pacchetto sandbox che quello con più oggetti. Per ulteriori informazioni, consulta la [guida agli oggetti supportati per gli strumenti sandbox](../../sandboxes/ui/sharing-packages-across-orgs.md). |

Per ulteriori informazioni sulle origini, consulta la [panoramica sulle origini](../../sandboxes/home.md).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I tipi di pubblico possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo brand.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Stime del pubblico | Le stime del pubblico ora vengono generate automaticamente in Segment Builder (Generatore di segmenti). Questo valore viene aggiornato ogni volta che modifichi il pubblico e riflette sempre le regole del pubblico più recenti. Inoltre, la stima verrà ora visualizzata come un **intervallo**, basato sull&#39;intervallo di affidabilità dei dati di campionamento. |

Per ulteriori informazioni, consulta la [[!DNL Segmentation Service] panoramica](../../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto di [!BADGE Beta]{type=Informative} per [!DNL Azure Private Links] nell&#39;interfaccia utente | È ora possibile utilizzare [!DNL Azure Private Links] per un gruppo selezionato di origini nell&#39;interfaccia utente. Utilizza questa funzione per creare un endpoint privato a cui l’origine può connettersi. Con gli endpoint privati, puoi impostare connessioni e flussi di dati che bypassano l’Internet pubblico, garantendo maggiore sicurezza e isolamento della rete per i dati sensibili. Il supporto per [!DNL Azure Private Links] è disponibile per le seguenti origini: <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li></ul> Per ulteriori informazioni, leggere la guida in [[!DNL Azure Private Links]](../../sources/tutorials/ui/private-link.md). |
| Autenticazione avanzata per [!DNL Azure Blob Storage] | È ora possibile utilizzare l&#39;autenticazione basata sull&#39;entità servizio per connettere l&#39;origine [!DNL Azure Blob Storage] ad Experience Platform. Utilizza l’autenticazione basata sull’entità servizio per una maggiore sicurezza, una rotazione delle credenziali più semplice e un controllo di accesso più granulare per il tuo account. Per ulteriori informazioni, consulta la [[!DNL Azure Blob Storage] panoramica](../../sources/connectors/cloud-storage/blob.md). |

Per ulteriori informazioni, consulta la [panoramica sulle origini](../../sources/home.md).

<!--
| [!DNL Marketo] source documentation updates | Get complete visibility into how your [!DNL Marketo] data is transformed when it enters Experience Platform. All field mappings now include detailed explanations of data transformations, so you can understand exactly how your `PersonID` becomes `leadID` and `eventType` becomes `activityType`. |
-->
