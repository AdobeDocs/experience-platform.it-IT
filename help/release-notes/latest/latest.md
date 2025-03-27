---
title: Note sulla versione di Adobe Experience Platform - Marzo 2025
description: Note sulla versione di Adobe Experience Platform di marzo 2025.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 16056a35624b4a053e9f50acef0ec3f63254a065
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 26%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 26 marzo 2025**

Aggiornamenti alle funzioni e alla documentazione esistenti in Adobe Experience Platform:

- [Note sulla versione di Adobe Experience Platform](#adobe-experience-platform-release-notes)

   - [Dashboard](#dashboards)
   - [Destinazioni](#destinations)
   - [Servizio di segmentazione](#segmentation-service)
   - [Origini](#sources)

## Dashboard {#dashboards}

Experience Platform fornisce più dashboard attraverso le quali è possibile visualizzare approfondimenti importanti sui dati della tua organizzazione, acquisiti durante le istantanee giornaliere.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Dashboard di utilizzo delle licenze basato su metriche | Il dashboard utilizzo licenze ora include un&#39;interfaccia utente semplificata con due schede: **Metriche** e **Prodotti**. La nuova scheda **Metriche** offre una visualizzazione consolidata di tutte le metriche delle licenze tracciabili nei prodotti acquistati. Ogni metrica include un’icona di informazioni in linea con le descrizioni e i prodotti associati. Gli utenti possono selezionare le sandbox di produzione o di sviluppo, visualizzare le tendenze storiche di utilizzo nei grafici interattivi ed esportare i dati specifici delle sandbox come file CSV. Questi aggiornamenti semplificano il tracciamento delle licenze e forniscono informazioni più chiare. Per ulteriori informazioni, consulta la [guida del dashboard utilizzo licenze](../../dashboards/guides/license-usage.md). |
| Frequenza di previsione aggiornata | Il dashboard utilizzo licenze fornisce ora informazioni più precise sui consumi previsti aggiornando le previsioni di utilizzo **settimanali** anziché mensili. Queste previsioni mostrano un utilizzo stimato nelle prossime sei settimane sulla base delle tendenze recenti. Questa modifica consente un processo decisionale più rapido, un intervento più rapido e una migliore pianificazione delle licenze. Per informazioni dettagliate, consulta la [guida del dashboard utilizzo licenze](../../dashboards/guides/license-usage.md#predicted-usage). |
| Descrizioni delle metriche aggiornate nell’interfaccia utente | Le definizioni delle metriche nel dashboard utilizzo licenze sono state riviste per maggiore chiarezza e coerenza. Ora puoi visualizzare le descrizioni aggiornate direttamente nel dashboard utilizzando le icone delle informazioni in linea accanto a ogni metrica nella scheda **Metriche**. Questi aggiornamenti consentono di comprendere più facilmente come vengono tracciate le metriche e a quali prodotti si applicano. Per ulteriori dettagli, consulta la [guida del dashboard utilizzo licenze](../../dashboards/guides/license-usage.md#available-metrics). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle dashboard, tra cui come concedere le autorizzazioni di accesso e creare widget personalizzati, consulta la [panoramica sulle dashboard](../../dashboards/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate** {#new-updated-destinations}

| Destinazione | Descrizione |
| --- | --- |
| [Connessione Demandbase People](/help/destinations/catalog/advertising/demandbase-people.md) | Utilizza la [!DNL Demandbase People] connessione per attivare i profili per le campagne Demandbase per la targeting, la personalizzazione e la soppressione del pubblico. |
| [Connessione account Bombora](/help/destinations/catalog/advertising/bombora.md) | Utilizza la  [!DNL Bombora] connessione per attivare i profili per le tue campagne Bombora per la targeting, la personalizzazione e la soppressione del pubblico, in base al [pubblico account](/help/segmentation/types/account-audiences.md). |
| Aggiornamento di [Attributi dirigibili](/help/destinations/catalog/mobile-engagement/airship-attributes.md) | A partire dal 25 marzo 2025, puoi visualizzare due schede **[!UICONTROL Attributi dirigibili]** affiancate nel catalogo delle destinazioni. Ciò è dovuto a un aggiornamento interno al servizio destinazioni. Il connettore di destinazione **[!UICONTROL Attributi dirigibile]** esistente è stato rinominato in **[!UICONTROL (obsoleto) Attributi dirigibile]** ed è ora disponibile una nuova scheda denominata **[!UICONTROL Attributi dirigibile]**. <br> Utilizza la connessione **[!UICONTROL Attributi dirigibili]** nel catalogo per i nuovi flussi di dati di attivazione. Se sono presenti flussi di dati attivi nella destinazione [!DNL (Deprecated) Airship Attributes], questi verranno aggiornati automaticamente, pertanto non è richiesta alcuna azione da parte dell&#39;utente. <br> Se si creano flussi di dati tramite l&#39;[API del servizio Flusso](https://developer.adobe.com/experience-platform-apis/references/destinations/), è necessario aggiornare [!DNL flow spec ID] e [!DNL connection spec ID] ai seguenti valori: <ul><li> Flusso ID specifica: `a862e0be-966e-4e5a-80d3-1bb566461986`</li><li> ID specifica di connessione: `594bc002-4a47-49b7-8a98-ac0d21045502`</li> </ul> |

{style="table-layout:auto"}

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzione | Descrizione |
| --- | --- |
| [Miglioramenti della precisione del reporting per le destinazioni di streaming](../../dataflows/ui/monitor-destinations.md) | A partire da marzo 2025, Adobe sta implementando un aggiornamento per aumentare la precisione dei rapporti per le destinazioni di streaming. Questo miglioramento garantisce un migliore allineamento tra la reportistica nelle piattaforme Experience Platform e in quella di destinazione. <br> Prima di questo aggiornamento, **[!UICONTROL Identità non riuscite]** includeva tutti i tentativi di attivazione. Dopo questo aggiornamento, nel conteggio totale viene incluso solo l’ultimo tentativo di attivazione. <br> Questo miglioramento si applica a tutte le destinazioni di streaming. <br> A seguito di questo miglioramento, gli utenti delle destinazioni di streaming potrebbero vedere un calo previsto nel conteggio delle identità **[!UICONTROL non riuscite]** . |
| [Supporto per l&#39;esportazione di campi di tipo mappa per destinazioni aziendali ed edge](/help/destinations/ui/export-arrays-maps-objects.md) | Quando si esportano dati nell&#39;Kinesis Amazon](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), nell&#39;API](/help/destinations/catalog/streaming/http-destination.md) HTTP, [in Hub eventi di](/help/destinations/catalog/cloud-storage/azure-event-hubs.md) Azure e [nelle destinazioni Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md), è ora possibile selezionare campi di tipo mappa per l&#39;esportazione [nel passaggio di mapping del workflow di attivazione[.<br> ![Esporta il campo di tipo mappa nella destinazione dell&#39;organizzazione.](../2025/assets/march/export-map.png "Esporta campo di tipo mappa nella destinazione dell&#39;organizzazione."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Per ulteriori informazioni, leggi la [panoramica sulle destinazioni](../../destinations/home.md).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I segmenti possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo marchio.

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti di Account Audience Builder | In Audience Builder, ora puoi filtrare gli attributi per visualizzare solo gli attributi compilati e i dati di riepilogo per questi attributi compilati. Ulteriori informazioni su questi miglioramenti sono disponibili nella documentazione di [Audience Builder](../../rtcdp/segmentation/audience-builder.md). |
| Disponibilità generale della valutazione flessibile del pubblico | La valutazione flessibile del pubblico è ora generalmente disponibile. Puoi utilizzare la valutazione flessibile del pubblico per creare nuovi tipi di pubblico su richiesta per comunicazioni sensibili al tempo. Ulteriori informazioni sulla valutazione flessibile del pubblico sono disponibili nella [panoramica sulla valutazione flessibile del pubblico](../../segmentation/methods/flexible-audience-evaluation.md). |

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

Utilizza le origini in Experience Platform per acquisire dati da un’applicazione Adobe o da un’origine dati di terze parti.

**Nuove origini**

| Funzione | Descrizione |
| --- | --- |
| [!DNL Bombora Intent] | L&#39;origine [!DNL Bombora Intent] è ora disponibile nel catalogo sorgenti. Utilizza questa fonte per: <ul><li>Integra i dati Company Surge Intent di Bombora per identificare gli account che ricercano attivamente i tuoi prodotti o servizi.</li><li>Dai la priorità agli account sul mercato per creare segmenti precisi ed eseguire campagne ABM iper-mirate, affinché le tue attività di marketing si concentrino sugli account che hanno più probabilità di conversione.</li><li>Sfruttare strategie basate su intent per ottimizzare la spesa pubblicitaria, aumentare il coinvolgimento e massimizzare il ROI.</li></ul> Per ulteriori informazioni, consulta la guida su [connessione dell&#39;account  [!DNL Bombora]  ad Experience Platform](../../sources/tutorials/ui/create/data-partners/bombora.md). |
| [!DNL Demandbase Intent] | La [!DNL Demandbase Intent] sorgente ̧ è ora disponibile nel catalogo sorgenti. Utilizza questa origine per: <ul><li>Integra i dati sulle intenzioni dell&#39;account di Demandbase per identificare gli account ad alta interesse in base alle interazioni in tempo reale.</li><li>Dando priorità ai segnali di intento più forti, puoi creare segmenti precisi e distribuire campagne iper-mirate per garantire che le attività di marketing si concentrino sugli account che hanno più probabilità di conversione.</li><li>Attiva strategie basate sulle intenzioni per consentire l’ottimizzazione della spesa pubblicitaria, un maggiore coinvolgimento e un ROI più elevato.</li></ul> Per ulteriori informazioni, consulta la guida su [connessione dell&#39;account  [!DNL Demandbase]  ad Experience Platform](../../sources/tutorials/ui/create/data-partners/demandbase.md). |

{style="table-layout:auto"}

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Miglioramenti all&#39;origine [!DNL Google Ads] | È ora possibile utilizzare [[!DNL Google Ads] source](../../sources/connectors/advertising/ads.md) per acquisire i dati aggregati. È possibile utilizzare [!DNL Google Ads Query Builder] per specificare gli attributi, i segmenti e le risorse da acquisire in Experience Platform. Per ulteriori informazioni, consulta la guida su [connessione dell&#39;account  [!DNL Google Ads]  ad Experience Platform](../../sources/tutorials/ui/create/advertising/ads.md). |
| Miglioramenti all&#39;origine [!DNL Microsoft Dynamics] | È ora possibile specificare la chiave primaria di una determinata tabella [!DNL Microsoft Dynamics] durante l&#39;esplorazione del contenuto e della struttura dei dati. Utilizza questa funzione per ottimizzare le tue query con l&#39;origine [!DNL Microsoft Dynamics] . Per ulteriori informazioni, leggi la guida su come [connettere l&#39;origine [!DNL Microsoft Dynamics] a Experience Platform utilizzando l&#39;API](../../sources/tutorials/api/create/crm/ms-dynamics.md). |
| Supporto per l&#39;autenticazione tramite chiave API nelle origini self-service (Batch SDK) | È ora possibile utilizzare l&#39;autenticazione tramite chiave API come tipo di autenticazione quando si integra una nuova origine con le origini self-service (Batch SDK). Per ulteriori informazioni, leggi la guida alla [configurazione delle specifiche di autenticazione in Batch SDK](../../sources/sources-sdk/config/authspec.md). |
| Supporto per il controllo accesso basato su attributi nelle origini | È ora possibile utilizzare funzioni di controllo accesso basate su attributi nei flussi di dati delle fonti. Per ulteriori informazioni, consulta le seguenti guide: <ul><li>[Applica etichette ai flussi di dati di origine utilizzando l&#39;API](../../sources/tutorials/api/labels.md)</li><li>[Applica etichette ai flussi di dati di origine tramite l&#39;interfaccia utente](../../sources/tutorials/ui/labels.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle origini](../../sources/home.md).
