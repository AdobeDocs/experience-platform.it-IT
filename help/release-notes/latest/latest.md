---
title: Note sulla versione di Adobe Experience Platform - Marzo 2025
description: Note sulla versione di Adobe Experience Platform di marzo 2025.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: f0879683629ba10ed1b799e52f0adf332f079daf
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 97%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 26 marzo 2025**

Aggiornamenti alle funzioni e alla documentazione esistenti di Adobe Experience Platform:

- [Note sulla versione di Adobe Experience Platform](#adobe-experience-platform-release-notes)

   - [Dashboard](#dashboards)
   - [Destinazioni](#destinations)
   - [Composizione di pubblico federato](#federated-audience-composition)
   - [Servizio di segmentazione](#segmentation-service)
   - [Origini](#sources)

## Dashboard {#dashboards}

Experience Platform fornisce più dashboard attraverso le quali è possibile visualizzare approfondimenti importanti sui dati della tua organizzazione, acquisiti durante le istantanee giornaliere.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Dashboard di utilizzo delle licenze basata su metriche | La dashboard di utilizzo delle licenze ora include un’interfaccia utente semplificata con due schede: **Metriche** e **Prodotti**. La nuova scheda **Metriche** offre una visualizzazione consolidata di tutte le metriche tracciabili delle licenze dei prodotti acquistati. Ogni metrica include un’icona di informazioni in linea con le descrizioni e i prodotti associati. L’utente può selezionare le sandbox di produzione o di sviluppo, visualizzare le tendenze storiche di utilizzo nei grafici interattivi ed esportare i dati specifici delle sandbox come file CSV. Questi aggiornamenti semplificano il tracciamento delle licenze e forniscono informazioni più chiare. Per ulteriori informazioni, consulta la [guida della dashboard di utilizzo delle licenze](../../dashboards/guides/license-usage.md). |
| Frequenza di previsione aggiornata | La dashboard di utilizzo delle licenze fornisce ora insight più precisi sui consumi previsti aggiornando le previsioni di utilizzo su base **settimanale** anziché mensile. Le previsioni mostrano una stima dell’utilizzo per le successive sei settimane in base alle tendenze recenti. Questa modifica consente un processo decisionale più veloce, interventi più rapidi e una migliore pianificazione delle licenze. Per ulteriori informazioni, consulta la [guida della dashboard di utilizzo delle licenze](../../dashboards/guides/license-usage.md#predicted-usage). |
| Descrizioni delle metriche aggiornate nell’interfaccia utente | Le definizioni delle metriche nella dashboard di utilizzo delle licenze sono state riviste per maggiore chiarezza e coerenza. Ora puoi visualizzare le descrizioni aggiornate direttamente nella dashboard mediante le icone delle informazioni in linea che si trovano accanto a ogni metrica nella scheda **Metriche**. Questi aggiornamenti consentono di comprendere più facilmente come vengono tracciate le metriche e a quali prodotti si applicano. Per ulteriori informazioni, consulta la [guida della dashboard di utilizzo delle licenze](../../dashboards/guides/license-usage.md#available-metrics). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle dashboard, tra cui come concedere le autorizzazioni di accesso e creare widget personalizzati, consulta la [panoramica sulle dashboard](../../dashboards/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Destinazioni nuove o aggiornate** {#new-updated-destinations}

| Destinazione | Descrizione |
| --- | --- |
| [Connessione Demandbase People](/help/destinations/catalog/advertising/demandbase-people.md) | Utilizza la connessione [!DNL Demandbase People] per attivare profili per le campagne Demandbase per il targeting del pubblico, la personalizzazione e la soppressione. |
| [Connessione account Bombora](/help/destinations/catalog/advertising/bombora.md) | Utilizza la connessione [!DNL Bombora] per attivare profili per le campagne Bombora per il targeting del pubblico, la personalizzazione e la soppressione, in base ai [tipi di pubblico basati su account](/help/segmentation/types/account-audiences.md). |
| Aggiornamento di [Airship Attributes](/help/destinations/catalog/mobile-engagement/airship-attributes.md) | A partire dal 25 marzo 2025, puoi visualizzare due schede **[!UICONTROL Airship Attributes]** affiancate nel catalogo delle destinazioni. Ciò è dovuto a un aggiornamento interno del servizio destinazioni. Il connettore della destinazione **[!UICONTROL Airship Attributes]** esistente è stato rinominato in **[!UICONTROL (Deprecated) Airship Attributes]** ed è ora disponibile una nuova scheda denominata **[!UICONTROL Airship Attributes]**. <br> Utilizza la connessione **[!UICONTROL Airship Attributes]** nel catalogo per i nuovi flussi di dati di attivazione. Se sono presenti flussi di dati attivi nella destinazione [!DNL (Deprecated) Airship Attributes], questi verranno aggiornati automaticamente e non è quindi richiesta alcuna azione da parte dell’utente. <br> Se si creano flussi di dati tramite [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/), è necessario aggiornare [!DNL flow spec ID] e [!DNL connection spec ID] ai seguenti valori: <ul><li> Flow spec ID: `a862e0be-966e-4e5a-80d3-1bb566461986`</li><li> Connection spec ID: `594bc002-4a47-49b7-8a98-ac0d21045502`</li> </ul> |

{style="table-layout:auto"}

**Funzionalità nuova o aggiornata** {#destinations-new-updated-functionality}

| Funzione | Descrizione |
| --- | --- |
| [Miglioramenti della precisione del reporting per le destinazioni di streaming](../../dataflows/ui/monitor-destinations.md) | A partire da marzo 2025, Adobe implementerà un aggiornamento per aumentare la precisione dei rapporti per le destinazioni di streaming. Questa ottimizzazione garantisce un migliore allineamento tra il reporting di Experience Platform e quello delle piattaforme di destinazione. <br> Prima di questo aggiornamento, **[!UICONTROL Identità non riuscite]** includeva tutti i tentativi di attivazione. Dopo questo aggiornamento, nel conteggio totale viene incluso solo l’ultimo tentativo di attivazione. <br> Questo miglioramento si applica a tutte le destinazioni di streaming. <br> In seguito a questo miglioramento, gli utenti delle destinazioni di streaming potrebbero notare un calo previsto nel relativo conteggio delle **[!UICONTROL Identità non riuscite]**. |
| [Supporto per l’esportazione di campi di tipo mappa per destinazioni Enterprise ed Edge](/help/destinations/ui/export-arrays-maps-objects.md) | Durante l’esportazione dei dati nelle destinazioni [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [HTTP API](/help/destinations/catalog/streaming/http-destination.md), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md) e [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md), è ora possibile selezionare i campi di tipo mappa da esportare nel passaggio di mappatura del flusso di lavoro di attivazione. <br> ![Esportazione del campo di tipo mappa nella destinazione dell’organizzazione.](../2025/assets/march/export-map.png "Esportazione del campo di tipo mappa nella destinazione dell’organizzazione."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Per ulteriori informazioni, leggi la [panoramica sulle destinazioni](../../destinations/home.md).

## Composizione di pubblico federato {#federated-audience-composition}

Per informazioni sugli ultimi aggiornamenti sulla Composizione di pubblico federato, consulta le specifiche [note sulla versione](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/release-notes).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I segmenti possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo marchio.

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti del Generatore di pubblico dell’account | All’interno di Generatore di pubblico, ora puoi filtrare gli attributi per visualizzare solo quelli compilati con i relativi dati di riepilogo. Ulteriori informazioni su questi miglioramenti sono disponibili nella documentazione sul [Generatore di pubblico](../../rtcdp/segmentation/audience-builder.md). |
| Disponibilità generale della valutazione del pubblico flessibile | La valutazione del pubblico flessibile è ora in disponibilità generale. Puoi utilizzare la valutazione del pubblico flessibile per creare nuovi tipi di pubblico on-demand per comunicazioni urgenti. Ulteriori informazioni sulla valutazione del pubblico flessibile sono disponibili nella [panoramica sulla valutazione del pubblico flessibile](../../segmentation/methods/flexible-audience-evaluation.md). |

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

Utilizza le origini in Experience Platform per acquisire dati da un’applicazione Adobe o da un’origine dati di terze parti.

**Nuove origini**

| Funzione | Descrizione |
| --- | --- |
| [!DNL Bombora Intent] | L&#39;origine [!DNL Bombora Intent] è ora disponibile nel catalogo delle origini. Utilizza questa origine per: <ul><li>Integrare i dati relativi all’intento di aumento dell’azienda Bombora per identificare gli account che stanno ricercando attivamente i tuoi prodotti o servizi.</li><li>Dare la priorità agli account nel mercato per creare segmenti precisi ed eseguire campagne ABM iper-mirate, affinché le tue attività di marketing si concentrino sugli account che hanno più probabilità di conversione.</li><li>Sfruttare strategie basate sull’intento per ottimizzare la spesa pubblicitaria, aumentare il coinvolgimento e massimizzare il ROI.</li></ul> Per ulteriori informazioni, consulta la guida sulla [connessione del tuo account [!DNL Bombora]  a Experience Platform](../../sources/tutorials/ui/create/data-partners/bombora.md). |
| [!DNL Demandbase Intent] | Il codice sorgente di [!DNL Demandbase Intent] è ora disponibile nel catalogo delle sorgenti. Utilizza questa origine per: <ul><li>Integrare i dati di Intento account di Demandbase per identificare gli account con interessi elevati in base a coinvolgimenti in tempo reale.</li><li>Dando priorità ai segnali di intento più forti, puoi creare segmenti precisi e distribuire campagne iper-mirate per garantire che le attività di marketing si concentrino sugli account che hanno più probabilità di conversione.</li><li>Attivare strategie basate sull’intento per consentire l’ottimizzazione della spesa pubblicitaria, un maggiore coinvolgimento e un ROI più elevato.</li></ul> Per ulteriori informazioni, consulta la guida sulla [connessione del tuo account  [!DNL Demandbase]  a Experience Platform](../../sources/tutorials/ui/create/data-partners/demandbase.md). |

{style="table-layout:auto"}

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Miglioramenti all’origine [!DNL Google Ads] | Ora puoi utilizzare l’origine ](../../sources/connectors/advertising/ads.md) [[!DNL Google Ads]  per acquisire i dati aggregati. Puoi utilizzare [!DNL Google Ads Query Builder] per specificare gli attributi, i segmenti e le risorse da acquisire in Experience Platform. Per ulteriori informazioni, consulta la guida sulla [connessione del tuo account  [!DNL Google Ads]  a Experience Platform](../../sources/tutorials/ui/create/advertising/ads.md). |
| Miglioramenti all’origine [!DNL Microsoft Dynamics] | Ora puoi specificare la chiave primaria di una determinata tabella [!DNL Microsoft Dynamics] durante l’esplorazione del contenuto e della struttura dei dati. Utilizza questa funzionalità per ottimizzare le query con l’origine [!DNL Microsoft Dynamics]. Per ulteriori informazioni, consulta la guida sulla [connessione di un’origine [!DNL Microsoft Dynamics]  a Experience Platform utilizzando l’API](../../sources/tutorials/api/create/crm/ms-dynamics.md). |
| Supporto per l’autenticazione tramite chiave API nelle origini self-service (SDK batch) | Ora puoi utilizzare l’autenticazione tramite chiave API come tipo di autenticazione durante l’integrazione di una nuova origine con origini self-service (SDK batch). Per ulteriori informazioni, consulta la guida alla [configurazione delle specifiche di autenticazione in SDK batch](../../sources/sources-sdk/config/authspec.md). |
| Supporto per il controllo degli accessi basato su attributi nelle origini | Ora puoi utilizzare funzioni di controllo degli accessi basate su attributi rispetto ai flussi di dati di origine. Per ulteriori informazioni, consulta le seguenti guide: <ul><li>[Applicare etichette ai flussi di dati di origine utilizzando l’API](../../sources/tutorials/api/labels.md)</li><li>[Applicare etichette ai flussi di dati di origine tramite l’interfaccia utente](../../sources/tutorials/ui/labels.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle origini](../../sources/home.md).
