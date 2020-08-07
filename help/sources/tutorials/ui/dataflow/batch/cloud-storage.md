---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Configurare un flusso di dati per un connettore batch di archiviazione cloud nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 86ded28b1830d3607c8b5214c8d31dfcbf446252
workflow-type: tm+mt
source-wordcount: '1421'
ht-degree: 0%

---


# Configurare un flusso di dati per un connettore batch di archiviazione cloud nell&#39;interfaccia utente

Un flusso di dati è un&#39;attività pianificata che recupera e trasferisce dati da un&#39;origine a un [!DNL Platform] set di dati. Questa esercitazione fornisce i passaggi per configurare un nuovo flusso di dati utilizzando l&#39;account di archiviazione cloud.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Inoltre, questa esercitazione richiede l&#39;utilizzo di un account di archiviazione cloud prestabilito. Un elenco di esercitazioni per la creazione di diversi account di archiviazione cloud nell&#39;interfaccia utente è disponibile nella panoramica [dei connettori](../../../../home.md)sorgente.

### Formati di file supportati

[!DNL Experience Platform] supporta i seguenti formati di file da acquisire da archivi esterni:

* Valori separati da delimitatore (DSV): Il supporto per i file di dati in formato DSV è attualmente limitato ai valori separati da virgola. Il valore delle intestazioni dei campi all&#39;interno dei file formattati DSV deve essere costituito solo da caratteri alfanumerici e caratteri di sottolineatura. In futuro verrà fornito il supporto per i file DSV generali.
* [!DNL JavaScript Object Notation] (JSON): I file di dati in formato JSON devono essere conformi allo standard XDM.
* [!DNL Apache Parquet]: I file di dati in formato parquet devono essere conformi allo standard XDM.

## Seleziona dati

Dopo aver creato l&#39;account di archiviazione cloud, viene visualizzato il *[!UICONTROL Select data]* passaggio che fornisce un&#39;interfaccia interattiva per esplorare la gerarchia di archiviazione cloud.

* La metà sinistra dell&#39;interfaccia è un browser di directory che visualizza i file e le directory del server.
* La metà destra dell&#39;interfaccia consente di visualizzare in anteprima fino a 100 righe di dati da un file compatibile.

Selezionando una cartella elencata potete scorrere la gerarchia delle cartelle in cartelle più profonde. Dopo aver selezionato un file o una cartella compatibile, viene visualizzato il **[!UICONTROL Select data format]** menu a discesa, in cui è possibile scegliere un formato per visualizzare i dati nella finestra di anteprima.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data.png)

Una volta completata la finestra di anteprima, potete selezionare **[!UICONTROL Next]** di caricare tutti i file nella cartella selezionata. Per caricare un file specifico, selezionatelo dall’elenco prima di selezionarlo **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data-preview.png)

### Inviare file Parquet o JSON

I formati di file supportati per un account di archiviazione cloud includono anche JSON e Parquet. I file JSON e Parquet devono essere conformi allo standard XDM. Per caricare i file JSON o Parquet, selezionate il formato di file appropriato dal browser directory e applicate il formato di dati compatibile dall&#39;interfaccia giusta. Selezionare **[!UICONTROL Next]** per continuare.

>[!IMPORTANT]
>
>A differenza dei tipi di file delimitati, i file in formato JSON e Parquet non sono disponibili per l’anteprima.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data-parquet.png)

## Mappatura dei campi dati su uno schema XDM

Viene visualizzato il *[!UICONTROL Mapping]* passaggio che fornisce un&#39;interfaccia interattiva per mappare i dati di origine a un [!DNL Platform] dataset. I file di origine formattati in JSON o Parquet devono essere conformi a XDM e non devono essere configurati manualmente. I file CSV, al contrario, richiedono la configurazione esplicita della mappatura, ma consentono di scegliere quali campi di dati di origine mappare.

Scegliere un set di dati in entrata in cui assimilare i dati. È possibile utilizzare un set di dati esistente o crearne uno nuovo.

**Utilizzare un dataset esistente**

Per assimilare i dati in un dataset esistente, selezionare **[!UICONTROL Existing dataset]**, quindi l&#39;icona del dataset.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-existing-data.png)

Viene visualizzata *[!UICONTROL Select dataset]* la finestra di dialogo. Trovare il set di dati che si desidera utilizzare, selezionarlo, quindi fare clic **[!UICONTROL Continue]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-existing-dataset.png)

**Utilizza un nuovo set di dati**

Per assimilare i dati in un nuovo dataset, selezionare **[!UICONTROL New dataset]** e immettere un nome e una descrizione per il dataset nei campi forniti. Per aggiungere uno schema, è possibile immettere un nome di schema esistente nella *[!UICONTROL Select schema]* finestra di dialogo. In alternativa, è possibile selezionare l&#39;opzione **[!UICONTROL Schema advanced search]** per cercare uno schema appropriato.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-new-dataset.png)

Viene visualizzata *[!UICONTROL Select schema]* la finestra di dialogo. Selezionare lo schema da applicare al nuovo dataset, quindi selezionare **[!UICONTROL Done]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-schema.png)

In base alle esigenze, è possibile scegliere di mappare direttamente i campi oppure utilizzare le funzioni di mappatura per trasformare i dati di origine in modo da derivare i valori calcolati o calcolati. Per ulteriori informazioni sulla mappatura dei dati e sulle funzioni di mappatura, consulta l’esercitazione sulla [mappatura dei dati CSV ai campi](../../../../../ingestion/tutorials/map-a-csv-file.md)dello schema XDM.

Una volta mappati i dati di origine, selezionare **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping.png)

## Pianificare le esecuzioni dell&#39;assimilazione

Viene visualizzato il *[!UICONTROL Scheduling]* passaggio che consente di configurare una pianificazione di assimilazione per l&#39;acquisizione automatica dei dati di origine selezionati tramite le mappature configurate. Nella tabella seguente sono riportati i diversi campi configurabili per la pianificazione:

| Campo | Descrizione |
| --- | --- |
| Frequenza | Le frequenze selezionabili includono `Once`, `Minute`, `Hour`, `Day`e `Week`. |
| Intervallo | Un numero intero che imposta l&#39;intervallo per la frequenza selezionata. |
| Ora di inizio | Una marca temporale UTC che indica quando è impostata la prima assimilazione. |
| Backfill | Un valore booleano che determina i dati inizialmente acquisiti. Se *[!UICONTROL Backfill]* è abilitata, tutti i file correnti nel percorso specificato verranno acquisiti durante la prima assimilazione pianificata. Se *Backfill* è disattivato, verranno acquisiti solo i file caricati tra la prima esecuzione dell&#39;assimilazione e il *[!UICONTROL Start time]* file. I file caricati prima di *[!UICONTROL Start time]* non verranno acquisiti. |

I flussi di dati sono progettati per l&#39;acquisizione automatica dei dati su base programmata. Per iniziare, selezionate la frequenza di assimilazione. Quindi, impostare l&#39;intervallo per specificare il periodo tra due esecuzioni di flusso. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero e deve essere impostato su maggiore o uguale a 15.

Per impostare l’ora di inizio dell’assimilazione, regolate la data e l’ora visualizzate nella casella Ora di inizio. In alternativa, potete selezionare l&#39;icona del calendario per modificare il valore dell&#39;ora di inizio. L&#39;ora di inizio deve essere maggiore o uguale all&#39;ora corrente in UTC.

Specificare i valori per la pianificazione e selezionare **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-interval-on.png)

### Impostazione di un flusso di dati per l’assimilazione una tantum

Per impostare l’inserimento una tantum, selezionate la freccia a discesa di frequenza e selezionate **[!UICONTROL Once]**. È possibile continuare a apportare modifiche a un set di flussi di dati per l’inserimento di una frequenza una tantum, purché l’ora di inizio rimanga in futuro. Una volta trascorso l’ora di inizio, il valore di frequenza una tantum non può più essere modificato.

>[!TIP]
>
>**[!UICONTROL Interval]** e non **[!UICONTROL Backfill]** sono visibili durante un&#39;assimilazione una tantum.

Dopo aver fornito i valori appropriati alla pianificazione, selezionare **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-once.png)

## Fornire i dettagli del flusso di dati

Viene visualizzato il *[!UICONTROL Dataflow detail]* passaggio che consente di assegnare un nome e una breve descrizione al nuovo flusso di dati.

Durante questo processo, potete anche abilitare *[!UICONTROL Partial ingestion]* e *[!UICONTROL Error diagnostics]*. L&#39;abilitazione *[!UICONTROL Partial ingestion]* consente di acquisire i dati contenenti errori, fino a una certa soglia che è possibile impostare. L&#39;attivazione *[!UICONTROL Error diagnostics]* fornirà dettagli su eventuali dati errati che vengono inseriti separatamente in batch. Per ulteriori informazioni, consultate la panoramica sull’assimilazione [parziale dei](../../../../../ingestion/batch-ingestion/partial.md)batch.

Immettete i valori per il flusso di dati e selezionate **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/dataflow-detail.png)

## Controllare il flusso di dati

Viene visualizzato il *[!UICONTROL Review]* passaggio che consente di rivedere il nuovo flusso di dati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

* *[!UICONTROL Connection]*: Mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all&#39;interno del file di origine.
* *[!UICONTROL Assign dataset & map fields]*: Mostra il set di dati in cui vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati aderisce.
* *[!UICONTROL Scheduling]*: Mostra il periodo, la frequenza e l’intervallo attivi della pianificazione di assimilazione.

Dopo aver rivisto il flusso di dati, fai clic su **[!UICONTROL Finish]** e consenti la creazione del flusso di dati.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/review.png)

## Monitorare ed eliminare il flusso di dati

Una volta creato il flusso di dati per l&#39;archiviazione cloud, potete monitorare i dati che vengono acquisiti tramite di esso. Per ulteriori informazioni sul monitoraggio e l’eliminazione dei flussi di dati, consulta l’esercitazione sul [monitoraggio dei flussi](../../../../../ingestion/quality/monitor-data-flows.md)di dati.

## Passaggi successivi

Seguendo questa esercitazione, hai creato con successo un flusso di dati per l&#39;inserimento di dati da un archivio cloud esterno e hai acquisito informazioni sul monitoraggio dei set di dati. Per saperne di più sulla creazione di flussi di dati, puoi completare l’apprendimento guardando il video sottostante. Inoltre, i dati in entrata possono ora essere utilizzati dai [!DNL Platform] servizi a valle come [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i documenti seguenti:

* [Panoramica del profilo cliente in tempo reale](../../../../../profile/home.md)
* [Panoramica di Analysis Workspace](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> L’ [!DNL Platform] interfaccia utente mostrata nel video seguente è obsoleta. Per informazioni sulle ultime funzionalità e videate dell’interfaccia, consulta la documentazione precedente.

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## Appendice

Le sezioni seguenti forniscono informazioni aggiuntive sull&#39;utilizzo dei connettori di origine.

### Disattivazione di un flusso di dati

Quando un flusso di dati viene creato, diventa immediatamente attivo e i dati vengono acquisiti in base alla pianificazione specificata. Puoi disattivare un flusso di dati attivo in qualsiasi momento seguendo le istruzioni riportate di seguito.

Nell’area di *[!UICONTROL Sources]* lavoro, fate clic sulla **[!UICONTROL Browse]** scheda. Quindi, fare clic sul nome dell&#39;account associato al flusso di dati attivo che si desidera disattivare.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Viene *[!UICONTROL Source activity]* visualizzata la pagina. Selezionate il flusso di dati attivo dall’elenco per aprire la relativa *[!UICONTROL Properties]* colonna sul lato destro dello schermo, che contiene un pulsante di **[!UICONTROL Enabled]** attivazione/disattivazione. Fate clic sull’interruttore per disattivare il flusso di dati. La stessa opzione può essere utilizzata per riattivare un flusso di dati dopo che è stato disabilitato.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/disable-source.png)

### Attivare i dati in entrata per la [!DNL Profile] popolazione

I dati in entrata provenienti dal connettore di origine possono essere utilizzati per arricchire e compilare [!DNL Real-time Customer Profile] i dati. Per ulteriori informazioni sulla compilazione dei [!DNL Profile] dati del cliente reale, consulta l’esercitazione sulla popolazione [del](../../profile.md)profilo.
