---
keywords: Experience Platform;home;argomenti comuni;monitorare account;monitorare flussi di dati;flussi di dati
description: I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione fornisce passaggi per il monitoraggio dei flussi di dati in streaming dall'area di lavoro Origini.
title: Monitorare i flussi di dati per le sorgenti di streaming nell’interfaccia utente
exl-id: b080e398-e71f-40bd-aea1-7ea3ce86b55d
source-git-commit: 647f2780798dcf55a68e156af3318924c352a442
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Monitorare i flussi di dati per le sorgenti di streaming nell’interfaccia utente

Questa esercitazione descrive i passaggi per il monitoraggio dei flussi di dati per le sorgenti di streaming che utilizzano [!UICONTROL Origini] workspace.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Flussi di dati](../../../dataflows/home.md): I flussi di dati sono una rappresentazione dei processi di trasferimento dei dati in Platform. I flussi di dati sono configurati su diversi servizi e consentono di spostare i dati dai connettori di origine ai set di dati di destinazione, fino a [!DNL Identity] e [!DNL Profile]e a [!DNL Destinations].
   * [Corse del flusso di dati](../../notifications.md): Le esecuzioni dei flussi di dati sono i processi pianificati ricorrenti in base alla configurazione della frequenza dei flussi di dati selezionati.
* [Origini](../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Monitorare i flussi di dati per le sorgenti in streaming

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in questa schermata vengono visualizzate diverse sorgenti per le quali è possibile creare un account.

Per visualizzare i flussi di dati esistenti per le origini di streaming, seleziona **[!UICONTROL Flussi di dati]** dall’intestazione superiore.

![catalogo](../../images/tutorials/monitor-streaming/catalog.png)

La [!UICONTROL Flussi di dati] contiene un elenco di tutti i flussi di dati esistenti nell’organizzazione, incluse informazioni sui relativi dati di origine, nome account e stato di esecuzione del flusso di dati.

Selezionare il nome del flusso di dati che si desidera visualizzare.

![flussi di dati](../../images/tutorials/monitor-streaming/dataflows.png)

La tabella seguente contiene ulteriori informazioni sugli stati di esecuzione del flusso di dati:

| Stato | Descrizione |
| ------ | ----------- |
| Completato | La `Completed` lo stato indica che tutti i record per l’esecuzione del flusso di dati corrispondente sono stati elaborati nel periodo di un’ora. A `Completed` lo stato può ancora contenere errori nelle esecuzioni del flusso di dati. |
| Operazione riuscita | La `Success` lo stato indica che tutti i record per l’esecuzione del flusso di dati corrispondente sono stati elaborati nel periodo di un’ora e che non sono stati rilevati errori durante l’esecuzione del flusso di dati. |
| Elaborazione | La `Processing` lo stato indica che un flusso di dati non è ancora attivo. Questo stato viene spesso rilevato immediatamente dopo la creazione di un nuovo flusso di dati. |
| Errore | La `Error` lo stato indica che il processo di attivazione di un flusso di dati è stato interrotto. |
| Nessuna esecuzione | La `No runs` lo stato indica che il flusso di dati è stato creato ma non sono state avviate esecuzioni del flusso di dati. |

La [!UICONTROL Attività flusso di dati] visualizza informazioni specifiche sul flusso di dati in streaming. Il banner superiore contiene il numero cumulativo di record acquisiti e di record non riusciti per tutti i flussi di dati in streaming eseguiti nell’intervallo di date selezionato.

![attività del flusso di dati](../../images/tutorials/monitor-streaming/dataflow-activity.png)

Per impostazione predefinita, i dati visualizzati contengono i tassi di acquisizione degli ultimi sette giorni. Seleziona **[!UICONTROL Ultimi 7 giorni]** per regolare l&#39;intervallo di tempo dei record visualizzati.

Viene visualizzata una finestra a comparsa del calendario che fornisce le opzioni per l’inserimento di intervalli di tempo alternativi. Puoi configurare l’intervallo di tempo di esecuzione del flusso di dati per visualizzare le esecuzioni dei flussi dei sette giorni precedenti o degli ultimi 30 giorni. In alternativa, puoi configurare il calendario interattivo per impostare un intervallo di tempo personalizzato desiderato. Al termine, seleziona **[!UICONTROL Applica]**.

![calendario](../../images/tutorials/monitor-streaming/calendar.png)

La metà inferiore della pagina visualizza informazioni sul numero di record ricevuti, acquisiti e non riusciti, per esecuzione di flusso. Ogni esecuzione di flusso viene registrata in una finestra oraria.

![esecuzione del flusso di dati](../../images/tutorials/monitor-streaming/dataflow-run.png)

### Metriche di esecuzione del flusso di dati {#dataflow-run-metrics}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_received"
>title="Record ricevuti"
>abstract="La metrica Record ricevuti indica il conteggio totale dei record ricevuti nel flusso di dati."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_ingested"
>title="Record acquisiti"
>abstract="La metrica Record ingestito indica il numero totale di record acquisiti in data lake."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_failed"
>title="Record non elaborati"
>abstract="La metrica Record non riusciti indica il conteggio totale dei record che non sono stati acquisiti nel data lake a causa di errori nei dati."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_warnings"
>title="Record con avvisi"
>abstract="I record con avvisi indicano il numero totale di record acquisiti con avvisi di trasformazione mappatura. Tutti gli errori di trasformazione della mappatura sono segnalati come avvisi e le righe parzialmente ingerite sono considerate corrette con un avviso"
>text="Learn more in documentation"

Ogni singola esecuzione di un flusso di dati mostra i seguenti dettagli:

* **[!UICONTROL Avvio esecuzione flusso di dati]**: Data di inizio dell&#39;esecuzione del flusso di dati.
* **[!UICONTROL Tempo di elaborazione]**: Il tempo necessario all’elaborazione del flusso di dati.
* **[!UICONTROL Record ricevuti]**: Numero totale di record ricevuti nel flusso di dati da un connettore di origine.
* **[!UICONTROL Record ingestiti]**: Numero totale di record acquisiti in [!DNL Data Lake].
* **[!UICONTROL Record con avvisi]**: Numero totale di record con avvisi acquisiti. Tutti gli errori di trasformazione della mappatura sono segnalati come avvisi e le righe che sono parzialmente ingerite sono etichettate come `success` con un avviso. **Nota**: Il supporto per l’acquisizione di record con avvisi è disponibile solo per le sorgenti di streaming.
* **[!UICONTROL Record non riusciti]**: Il numero di record in cui non sono stati acquisiti [!DNL Data Lake] a causa di errori nei dati.
* **[!UICONTROL Tasso di acquisizione]**: Tasso di successo dei record acquisiti in [!DNL Data Lake]. Questa metrica è applicabile quando [!UICONTROL Acquisizione parziale] è abilitato.
* **[!UICONTROL Stato]**: Rappresenta lo stato in cui si trova il flusso di dati: o [!UICONTROL Completato] o [!UICONTROL Elaborazione]. [!UICONTROL Completato] significa che tutti i record per l’esecuzione del flusso di dati corrispondente sono stati elaborati entro un periodo di un’ora. [!UICONTROL Elaborazione] significa che l’esecuzione del flusso di dati non è ancora stata completata.

La [!UICONTROL Panoramica dell&#39;esecuzione del dataflow] contiene informazioni aggiuntive sul flusso di dati, ad esempio l’ID di esecuzione del flusso di dati corrispondente, il set di dati di destinazione e l’ID organizzazione.

Un&#39;esecuzione di flusso con errori contiene anche [!UICONTROL Errori di esecuzione del flusso di dati] , che visualizza il particolare errore che ha causato l’errore dell’esecuzione, nonché il conteggio totale dei record con errore.

![panoramica del flusso di dati](../../images/tutorials/monitor-streaming/dataflow-run-overview.png)

### Visualizza record con avvisi {#warnings}

[!UICONTROL Record con avvisi] visualizza un elenco degli avvisi di trasformazione mappatura che si sono verificati durante l&#39;esecuzione del flusso. Le righe parzialmente acquisite vengono considerate di successo e vengono aggiunte delle avvertenze se vengono rilevati errori di trasformazione di mappatura.

Per impostazione predefinita, tutti gli errori di trasformazione di mappatura sono considerati avvisi, a meno che non siano uno dei seguenti:

* Errori di sintassi
* Riferimenti ad attributi inesistenti
* Una mancata corrispondenza dei tipi di dati XDM

Per visualizzare la diagnostica degli errori, seleziona **[!UICONTROL Anteprima della diagnostica degli errori]**.

![record con avvisi](../../images/tutorials/monitor-streaming/records-with-warnings.png)

La [!UICONTROL Anteprima diagnostica errori] La finestra ti consente di visualizzare in anteprima fino a 100 errori e/o avvisi relativi all’esecuzione del flusso di dati. Da qui, puoi anche scaricare il manifesto dell’errore di acquisizione per ulteriori informazioni, utilizzando il [!DNL Data Access] API.

![diagnostica](../../images/tutorials/monitor-streaming/diagnostics.png)

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente il [!UICONTROL Origini] area di lavoro per monitorare i flussi di dati in streaming e identificare gli errori che hanno portato a eventuali flussi di dati non riusciti. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica delle origini](../../home.md)
* [Panoramica dei dataflows](../../../dataflows/home.md)
