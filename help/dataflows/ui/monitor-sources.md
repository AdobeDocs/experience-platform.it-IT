---
keywords: Experience Platform;home;argomenti comuni;monitorare account;monitorare flussi di dati;flussi di dati;origini
description: Questa esercitazione fornisce passaggi per monitorare il flusso di dati, utilizzando sia la visualizzazione di monitoraggio aggregato che il monitoraggio tra più servizi.
solution: Experience Platform
title: Monitorare i flussi di dati per le sorgenti nell’interfaccia utente
topic-legacy: overview
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: a5b52d7cc2a39ce15b5a9568df14c86624ae069a
workflow-type: tm+mt
source-wordcount: '1673'
ht-degree: 0%

---

# Monitorare i flussi di dati per le sorgenti nell’interfaccia utente

>[!IMPORTANT]
>
>Le origini di streaming, come [origine API HTTP](../../sources/connectors/streaming/http.md), non sono attualmente supportate dal dashboard di monitoraggio. Al momento, è possibile utilizzare il dashboard solo per monitorare le origini batch.

In Adobe Experience Platform, i dati vengono acquisiti da un’ampia varietà di sorgenti, analizzati all’interno di Experience Platform, e attivati in un’ampia varietà di destinazioni. Platform facilita il processo di tracciamento di questo flusso di dati potenzialmente non lineare grazie alla trasparenza dei flussi di dati.

Il dashboard di monitoraggio fornisce una rappresentazione visiva del percorso di un flusso di dati. Puoi utilizzare una visualizzazione di monitoraggio aggregato e navigare verticalmente dal livello di origine, a un flusso di dati e a un’esecuzione di un flusso di dati, per visualizzare le metriche corrispondenti che contribuiscono al successo o al fallimento di un flusso di dati. Puoi inoltre utilizzare la capacità di monitoraggio cross-service del dashboard di monitoraggio per monitorare il percorso di un flusso di dati da un’origine, a [!DNL Identity Service] e a [!DNL Profile].

Questa esercitazione fornisce passaggi per monitorare il flusso di dati, utilizzando sia la visualizzazione di monitoraggio aggregato che il monitoraggio tra più servizi.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Flussi di dati](../home.md): I flussi di dati sono una rappresentazione dei processi di trasferimento dei dati in Platform. I flussi di dati sono configurati su diversi servizi e consentono di spostare i dati dai connettori di origine ai set di dati di destinazione, a [!DNL Identity] e [!DNL Profile] e a [!DNL Destinations].
   * [Il flusso di dati viene eseguito](../../sources/notifications.md): Le esecuzioni dei flussi di dati sono i processi pianificati ricorrenti in base alla configurazione della frequenza dei flussi di dati selezionati.
* [Origini](../../sources/home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Servizio](../../identity-service/home.md) identità: Ottieni una visione migliore dei singoli clienti e del loro comportamento attraverso il collegamento delle identità tra dispositivi e sistemi.
* [Profilo](../../profile/home.md) cliente in tempo reale: Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Vista di monitoraggio aggregato

Nella [Interfaccia utente della piattaforma](https://platform.adobe.com), seleziona **[!UICONTROL Monitoraggio]** dal menu di navigazione a sinistra per accedere al dashboard [!UICONTROL Monitoraggio]. Il dashboard [!UICONTROL Monitoraggio] contiene metriche e informazioni su tutti i flussi di dati di origine, comprese informazioni sullo stato del traffico dei dati da un&#39;origine a [!DNL Identity Service] e a [!DNL Profile].

Al centro del dashboard c&#39;è il pannello [!UICONTROL Origine ingestione], che contiene metriche e grafici che mostrano i dati sui record acquisiti e i record non riusciti.

![dashboard di monitoraggio](../assets/ui/monitor-sources/monitoring-dashboard.png)

Per impostazione predefinita, i dati visualizzati contengono i tassi di acquisizione delle ultime 24 ore. Selezionare **[!UICONTROL Ultime 24 ore]** per regolare l&#39;intervallo di tempo dei record visualizzati.

![cambia data](../assets/ui/monitor-sources/change-date.png)

Viene visualizzata una finestra a comparsa del calendario che fornisce le opzioni per l’inserimento di intervalli di tempo alternativi. Seleziona **[!UICONTROL Ultimi 30 giorni]**, quindi seleziona **[!UICONTROL Applica]**

![regolazione del tempo](../assets/ui/monitor-sources/adjust-timeframe.png)

I grafici sono attivati per impostazione predefinita ed è possibile disattivarli per espandere l&#39;elenco delle origini riportate di seguito. Seleziona l&#39;interruttore **[!UICONTROL Metriche e grafici]** per disattivare i grafici.

![metriche e grafici](../assets/ui/monitor-sources/metrics-graphs.png)

| Acquisizione sorgente | Descrizione |
| ---------------- | ----------- |
| [!UICONTROL Record acquisiti  ] | Numero totale di record acquisiti. |
| [!UICONTROL Record non elaborati] | Numero totale di record che non sono stati acquisiti a causa di errori nei dati. |
| [!UICONTROL Totale flussi di dati non riusciti] | Il numero totale di flussi di dati con stato `failed`. |

Nell’elenco di acquisizione di origine sono visualizzate tutte le origini che contengono almeno un account esistente. L’elenco include inoltre informazioni sul tasso di acquisizione di ogni origine, sul numero di record con errore e sul numero totale di flussi di dati con errore in base all’intervallo di tempo applicato.

![acquisizione di origine](../assets/ui/monitor-sources/source-ingestion.png)

Per ordinare l&#39;elenco delle origini, selezionare **[!UICONTROL Risorse personali]**, quindi selezionare la categoria scelta dal menu a discesa. Ad esempio, per concentrarti sugli archivi cloud, seleziona **[!UICONTROL Cloud storage]**

![ordinabile per categoria](../assets/ui/monitor-sources/sort-by-category.png)

Per visualizzare tutti i flussi di dati esistenti in tutte le origini, selezionare **[!UICONTROL Flussi di dati]**.

![view-all-dataflows](../assets/ui/monitor-sources/view-all-dataflows.png)

In alternativa, è possibile inserire una sorgente nella barra di ricerca per isolare una singola sorgente. Una volta identificata la sorgente, seleziona l’icona del filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto a essa per visualizzare un elenco dei relativi flussi di dati attivi.

![ricerca](../assets/ui/monitor-sources/search.png)

Viene visualizzato un elenco di flussi di dati. Per limitare l&#39;elenco e attivare i flussi di dati con errori, selezionare **[!UICONTROL Mostra solo errori]**.

![show-failed-only](../assets/ui/monitor-sources/show-failures-only.png)

Individua il flusso di dati che desideri monitorare e quindi seleziona l&#39;icona del filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto a esso, per visualizzare ulteriori informazioni sullo stato di esecuzione.

![flusso dati](../assets/ui/monitor-sources/dataflow.png)

La pagina di esecuzione del flusso di dati visualizza informazioni sulla data di inizio dell’esecuzione del flusso di dati, sulle dimensioni dei dati, sullo stato e sulla relativa durata del tempo di elaborazione. Per visualizzare i dettagli dell’esecuzione del flusso di dati, seleziona l’icona filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto al tempo di avvio del flusso di dati.

![dataflow-run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

La pagina [!UICONTROL Dettagli esecuzione flusso di dati] visualizza informazioni sui metadati del flusso di dati, sullo stato di inserimento parziale e sul riepilogo degli errori. Il riepilogo degli errori contiene lo specifico errore di livello principale che mostra in quale fase il processo di acquisizione ha rilevato un errore.

Scorri verso il basso per visualizzare informazioni più specifiche sull’errore che si è verificato.

![dataflow-run-details](../assets/ui/monitor-sources/dataflow-run-details.png)

Il pannello [!UICONTROL Errori di esecuzione del flusso di dati] visualizza l&#39;errore specifico e il codice di errore che hanno causato l&#39;errore di inserimento del flusso di dati. In questo scenario, si è verificato un errore di trasformazione di mappatura, con conseguente errore di 24 record.

Seleziona **[!UICONTROL File]** per ulteriori informazioni.

![errori di esecuzione del flusso di dati](../assets/ui/monitor-sources/dataflow-run-errors.png)

Il pannello [!UICONTROL File] contiene informazioni sul nome e il percorso del file.

Per una rappresentazione più granulare dell&#39;errore, selezionare **[!UICONTROL Anteprima diagnostica errori]**.

![file](../assets/ui/monitor-sources/files.png)

Viene visualizzata la finestra [!UICONTROL Anteprima diagnostica errori], che visualizza un&#39;anteprima di un massimo di 100 errori nel flusso di dati. È possibile selezionare **[!UICONTROL Scarica]** per recuperare un comando curl, che consente di scaricare la diagnostica dell&#39;errore.

Al termine, seleziona **[!UICONTROL Chiudi]**

![diagnostica degli errori](../assets/ui/monitor-sources/error-diagnostics.png)

Puoi usare il sistema di breadcrumb nell&#39;intestazione superiore per tornare al dashboard [!UICONTROL Monitoraggio]. Seleziona **[!UICONTROL Esegui inizio: 14/02/2021, 9:47 PM]** per tornare alla pagina precedente, quindi selezionare **[!UICONTROL Flusso di dati: Demo di acquisizione dei dati fedeltà - Non riuscito]** a tornare alla pagina dei flussi di dati.

![breadcrumb](../assets/ui/monitor-sources/breadcrumbs.png)

## Monitoraggio interservizi

La parte superiore del dashboard contiene una rappresentazione del flusso di acquisizione dal livello di origine a [!DNL Identity Service] e a [!DNL Profile]. Ogni cella include un marcatore punto che indica la presenza di errori che si sono verificati in quella fase di acquisizione. Un punto verde indica un’acquisizione senza errori, mentre un punto rosso indica che si è verificato un errore in quel particolare passaggio di acquisizione.

![monitoraggio incrociato](../assets/ui/monitor-sources/cross-service-monitoring.png)

Dalla pagina dei flussi di dati, individua un flusso di dati di successo e seleziona l’icona del filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto a esso per visualizzarne le informazioni di esecuzione del flusso di dati.

![dataflow-success](../assets/ui/monitor-sources/dataflow-success.png)

La pagina [!UICONTROL Origine ingestione] contiene informazioni che confermano il corretto inserimento del flusso di dati. Da qui, puoi iniziare a monitorare il percorso del flusso di dati dal livello di origine a [!DNL Identity Service] e quindi a [!DNL Profile].

Seleziona **[!UICONTROL Identità]** per visualizzare l’acquisizione nel passaggio [!UICONTROL Identità] .

![origini](../assets/ui/monitor-sources/sources.png)

### [!DNL Identity] metriche

La pagina [!UICONTROL Elaborazione identità] contiene informazioni sui record acquisiti in [!DNL Identity Service], tra cui il numero di identità aggiunte, i grafici creati e i grafici aggiornati.

Seleziona l’icona del filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto all’ora di avvio del flusso di dati per visualizzare ulteriori informazioni sull’esecuzione del flusso di dati [!DNL Identity].

![identità](../assets/ui/monitor-sources/identities.png)

| Metriche di identità | Descrizione |
| ---------------- | ----------- |
| [!UICONTROL Record ricevuti] | Il numero di record ricevuti da [!DNL Data Lake]. |
| [!UICONTROL Record non elaborati] | Il numero di record che non sono stati acquisiti in Platform a causa di errori nei dati. |
| [!UICONTROL Record saltati] | Il numero di record acquisiti, ma non in [!DNL Identity Service] perché nella riga del record era presente un solo identificatore. |
| [!UICONTROL Record acquisiti] | Il numero di record acquisiti in [!DNL Identity Service]. |
| [!UICONTROL Record totali] | Il conteggio totale di tutti i record, inclusi quelli non riusciti, i record saltati, [!DNL Identities] aggiunti e i record duplicati. |
| [!UICONTROL Identità aggiunte] | Numero di nuovi identificatori netti aggiunti a [!DNL Identity Service]. |
| [!UICONTROL Grafici creati] | Numero di nuovi grafici di identità netti creati in [!DNL Identity Service]. |
| [!UICONTROL Grafici aggiornati] | Numero di grafici di identità esistenti aggiornati con nuovi bordi. |
| [!UICONTROL Esecuzione del flusso di dati non riuscita] | Numero di esecuzioni del flusso di dati che non sono riuscite. |
| [!UICONTROL Tempo di elaborazione] | La marca temporale dall’inizio dell’acquisizione al completamento. |
| [!UICONTROL Stato] | Definisce lo stato generale di un flusso di dati. I possibili valori di stato sono: <ul><li>`Success`: Indica che un flusso di dati è attivo e sta acquisendo i dati in base alla pianificazione fornita.</li><li>`Failed`: Indica che il processo di attivazione di un flusso di dati è stato interrotto a causa di errori. </li><li>`Processing`: Indica che il flusso di dati non è ancora attivo. Questo stato viene spesso rilevato immediatamente dopo la creazione di un nuovo flusso di dati.</li></ul> |

Nella pagina [!UICONTROL Dettagli esecuzione flusso di dati] vengono visualizzate ulteriori informazioni sull&#39;esecuzione del flusso di dati [!DNL Identity], inclusi l&#39;ID organizzazione IMS e l&#39;ID esecuzione del flusso di dati. In questa pagina vengono visualizzati anche il codice di errore e il messaggio di errore corrispondenti forniti da [!DNL Identity Service], nel caso in cui si verifichino errori nel processo di acquisizione.

Seleziona **[!UICONTROL Esegui inizio: 14/02/2021, alle 9:47 PM]** per tornare alla pagina precedente.

![identity-dataflow-run](../assets/ui/monitor-sources/identities-dataflow-run.png)

Dalla pagina [!UICONTROL Elaborazione identità], seleziona **[!UICONTROL Profili]** per visualizzare lo stato dell’acquisizione dei record nel passaggio [!UICONTROL Profili] .

![select-profiles](../assets/ui/monitor-sources/select-profiles.png)

### [!DNL Profile] metriche

La pagina [!UICONTROL Elaborazione profilo] contiene informazioni sui record acquisiti in [!DNL Profile], tra cui il numero di frammenti di profilo creati, i frammenti di profilo aggiornati e il numero totale di frammenti di profilo.

Seleziona l’icona del filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto all’ora di avvio del flusso di dati per visualizzare ulteriori informazioni sull’esecuzione del flusso di dati [!DNL Profile].

![profiles](../assets/ui/monitor-sources/profiles.png)

| Metriche del profilo | Descrizione |
| --------------- | ----------- |
| [!UICONTROL Record ricevuti] | Il numero di record ricevuti da [!DNL Data Lake]. |
| [!UICONTROL Record non elaborati  ] | Il numero di record acquisiti, ma non in [!DNL Profile] a causa di errori. |
| [!UICONTROL Frammenti di profilo aggiunti] | Numero di nuovi frammenti [!DNL Profile] aggiunti. |
| [!UICONTROL Frammenti di profilo aggiornati] | Numero di frammenti [!DNL Profile] esistenti aggiornati |
| [!UICONTROL Frammenti di profilo totali] | Numero totale di record scritti in [!DNL Profile], inclusi tutti i frammenti [!DNL Profile] esistenti aggiornati e i nuovi frammenti [!DNL Profile] creati. |
| [!UICONTROL Esecuzione del flusso di dati non riuscita] | Numero di esecuzioni del flusso di dati che non sono riuscite. |
| [!UICONTROL Tempo di elaborazione] | La marca temporale dall’inizio dell’acquisizione al completamento. |
| [!UICONTROL Stato] | Definisce lo stato generale di un flusso di dati. I possibili valori di stato sono: <ul><li>`Success`: Indica che un flusso di dati è attivo e sta acquisendo i dati in base alla pianificazione fornita.</li><li>`Failed`: Indica che il processo di attivazione di un flusso di dati è stato interrotto a causa di errori. </li><li>`Processing`: Indica che il flusso di dati non è ancora attivo. Questo stato viene spesso rilevato immediatamente dopo la creazione di un nuovo flusso di dati.</li></ul> |

Nella pagina [!UICONTROL Dettagli esecuzione flusso di dati] vengono visualizzate ulteriori informazioni sull&#39;esecuzione del flusso di dati [!DNL Profile], inclusi l&#39;ID organizzazione IMS e l&#39;ID esecuzione del flusso di dati. In questa pagina vengono visualizzati anche il codice di errore e il messaggio di errore corrispondenti forniti da [!DNL Profile], nel caso in cui si verifichino errori nel processo di acquisizione.

![profiles-dataflow-run](../assets/ui/monitor-sources/profiles-dataflow-run.png)

## Passaggi successivi

Seguendo questa esercitazione, hai monitorato correttamente il flusso di dati di acquisizione da livello di origine a [!DNL Identity Service] e a [!DNL Profile] utilizzando il dashboard **[!UICONTROL Monitoraggio]**. Hai inoltre identificato con successo gli errori che hanno contribuito al fallimento dei flussi di dati durante il processo di acquisizione. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica del profilo cliente in tempo reale](../../profile/home.md)
* [Panoramica di Data Science Workspace](../../data-science-workspace/home.md)
