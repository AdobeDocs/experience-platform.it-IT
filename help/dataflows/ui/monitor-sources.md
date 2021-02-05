---
keywords: ' Experience Platform;home;argomenti popolari;monitorare account;monitorare flussi di dati;flussi di dati;origini'
description: I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per visualizzare i flussi di dati esistenti dall'area di lavoro Origini.
solution: Experience Platform
title: Monitorare i flussi di dati per le origini nell'interfaccia utente
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: f8186e467dc982003c6feb01886ed16d23572955
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 1%

---


# Monitorare i flussi di dati per le sorgenti nell’interfaccia utente

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per visualizzare i flussi di dati esistenti dall&#39;area di lavoro [!UICONTROL Sources].

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Origini](../../sources/home.md):  [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
- [Sandbox](../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

## Monitorare i flussi di dati

Accedete all&#39;interfaccia utente del Experience Platform [](https://platform.adobe.com), quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Sources]. Selezionare **[!UICONTROL Dataflows]** dall&#39;intestazione superiore per visualizzare i flussi di dati esistenti.

![catalog-dataflows](../assets/ui/monitor-sources/catalog-dataflows.png)

Viene visualizzato un elenco dei flussi di dati esistenti. In questa pagina è presente un elenco di flussi di dati visualizzabili, con informazioni sull’origine, il nome utente, il numero di flussi di dati e lo stato.

Per ulteriori informazioni sugli stati, vedere la tabella seguente:

| Stato | Descrizione |
| ------ | ----------- |
| Abilitata | Lo stato `Enabled` indica che un flusso di dati è attivo e sta acquisendo i dati in base alla pianificazione fornita. |
| Disabilitata | Lo stato `Disabled` indica che un flusso di dati è inattivo e non sta acquisendo alcun dato. |
| Elaborazione | Lo stato `Processing` indica che un flusso di dati non è ancora attivo. Questo stato si verifica spesso subito dopo la creazione di un nuovo flusso di dati. |
| Errore | Lo stato `Error` indica che il processo di attivazione di un flusso di dati è stato interrotto. |

Selezionate l’icona funnel in alto a sinistra per ordinare i dati.

![elenco dei flussi di dati](../assets/ui/monitor-sources/dataflows-list.png)

Viene visualizzato il pannello di ordinamento. Selezionate la sorgente a cui desiderate accedere dal menu di scorrimento e selezionate il flusso di dati dall’elenco a destra. È inoltre possibile selezionare il pulsante con le ellissi (`...`) per visualizzare ulteriori opzioni disponibili per il flusso di dati selezionato.

![sort-dataflows](../assets/ui/monitor-sources/dataflows-sort.png)

La pagina **[!UICONTROL Dataflow activity]** contiene dettagli sul numero di record ingeriti e di record non riusciti, nonché informazioni sullo stato del flusso di dati e sui tempi di elaborazione. Selezionate l’icona del calendario sopra il flusso di dati per regolare l’intervallo di tempo dei record di assimilazione.

![datflow-activity](../assets/ui/monitor-sources/dataflow-activity.png)

Il calendario consente di visualizzare i diversi intervalli di tempo per i record acquisiti. Potete scegliere una delle due opzioni preimpostate &quot;[!UICONTROL Last 7 days]&quot; o &quot;[!UICONTROL Last 30 days]&quot;. In alternativa, potete impostare un intervallo di tempo personalizzato utilizzando il calendario. Selezionare l&#39;intervallo di tempo desiderato e selezionare **[!UICONTROL Apply]** per continuare.

![flow-Calendar](../assets/ui/monitor-sources/flow-calendar.png)

Per impostazione predefinita, il **[!UICONTROL Dataflow activity]** visualizza il pannello **[!UICONTROL Properties]** associato al flusso di dati. Selezionare l&#39;esecuzione del flusso dall&#39;elenco per visualizzare i metadati associati, incluse le informazioni sul relativo ID di esecuzione univoco.

Selezionare **[!UICONTROL Dataflow run start]** per accedere al **[!UICONTROL Dataflow run overview]**.

![run](../assets/ui/monitor-sources/run-metadata.png)

Il **[!UICONTROL Dataflow run overview]** visualizza informazioni sul flusso di dati, inclusi i metadati, lo stato di assimilazione parziale e la soglia di errore assegnata. L&#39;intestazione superiore include anche un riepilogo degli errori. Il **[!UICONTROL Error summary]** contiene l&#39;errore di livello principale specifico che mostra in quale fase il processo di assimilazione ha rilevato un errore.

![dataflow-run-overview](../assets/ui/monitor-sources/dataflow-run-overview.png)

Fare riferimento alla tabella seguente per gli errori che è possibile visualizzare in **[!UICONTROL Error summary]**.

| Errore | Descrizione |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Errore durante la copia dei dati da un&#39;origine. |
| `CONNECTOR-2001-500` | Errore durante l&#39;elaborazione dei dati copiati su [!DNL Platform]. Questo errore può riguardare l&#39;analisi, la convalida o la trasformazione. |

La metà inferiore dello schermo contiene informazioni su **[!UICONTROL Dataflow run errors]**. Da qui, potete anche visualizzare i file acquisiti, visualizzare in anteprima e scaricare la diagnostica degli errori, oppure scaricare il file manifesto.

Nella sezione **[!UICONTROL Dataflow run errors]** viene visualizzato il codice di errore, il numero di record non riusciti e le informazioni che descrivono l&#39;errore.

Selezionare **[!UICONTROL Preview error diagnostics]** per visualizzare ulteriori informazioni sull&#39;errore di inserimento.

![Errori di esecuzione dei dataflow](../assets/ui/monitor-sources/dataflow-run-errors.png)

Viene visualizzato il pannello **[!UICONTROL Error diagnostics preview]**. In questa schermata vengono visualizzate informazioni specifiche relative all&#39;errore di inserimento, incluso il nome del file, il codice di errore, il nome della colonna in cui si è verificato l&#39;errore e una descrizione dell&#39;errore.

Questa sezione include anche un&#39;anteprima della colonna che contiene l&#39;errore.

>[!IMPORTANT]
>
>Per abilitare **[!UICONTROL Error diagnostics preview]** è necessario attivare **[!UICONTROL Partial ingestion]** e **[!UICONTROL Error diagnostics]** durante la configurazione di un flusso di dati. In questo modo il sistema potrà eseguire la scansione di tutti i record acquisiti durante l&#39;esecuzione del flusso.

![Anteprima-errore-diagnostica](../assets/ui/monitor-sources/preview-error-diagnostics.png)

Dopo aver visualizzato l&#39;anteprima degli errori, potete selezionare **[!UICONTROL Download]** dal pannello **[!UICONTROL dataflow runs overview]** per accedere alla diagnostica completa degli errori e scaricare il file manifesto. Per ulteriori informazioni, consultare i documenti relativi alla [diagnostica degli errori](../../ingestion/batch-ingestion/partial.md#retrieve-errors) e al [download dei metadati](../../ingestion/batch-ingestion/partial.md#download-metadata).

![Anteprima-errore-diagnostica](../assets/ui/monitor-sources/download.png)

Per ulteriori informazioni sul monitoraggio dei flussi di dati e sull&#39;assimilazione, fare riferimento all&#39;esercitazione sul [monitoraggio dei flussi di dati ](../../ingestion/quality/monitor-data-ingestion.md).

## Passaggi successivi

Seguendo questa esercitazione, è stato possibile accedere agli account e ai flussi di dati esistenti dall&#39;area di lavoro **[!UICONTROL Sources]**. I dati in entrata possono ora essere utilizzati dai servizi a valle [!DNL Platform] quali [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i documenti seguenti:

- [Panoramica del profilo cliente in tempo reale](../../profile/home.md)
- [Panoramica di Analysis Workspace](../../data-science-workspace/home.md)
