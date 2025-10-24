---
title: Note sulla versione di Adobe Experience Platform di ottobre 2025
description: Note sulla versione di Adobe Experience Platform di ottobre 2025.
source-git-commit: 0191fc8419c696d8cd114a5eb575b8cc0a815a72
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 26%

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

**Data di rilascio: giovedì 22 ottobre 2025**

Nuove funzioni e aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Avvisi](#alerts)
- [Destinazioni](#destinations)
- [Real-Time CDP B2B Edition](#b2b)
- [Origini](#sources)

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator di Adobe Experience Platform è il nuovo livello di agente in Adobe Experience Platform.

**Funzioni aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Agente Audience | Audience Agent ora supporta i tipi di pubblico basati sull’account per l’esplorazione del pubblico conversazionale e il rilevamento di tipi di pubblico duplicati. Per ulteriori informazioni, consulta la [documentazione su Agente Audience](https://experienceleague.adobe.com/it/docs/experience-cloud-ai/experience-cloud-ai/agents/audience). |

Per ulteriori informazioni sugli agenti, leggere la [documentazione di Agent Orchestrator](https://experienceleague.adobe.com/it/docs/experience-cloud-ai/experience-cloud-ai/home).

## Avvisi {#alerts}

Experience Platform consente di iscriverti agli avvisi basati su eventi per varie attività di Experience Platform. È possibile abbonarsi a diverse regole di avviso tramite la scheda [!UICONTROL Alerts] nell&#39;interfaccia utente di Experience Platform e scegliere di ricevere messaggi di avviso all&#39;interno dell&#39;interfaccia utente stessa o tramite notifiche e-mail.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Avviso di tasso di errore di attivazione | È stato aggiunto un nuovo avviso per le destinazioni: **La frequenza degli errori di attivazione supera la soglia**. Questo avviso notifica quando il numero di record non riusciti durante l&#39;attivazione dei dati supera la soglia consentita, consentendo di rispondere rapidamente ai problemi di attivazione. Per ulteriori informazioni, consulta la documentazione sulle [regole di avvisi standard](../../observability/alerts/rules.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sugli avvisi, consulta la [[!DNL Observability Insights] panoramica](../../observability/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate**

| Destinazione | Descrizione |
| --- | --- |
| [!DNL Adform] | Utilizzare questa destinazione per inviare i tipi di pubblico di Adobe Real-Time CDP a [!DNL Adform] per l&#39;attivazione in base all&#39;Experience Cloud ID (ECID) e all&#39;ID Fusion di [!DNL Adform]. ID Fusion di [!DNL Adform] è un servizio di risoluzione ID che consente di attivare i tipi di pubblico di prime parti in base all&#39;Experience Cloud ID (ECID). Leggi la [[!DNL Adform] documentazione](../../destinations/catalog/advertising/adform.md) per ulteriori informazioni |
| [!DNL Amazon Ads] | È stato aggiunto un ulteriore supporto per gli identificatori personali. Sono inclusi campi come `firstName`, `lastName`, `street`, `city`, `state`, `zip` e `country`. La mappatura di questi campi come identità di destinazione può migliorare le percentuali di corrispondenza del pubblico. Per ulteriori informazioni, consulta la [[!DNL Amazon Ads] documentazione](../../destinations/catalog/advertising/amazon-ads.md). |
| [!DNL Snowflake Batch] (disponibilità limitata) | Crea una condivisione dati live di [!DNL Snowflake] per ricevere aggiornamenti giornalieri sul pubblico direttamente come tabelle condivise nel tuo account. Questa integrazione è attualmente disponibile per le organizzazioni dei clienti con provisioning nell&#39;area VA7. Per ulteriori informazioni, consulta la [[!DNL Snowflake Batch] documentazione](../../destinations/catalog/warehouses/snowflake-batch.md). |
| [!DNL Snowflake Streaming] (disponibilità limitata) | Crea una condivisione dati live di [!DNL Snowflake] per ricevere aggiornamenti del pubblico in streaming direttamente come tabelle condivise nel tuo account. Questa integrazione è attualmente disponibile per le organizzazioni dei clienti con provisioning nell&#39;area VA7. Per ulteriori informazioni, consulta la [[!DNL Snowflake Streaming] documentazione](../../destinations/catalog/warehouses/snowflake.md). |

{style="table-layout:auto"}

**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| [Diverse nuove destinazioni supportano il monitoraggio a livello di pubblico](../../dataflows/ui/monitor-destinations.md#audience-level-view) | Le seguenti destinazioni supportano ora il monitoraggio a livello di pubblico: <ul><li>[!DNL Airship Tags]</li><li>(API) [!DNL Salesforce Marketing Cloud]</li><li>[!DNL Marketo Engage]</li><li>[!DNL Microsoft Bing]</li><li>(V1) [!DNL Pega CDH Realtime Audience]</li><li>(V2) [!DNL Pega CDH Realtime Audience]</li><li>Coinvolgimento dell&#39;account [!DNL Salesforce Marketing Cloud]</li><li>[!DNL The Trade Desk]</li></ul> |
| Correzione dei guardrail di esportazione del set di dati | È stata implementata una correzione ai guardrail di esportazione del set di dati. In precedenza, alcuni set di dati che includevano una colonna timestamp ma erano _non_ in base allo schema XDM Experience Events venivano trattati erroneamente come set di dati Experience Events, limitando le esportazioni a un intervallo di lookback di 365 giorni. Il guardrail di lookback documentato di 365 giorni ora si applica esclusivamente ai set di dati Experience Events. I set di dati che utilizzano uno schema diverso da XDM Experience Events sono ora governati dal guardrail di 10 miliardi di record. Alcuni clienti potrebbero notare un aumento delle esportazioni di set di dati che erroneamente rientravano nell’intervallo di lookback di 365 giorni. Questo consente di esportare set di dati per flussi di lavoro predittivi con un intervallo di lookback lungo. Per ulteriori informazioni, leggere le [protezioni di esportazione del set di dati](../../destinations/guardrails.md#dataset-exports). |
| Generazione di rapporti migliorati a livello di pubblico per le destinazioni enterprise | Dopo questa versione, i clienti vedranno numeri di reporting del pubblico più precisi che includono solo i tipi di pubblico rilevanti per la destinazione selezionata. Questo aggiustamento di monitoraggio assicura che i rapporti includano solo i tipi di pubblico mappati sul flusso di dati, fornendo informazioni più chiare sull’effettiva attivazione dei dati. Questo non influisce sulla quantità di dati attivati, ma si tratta semplicemente di un miglioramento del monitoraggio per migliorare l’accuratezza della generazione di rapporti. |
| Flussi di dati disattivati dall’interfaccia utente a causa di etichette di accesso | Per risolvere il problema relativo alla visualizzazione di pagine vuote da parte di alcuni utenti a causa del fatto che i flussi di dati di destinazione a cui non avevano accesso erano completamente nascosti, l’interfaccia utente ora visualizza tali flussi di dati con restrizioni in uno stato di disattivazione anziché ometterli completamente. Per ulteriori dettagli, leggere la documentazione su [utilizzo delle etichette di accesso per gestire l&#39;accesso degli utenti ai flussi di dati di destinazione](../../access-control/abac/apply-access-labels-destinations.md#important-callouts-and-items-to-know). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Real-Time CDP B2B Edition {#b2b}

Real-Time CDP B2B Edition fornisce funzionalità complete di gestione dei dati della clientela B2B, consentendo alle organizzazioni di creare profili cliente unificati, creare tipi di pubblico B2B sofisticati e attivare i dati su vari canali di marketing.

**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto B2B obsoleto per relazioni non standard tra entità B2B | A partire da gennaio 2026, Real-Time CDP B2B edition non supporterà più **relazioni non standard** tra entità B2B. Si consiglia pertanto di aggiornare le entità B2B in modo da utilizzare le relazioni standard descritte nella [guida degli spazi dei nomi e degli schemi B2B](../../rtcdp/schemas/b2b.md). |

{style="table-layout:auto"}

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Modifica nella creazione del set di dati per l’origine Adobe Analytics | Come parte del processo di creazione del flusso di dati tra Adobe Analytics e Experience Platform, viene creato un set di dati tramite Catalog Service. Questo set di dati funge da contenitore per i dati da recapitare. Attualmente, questo processo coinvolge un ID DataSource che viene estratto dalla suite di rapporti di Analytics, inviato a Catalog Service e quindi associato al set di dati appena creato. Dopo la modifica, l’opzione per fornire l’ID DataSource non sarà più disponibile durante la creazione del set di dati. Pertanto, ai nuovi set di dati creati dall’origine Analytics non verrà più associato un ID DataSource in Catalog Service. Questa modifica si applica solo ai metadati e non modifica in alcun modo l’archiviazione dei dati nel set di dati. Tuttavia, è importante sapere che l’ID DataSource fornito da Catalog Service non sarà più disponibile nei nuovi set di dati creati per Adobe Analytics. Per ulteriori informazioni sul connettore di origine di Adobe Analytics, consulta la [documentazione di origine di Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Disponibilità generale dell&#39;origine [!DNL Google Ads] (solo API) | La versione [API dell&#39;origine  [!DNL Google Ads]](../../sources/tutorials/api/create/advertising/ads.md) è ora in Disponibilità generale. La documentazione API è stata aggiornata per indicare che la versione più recente è ora `v21` e che Experience Platform supporta tutte le versioni v19 e successive. [La versione dell&#39;interfaccia utente](../../sources/tutorials/ui/create/advertising/ads.md) rimane in versione beta e supporta solo l&#39;acquisizione una tantum. Per utilizzare l’acquisizione dati incrementale, utilizza la route API. |
| Supporto per la rete virtuale [!DNL Azure Event Hubs] | Adobe ora supporta esplicitamente le connessioni di rete virtuale a [[!DNL Azure Event Hubs]](../../sources/connectors/cloud-storage/eventhub.md), consentendo il trasferimento di dati su reti private anziché pubbliche. I clienti possono inserire nell&#39;elenco Consentiti Experience Platform VNet per instradare il traffico dei hub eventi in modo privato tramite la dorsale privata di Azure, fornendo sicurezza e conformità migliorate per i flussi di lavoro di acquisizione dei dati. |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle origini](../../sources/home.md).

<!--
| Source | Description |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Talon.one] sources for loyalty data | Use the [[!DNL Talon.One] sources](../../sources/connectors/loyalty/talon-one.md) to ingest batch and streaming loyalty data into Experience Platform. The connector supports streaming of profile data, transaction data, and loyalty data including points earned, points redeemed, points expired, and tier data. For more information, read the [!DNL Talon.One] [batch](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) and [streaming](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md) documentation. |
-->