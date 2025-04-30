---
description: Scopri come utilizzare il dashboard di monitoraggio per monitorare i dati acquisiti nel data lake.
title: Monitorare l’acquisizione del data lake
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: f671188fbc694b0d2d808577265f91788cb0d8e9
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 10%

---

# Monitorare l’acquisizione del data lake

>[!IMPORTANT]
>
>Le origini di streaming, ad esempio l&#39;[origine API HTTP](../../sources/connectors/streaming/http.md), non sono attualmente supportate dal dashboard di monitoraggio. Al momento, è possibile utilizzare il dashboard solo per monitorare le origini batch.

Leggi questo documento per scoprire come utilizzare il dashboard di monitoraggio per monitorare l’acquisizione del data lake nell’interfaccia utente di Experience Platform.

## Introduzione {#get-started}

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Flussi dati](../home.md): i flussi dati sono una rappresentazione dei processi di dati che spostano i dati in Experience Platform. I flussi di dati sono configurati tra servizi diversi, consentendo di spostare i dati dai connettori di origine ai set di dati di destinazione, a [!DNL Identity] e [!DNL Profile] e a [!DNL Destinations].
   * [Esecuzioni flusso di dati](../../sources/notifications.md): le esecuzioni del flusso di dati sono i processi pianificati ricorrenti in base alla configurazione della frequenza dei flussi di dati selezionati.
* [Origini](../../sources/home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Identity Service](../../identity-service/home.md): ottieni una migliore visione dei singoli clienti e del loro comportamento collegando le identità tra dispositivi e sistemi.
* [Profilo cliente in tempo reale](../../profile/home.md): fornisce un profilo consumatore unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Utilizza il dashboard di monitoraggio per l’acquisizione del data lake

>[!CONTEXTUALHELP]
>id="platform_monitoring_source_ingestion"
>title="Acquisizione di origine"
>abstract="La vista Acquisizione di origine contiene informazioni sullo stato e le metriche delle attività dui dati nel servizio Data Lake, compresi i record acquisiti e quelli con errori. Consulta la guida alla definizione delle metriche per ulteriori informazioni su metriche e grafi."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_ingestion"
>title="Dettagli dell’esecuzione del flusso di dati"
>abstract="L’elaborazione delle origini contiene informazioni sullo stato e le metriche delle attività sui dati nel servizio Data Lake, compresi i record acquisiti e quelli con errori. Consulta la guida alla definizione delle metriche per ulteriori informazioni su metriche e grafi."
>text="Learn more in documentation"

Seleziona **[!UICONTROL Data lake]** dall&#39;intestazione principale nel dashboard di monitoraggio per visualizzare il tasso di acquisizione del data lake.

![Dashboard di monitoraggio con la scheda delle origini selezionata.](../assets/ui/monitor-sources/data-lake.png)

Il grafico [!UICONTROL Tasso di acquisizione] visualizza il tasso di acquisizione dei dati in base all&#39;intervallo di tempo configurato. Per impostazione predefinita, nel dashboard di monitoraggio vengono visualizzate le percentuali di acquisizione delle ultime 24 ore. Per i passaggi su come configurare l&#39;intervallo di tempo, leggere la guida alla [configurazione dell&#39;intervallo di tempo di monitoraggio](monitor.md#configure-monitoring-time-frame).

Per impostazione predefinita, il grafico è abilitato alla visualizzazione. Per nascondere il grafico, selezionare **[!UICONTROL Metriche e grafici]** per disabilitare l&#39;attivazione e nascondere il grafico.

![Grafico delle metriche del tasso di acquisizione.](../assets/ui/monitor-sources/metrics-graph.png)

Nella parte inferiore del dashboard viene visualizzata una tabella che illustra il rapporto delle metriche correnti per tutti i flussi di dati di origine esistenti.

![Tabella delle metriche del dashboard di monitoraggio.](../assets/ui/monitor-sources/metrics-table.png)

| Metriche | Descrizione |
| --- | --- |
| Record ricevuti | Numero totale di record ricevuti da una determinata origine. |
| Record acquisiti | Numero totale di record acquisiti nel data lake. |
| Record ignorati | Numero totale di record ignorati. Un record ignorato si riferisce a campi che sono stati ignorati perché non erano necessari per l’acquisizione. Ad esempio, se crei un flusso di dati di origini con acquisizione parziale abilitata, puoi configurare una soglia di tasso di errore accettabile. Durante il processo di acquisizione, i record dei campi non obbligatori, come i campi di identità, vengono ignorati se rientrano nella soglia di errore. |
| Record con errori | Numero totale di record che non è stato possibile acquisire a causa di errori. |
| Tasso acquisiti | La percentuale di record acquisiti in base al numero totale di record ricevuti. |
| Totale flussi dati totali non riusciti | Numero totale di flussi di dati non riusciti. |

{style="table-layout:auto"}

Puoi filtrare ulteriormente i dati utilizzando le opzioni fornite sopra la tabella delle metriche:

| Opzioni di filtro | Descrizione |
| --- | --- |
| Cerca | Utilizzare la barra di ricerca per filtrare la visualizzazione in base a un singolo tipo di origine. |
| Origini | Seleziona **[!UICONTROL Origini]** per filtrare la visualizzazione e visualizzare i dati delle metriche in base al tipo di origine. Questa è la visualizzazione predefinita utilizzata dal dashboard di monitoraggio. |
| Flussi di dati | Seleziona **[!UICONTROL Flussi dati]** per filtrare la visualizzazione e visualizzare i dati delle metriche per flusso di dati. |
| Mostra solo errori | Seleziona **[!UICONTROL Mostra solo errori]** per filtrare la visualizzazione e visualizzare solo i flussi di dati che hanno segnalato errori di acquisizione. |
| Le mie fonti | Puoi filtrare ulteriormente la vista utilizzando il menu a discesa [!UICONTROL Risorse personali]. Utilizza il menu a discesa per filtrare la vista per categoria. In alternativa, è possibile selezionare **[!UICONTROL Tutte le origini]** per visualizzare le metriche su tutte le origini o, oppure selezionare **[!UICONTROL Le mie origini]** per visualizzare solo le origini con cui si dispone di un account corrispondente. |

{style="table-layout:auto"}

Per monitorare i dati che vengono acquisiti in un flusso di dati specifico, seleziona l&#39;icona del filtro ![filter](/help/images/icons/filter-add.png) accanto a un&#39;origine.

![Monitorare un flusso di dati specifico selezionando l&#39;icona del filtro accanto a una determinata origine.](../assets/ui/monitor-sources/monitor-dataflow.png)

La tabella delle metriche viene aggiornata con una tabella di flussi di dati attivi che corrispondono all’origine selezionata. Durante questo passaggio, puoi visualizzare ulteriori informazioni sui flussi di dati, tra cui il set di dati e il tipo di dati corrispondenti, nonché una marca temporale per indicare quando sono stati attivi per l’ultima volta.

Per esaminare ulteriormente un flusso di dati, seleziona l&#39;icona filtro ![filter](/help/images/icons/filter-add.png) accanto a un flusso di dati.

![Tabella dei flussi di dati nel dashboard di monitoraggio.](../assets/ui/monitor-sources/select-dataflow.png)

Viene quindi visualizzata un’interfaccia che elenca tutte le iterazioni di esecuzione del flusso di dati selezionato.

Le esecuzioni del flusso di dati rappresentano un’istanza dell’esecuzione del flusso di dati. Ad esempio, se un flusso di dati è pianificato per essere eseguito ogni ora alle 09:00, alle 00:00 e alle 00:00, sono disponibili tre istanze di un flusso. Le esecuzioni del flusso sono specifiche per la tua particolare organizzazione.

Per verificare le metriche di una specifica iterazione di esecuzione del flusso di dati, seleziona l&#39;icona del filtro ![filter](/help/images/icons/filter-add.png) accanto al flusso di dati.

![Pagina delle metriche di esecuzione del flusso di dati.](../assets/ui/monitor-sources/dataflow-page.png)

Utilizza la pagina dei dettagli dell’esecuzione del flusso di dati per visualizzare le metriche e le informazioni dell’iterazione di esecuzione selezionata.

![Pagina dei dettagli di esecuzione del flusso di dati.](../assets/ui/monitor-sources/dataflow-run-details.png)

| Dettagli dell’esecuzione del flusso di dati | Descrizione |
| --- | --- |
| Record acquisiti | Numero totale di record acquisiti dall’esecuzione del flusso di dati. |
| Record con errori | Numero totale di record che non sono stati acquisiti a causa di errori nell’esecuzione del flusso di dati. |
| File totali | Numero totale di file nell’esecuzione del flusso di dati. |
| Dimensione dei dati | Dimensione totale dei dati contenuti nell’esecuzione del flusso di dati. |
| ID esecuzione flusso di dati | ID dell’iterazione di esecuzione del flusso di dati. |
| ID organizzazione | ID dell’organizzazione in cui è stata creata l’esecuzione del flusso di dati. |
| Stato | Stato dell’esecuzione del flusso di dati. |
| Avvio dell’esecuzione flusso di dati | Un timestamp che indica quando è iniziata l’esecuzione del flusso di dati. |
| Fine esecuzione flusso di dati | Un timestamp che indica quando è terminata l’esecuzione del flusso di dati. |
| Set di dati | Set di dati utilizzato per creare il flusso di dati. |
| Tipo di dati | Il tipo di dati che era nel flusso di dati. |
| Acquisizione parziale | L’acquisizione in batch parziale consente di acquisire dati contenenti errori, fino a una determinata soglia configurabile. Questa funzione consente di acquisire correttamente in Experience Platform tutti i dati accurati, mentre tutti i dati errati vengono raggruppati separatamente con informazioni sul motivo della validità. Puoi abilitare l’acquisizione parziale durante il processo di creazione del flusso di dati. |
| Diagnostica degli errori | La diagnostica degli errori indica all’origine di produrre diagnostica degli errori a cui puoi fare riferimento in seguito durante il monitoraggio dell’attività del set di dati e dello stato del flusso di dati. Puoi abilitare la diagnostica degli errori durante il processo di creazione del flusso di dati. |
| Riepilogo errori | Dato un flusso di dati non riuscito, nel riepilogo degli errori vengono visualizzati un codice e una descrizione di errore che riepilogano il motivo per cui l’iterazione dell’esecuzione non è riuscita. |

{style="table-layout:auto"}

Se il flusso di dati segnala errori, puoi scorrere verso il basso fino alla parte inferiore della pagina e utilizzare l&#39;interfaccia [!UICONTROL Errori di esecuzione flusso di dati].

Utilizzare la sezione [!UICONTROL Record non riusciti] per visualizzare le metriche nei record non acquisiti a causa di errori. Per visualizzare un report completo degli errori, selezionare **[!UICONTROL Anteprima diagnostica errori]**. Per scaricare una copia della diagnostica degli errori e del manifesto del file, selezionare **[!UICONTROL Scarica]**, quindi copiare la chiamata API di esempio da utilizzare con l&#39;API [!DNL Data Access].

>[!NOTE]
>
>È possibile utilizzare la diagnostica degli errori solo se la funzione è stata abilitata durante il processo di creazione della connessione di origine.

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai imparato a monitorare il tasso di acquisizione del data lake utilizzando il dashboard **[!UICONTROL Monitoraggio]**. Hai anche imparato a identificare gli errori che causano errori del flusso di dati durante l’acquisizione. Per ulteriori informazioni, consulta i seguenti documenti:

* [Monitoraggio dei dati di identità](./monitor-identities.md).
* [Monitoraggio dei dati del profilo](./monitor-profiles.md).
