---
keywords: Experience Platform;home;argomenti comuni;monitorare account;monitorare flussi di dati;flussi di dati;origini
description: Questa esercitazione fornisce passaggi per monitorare il flusso di dati, utilizzando sia la visualizzazione di monitoraggio aggregato che il monitoraggio tra più servizi.
solution: Experience Platform
title: Monitorare i flussi di dati per le sorgenti nell’interfaccia utente
topic-legacy: overview
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: 241deb93b3500139b79425a4da79258670e044a8
workflow-type: tm+mt
source-wordcount: '1806'
ht-degree: 0%

---

# Monitorare i flussi di dati per le sorgenti nell’interfaccia utente

>[!IMPORTANT]
>
>Sorgenti in streaming, ad esempio [Origine API HTTP](../../sources/connectors/streaming/http.md) al momento non sono supportati dal dashboard di monitoraggio. Al momento, è possibile utilizzare il dashboard solo per monitorare le origini batch.

In Adobe Experience Platform, i dati vengono acquisiti da un’ampia varietà di sorgenti, analizzati all’interno di Experience Platform, e attivati in un’ampia varietà di destinazioni. Platform facilita il processo di tracciamento di questo flusso di dati potenzialmente non lineare grazie alla trasparenza dei flussi di dati.

Il dashboard di monitoraggio fornisce una rappresentazione visiva del percorso di un flusso di dati. Puoi utilizzare una visualizzazione di monitoraggio aggregato e navigare verticalmente dal livello di origine, a un flusso di dati e a un’esecuzione di un flusso di dati, per visualizzare le metriche corrispondenti che contribuiscono al successo o al fallimento di un flusso di dati. È inoltre possibile utilizzare la capacità di monitoraggio cross-service del dashboard di monitoraggio per monitorare il percorso di un flusso di dati da un&#39;origine a [!DNL Identity Service]e a [!DNL Profile].

Questa esercitazione fornisce passaggi per monitorare il flusso di dati, utilizzando sia la visualizzazione di monitoraggio aggregato che il monitoraggio tra più servizi.

## Introduzione {#getting-started}

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Flussi di dati](../home.md): I flussi di dati sono una rappresentazione dei processi di trasferimento dei dati in Platform. I flussi di dati sono configurati su diversi servizi e consentono di spostare i dati dai connettori di origine ai set di dati di destinazione, fino a [!DNL Identity] e [!DNL Profile]e a [!DNL Destinations].
   * [Corse del flusso di dati](../../sources/notifications.md): Le esecuzioni dei flussi di dati sono i processi pianificati ricorrenti in base alla configurazione della frequenza dei flussi di dati selezionati.
* [Origini](../../sources/home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Servizio identità](../../identity-service/home.md): Ottieni una visione migliore dei singoli clienti e del loro comportamento attraverso il collegamento delle identità tra dispositivi e sistemi.
* [Profilo cliente in tempo reale](../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Vista di monitoraggio aggregato {#aggregated-monitoring-view}

>[!CONTEXTUALHELP]
>id="platform_monitoring_source_ingestion"
>title="Acquisizione sorgente"
>abstract="L&#39;elaborazione delle origini contiene informazioni sullo stato e le metriche dell&#39;attività dati nel servizio data lake, compresi i record acquisiti e i record non riusciti. Consulta la guida alla definizione delle metriche per ulteriori informazioni su metriche e grafici."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_ingestion"
>title="Dettagli dell&#39;esecuzione del dataflow"
>abstract="L&#39;elaborazione delle origini contiene informazioni sullo stato e le metriche dell&#39;attività dati nel servizio data lake, compresi i record acquisiti e i record non riusciti. Consulta la guida alla definizione delle metriche per ulteriori informazioni su metriche e grafici."
>text="Learn more in documentation"

In [Interfaccia utente della piattaforma](https://platform.adobe.com), seleziona **[!UICONTROL Monitoraggio]** dalla navigazione a sinistra per accedere al [!UICONTROL Monitoraggio] dashboard. La [!UICONTROL Monitoraggio] dashboard contiene metriche e informazioni su tutti i flussi di dati di origine, comprese informazioni sullo stato del traffico dei dati da un’origine a [!DNL Identity Service]e a [!DNL Profile].

Al centro del dashboard è [!UICONTROL Acquisizione sorgente] , che contiene metriche e grafici che visualizzano dati sui record acquisiti e record non riusciti.

![dashboard di monitoraggio](../assets/ui/monitor-sources/monitoring-dashboard.png)

Per impostazione predefinita, i dati visualizzati contengono i tassi di acquisizione delle ultime 24 ore. Seleziona **[!UICONTROL Ultime 24 ore]** per regolare l&#39;intervallo di tempo dei record visualizzati.

![cambia data](../assets/ui/monitor-sources/change-date.png)

Viene visualizzata una finestra a comparsa del calendario che fornisce le opzioni per l’inserimento di intervalli di tempo alternativi. Seleziona **[!UICONTROL Ultimi 30 giorni]** quindi seleziona **[!UICONTROL Applica]**

![regolazione del tempo](../assets/ui/monitor-sources/adjust-timeframe.png)

I grafici sono attivati per impostazione predefinita ed è possibile disattivarli per espandere l&#39;elenco delle origini riportate di seguito. Seleziona la **[!UICONTROL Metriche e grafici]** per disattivare i grafici.

![metriche e grafici](../assets/ui/monitor-sources/metrics-graphs.png)

| Acquisizione sorgente | Descrizione |
| ---------------- | ----------- |
| [!UICONTROL Record acquisiti ] | Numero totale di record acquisiti. |
| [!UICONTROL Record non elaborati] | Numero totale di record che non sono stati acquisiti a causa di errori nei dati. |
| [!UICONTROL Totale flussi di dati non riusciti] | Il numero totale di flussi di dati con un `failed` stato. |

Nell’elenco di acquisizione di origine sono visualizzate tutte le origini che contengono almeno un account esistente. L’elenco include inoltre informazioni sul tasso di acquisizione di ogni origine, sul numero di record con errore e sul numero totale di flussi di dati con errore in base all’intervallo di tempo applicato.

![acquisizione di origine](../assets/ui/monitor-sources/source-ingestion.png)

Per ordinare l&#39;elenco delle origini, selezionare **[!UICONTROL Le mie fonti]** quindi seleziona la categoria scelta dal menu a discesa. Ad esempio, per concentrarti sugli archivi cloud, seleziona  **[!UICONTROL archiviazione cloud]**

![ordinabile per categoria](../assets/ui/monitor-sources/sort-by-category.png)

Per visualizzare tutti i flussi di dati esistenti in tutte le origini, seleziona **[!UICONTROL Flussi di dati]**.

![view-all-dataflows](../assets/ui/monitor-sources/view-all-dataflows.png)

In alternativa, è possibile inserire una sorgente nella barra di ricerca per isolare una singola sorgente. Una volta identificata la sorgente, seleziona l’icona del filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto a per visualizzare un elenco dei relativi flussi di dati attivi.

![ricerca](../assets/ui/monitor-sources/search.png)

Viene visualizzato un elenco di flussi di dati. Per restringere l’elenco e concentrarsi sui flussi di dati con errori, seleziona **[!UICONTROL Mostra solo errori]**.

![show-failed-only](../assets/ui/monitor-sources/show-failures-only.png)

Individua il flusso di dati da monitorare, quindi seleziona l’icona del filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto a esso, per visualizzare ulteriori informazioni sullo stato di esecuzione.

![flusso dati](../assets/ui/monitor-sources/dataflow.png)

La pagina di esecuzione del flusso di dati visualizza informazioni sulla data di inizio dell’esecuzione del flusso di dati, sulle dimensioni dei dati, sullo stato e sulla relativa durata del tempo di elaborazione. Seleziona l’icona del filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto all’ora di avvio del flusso di dati per visualizzare i dettagli dell’esecuzione del flusso di dati.

![dataflow-run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

La [!UICONTROL Dettagli dell&#39;esecuzione del dataflow] In questa pagina sono visualizzate informazioni sui metadati del flusso di dati, sullo stato di acquisizione parziale e sul riepilogo degli errori. Il riepilogo degli errori contiene lo specifico errore di livello principale che mostra in quale fase il processo di acquisizione ha rilevato un errore.

Scorri verso il basso per visualizzare informazioni più specifiche sull’errore che si è verificato.

![dataflow-run-details](../assets/ui/monitor-sources/dataflow-run-details.png)

La [!UICONTROL Errori di esecuzione del flusso di dati] Il pannello visualizza l’errore e il codice di errore specifici che hanno causato un errore di inserimento del flusso di dati. In questo scenario, si è verificato un errore di trasformazione di mappatura, con conseguente errore di 24 record.

Seleziona **[!UICONTROL File]** per ulteriori informazioni.

![errori di esecuzione del flusso di dati](../assets/ui/monitor-sources/dataflow-run-errors.png)

La [!UICONTROL File] contiene informazioni sul nome e il percorso del file.

Per una rappresentazione più granulare dell’errore, seleziona **[!UICONTROL Anteprima della diagnostica degli errori]**.

![file](../assets/ui/monitor-sources/files.png)

La [!UICONTROL Anteprima diagnostica errori] viene visualizzata una finestra in cui è visualizzata un&#39;anteprima di un massimo di 100 errori nel flusso di dati. È possibile selezionare **[!UICONTROL Scarica]** per recuperare un comando curl, che consente di scaricare la diagnostica dell&#39;errore.

Al termine, seleziona **[!UICONTROL Chiudi]**

![diagnostica degli errori](../assets/ui/monitor-sources/error-diagnostics.png)

Puoi usare il sistema di breadcrumb nell’intestazione superiore per tornare alla [!UICONTROL Monitoraggio] dashboard. Seleziona **[!UICONTROL Inizio esecuzione: 14/02/2021, 19:47]** per tornare alla pagina precedente, quindi seleziona **[!UICONTROL Flusso di dati: Demo di acquisizione dati fedeltà - Non riuscito]** per tornare alla pagina dei flussi di dati.

![breadcrumb](../assets/ui/monitor-sources/breadcrumbs.png)

## Monitoraggio interservizi {#cross-service-monitoring}

La parte superiore del dashboard contiene una rappresentazione del flusso di acquisizione dal livello di origine a [!DNL Identity Service]e a [!DNL Profile]. Ogni cella include un marcatore punto che indica la presenza di errori che si sono verificati in quella fase di acquisizione. Un punto verde indica un’acquisizione senza errori, mentre un punto rosso indica che si è verificato un errore in quel particolare passaggio di acquisizione.

![monitoraggio incrociato](../assets/ui/monitor-sources/cross-service-monitoring.png)

Dalla pagina dei flussi di dati, individua un flusso di dati di successo e seleziona l’icona del filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto a esso, per visualizzare le informazioni di esecuzione del flusso di dati.

![dataflow-success](../assets/ui/monitor-sources/dataflow-success.png)

La [!UICONTROL Acquisizione sorgente] La pagina contiene informazioni che confermano il corretto inserimento del flusso di dati. Da qui, puoi iniziare a monitorare il percorso del flusso di dati dal livello di origine a [!DNL Identity Service]e quindi a [!DNL Profile].

Seleziona **[!UICONTROL Identità]** per visualizzare l’acquisizione in [!UICONTROL Identità] stadio.

![origini](../assets/ui/monitor-sources/sources.png)

### [!DNL Identity] metriche {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="Elaborazione identità"
>abstract="L’elaborazione delle identità contiene informazioni sui record acquisiti nel servizio Identity, tra cui il numero di identità aggiunte, i grafici creati e i grafici aggiornati. Consulta la guida alla definizione delle metriche per ulteriori informazioni su metriche e grafici."
>text="Learn more in documentation"

La [!UICONTROL Elaborazione identità] contiene informazioni sui record acquisiti in [!DNL Identity Service], compreso il numero di identità aggiunte, i grafici creati e i grafici aggiornati.

Seleziona l’icona del filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto all&#39;ora di avvio del flusso di dati per visualizzare ulteriori informazioni sul [!DNL Identity] esecuzione del flusso di dati.

![identità](../assets/ui/monitor-sources/identities.png)

| Metriche di identità | Descrizione |
| ---------------- | ----------- |
| [!UICONTROL Record ricevuti] | Numero di record ricevuti da [!DNL Data Lake]. |
| [!UICONTROL Record non elaborati] | Il numero di record che non sono stati acquisiti in Platform a causa di errori nei dati. |
| [!UICONTROL Record saltati] | Il numero di record acquisiti, ma non in [!DNL Identity Service] perché nella riga record era presente un solo identificatore. |
| [!UICONTROL Record acquisiti] | Il numero di record acquisiti in [!DNL Identity Service]. |
| [!UICONTROL Record totali] | Il conteggio totale di tutti i record, compresi i record non riusciti, i record saltati, [!DNL Identities] record aggiunti e duplicati. |
| [!UICONTROL Identità aggiunte] | Numero di nuovi identificatori netti aggiunti a [!DNL Identity Service]. |
| [!UICONTROL Grafici creati] | Numero di nuovi grafici di identità netti creati in [!DNL Identity Service]. |
| [!UICONTROL Grafici aggiornati] | Numero di grafici di identità esistenti aggiornati con nuovi bordi. |
| [!UICONTROL Esecuzione del flusso di dati non riuscita] | Numero di esecuzioni del flusso di dati che non sono riuscite. |
| [!UICONTROL Tempo di elaborazione] | La marca temporale dall’inizio dell’acquisizione al completamento. |
| [!UICONTROL Stato] | Definisce lo stato generale di un flusso di dati. I possibili valori di stato sono: <ul><li>`Success`: Indica che un flusso di dati è attivo e sta acquisendo i dati in base alla pianificazione fornita.</li><li>`Failed`: Indica che il processo di attivazione di un flusso di dati è stato interrotto a causa di errori. </li><li>`Processing`: Indica che il flusso di dati non è ancora attivo. Questo stato viene spesso rilevato immediatamente dopo la creazione di un nuovo flusso di dati.</li></ul> |

La [!UICONTROL Dettagli dell&#39;esecuzione del dataflow] visualizza ulteriori informazioni sul [!DNL Identity] esecuzione del flusso di dati, compreso l’ID organizzazione IMS e l’ID di esecuzione del flusso di dati. In questa pagina vengono visualizzati anche il codice di errore e il messaggio di errore corrispondenti forniti da [!DNL Identity Service], in caso di errori nel processo di acquisizione.

Seleziona **[!UICONTROL Inizio esecuzione: 14/02/2021, 19:47]** per tornare alla pagina precedente.

![identity-dataflow-run](../assets/ui/monitor-sources/identities-dataflow-run.png)

Da [!UICONTROL Elaborazione identità] pagina, seleziona **[!UICONTROL Profili]** per visualizzare lo stato dell&#39;acquisizione dei record nel [!UICONTROL Profili] stadio.

![select-profiles](../assets/ui/monitor-sources/select-profiles.png)

### [!DNL Profile] metriche {#profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profile_processing"
>title="Elaborazione del profilo"
>abstract="L’elaborazione del profilo contiene informazioni sui record acquisiti nel servizio Profilo, tra cui il numero di frammenti di profilo creati, i frammenti di profilo aggiornati e il numero totale di frammenti di profilo."
>text="Learn more in documentation"

La [!UICONTROL Elaborazione del profilo] contiene informazioni sui record acquisiti in [!DNL Profile], compreso il numero di frammenti di profilo creati, i frammenti di profilo aggiornati e il numero totale di frammenti di profilo.

Seleziona l’icona del filtro ![filter](../assets/ui/monitor-sources/filter.png) accanto all&#39;ora di avvio del flusso di dati per visualizzare ulteriori informazioni sul [!DNL Profile] esecuzione del flusso di dati.

![profiles](../assets/ui/monitor-sources/profiles.png)

| Metriche del profilo | Descrizione |
| --------------- | ----------- |
| [!UICONTROL Record ricevuti] | Numero di record ricevuti da [!DNL Data Lake]. |
| [!UICONTROL Record non elaborati ] | Il numero di record acquisiti, ma non in [!DNL Profile] a causa di errori. |
| [!UICONTROL Frammenti di profilo aggiunti] | Numero di nuove reti [!DNL Profile] frammenti aggiunti. |
| [!UICONTROL Frammenti di profilo aggiornati] | Numero di [!DNL Profile] frammenti aggiornati |
| [!UICONTROL Frammenti di profilo totali] | Numero totale di record scritti in [!DNL Profile], compresi tutti gli [!DNL Profile] frammenti aggiornati e nuovi [!DNL Profile] frammenti creati. |
| [!UICONTROL Esecuzione del flusso di dati non riuscita] | Numero di esecuzioni del flusso di dati che non sono riuscite. |
| [!UICONTROL Tempo di elaborazione] | La marca temporale dall’inizio dell’acquisizione al completamento. |
| [!UICONTROL Stato] | Definisce lo stato generale di un flusso di dati. I possibili valori di stato sono: <ul><li>`Success`: Indica che un flusso di dati è attivo e sta acquisendo i dati in base alla pianificazione fornita.</li><li>`Failed`: Indica che il processo di attivazione di un flusso di dati è stato interrotto a causa di errori. </li><li>`Processing`: Indica che il flusso di dati non è ancora attivo. Questo stato viene spesso rilevato immediatamente dopo la creazione di un nuovo flusso di dati.</li></ul> |

La [!UICONTROL Dettagli dell&#39;esecuzione del dataflow] visualizza ulteriori informazioni sul [!DNL Profile] esecuzione del flusso di dati, compreso l’ID organizzazione IMS e l’ID di esecuzione del flusso di dati. In questa pagina vengono visualizzati anche il codice di errore e il messaggio di errore corrispondenti forniti da [!DNL Profile], in caso di errori nel processo di acquisizione.

![profiles-dataflow-run](../assets/ui/monitor-sources/profiles-dataflow-run.png)

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai monitorato correttamente il flusso di dati di acquisizione dal livello di origine a [!DNL Identity Service]e a [!DNL Profile], utilizzando **[!UICONTROL Monitoraggio]** dashboard. Hai inoltre identificato con successo gli errori che hanno contribuito al fallimento dei flussi di dati durante il processo di acquisizione. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica del profilo cliente in tempo reale](../../profile/home.md)
* [Panoramica di Data Science Workspace](../../data-science-workspace/home.md)
