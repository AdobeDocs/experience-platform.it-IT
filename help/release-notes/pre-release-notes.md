---
title: Note pre-release di Experience Platform
description: Un’anteprima delle ultime note sulla versione di Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 9cf809f8fd6e424b4dcd800c3d554e4eb0e337dc
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 33%

---

# Note preliminari su Adobe Experience Platform

>[!IMPORTANT]
>
>Questo documento è destinato ad essere **anteprima** delle note sulla versione per il mese corrente. Gli elementi da rilasciare sono soggetti a modifiche e possono essere aggiunti o rimossi nella versione finale.

>[!TIP]
>
>Per le note sulla versione di altre applicazioni Adobe Experience Platform, consulta la seguente documentazione:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/it/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/it/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composizione di pubblico federato](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/it/docs/real-time-cdp-collaboration/using/latest)

**Data di rilascio: ottobre 2025**

Nuove funzioni e aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Avvisi](#alerts)
- [Destinazioni](#destinations)
- [Servizio di segmentazione](#segmentation-service)
- [Origini](#sources)

## Avvisi {#alerts}

Experience Platform consente di iscriverti agli avvisi basati su eventi per varie attività di Experience Platform. Puoi iscriverti a diverse regole di avviso tramite la scheda [!UICONTROL Avvisi] nell’interfaccia utente di Experience Platform e scegliere di ricevere messaggi di avviso nell’interfaccia stessa o tramite notifiche e-mail.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Avviso sulla percentuale di errori della destinazione | È stato aggiunto un nuovo avviso per le destinazioni: **La frequenza degli errori di destinazione supera la soglia**. Questo avviso notifica quando il numero di record non riusciti durante l&#39;attivazione dei dati supera la soglia consentita, consentendo di rispondere rapidamente ai problemi di attivazione. |

{style="table-layout:auto"}

Per ulteriori informazioni sugli avvisi, consulta la [[!DNL Observability Insights] panoramica](../observability/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate**

| Destinazione | Descrizione |
| --- | --- |
| [!DNL AdForm] | Utilizzare questa destinazione per inviare i tipi di pubblico di Adobe Real-Time CDP a [!DNL AdForm] per l&#39;attivazione in base all&#39;Experience Cloud ID (ECID) e all&#39;ID Fusion di [!DNL AdForm]. ID Fusion di [!DNL AdForm] è un servizio di risoluzione ID che consente di attivare i tipi di pubblico di prime parti in base all&#39;Experience Cloud ID (ECID). |
| `Amazon Ads` | Sono stati aggiunti identificatori personali aggiuntivi di supporto, ad esempio `firstName`, `lastName`, `street`, `city`, `state`, `zip` e `country`. La mappatura di questi campi come identità di destinazione può migliorare le percentuali di corrispondenza del pubblico. |

**Funzionalità nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per la crittografia lato server di [!DNL AES256] in [!DNL Amazon S3] destinazioni | [!DNL Amazon S3] destinazioni ora supportano [!DNL AES256] crittografia lato server, fornendo maggiore sicurezza per i dati esportati. È possibile configurare questo metodo di crittografia durante la configurazione o l&#39;aggiornamento delle connessioni di destinazione [!DNL Amazon S3], assicurandosi che i dati vengano crittografati inattivi utilizzando gli algoritmi di crittografia [!DNL AES256] standard del settore. Per ulteriori informazioni, consulta la [[!DNL Amazon] documentazione](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingEncryption.html). |
| [Diverse nuove destinazioni supportano il monitoraggio a livello di pubblico](../dataflows/ui/monitor-destinations.md#audience-level-view) | Le seguenti destinazioni supportano ora il monitoraggio a livello di pubblico: <ul><li>[!DNL Airship Tags]</li><li>(API) [!DNL Salesforce Marketing Cloud]</li><li>[!DNL Marketo Engage]</li><li>[!DNL Microsoft Bing]</li><li>(V1) [!DNL Pega CDH Realtime Audience]</li><li>(V2) [!DNL Pega CDH Realtime Audience]</li><li>Coinvolgimento dell&#39;account [!DNL Salesforce Marketing Cloud]</li><li>[!DNL The Trade Desk]</li></ul> |
| Correzione dei guardrail di esportazione del set di dati | È stata implementata una correzione ai guardrail di esportazione del set di dati. In precedenza, alcuni set di dati che includevano una colonna timestamp ma erano _non_ in base allo schema XDM Experience Events venivano trattati erroneamente come set di dati Experience Events, limitando le esportazioni a un intervallo di lookback di 365 giorni. Il guardrail di lookback documentato di 365 giorni ora si applica esclusivamente ai set di dati Experience Events. I set di dati che utilizzano uno schema diverso da XDM Experience Events sono ora governati dal guardrail di 10 miliardi di record. Alcuni clienti potrebbero notare un aumento delle esportazioni di set di dati che erroneamente rientravano nell’intervallo di lookback di 365 giorni. Questo consente di esportare set di dati per flussi di lavoro predittivi con un intervallo di lookback lungo. Per ulteriori informazioni, leggere le [protezioni di esportazione del set di dati](../destinations/guardrails.md#dataset-exports). |
| Generazione di rapporti migliorati a livello di pubblico per le destinazioni enterprise | È stata migliorata la logica di reporting a livello di pubblico per le destinazioni enterprise. Dopo questa versione, i clienti vedranno numeri di reporting del pubblico più precisi che includono solo i tipi di pubblico rilevanti per la destinazione selezionata. Questo aggiustamento di monitoraggio assicura che i rapporti includano solo i tipi di pubblico mappati sul flusso di dati, fornendo informazioni più chiare sull’effettiva attivazione dei dati. Questo non influisce sulla quantità di dati attivati, ma si tratta semplicemente di un miglioramento del monitoraggio per migliorare l’accuratezza della generazione di rapporti. |

Per ulteriori informazioni, consulta la [panoramica sulle destinazioni](../destinations/home.md).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I tipi di pubblico possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo brand.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Monitoraggio della segmentazione in streaming | Il monitoraggio in tempo reale per la segmentazione in streaming fornisce trasparenza in termini di tasso di valutazione, latenza e metriche di qualità dei dati a livello di sandbox, set di dati e pubblico. In questo modo è possibile inviare avvisi proattivi e ottenere informazioni utili per aiutare i data engineer a identificare le violazioni della capacità e i problemi di acquisizione. Le metriche di monitoraggio includono il tasso di valutazione, la latenza di acquisizione P95, nonché i record ricevuti, valutati, non riusciti e saltati. Le funzionalità View-by-DataSet e View-by-Audience forniscono una visibilità completa sui nuovi profili qualificati e non qualificati. |

Per ulteriori informazioni, consulta la [[!DNL Segmentation Service] panoramica](../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Origini nuove o aggiornate**

| Origine | Descrizione |
| --- | --- |
| [!BADGE Origini di Beta]{type=Informative} [!DNL Talon.one] per i dati fedeltà | Utilizza le origini [!DNL Talon.One] per acquisire i dati batch e di fedeltà in streaming in Experience Platform. Il connettore supporta lo streaming di dati di profilo, dati sulle transazioni e dati sulla fedeltà, tra cui punti guadagnati, punti riscattati, punti scaduti e dati a livello. |

**Origini aggiornate**

| Origine | Descrizione |
| --- | --- |
| Disponibilità generale dell&#39;origine [!DNL Google Ads] (solo API) | La versione API dell&#39;origine [!DNL Google Ads] è ora in Disponibilità generale. La documentazione API è stata aggiornata per indicare che la versione più recente è ora `v21` e che Experience Platform supporta tutte le versioni v19 e successive. La versione dell’interfaccia utente rimane in versione beta e supporta l’acquisizione una tantum. Per utilizzare l’acquisizione dati incrementale, utilizza la route API. |
| Supporto per la rete virtuale [!DNL Azure Event Hubs] | Adobe ora supporta esplicitamente le connessioni di rete virtuale agli hub eventi di Azure, consentendo il trasferimento dei dati su reti private anziché pubbliche. I clienti possono inserire nell&#39;elenco Consentiti Experience Platform VNet per instradare il traffico dei hub eventi in modo privato tramite la dorsale privata di Azure, fornendo sicurezza e conformità migliorate per i flussi di lavoro di acquisizione dei dati. |

Per ulteriori informazioni, consulta la [panoramica sulle origini](../sources/home.md).
