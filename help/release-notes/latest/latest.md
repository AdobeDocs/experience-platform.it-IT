---
title: Note sulla versione di Adobe Experience Platform di ottobre 2024
description: Note sulla versione di Adobe Experience Platform di ottobre 2024.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: f30a124a40928abf69366d311131e353c2779191
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 78%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 29 ottobre 2024**

Aggiornamenti alle funzioni e alla documentazione esistenti in Adobe Experience Platform:

- [Dashboard](#dashboards)
- [Raccolta dati](#data-collection-)
- [Destinazioni](#destinations)
- [Servizio di segmentazione](#segmentation-service)
- [Sandbox](#sandboxes)
- [Origini](#sources)

## Dashboard {#dashboards}

Experience Platform fornisce più dashboard attraverso le quali è possibile visualizzare approfondimenti importanti sui dati della tua organizzazione, acquisiti durante le istantanee giornaliere.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Modelli di Data Distiller | Esplora più modelli per ottenere informazioni strutturate sui dati del pubblico. Utilizza dashboard come **Advanced [!UICONTROL Audience Overlaps]**, **[!UICONTROL Audience Comparison]**, **[!UICONTROL Audience Trends]** e **[!UICONTROL Audience Identity Overlaps]** per prendere decisioni basate sui dati, ottimizzare la segmentazione e migliorare le strategie di coinvolgimento. Per ulteriori dettagli, consulta la [Guida ai modelli di Data Distiller](../../dashboards/sql-insights-query-pro-mode/templates/overview.md). |
| Sovrapposizioni del pubblico avanzate | Analizza rapidamente le intersezioni del pubblico per tipi di pubblico specifici o visualizza tutte le sovrapposizioni per scoprire informazioni importanti sull’intero set di pubblico. Utilizza queste informazioni per perfezionare la segmentazione, ridurre la messaggistica ridondante e creare campagne più mirate per migliorare l’efficienza del marketing. Per ulteriori dettagli, consulta la [guida Advanced Audience Overlaps](../../dashboards/sql-insights-query-pro-mode/templates/overlaps.md). |
| Miglioramenti apportati al confronto dei tipi di pubblico | Visualizza un confronto affiancato delle metriche chiave tra gruppi di pubblico diversi utilizzando la dashboard **Confronto pubblico**. Con questa dashboard puoi selezionare intervalli di tempo e KPI specifici, ad esempio la dimensione e la composizione dell’identità del pubblico, per prendere decisioni più informate sulla segmentazione del pubblico e sulle strategie di targeting. Per ulteriori informazioni, leggere la [Guida al confronto dei tipi di pubblico](../../dashboards/sql-insights-query-pro-mode/templates/comparison.md). |
| Visualizzazione tendenze pubblico | Analizza le metriche del pubblico nel tempo con la dashboard **[!UICONTROL Tendenze pubblico]**. Visualizza le tendenze relative alle dimensioni del pubblico, al numero di identità e al numero di profili di identità singoli, per monitorare l’evoluzione del pubblico, misurare la crescita e perfezionare le strategie di coinvolgimento. Per ulteriori dettagli, consulta la [guida sulle tendenze del pubblico](../../dashboards/sql-insights-query-pro-mode/templates/trends.md). |
| Analisi delle sovrapposizioni delle identità | Analizza le sovrapposizioni di identità nei tipi di pubblico selezionati con il dashboard **[!UICONTROL Sovrapposizioni di identità del pubblico]**. Visualizza le tendenze e i raggruppamenti delle identità per comprendere come si relazionano i diversi tipi di identità nel pubblico, migliorando l’unione delle identità e la precisione della segmentazione del cliente. Per ulteriori informazioni, consulta la [Guida alle sovrapposizioni delle identità del pubblico](../../dashboards/sql-insights-query-pro-mode/templates/identity-overlaps.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle dashboard, tra cui come concedere le autorizzazioni di accesso e creare widget personalizzati, consulta la [panoramica sulle dashboard](../../dashboards/home.md).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli a Edge Network di Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Nuove funzioni**

| Tipo | Funzione | Descrizione |
| --- | --- | --- |
| Tag ed estensioni | Visualizzazione JSON di Adobe Analytics | Ora è possibile utilizzare l’estensione dei tag Adobe Analytics per esaminare eVar, prop ed impostazioni evento come JSON, che adesso può essere incluso nell’estensione Web SDK ed esportato per la modifica. È possibile inoltre caricare o copiare questi dati e memorizzarli sul proprio dispositivo. Per ulteriori informazioni, consulta la [documentazione dell’estensione Adobe Analytics](../../tags/extensions/client/analytics/overview.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica della raccolta dati](../../collection/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzione | Descrizione |
| ----------- | ----------- |
| [Supporto per l’esportazione di array in disponibilità generale](../../destinations/ui/export-arrays-calculated-fields.md) | La clientela adesso può utilizzare l’opzione **[!UICONTROL Aggiungi campo calcolato]** durante l’attivazione dei tipi di pubblico *in destinazioni basate su file* per esportare interi array o elementi di array. È comunque necessario utilizzare la funzione `array_to_string` per ridurre l’array in una stringa nel file di destinazione. <br> ![Aggiungere la selezione di campo calcolato con funzioni e campi.](../2024/assets/october/array-export.gif "Aggiungere un campo calcolato con una selezione della funzione array_to_string e dell’array di organizzazioni."){width="250" align="center" zoomable="yes"} |
| [Miglioramenti della precisione del reporting per le destinazioni di streaming](/help/destinations/ui/export-datasets.md) | A partire da ottobre 2024, Adobe implementerà un aggiornamento per aumentare la precisione dei rapporti per le destinazioni di streaming. Questo miglioramento garantisce un migliore allineamento tra il reporting di Experience Platform e quello delle piattaforme di destinazione. <br> Prima di questo aggiornamento, **[!UICONTROL Identità non riuscite]** includeva tutti i tentativi di attivazione. Dopo questo aggiornamento, nel conteggio totale viene incluso solo l’ultimo tentativo di attivazione. <br> Questo miglioramento è applicato attualmente alla [destinazione Customer Match di Google](../../destinations/catalog/advertising/google-customer-match.md), ma verrà implementata gradualmente in altre destinazioni di streaming di Experience Platform. In seguito a questo miglioramento, gli utenti della [destinazione Customer Match di Google](../../destinations/catalog/advertising/google-customer-match.md) potrebbero notare un calo previsto nel relativo conteggio delle **[!UICONTROL Identità non riuscite]**. |
| Implicazioni della valutazione del pubblico flessibile in [attivazione del pubblico in batch](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files) | Se si esegue una [valutazione del pubblico](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation) su tipi di pubblico già impostati per essere attivati dopo la valutazione del segmento, i tipi di pubblico verranno attivati al termine del processo di valutazione del pubblico flessibile, indipendentemente da ogni processo di attivazione giornaliero precedente. <br> Questo potrebbe comportare l’esportazione di tipi di pubblico più volte al giorno, in base alle azioni eseguite. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggi la [panoramica sulle destinazioni](../../destinations/home.md).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I segmenti possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo marchio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| [!BADGE Disponibilità limitata]{type=Informative} Valutazione del pubblico flessibile | La valutazione del pubblico flessibile consente di creare rapidamente nuovi tipi di pubblico su richiesta per comunicazioni urgenti. Ulteriori informazioni su questa nuova funzione sono disponibili nella [documentazione di Audience Portal](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation). |

{style="table-layout:auto"}

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa. Per rispondere a questa esigenza, Experience Platform fornisce ambienti sandbox che permettono di suddividere una singola istanza di Platform in ambienti virtuali separati, utili per le attività di sviluppo e evoluzione delle applicazioni di esperienza digitale.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Condivisione del pacchetto di strumenti sandbox | Ora puoi utilizzare gli strumenti sandbox per esportare e importare facilmente le configurazioni sandbox tra sandbox di organizzazioni diverse. Sono ora disponibili due categorie di pacchetti condivisi:<br><ul><li>**[Pacchetto privato](../../sandboxes/ui/sharing-packages-across-orgs.md#private-packages):** è possibile utilizzare la condivisione di un pacchetto privato con organizzazioni che hanno approvato la richiesta di condivisione dall’organizzazione di origine.</li><li>**[Pacchetto pubblico](../../sandboxes/ui/sharing-packages-across-orgs.md#public-packages):** i pacchetti pubblici possono essere condivisi senza approvazioni aggiuntive e possono essere importati facilmente utilizzando il payload del pacchetto.</li></ul><br>Per ulteriori informazioni su queste funzioni, consulta la guida su [condivisione di pacchetti tra organizzazioni](../../sandboxes/ui/sharing-packages-across-orgs.md). |
| [Condivisione pacchetto](https://experienceleague.adobe.com/it/docs/experience-platform/sandbox/sandbox-tooling-api/packages#org-linking) nell’API di strumenti di sandbox | È possibile utilizzare l’API degli strumenti di sandbox per effettuare richieste a due nuovi endpoint `/handshake` e `/transfer` per la condivisione tra organizzazioni, il recupero e la creazione di richieste di condivisione del pacchetto. È stata aggiunta una richiesta aggiuntiva all’endpoint `/packages` per recuperare il payload di un pacchetto. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle sandbox, consulta la [panoramica sulle sandbox](../../sandboxes/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

Utilizza le origini in Experience Platform per acquisire dati da un’applicazione Adobe o da un’origine dati di terze parti.

**Funzione aggiornata**

| Funzione | Descrizione |
| --- | --- |
| Supporto per il filtro delle entità di attività standard in [!DNL Marketo Engage] | Ora è possibile utilizzare l’API [!DNL Flow Service] per filtrare le entità di attività standard durante l’acquisizione dei dati dall’origine [!DNL Marketo Engage]. Per ulteriori informazioni, consulta la guida su [filtro di  [!DNL Marketo] dati di attività standard](../../sources/tutorials/api/filter.md#filter-activity-entities-for-marketo-engage). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle origini](../../sources/home.md).