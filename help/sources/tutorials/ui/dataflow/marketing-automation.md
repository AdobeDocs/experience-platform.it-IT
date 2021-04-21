---
keywords: Experience Platform;home;argomenti popolari;connettore di automazione marketing
solution: Experience Platform
title: Configurare un flusso di dati per una connessione sorgente di automazione marketing nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Un flusso di dati è un’attività pianificata che recupera e acquisisce dati da un’origine a un set di dati [!DNL Platform] . Questa esercitazione fornisce i passaggi per configurare un nuovo flusso di dati utilizzando l’account di automazione del marketing.
exl-id: 8d31fc2d-b952-44f7-98e7-f51b0acc19ed
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 0%

---

# Configurare un flusso di dati per una connessione di automazione marketing nell’interfaccia utente

Un flusso di dati è un’attività pianificata che recupera e acquisisce dati da un’origine a un set di dati [!DNL Platform]. Questa esercitazione fornisce i passaggi per configurare un nuovo flusso di dati utilizzando l’account di automazione del marketing.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   - [Nozioni di base sulla composizione](../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione](../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-time Customer Profile]](../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Inoltre, questa esercitazione richiede che tu abbia già creato un account di automazione del marketing. Un elenco di esercitazioni per la creazione di diversi connettori di automazione marketing nell&#39;interfaccia utente è disponibile nella [panoramica dei connettori sorgente](../../../home.md).

## Seleziona dati

Dopo aver creato l&#39;account di automazione di marketing, viene visualizzato il passaggio *Seleziona dati* , che fornisce un&#39;interfaccia interattiva per esplorare la gerarchia dei file.

- La metà sinistra dell&#39;interfaccia è un browser di directory che visualizza i file e le directory del server.
- La metà destra dell’interfaccia consente di visualizzare in anteprima fino a 100 righe di dati da un file compatibile.

Puoi utilizzare l’opzione **[!UICONTROL Search]** nella parte superiore della pagina per identificare rapidamente i dati di origine che intendi utilizzare.

>[!NOTE]
>
>L’opzione per i dati dell’origine di ricerca è disponibile per tutti i connettori sorgente basati su tabelle, esclusi i connettori Analytics, Classificazioni, Hubs evento e Kinesis.

Una volta trovati i dati di origine, seleziona la directory, quindi fai clic su **[!UICONTROL Next]**.

![select-data](../../../images/tutorials/dataflow/all-tabular/select-data.png)

## Mappatura di campi dati su uno schema XDM

Viene visualizzato il passaggio **[!UICONTROL Mapping]** che fornisce un&#39;interfaccia interattiva per mappare i dati di origine a un set di dati [!DNL Platform].

Scegli un set di dati in entrata in cui acquisire i dati. Puoi utilizzare un set di dati esistente o crearne uno nuovo.

### Utilizzare un set di dati esistente

Per acquisire dati in un set di dati esistente, seleziona **[!UICONTROL Use existing dataset]**, quindi fai clic sull’icona del set di dati.

![use-existing-dataset](../../../images/tutorials/dataflow/marketing-automation/use-existing-dataset.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Select dataset]**. Trova il set di dati che desideri utilizzare, selezionalo, quindi fai clic su **[!UICONTROL Continue]**.

![select-existing-dataset](../../../images/tutorials/dataflow/marketing-automation/select-existing-dataset.png)

### Utilizzare un nuovo set di dati

Per acquisire i dati in un nuovo set di dati, seleziona **[!UICONTROL Create new dataset]** e immetti un nome e una descrizione per il set di dati nei campi forniti.

È possibile allegare un campo schema immettendo un nome schema nella barra di ricerca **[!UICONTROL Select schema]**. Puoi anche selezionare l’icona a discesa per visualizzare un elenco degli schemi esistenti. In alternativa, puoi selezionare **[!UICONTROL Advanced search]** per accedere alla schermata degli schemi esistenti, inclusi i rispettivi dettagli.

Durante questo passaggio, puoi abilitare il set di dati per [!DNL Real-time Customer Profile] e creare una visualizzazione olistica degli attributi e dei comportamenti di un’entità. I dati di tutti i set di dati abilitati verranno inclusi in [!DNL Profile] e le modifiche vengono applicate al salvataggio del flusso di dati.

Attiva il pulsante **[!UICONTROL Profile dataset]** per abilitare il set di dati di destinazione per [!DNL Profile].

![create-new-dataset](../../../images/tutorials/dataflow/marketing-automation/new-dataset.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Select schema]**. Seleziona lo schema da applicare al nuovo set di dati, quindi fai clic su **[!UICONTROL Done]**.

![select-schema](../../../images/tutorials/dataflow/marketing-automation/select-schema.png)

In base alle tue esigenze, puoi scegliere di mappare direttamente i campi oppure utilizzare funzioni di mappatura per trasformare i dati di origine in valori calcolati o calcolati. Per ulteriori informazioni sulla mappatura dei dati e sulle funzioni di mappatura, consulta l’esercitazione sulla [mappatura dei dati CSV nei campi dello schema XDM](../../../../ingestion/tutorials/map-a-csv-file.md).

>[!TIP]
>
>[!DNL Platform] fornisce consigli intelligenti per i campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso.

![](../../../images/tutorials/dataflow/all-tabular/mapping.png)

Seleziona **[!UICONTROL Preview data]** per visualizzare i risultati della mappatura di fino a 100 righe di dati di esempio dal set di dati selezionato.

Durante l’anteprima, la colonna Identity ha la priorità come primo campo, in quanto rappresenta le informazioni chiave necessarie per la convalida dei risultati della mappatura.

![](../../../images/tutorials/dataflow/all-tabular/mapping-preview.png)

Una volta mappati i dati di origine, seleziona **[!UICONTROL Close]**.

## Pianifica esecuzioni di acquisizione

Viene visualizzato il passaggio **[!UICONTROL Scheduling]** , che consente di configurare una pianificazione dell’acquisizione per acquisire automaticamente i dati di origine selezionati utilizzando le mappature configurate. La tabella seguente illustra i diversi campi configurabili per la pianificazione:

| Campo | Descrizione |
| --- | --- |
| Frequenza | Le frequenze selezionabili sono `Once`, `Minute`, `Hour`, `Day` e `Week`. |
| Intervallo | Un numero intero che imposta l&#39;intervallo per la frequenza selezionata. |
| Ora di inizio | Una marca temporale UTC che indica quando è impostata la prima acquisizione. |
| Backfill | Un valore booleano che determina i dati inizialmente acquisiti. Se **[!UICONTROL Backfill]** è abilitato, tutti i file correnti nel percorso specificato verranno acquisiti durante la prima acquisizione pianificata. Se **[!UICONTROL Backfill]** è disabilitato, verranno acquisiti solo i file caricati tra la prima esecuzione dell’acquisizione e l’ora di inizio. I file caricati prima dell’ora di inizio non vengono acquisiti. |
| Colonna Delta | Opzione con un set filtrato di campi dello schema di origine di tipo, data o ora. Questo campo viene utilizzato per distinguere tra dati nuovi ed esistenti. I dati incrementali verranno acquisiti in base al timestamp della colonna selezionata. |

I flussi di dati sono progettati per acquisire automaticamente i dati su base pianificata. Inizia selezionando la frequenza di acquisizione. Quindi, impostare l&#39;intervallo per indicare il periodo tra due esecuzioni di flusso. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero e deve essere impostato su maggiore o uguale a 15.

Per impostare l’ora di inizio per l’acquisizione, regola la data e l’ora visualizzate nella casella dell’ora di inizio. In alternativa, puoi selezionare l’icona del calendario per modificare il valore dell’ora di inizio. L’ora di inizio deve essere maggiore o uguale all’ora UTC corrente.

Seleziona **[!UICONTROL Load incremental data by]** per assegnare la colonna delta. Questo campo distingue tra dati nuovi ed esistenti.

![](../../../images/tutorials/dataflow/databases/schedule-interval-on.png)

### Configurare un flusso di dati di acquisizione una tantum

Per impostare l’acquisizione una tantum, seleziona la freccia a discesa della frequenza e seleziona **[!UICONTROL Once]**.

>[!TIP]
>
>**[!UICONTROL Interval]** e non  **[!UICONTROL Backfill]** sono visibili durante un’acquisizione una tantum.

Dopo aver fornito i valori appropriati alla pianificazione, seleziona **[!UICONTROL Next]**.

![](../../../images/tutorials/dataflow/databases/schedule-once.png)

## Fornire i dettagli del flusso di dati

Viene visualizzato il passaggio **[!UICONTROL Dataflow detail]** , che consente di assegnare un nome e una breve descrizione del nuovo flusso di dati.

Durante questo processo, puoi anche abilitare **[!UICONTROL Partial ingestion]** e **[!UICONTROL Error diagnostics]**. L’abilitazione di **[!UICONTROL Partial ingestion]** consente di acquisire dati contenenti errori fino a una determinata soglia. Una volta abilitato **[!UICONTROL Partial ingestion]**, trascina il comando **[!UICONTROL Error threshold %]** per regolare la soglia di errore del batch. In alternativa, è possibile regolare manualmente la soglia selezionando la casella di input. Per ulteriori informazioni, consulta la [panoramica sull’acquisizione parziale dei batch](../../../../ingestion/batch-ingestion/partial.md).

Immetti i valori per il flusso di dati e seleziona **[!UICONTROL Next]**.

![dataflow-details](../../../images/tutorials/dataflow/all-tabular/dataflow-detail.png)

## Controlla il tuo flusso di dati

Viene visualizzato il passaggio **[!UICONTROL Review]** , che consente di rivedere il nuovo flusso di dati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

- **[!UICONTROL Connection]**: Mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all&#39;interno del file di origine.
- **[!UICONTROL Assign dataset & map fields]**: Mostra il set di dati in cui vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati aderisce.
- **[!UICONTROL Scheduling]**: Mostra il periodo, la frequenza e l’intervallo attivi della pianificazione dell’acquisizione.

Dopo aver esaminato il flusso di dati, fai clic su **[!UICONTROL Finish]** e consenti la creazione del flusso di dati.

![revisione](../../../images/tutorials/dataflow/marketing-automation/review.png)

## Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni sui tassi di acquisizione, sul successo e sugli errori. Per ulteriori informazioni su come monitorare il flusso di dati, consulta l’esercitazione su [monitoraggio di account e flussi di dati nell’interfaccia utente](../monitor.md).

## Elimina il flusso di dati

È possibile eliminare i flussi di dati che non sono più necessari o che sono stati creati in modo errato utilizzando la funzione **[!UICONTROL Delete]** disponibile nell&#39;area di lavoro **[!UICONTROL Dataflows]**. Per ulteriori informazioni su come eliminare i flussi di dati, consulta l’esercitazione sull’ [eliminazione dei flussi di dati nell’interfaccia utente](../delete.md).

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente un flusso di dati per inserire i dati da un sistema di automazione del marketing e hai acquisito informazioni sul monitoraggio dei set di dati. I dati in entrata possono ora essere utilizzati dai servizi a valle [!DNL Platform] come [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i seguenti documenti:

- [[!DNL Real-time Customer Profile] panoramica](../../../../profile/home.md)
- [[!DNL Data Science Workspace] panoramica](../../../../data-science-workspace/home.md)

## Appendice

Le sezioni seguenti forniscono informazioni aggiuntive per l’utilizzo dei connettori sorgente.

### Disattiva un flusso di dati

Quando un flusso di dati viene creato, diventa immediatamente attivo e acquisisce i dati in base alla pianificazione specificata. Puoi disattivare un flusso di dati attivo in qualsiasi momento seguendo le istruzioni riportate di seguito.

Nella schermata **[!UICONTROL authentication]** , seleziona il nome della connessione associata al flusso di dati che desideri disattivare.

![](../../../images/tutorials/dataflow/marketing-automation/monitor.png)

Viene visualizzata la pagina **[!UICONTROL Source activity]** . Seleziona il flusso di dati attivo dall’elenco per aprire la relativa colonna **[!UICONTROL Properties]** sul lato destro dello schermo, che contiene un pulsante di attivazione/disattivazione **[!UICONTROL Enabled]**. Fai clic sull’interruttore per disattivare il flusso di dati. La stessa opzione può essere utilizzata per riattivare un flusso di dati dopo che è stato disabilitato.

![disable](../../../images/tutorials/dataflow/marketing-automation/disable.png)

### Attivare i dati in entrata per la popolazione [!DNL Profile]

I dati in entrata provenienti dal connettore di origine possono essere utilizzati per arricchire e popolare i dati [!DNL Real-time Customer Profile]. Per ulteriori informazioni sulla compilazione dei dati [!DNL Real-time Customer Profile], consulta l’esercitazione su [Popolazione di profili](../profile.md).
