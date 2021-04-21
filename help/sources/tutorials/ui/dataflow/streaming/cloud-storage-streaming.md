---
keywords: Experience Platform;home;argomenti comuni;connettore di archiviazione cloud;archiviazione cloud
solution: Experience Platform
title: Configurare un flusso di dati per un connettore di streaming di archiviazione cloud nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Un flusso di dati è un’attività pianificata che recupera e acquisisce dati da un’origine a un set di dati della Platform. Questa esercitazione fornisce i passaggi per configurare un nuovo flusso di dati utilizzando il connettore base di archiviazione cloud.
exl-id: 75deead6-ef3c-48be-aed2-c43d1f432178
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 1%

---

# Configurare un flusso di dati per una connessione in streaming di archiviazione cloud nell’interfaccia utente

Un flusso di dati è un’attività pianificata che recupera e acquisisce dati da un’origine a un set di dati [!DNL Platform]. Questa esercitazione fornisce i passaggi per configurare un nuovo flusso di dati utilizzando il connettore base di archiviazione cloud.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   - [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Inoltre, questa esercitazione richiede che sia già stato creato un connettore di archiviazione cloud. Un elenco di esercitazioni per la creazione di diversi connettori di archiviazione cloud nell&#39;interfaccia utente è disponibile nella [panoramica dei connettori sorgente](../../../../home.md).

## Seleziona dati

Dopo aver creato il connettore di archiviazione cloud, viene visualizzato il passaggio *Seleziona dati* , che fornisce un&#39;interfaccia per selezionare il flusso da cui si desidera eseguire lo streaming dei dati.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-data.png)

## Mappatura di campi dati su uno schema XDM

Viene visualizzato il passaggio **[!UICONTROL Mapping]** che fornisce un&#39;interfaccia interattiva per mappare i dati di origine a un set di dati [!DNL Platform].

Scegli un set di dati in entrata in cui acquisire i dati. Puoi utilizzare un set di dati esistente o crearne uno nuovo.

**Utilizzare un set di dati esistente**

Per acquisire dati in un set di dati esistente, seleziona **[!UICONTROL Use existing dataset]**, quindi fai clic sull’icona del set di dati.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-existing-data.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Select dataset]**. Trova il set di dati che desideri utilizzare, selezionalo, quindi fai clic su **[!UICONTROL Continue]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-existing-data.png)

**Utilizzare un nuovo set di dati**

Per acquisire dati in un nuovo set di dati, seleziona **[!UICONTROL Create new dataset]** e immetti un nome e una descrizione per il set di dati nei campi forniti. Quindi, seleziona lo schema da utilizzare nel menu a discesa .

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-new-dataset.png)

## Assegnare un nome al flusso di dati

Viene visualizzato il passaggio **[!UICONTROL Dataflow detail]** , che consente di assegnare un nome e una breve descrizione del nuovo flusso di dati.

Immetti i valori per il flusso di dati e fai clic su **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/name-your-dataflow.png)

### Controlla il tuo flusso di dati

Viene visualizzato il passaggio **[!UICONTROL Review]** , che consente di rivedere il nuovo flusso di dati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

- **[!UICONTROL Source details]**: Mostra il tipo di origine e altri dettagli relativi all&#39;origine.
- **[!UICONTROL Target details]**: Mostra il set di dati in cui vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati aderisce.

Dopo aver esaminato il flusso di dati, fai clic su **[!UICONTROL Finish]** e consenti la creazione del flusso di dati.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Monitorare ed eliminare il flusso di dati

Una volta creato il flusso di dati di archiviazione cloud, puoi monitorare i dati che vengono acquisiti tramite di esso. Per ulteriori informazioni sul monitoraggio e l&#39;eliminazione dei flussi di dati, consulta l&#39;esercitazione sul [monitoraggio dei flussi di dati](../../../../../ingestion/quality/monitor-data-ingestion.md).

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente un flusso di dati per inserire dati da un archivio cloud esterno e hai acquisito informazioni sul monitoraggio dei set di dati. I dati in entrata possono ora essere utilizzati dai servizi a valle [!DNL Platform] come [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i seguenti documenti:

- [[!DNL Real-time Customer Profile] panoramica](../../../../../profile/home.md)
- [[!DNL Data Science Workspace] panoramica](../../../../../data-science-workspace/home.md)

## Appendice

Le sezioni seguenti forniscono informazioni aggiuntive per l’utilizzo dei connettori sorgente.

### Disattiva un flusso di dati

Quando un flusso di dati viene creato, diventa immediatamente attivo e acquisisce i dati in base alla pianificazione specificata. Puoi disattivare un flusso di dati attivo in qualsiasi momento seguendo le istruzioni riportate di seguito.

Nell&#39;area di lavoro **[!UICONTROL Sources]** fare clic sulla scheda **[!UICONTROL Browse]**. Quindi, fare clic sul nome della connessione associata al flusso di dati attivo che si desidera disattivare.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/browse.png)

Viene visualizzata la pagina **[!UICONTROL Source activity]** . Seleziona il flusso di dati attivo dall’elenco per aprire la relativa colonna **[!UICONTROL Properties]** sul lato destro dello schermo, che contiene un pulsante di attivazione/disattivazione **[!UICONTROL Enabled]**. Fai clic sull’interruttore per disattivare il flusso di dati. La stessa opzione può essere utilizzata per riattivare un flusso di dati dopo che è stato disabilitato.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/disable-source.png)

### Attivare i dati in entrata per la popolazione [!DNL Profile]

I dati in entrata provenienti dal connettore di origine possono essere utilizzati per arricchire e popolare i dati [!DNL Real-time Customer Profile]. Per ulteriori informazioni sulla compilazione dei dati [!DNL Real-time Customer Profile], consulta l’esercitazione su [Popolazione di profili](../../profile.md).
