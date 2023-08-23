---
title: Acquisizione su richiesta per flussi di dati di origini nell’interfaccia utente
description: Scopri come creare flussi di dati on-demand per le connessioni sorgente utilizzando l’interfaccia utente di Experienci Platform.
source-git-commit: ce1e6c08d1e53346c11f9746cea524689f402031
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---

# Acquisizione su richiesta per i flussi di dati di origine nell’interfaccia utente

Puoi utilizzare l’acquisizione su richiesta per attivare un’iterazione di esecuzione del flusso di un flusso di dati esistente utilizzando l’area di lavoro origini nell’interfaccia utente di Adobe Experience Platform.

In questo documento vengono descritti i passaggi per la creazione di flussi di dati su richiesta per le origini, nonché i tentativi di esecuzione di flussi elaborati o non riusciti.

>[!BEGINSHADEBOX]

**Che cos&#39;è un&#39;esecuzione di flusso?**

Le esecuzioni del flusso rappresentano un’istanza dell’esecuzione del flusso di dati. Ad esempio, se un flusso di dati è pianificato per essere eseguito ogni ora alle 09:00, alle 00:00 e alle 00:00, sono disponibili tre istanze di un flusso. Le esecuzioni del flusso sono specifiche per la tua particolare organizzazione.

>[!ENDSHADEBOX]

## Introduzione

Questo documento richiede una buona conoscenza dei seguenti elementi di Experience Platform:

* [Sorgenti](../../home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Flussi dati](../../../dataflows/home.md): un flusso di dati è una rappresentazione dei processi di dati che spostano i dati in Platform. I flussi di dati sono configurati tra servizi diversi, consentendo di spostare i dati dai connettori di origine ai set di dati di destinazione, al servizio Identity, al profilo cliente in tempo reale e alle destinazioni.
* [Sandbox](../../../sandboxes/home.md): Experienci Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Creare un flusso di dati su richiesta {#create-a-dataflow-on-demand}

Accedi a *[!UICONTROL Flussi dati]* dell&#39;area di lavoro origini. Da qui, individua il flusso di dati che desideri eseguire su richiesta, quindi seleziona i puntini di sospensione (**`...`**) accanto al nome del flusso di dati.

![Elenco di flussi di dati nell’area di lavoro delle origini.](../../images/tutorials/on-demand/select-dataflow.png)

Quindi, seleziona **[!UICONTROL Esegui su richiesta]** dal menu a discesa visualizzato.

![Un menu a discesa con l’opzione Esegui su richiesta selezionata.](../../images/tutorials/on-demand/run-on-demand.png)

Configura la pianificazione dell’acquisizione on-demand. Seleziona la **[!UICONTROL Ora di inizio acquisizione]**, il **[!UICONTROL Ora di inizio intervallo di date]** e **[!UICONTROL Ora di fine intervallo di date]**.

| Configurazione pianificazione | Descrizione |
| --- | --- |
| [!UICONTROL Ora di inizio acquisizione] | L’ora di inizio pianificata in UTC di quando inizierà il flusso di dati su richiesta. |
| [!UICONTROL Ora di inizio intervallo di date] | La data e l’ora di inizio da cui i dati verranno estratti. |
| [!UICONTROL Ora di fine intervallo di date] | La data e l’ora di fine a partire dalle quali i dati verranno estratti. |

Seleziona **[!UICONTROL Pianificazione]** e attendi alcuni istanti per l’attivazione del flusso di dati on-demand.

![Finestra di configurazione della pianificazione per l’acquisizione su richiesta.](../../images/tutorials/on-demand/configure-schedule.png)

Seleziona il nome del flusso di dati per visualizzare l’attività del flusso di dati. Qui verrà visualizzato un elenco delle esecuzioni del flusso di dati che sono state elaborate. Seleziona un’esecuzione del flusso di dati, quindi seleziona **[!UICONTROL Riprova]** dalla barra a destra per ritentare l’acquisizione per un’iterazione di esecuzione del flusso di dati selezionata.

![Elenco dei flussi elaborati eseguiti per un flusso di dati selezionato.](../../images/tutorials/on-demand/processed.png)

Seleziona **[!UICONTROL Pianificato]** per visualizzare un elenco delle esecuzioni del flusso di dati pianificate per l’acquisizione futura.

![Elenco di flussi pianificati eseguiti per un flusso di dati selezionato.](../../images/tutorials/on-demand/scheduled.png)

## Passaggi successivi

Dopo aver letto questo documento, hai imparato a creare flussi eseguiti su richiesta per flussi di dati di origini esistenti. Per ulteriori informazioni sulle origini, leggere [panoramica sulle origini](../../home.md)