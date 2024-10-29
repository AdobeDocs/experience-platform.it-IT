---
title: Note sulla versione di Adobe Experience Platform - Ottobre 2024
description: Note sulla versione di Adobe Experience Platform di ottobre 2024.
source-git-commit: a381bdc45ee9c3c7ffb32bb7a7ec43a1233d1556
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 41%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 29 ottobre 2024**

Aggiornamenti alle funzioni e alla documentazione esistenti in Adobe Experience Platform:

- [Raccolta dati](#data-collection)
- [Destinazioni](#destinations)
- [Servizio di segmentazione](#segmentation-service)
- [Sandbox](#sandboxes)
- [Origini](#sources)

<!-- ## Dashboards {#dashboards}

Experience Platform provides multiple dashboards through which you can view important insights about your organization's data, as captured during daily snapshots.

**New or updated features**

| Feature | Description |
| --- | --- |
| Data Distiller Templates | Explore multiple templates to gain structured insights into audience data. Use dashboards like **Advanced [!UICONTROL Audience Overlaps]**, **[!UICONTROL Audience Comparison]**, **[!UICONTROL Audience Trends]**, and **[!UICONTROL Audience Identity Overlaps]** to make data-driven decisions, optimize segmentation, and enhance engagement strategies. See the [Data Distiller Templates guide](../../dashboards/sql-insights-query-pro-mode/templates/overview.md) for more details. |
| Advanced Audience Overlaps | Quickly analyze audience intersections for specific audiences or view all overlaps to uncover valuable insights across your entire audience set. Use these insights to refine segmentation, reduce redundant messaging, and create more targeted campaigns for improved marketing efficiency. See the [Advanced Audience Overlaps guide](../../dashboards/sql-insights-query-pro-mode/templates/overlaps.md) for more details. |
| Audience Comparison enhancements | View a side-by-side comparison of key metrics between different audience groups using the **Audience Comparison** dashboard. With this dashboard you can select specific time frames and KPIs, such as audience size and identity composition, to make more informed decisions about audience segmentation and targeting strategies. Read the [Audience Comparison guide](../../dashboards/sql-insights-query-pro-mode/templates/comparison.md) for more information. |
| Audience Trends Visualization | Analyze audience metrics over time with the **[!UICONTROL Audience Trends]** dashboard. Visualize trends for audience size, number of identities, and number of single identity profiles to help you monitor audience evolution, measure growth, and refine your engagement strategies. See the [Audience Trends guide](../../dashboards/sql-insights-query-pro-mode/templates/trends.md) for more details. |
| Identity Overlaps Analysis | Analyze identity overlaps in selected audiences with the **[!UICONTROL Audience Identity Overlaps]** dashboard. View identity trends and breakdowns to understand how different identity types relate within your audience, enhancing identity stitching and improving customer segmentation accuracy. Refer to the [Audience Identity Overlaps guide](../../dashboards/sql-insights-query-pro-mode/templates/identity-overlaps.md) for more details. |

{style="table-layout:auto"}

For more information on dashboards, including how to grant access permissions and create custom widgets, begin by reading the [dashboards overview](../../dashboards/home.md). -->

## Raccolta dati {#collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli a Edge Network di Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Nuove funzioni**

| Tipo | Funzione | Descrizione |
| --- | --- | --- |
| Tag ed estensioni | Visualizzazione JSON di Adobe Analytics | Ora puoi utilizzare l’estensione tag Adobe Analytics per esaminare eVar, prop ed impostazioni evento come JSON, che ora può essere incluso nell’estensione Web SDK ed esportato per la modifica. Puoi anche caricare o copiare questi dati e memorizzarli sul tuo dispositivo. Per ulteriori informazioni, consulta la [documentazione dell&#39;estensione Adobe Analytics](../../tags/extensions/client/analytics/overview.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica della raccolta dati](../../collection/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzione | Descrizione |
| ----------- | ----------- |
| [Supporto per l&#39;esportazione di array generalmente disponibile](../../destinations/ui/export-arrays-calculated-fields.md) | Tutti i clienti ora possono utilizzare l&#39;opzione **[!UICONTROL Aggiungi campo calcolato]** durante l&#39;attivazione dei tipi di pubblico *in destinazioni basate su file* per esportare intere matrici o elementi di matrici. È comunque necessario utilizzare la funzione `array_to_string` per appiattire l&#39;array in una stringa nel file di destinazione. <br> ![Aggiungere la selezione di campi calcolati con funzioni e campi.](../2024/assets/october/array-export.gif "Aggiungere un campo calcolato con una selezione della funzione array_to_string e dell&#39;array di organizzazioni."){width="250" align="center" zoomable="yes"} |
| [Miglioramenti della precisione del reporting per le destinazioni di streaming](/help/destinations/ui/export-datasets.md) | A partire da ottobre 2024, Adobe sta implementando un aggiornamento per aumentare la precisione dei rapporti per le destinazioni di streaming. Questo miglioramento garantisce un migliore allineamento tra il reporting dell’Experience Platform e quello delle piattaforme di destinazione. <br> Prima di questo aggiornamento, **[!UICONTROL Identità non riuscite]** includeva tutti i tentativi di attivazione. Dopo questo aggiornamento, nel conteggio totale viene incluso solo l’ultimo tentativo di attivazione. <br> Questo miglioramento si applica attualmente alla [destinazione Customer Match di Google](../../destinations/catalog/advertising/google-customer-match.md), ma verrà introdotto gradualmente in altre destinazioni di streaming di Experienci Platform. In seguito a questo miglioramento, gli utenti della [destinazione Customer Match di Google](../../destinations/catalog/advertising/google-customer-match.md) potrebbero notare un calo previsto nel conteggio di **[!UICONTROL Identità non riuscite]**. |
| Implicazioni di valutazione flessibile del pubblico in [attivazione batch del pubblico](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files) | Se esegui [valutazione flessibile del pubblico](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation) su tipi di pubblico già impostati per essere attivati dopo la valutazione dei segmenti, i tipi di pubblico verranno attivati al termine del processo di valutazione flessibile, indipendentemente da eventuali processi di attivazione giornalieri precedenti. <br> Questo potrebbe comportare l&#39;esportazione di tipi di pubblico più volte al giorno, in base alle azioni eseguite. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggi la [panoramica sulle destinazioni](../../destinations/home.md).

## Servizio di segmentazione {#segmentation-service}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I segmenti possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo marchio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| [!BADGE Disponibilità limitata]{type=Informative} Valutazione flessibile del pubblico | La valutazione flessibile del pubblico consente di creare rapidamente nuovi tipi di pubblico su richiesta per comunicazioni urgenti. Ulteriori informazioni su questa nuova funzionalità sono disponibili nella [documentazione di Audience Portal](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation). |

{style="table-layout:auto"}

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa. Per rispondere a questa esigenza, Experience Platform fornisce ambienti sandbox che permettono di suddividere una singola istanza di Platform in ambienti virtuali separati, utili per le attività di sviluppo e evoluzione delle applicazioni di esperienza digitale.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Condivisione pacchetti di strumenti sandbox | È ora possibile utilizzare gli strumenti sandbox per esportare e importare facilmente le configurazioni sandbox tra sandbox di organizzazioni diverse. Sono ora disponibili due categorie di pacchetti condivisi:<br><ul><li>**[Pacchetto privato](../../sandboxes/ui/sharing-packages-across-orgs.md#private-packages):** Utilizza la condivisione di pacchetti privati con organizzazioni che hanno approvato la richiesta di condivisione dall&#39;organizzazione di origine.</li><li>**[Pacchetto pubblico](../../sandboxes/ui/sharing-packages-across-orgs.md#public-packages):** I pacchetti pubblici possono essere condivisi senza ulteriori approvazioni e possono essere importati facilmente utilizzando il payload del pacchetto.</li></ul><br>Per ulteriori informazioni su queste funzionalità, leggere la guida su [condivisione di pacchetti tra organizzazioni](../../sandboxes/ui/sharing-packages-across-orgs.md). |
| [Condivisione pacchetti](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/packages#org-linking) nell&#39;API di strumenti sandbox | Utilizzare l&#39;API per gli strumenti sandbox per effettuare richieste a due nuovi endpoint, `/handshake` e `/transfer` per la condivisione tra organizzazioni, il recupero e la creazione di richieste di condivisione dei pacchetti. È stata aggiunta una richiesta aggiuntiva all&#39;endpoint `/packages` per recuperare il payload di un pacchetto. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, consulta la [panoramica sulle origini](../../sandboxes/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

Utilizza le origini in Experience Platform per acquisire dati da un’applicazione Adobe o da un’origine dati di terze parti.

**Funzione aggiornata**

| Funzione | Descrizione |
| --- | --- |
| Supporto per il filtro delle entità attività standard in [!DNL Marketo Engage] | È possibile utilizzare l&#39;API [!DNL Flow Service] per filtrare le entità attività standard durante l&#39;acquisizione dei dati dall&#39;origine [!DNL Marketo Engage]. Per ulteriori informazioni, consulta la guida su [filtraggio [!DNL Marketo] dati attività standard](../../sources/tutorials/api/filter.md#filter-activity-entities-for-marketo-engage). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la [panoramica sulle origini](../../sources/home.md).
