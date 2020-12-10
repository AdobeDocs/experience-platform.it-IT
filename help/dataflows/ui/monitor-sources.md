---
keywords: Experience Platform;home;popular topics;monitor accounts;monitor dataflows;dataflows;sources
description: I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per visualizzare i flussi di dati esistenti dall'area di lavoro Origini.
solution: Experience Platform
title: Monitorare i flussi di dati
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 4d99526a592e173e3b46e1fa2a3f869b1fe5d4f2
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 1%

---


# Monitorare i flussi di dati per le sorgenti nell’interfaccia utente

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per visualizzare i flussi di dati esistenti dall&#39; [!UICONTROL Sources] area di lavoro.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Origini](../../sources/home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] i servizi.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

## Monitorare i flussi di dati

Accedete all&#39;interfaccia utente [del Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dal menu di navigazione a sinistra per accedere all&#39; [!UICONTROL Sources] area di lavoro. Selezionate **[!UICONTROL Dataflows]** dall’intestazione superiore per visualizzare i flussi di dati esistenti.

![catalog-dataflows](../assets/ui/monitor-sources/catalog-dataflows.png)

Viene visualizzato un elenco dei flussi di dati esistenti. In questa pagina è presente un elenco di flussi di dati visualizzabili, con informazioni sull’origine, il nome utente, il numero di flussi di dati e lo stato.

Per ulteriori informazioni sugli stati, vedere la tabella seguente:

| Stato | Descrizione |
| ------ | ----------- |
| Abilitata | Lo `Enabled` stato indica che un flusso di dati è attivo e che sta acquisendo i dati in base alla pianificazione fornita. |
| Disabilitata | Lo `Disabled` stato indica che un flusso di dati è inattivo e non sta acquisendo alcun dato. |
| Elaborazione | Lo `Processing` stato indica che un flusso di dati non è ancora attivo. Questo stato si verifica spesso subito dopo la creazione di un nuovo flusso di dati. |
| Errore | Lo `Error` stato indica che il processo di attivazione di un flusso di dati è stato interrotto. |

Selezionate l’icona funnel in alto a sinistra per ordinare i dati.

![elenco dei flussi di dati](../assets/ui/monitor-sources/dataflows-list.png)

Viene visualizzato il pannello di ordinamento. Selezionate la sorgente a cui desiderate accedere dal menu di scorrimento e selezionate il flusso di dati dall’elenco a destra. È inoltre possibile selezionare il pulsante`...`con le ellissi per visualizzare ulteriori opzioni disponibili per il flusso di dati selezionato.

![sort-dataflows](../assets/ui/monitor-sources/dataflows-sort.png)

La **[!UICONTROL Dataflow activity]** pagina contiene dettagli sul numero di record acquisiti e di record non riusciti, nonché informazioni sullo stato del flusso di dati e sui tempi di elaborazione. Selezionate l’icona del calendario sopra il flusso di dati per regolare l’intervallo di tempo dei record di assimilazione.

![datflow-activity](../assets/ui/monitor-sources/dataflow-activity.png)

Il calendario consente di visualizzare i diversi intervalli di tempo per i record acquisiti. Potete scegliere una delle due opzioni preimpostate &quot;[!UICONTROL Last 7 days]&quot; o &quot;[!UICONTROL Last 30 days]&quot;. In alternativa, potete impostare un intervallo di tempo personalizzato utilizzando il calendario. Selezionare l&#39;intervallo di tempo desiderato e selezionare **[!UICONTROL Apply]** per continuare.

![flow-Calendar](../assets/ui/monitor-sources/flow-calendar.png)

Per impostazione predefinita, **[!UICONTROL Dataflow activity]** visualizza il **[!UICONTROL Properties]** pannello associato al flusso di dati. Selezionare l&#39;esecuzione del flusso dall&#39;elenco per visualizzare i metadati associati, incluse le informazioni sul relativo ID di esecuzione univoco.

Selezionate **[!UICONTROL Dataflow run start]** per accedere al **[!UICONTROL Dataflow run overview]**.

![run](../assets/ui/monitor-sources/run-metadata.png)

Il **[!UICONTROL Dataflow run overview]** file visualizza informazioni sul flusso di dati, inclusi i relativi metadati, lo stato di inserimento parziale e la soglia di errore assegnata. L&#39;intestazione superiore include anche un riepilogo degli errori. Il **[!UICONTROL Error summary]** contiene l&#39;errore di livello principale specifico che mostra in quale fase il processo di assimilazione ha rilevato un errore.

![dataflow-run-overview](../assets/ui/monitor-sources/dataflow-run-overview.png)

Fare riferimento alla tabella seguente per gli errori che è possibile visualizzare nella **[!UICONTROL Error summary]**.

| Errore | Descrizione |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Errore durante la copia dei dati da un&#39;origine. |
| `CONNECTOR-2001-500` | Errore durante l&#39;elaborazione dei dati copiati in [!DNL Platform]. Questo errore può riguardare l&#39;analisi, la convalida o la trasformazione. |

La metà inferiore dello schermo contiene informazioni su **[!UICONTROL Dataflow run errors]**. Da qui, potete anche visualizzare i file acquisiti, visualizzare in anteprima e scaricare la diagnostica degli errori, oppure scaricare il file manifesto.

Nella **[!UICONTROL Dataflow run errors]** sezione sono visualizzati il codice di errore, il numero di record con errore e le informazioni che descrivono l&#39;errore.

Selezionate **[!UICONTROL Preview error diagnostics]** per visualizzare ulteriori informazioni sull’errore di inserimento.

![Errori di esecuzione dei dataflow](../assets/ui/monitor-sources/dataflow-run-errors.png)

Viene visualizzato il **[!UICONTROL Error diagnostics preview]** pannello. In questa schermata vengono visualizzate informazioni specifiche relative all&#39;errore di inserimento, incluso il nome del file, il codice di errore, il nome della colonna in cui si è verificato l&#39;errore e una descrizione dell&#39;errore.

Questa sezione include anche un&#39;anteprima della colonna che contiene l&#39;errore.

>[!IMPORTANT]
>
>Per abilitare **[!UICONTROL Error diagnostics preview]** è necessario attivare **[!UICONTROL Partial ingestion]** e **[!UICONTROL Error diagnostics]** durante la configurazione di un flusso di dati. In questo modo il sistema potrà eseguire la scansione di tutti i record acquisiti durante l&#39;esecuzione del flusso.

![Anteprima-errore-diagnostica](../assets/ui/monitor-sources/preview-error-diagnostics.png)

Dopo aver visualizzato l’anteprima degli errori, potete selezionare **[!UICONTROL Download]** dal **[!UICONTROL dataflow runs overview]** pannello per accedere alla diagnostica completa degli errori e scaricare il file manifesto. Per ulteriori informazioni, consultate i documenti sulla diagnostica [degli](../../ingestion/batch-ingestion/partial.md#retrieve-errors) errori e [il download dei metadati](../../ingestion/batch-ingestion/partial.md#download-metadata) .

![Anteprima-errore-diagnostica](../assets/ui/monitor-sources/download.png)

Per ulteriori informazioni sul monitoraggio dei flussi di dati e sull’assimilazione, consulta l’esercitazione sul [monitoraggio dei flussi di dati](../../ingestion/quality/monitor-data-ingestion.md).

## Passaggi successivi

Seguendo questa esercitazione, è stato possibile accedere agli account e ai flussi di dati esistenti dall&#39; **[!UICONTROL Sources]** area di lavoro. I dati in entrata possono ora essere utilizzati dai [!DNL Platform] servizi a valle come [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i documenti seguenti:

- [Panoramica del profilo cliente in tempo reale](../../profile/home.md)
- [Panoramica di Analysis Workspace](../../data-science-workspace/home.md)
