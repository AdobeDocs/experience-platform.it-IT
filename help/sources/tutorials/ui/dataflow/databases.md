---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Configurare un flusso di dati per un connettore di database nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 91714bea4e165d64bcc33e32e73d1d32a505ba00
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---


# Configurare un flusso di dati per un connettore di database nell&#39;interfaccia utente

Un flusso di dati è un&#39;attività pianificata che recupera e trasferisce dati da un&#39;origine a un set di dati Platform. Questa esercitazione fornisce i passaggi per configurare un nuovo flusso di dati utilizzando l&#39;account del database.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei seguenti componenti del  Adobe Experience Platform:

- [Sistema](../../../../xdm/home.md)XDM (Experience Data Model): Il framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   - [Nozioni di base sulla composizione](../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [Profilo](../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Inoltre, questa esercitazione richiede che sia già stato creato un account di database. Un elenco di esercitazioni per la creazione di diversi connettori di database nell&#39;interfaccia utente è disponibile nella panoramica [dei connettori](../../../home.md)sorgente.

## Seleziona dati

Dopo aver creato l&#39;account del database, viene visualizzato il *[!UICONTROL Select data]* passaggio che fornisce un&#39;interfaccia interattiva per esplorare la gerarchia del database.

- La metà sinistra dell&#39;interfaccia è un browser, che visualizza l&#39;elenco dei database dell&#39;account.
- La metà destra dell&#39;interfaccia consente di visualizzare un&#39;anteprima di fino a 100 righe di dati.

Selezionate il database da utilizzare, quindi fate clic su **[!UICONTROL Next]**.

![](../../../images/tutorials/dataflow/databases/add-data.png)

## Mappatura dei campi dati su uno schema XDM

Viene visualizzato il passaggio *Mapping* , che fornisce un&#39;interfaccia interattiva per mappare i dati di origine a un set di dati Platform.

Scegliere un set di dati in entrata in cui assimilare i dati. È possibile utilizzare un set di dati esistente o crearne uno nuovo.

### Utilizzare un dataset esistente

Per assimilare i dati in un dataset esistente, selezionare **[!UICONTROL Existing dataset]**, quindi fare clic sull&#39;icona del dataset.

![](../../../images/tutorials/dataflow/databases/existing-dataset.png)

Viene visualizzata *[!UICONTROL Select dataset]* la finestra di dialogo. Trovare il set di dati che si desidera utilizzare, selezionarlo, quindi fare clic **[!UICONTROL Continue]**.

![](../../../images/tutorials/dataflow/databases/select-existing-dataset.png)

### Utilizza un nuovo set di dati

Per assimilare i dati in un nuovo dataset, selezionare **[!UICONTROL New dataset]** e immettere un nome e una descrizione per il dataset nei campi forniti.

È possibile allegare un campo dello schema immettendo un nome dello schema nella barra di **[!UICONTROL Select schema]** ricerca. Potete anche selezionare l&#39;icona a discesa per visualizzare un elenco degli schemi esistenti. In alternativa, potete scegliere **[!UICONTROL Advanced search]** di accedere alla schermata degli schemi esistenti, inclusi i rispettivi dettagli.

![create-new-dataset](../../../images/tutorials/dataflow/all-tabular/new-target-dataset.png)

Viene visualizzata *[!UICONTROL Select schema]* la finestra di dialogo. Selezionare lo schema che si desidera applicare al nuovo dataset, quindi fare clic su **[!UICONTROL Done]**.

![](../../../images/tutorials/dataflow/databases/select-existing-schema.png)

In base alle esigenze, è possibile scegliere di mappare direttamente i campi oppure utilizzare le funzioni di mappatura per trasformare i dati di origine in modo da derivare i valori calcolati o calcolati. Per ulteriori informazioni sulla mappatura dei dati e sulle funzioni di mappatura, consulta l’esercitazione sulla [mappatura dei dati CSV ai campi](../../../../ingestion/tutorials/map-a-csv-file.md)dello schema XDM.

Una volta mappati i dati di origine, fai clic su **[!UICONTROL Next]**.

![](../../../images/tutorials/dataflow/all-tabular/mapping-updated.png)

## Pianificare le esecuzioni dell&#39;assimilazione

Viene visualizzato il *[!UICONTROL Scheduling]* passaggio che consente di configurare una pianificazione di assimilazione per l&#39;acquisizione automatica dei dati di origine selezionati tramite le mappature configurate. Nella tabella seguente sono riportati i diversi campi configurabili per la pianificazione:

| Campo | Descrizione |
| --- | --- |
| Frequenza | Le frequenze selezionabili includono `Once`, `Minute`, `Hour`, `Day`e `Week`. |
| Intervallo | Un numero intero che imposta l&#39;intervallo per la frequenza selezionata. |
| Ora di inizio | Una marca temporale UTC che indica quando è impostata la prima assimilazione. |
| Backfill | Un valore booleano che determina i dati inizialmente acquisiti. Se *[!UICONTROL Backfill]* è abilitata, tutti i file correnti nel percorso specificato verranno acquisiti durante la prima assimilazione pianificata. Se *Backfill* è disattivato, verranno acquisiti solo i file caricati tra la prima esecuzione dell&#39;assimilazione e il *[!UICONTROL Start time]* file. I file caricati prima di *[!UICONTROL Start time]* non verranno acquisiti. |
| Colonna Delta | Opzione con un set filtrato di campi dello schema di origine di tipo, data o ora. Questo campo è utilizzato per distinguere tra dati nuovi ed esistenti. I dati incrementali verranno acquisiti in base alla marca temporale della colonna selezionata. |

I flussi di dati sono progettati per l&#39;acquisizione automatica dei dati su base programmata. Per iniziare, selezionate la frequenza di assimilazione. Quindi, impostare l&#39;intervallo per specificare il periodo tra due esecuzioni di flusso. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero e deve essere impostato su maggiore o uguale a 15.

Per impostare l’ora di inizio dell’assimilazione, regolate la data e l’ora visualizzate nella casella Ora di inizio. In alternativa, potete selezionare l&#39;icona del calendario per modificare il valore dell&#39;ora di inizio. L&#39;ora di inizio deve essere maggiore o uguale all&#39;ora UTC corrente.

Selezionare **[!UICONTROL Load incremental data by]** per assegnare la colonna delta. Questo campo consente di distinguere tra dati nuovi ed esistenti.

![](../../../images/tutorials/dataflow/databases/schedule-interval-on.png)

### Impostazione di un flusso di dati per l’assimilazione una tantum

Per impostare l’inserimento una tantum, selezionate la freccia a discesa di frequenza e selezionate **[!UICONTROL Once]**.

>[!TIP] **[!UICONTROL Interval]** e non **[!UICONTROL Backfill]** sono visibili durante un&#39;assimilazione una tantum.

Dopo aver fornito i valori appropriati alla pianificazione, selezionare **[!UICONTROL Next]**.

![](../../../images/tutorials/dataflow/databases/schedule-once.png)

## Fornire i dettagli del flusso di dati

Viene visualizzato il *[!UICONTROL Dataflow detail]* passaggio che consente di assegnare un nome e una breve descrizione al nuovo flusso di dati.

Durante questo processo, potete anche abilitare *[!UICONTROL Partial ingestion]* e *[!UICONTROL Error diagnostics]*. L&#39;attivazione *[!UICONTROL Partial ingestion]* consente di assimilare i dati contenenti errori fino a una determinata soglia. Una volta *[!UICONTROL Partial ingestion]* attivato, trascinare il *[!UICONTROL Error threshold %]* quadrante per regolare la soglia di errore del batch. In alternativa, è possibile regolare manualmente la soglia selezionando la casella di input. Per ulteriori informazioni, consultate la panoramica sull’assimilazione [parziale dei](../../../../ingestion/batch-ingestion/partial.md)batch.
Immettete i valori per il flusso di dati e selezionate **[!UICONTROL Next]**.

Immettete i valori per il flusso di dati e selezionate **[!UICONTROL Next]**.

![](../../../images/tutorials/dataflow/databases/dataflow-detail.png)

## Controllare il flusso di dati

Viene visualizzato il *[!UICONTROL Review]* passaggio che consente di rivedere il nuovo flusso di dati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

- *[!UICONTROL Connection]*: Mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all&#39;interno del file di origine.
- *[!UICONTROL Assign dataset & map fields]*: Mostra il set di dati in cui vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati aderisce.
- *[!UICONTROL Scheduling]*: Mostra il periodo, la frequenza e l’intervallo attivi della pianificazione di assimilazione.

Dopo aver rivisto il flusso di dati, fai clic su **[!UICONTROL Finish]** e consenti la creazione del flusso di dati.

![](../../../images/tutorials/dataflow/databases/review.png)

## Monitorare ed eliminare il flusso di dati

Una volta creato il flusso di dati, potete monitorare i dati che vengono acquisiti tramite di esso. Per ulteriori informazioni su come monitorare ed eliminare il flusso di dati, consulta l’esercitazione sul [monitoraggio e l’eliminazione dei flussi di dati](../monitor.md).

## Passaggi successivi

Seguendo questa esercitazione, è stato creato un flusso di dati per inserire i dati da un database esterno e ottenere informazioni dettagliate sul monitoraggio dei set di dati. I dati in entrata possono ora essere utilizzati dai servizi Platform a valle, come Profilo cliente in tempo reale e Data Science Workspace. Per ulteriori informazioni, consulta i documenti seguenti:

- [Panoramica del profilo cliente in tempo reale](../../../../profile/home.md)
- [Panoramica di Analysis Workspace](../../../../data-science-workspace/home.md)

## Appendice

Le sezioni seguenti forniscono informazioni aggiuntive sull&#39;utilizzo dei connettori di origine.

### Disattivazione di un flusso di dati

Quando un flusso di dati viene creato, diventa immediatamente attivo e i dati vengono acquisiti in base alla pianificazione specificata. Puoi disattivare un flusso di dati attivo in qualsiasi momento seguendo le istruzioni riportate di seguito.

Nell’area di *[!UICONTROL Sources]* lavoro, selezionate la **[!UICONTROL Dataflowss]** scheda. Quindi, selezionate il flusso di dati da disattivare.

![](../../../images/tutorials/dataflow/databases/list-of-dataflows.png)

La *[!UICONTROL Properties]* colonna viene visualizzata sul lato destro dello schermo, con un pulsante di **[!UICONTROL Enabled]** attivazione/disattivazione. Selezionate l’opzione per disattivare il flusso di dati. La stessa opzione può essere utilizzata per riattivare un flusso di dati dopo che è stato disabilitato.

![](../../../images/tutorials/dataflow/databases/disable.png)

### Attivare i dati in entrata per la [!DNL Profile] popolazione

I dati in entrata provenienti dal connettore di origine possono essere utilizzati per arricchire e compilare [!DNL Real-time Customer Profile] i dati. Per ulteriori informazioni sulla compilazione [!DNL Real-time Customer Profile] dei dati, consulta l’esercitazione sulla popolazione [di](../profile.md)profili.