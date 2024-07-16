---
title: Acquisizione su richiesta per flussi di dati di origini nell’interfaccia utente
description: Scopri come creare flussi di dati on-demand per le connessioni sorgente utilizzando l’interfaccia utente di Experience Platform.
exl-id: e5a70044-2484-416a-8098-48e6d99c2d98
source-git-commit: 38da1c1d5e563ea3f66cc25a69ad726f709784d0
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---

# Acquisizione su richiesta per i flussi di dati di origine nell’interfaccia utente

Puoi utilizzare l’acquisizione su richiesta per attivare un’iterazione di esecuzione del flusso di un flusso di dati esistente utilizzando l’area di lavoro origini nell’interfaccia utente di Adobe Experience Platform.

In questo documento vengono descritti i passaggi per la creazione di flussi di dati su richiesta per le origini, nonché i tentativi di esecuzione di flussi elaborati o non riusciti.

>[!BEGINSHADEBOX]

**Cos&#39;è un&#39;esecuzione di flusso?**

Le esecuzioni del flusso rappresentano un’istanza dell’esecuzione del flusso di dati. Ad esempio, se un flusso di dati è pianificato per essere eseguito ogni ora alle 09:00, alle 00:00 e alle 00:00, sono disponibili tre istanze di un flusso. Le esecuzioni del flusso sono specifiche per la tua particolare organizzazione.

>[!ENDSHADEBOX]

## Introduzione

>[!NOTE]
>
>Per creare un’esecuzione del flusso, devi innanzitutto disporre dell’ID di flusso di un flusso di dati pianificato per l’acquisizione una tantum.

Questo documento richiede una buona conoscenza dei seguenti elementi di Experience Platform:

* [Origini](../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Flussi dati](../../../dataflows/home.md): un flusso di dati è una rappresentazione dei processi di dati che spostano i dati in Platform. I flussi di dati sono configurati tra servizi diversi, consentendo di spostare i dati dai connettori di origine ai set di dati di destinazione, al servizio Identity, al profilo cliente in tempo reale e alle destinazioni.
* [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Creare un flusso di dati su richiesta {#create-a-dataflow-on-demand}

Passa alla scheda *[!UICONTROL Flussi dati]* dell&#39;area di lavoro origini. Da qui, individua il flusso di dati che desideri eseguire su richiesta, quindi seleziona i puntini di sospensione (**`...`**) accanto al nome del flusso di dati.

![Elenco di flussi di dati nell&#39;area di lavoro di origine.](../../images/tutorials/on-demand/select-dataflow.png)

Selezionare **[!UICONTROL Esegui su richiesta]** dal menu a discesa visualizzato.

![Menu a discesa con l&#39;opzione Esegui su richiesta selezionata.](../../images/tutorials/on-demand/run-on-demand.png)

Configura la pianificazione dell’acquisizione on-demand. Seleziona l&#39;**[!UICONTROL Ora di inizio acquisizione]**, l&#39;**[!UICONTROL Ora di inizio intervallo date]** e l&#39;**[!UICONTROL Ora di fine intervallo date]**.

| Configurazione pianificazione | Descrizione |
| --- | --- |
| [!UICONTROL Ora di inizio acquisizione] | L’ora programmata di inizio dell’esecuzione del flusso su richiesta. |
| [!UICONTROL Ora di inizio intervallo di date] | La prima data e ora da cui verranno recuperati i dati. |
| [!UICONTROL Data e ora di fine intervallo] | La data e l’ora in cui i dati verranno recuperati. |

Seleziona **[!UICONTROL Pianifica]** e attendi alcuni istanti per l&#39;attivazione del flusso di dati on-demand.

![Finestra di configurazione della pianificazione per l&#39;acquisizione su richiesta.](../../images/tutorials/on-demand/configure-schedule.png)

Seleziona il nome del flusso di dati per visualizzare l’attività del flusso di dati. Qui verrà visualizzato un elenco delle esecuzioni del flusso di dati che sono state elaborate. Seleziona un&#39;esecuzione del flusso di dati, quindi seleziona **[!UICONTROL Riprova]** dalla barra a destra per riprovare l&#39;acquisizione per un&#39;iterazione di esecuzione del flusso di dati selezionata.

![Un elenco di flussi elaborati viene eseguito per un flusso di dati selezionato.](../../images/tutorials/on-demand/processed.png)

Seleziona **[!UICONTROL Pianificato]** per visualizzare un elenco di esecuzioni del flusso di dati pianificate per l&#39;acquisizione futura.

![Un elenco di flussi pianificati viene eseguito per un flusso di dati selezionato.](../../images/tutorials/on-demand/scheduled.png)

## Passaggi successivi

Dopo aver letto questo documento, hai imparato a creare flussi eseguiti su richiesta per flussi di dati di origini esistenti. Per ulteriori informazioni sulle origini, leggere la [panoramica delle origini](../../home.md)
