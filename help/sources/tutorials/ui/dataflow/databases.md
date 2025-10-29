---
keywords: Experience Platform;home;argomenti comuni;database connector;;home;popular topic;database connector
solution: Experience Platform
title: Creare un flusso di dati utilizzando un Database Source nell’interfaccia utente
type: Tutorial
description: Un flusso di dati è un’attività pianificata che recupera e acquisisce dati da un’origine a un set di dati di Experience Platform. Questo tutorial illustra come creare un flusso di dati per un’origine di database utilizzando l’interfaccia utente di Experience Platform.
exl-id: 9fd8a7ec-bbd8-4890-9860-e6defc6cade3
source-git-commit: 6de14e210b78b321ed7d2c4c30769c260694f474
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 1%

---

# Creare un flusso di dati utilizzando un’origine di database nell’interfaccia utente

Un flusso di dati è un’attività pianificata che recupera e acquisisce dati da un’origine a un set di dati in Adobe Experience Platform. Questo tutorial illustra come creare un flusso di dati per un’origine di database utilizzando l’interfaccia utente di Experience Platform.

>[!NOTE]
>
>* Per creare un flusso di dati, è necessario disporre già di un account autenticato con un’origine di database. Un elenco di esercitazioni per la creazione di diversi account di origine del database nell&#39;interfaccia utente è disponibile nella [panoramica sulle origini](../../../home.md#database).
>
>* Affinché Experience Platform possa acquisire i dati, i fusi orari per tutte le origini batch basate su tabelle devono essere configurati in formato UTC. L&#39;unico indicatore orario supportato per l&#39;[[!DNL Snowflake] origine](../../../connectors/databases/snowflake.md) è TIMESTAMP_NTZ con ora UTC.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM)] Sistema](../../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Data Prep]](../../../../data-prep/home.md): consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

## Aggiungi dati

Dopo aver creato l&#39;account di origine del database, viene visualizzato il passaggio **[!UICONTROL Add data]** che fornisce un&#39;interfaccia per esplorare la gerarchia delle tabelle dell&#39;account di origine del database.

* La metà sinistra dell’interfaccia è un browser che visualizza un elenco di tabelle di dati contenute nell’account. L’interfaccia include anche un’opzione di ricerca che consente di identificare rapidamente i dati di origine che intendi utilizzare.
* La metà destra dell’interfaccia è un pannello di anteprima che consente di visualizzare fino a 100 righe di dati in anteprima.

>[!NOTE]
>
>L&#39;opzione di ricerca dei dati di origine è disponibile per tutte le origini basate su tabelle ad eccezione di Adobe Analytics, [!DNL Amazon Kinesis] e [!DNL Azure Event Hubs].

Una volta trovati i dati di origine, selezionare la tabella, quindi selezionare **[!UICONTROL Next]**.

![select-data](../../../images/tutorials/dataflow/table-based/select-data.png)

## Fornisci i dettagli del flusso di dati

La pagina [!UICONTROL Dataflow detail] consente di scegliere se utilizzare un set di dati esistente o nuovo. Durante questo processo è inoltre possibile configurare le impostazioni per [!UICONTROL Profile dataset], [!UICONTROL Error diagnostics], [!UICONTROL Partial ingestion] e [!UICONTROL Alerts].

![dettagli flusso di dati](../../../images/tutorials/dataflow/table-based/dataflow-detail.png)

### Usa un set di dati esistente

Per acquisire dati in un set di dati esistente, selezionare **[!UICONTROL Existing dataset]**. È possibile recuperare un set di dati esistente utilizzando l&#39;opzione [!UICONTROL Advanced search] oppure scorrendo l&#39;elenco dei set di dati esistenti nel menu a discesa. Dopo aver selezionato un set di dati, fornisci un nome e una descrizione per il flusso di dati.

![set di dati esistente](../../../images/tutorials/dataflow/table-based/existing-dataset.png)

### Utilizza un nuovo set di dati

Per acquisire in un nuovo set di dati, selezionare **[!UICONTROL New dataset]**, quindi fornire un nome per il set di dati di output e una descrizione facoltativa. Quindi, selezionare uno schema a cui mappare utilizzando l&#39;opzione [!UICONTROL Advanced search] o scorrendo l&#39;elenco degli schemi esistenti nel menu a discesa. Dopo aver selezionato uno schema, fornisci un nome e una descrizione per il flusso di dati.

![nuovo-set di dati](../../../images/tutorials/dataflow/table-based/new-dataset.png)

### Abilita [!DNL Profile] e diagnostica errori

Quindi, seleziona l&#39;interruttore **[!UICONTROL Profile dataset]** per abilitare il set di dati per [!DNL Profile]. Questo consente di creare una vista olistica degli attributi e dei comportamenti di un’entità. I dati di tutti i set di dati abilitati per [!DNL Profile] verranno inclusi in [!DNL Profile] e le modifiche verranno applicate al momento del salvataggio del flusso di dati.

[!UICONTROL Error diagnostics] consente la generazione di messaggi di errore dettagliati per tutti i record errati che si verificano nel flusso di dati, mentre [!UICONTROL Partial ingestion] consente di acquisire dati contenenti errori, fino a una determinata soglia definita manualmente. Per ulteriori informazioni, consulta la [panoramica sull&#39;acquisizione batch parziale](../../../../ingestion/batch-ingestion/partial.md).

![profile-and-errors](../../../images/tutorials/dataflow/table-based/profile-and-errors.png)

### Abilita avvisi

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi di origini tramite l&#39;interfaccia utente](../alerts.md).

Dopo aver fornito i dettagli al flusso di dati, selezionare **[!UICONTROL Next]**.

![avvisi](../../../images/tutorials/dataflow/table-based/alerts.png)

## Mappare i campi dati su uno schema XDM

Viene visualizzato il passaggio [!UICONTROL Mapping], che fornisce un&#39;interfaccia per mappare i campi sorgente dallo schema sorgente ai campi XDM di destinazione appropriati nello schema di destinazione.

Experience Platform fornisce consigli intelligenti per campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso. In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull&#39;utilizzo dell&#39;interfaccia mapper e dei campi calcolati, consulta la [guida dell&#39;interfaccia utente della preparazione dati](../../../../data-prep/ui/mapping.md).

>[!NOTE]
>
>Quando esegui il mapping a schemi relazionali, assicurati che i dati di origine includano i campi obbligatori, ad esempio una chiave primaria e un identificatore di versione o un identificatore di marca temporale per gli schemi di serie temporali, .

Le colonne di controllo come `_change_request_type`, utilizzate per l&#39;acquisizione dei dati di modifica, vengono lette durante l&#39;acquisizione ma non sono memorizzate nello schema di destinazione.

Gli schemi relazionali supportano anche le relazioni tra set di dati utilizzando mappature di chiave primaria ed esterna.

Per ulteriori informazioni, consulta la [panoramica di Data Mirror](../../../../xdm/data-mirror/overview.md) e la [documentazione tecnica sugli schemi relazionali](../../../../xdm/schema/relational.md).

Una volta mappati correttamente i dati di origine, selezionare **[!UICONTROL Next]**.

![mappatura](../../../images/tutorials/dataflow/table-based/mapping.png)

## Pianificazione esecuzioni dell’acquisizione

Viene visualizzato il passaggio [!UICONTROL Scheduling], che consente di configurare una pianificazione di acquisizione per acquisire automaticamente i dati di origine selezionati utilizzando le mappature configurate. Per impostazione predefinita, la pianificazione è impostata su `Once`. Per regolare la frequenza di acquisizione, selezionare **[!UICONTROL Frequency]**, quindi selezionare un&#39;opzione dal menu a discesa.

>[!TIP]
>
>L’intervallo e la retrocompilazione non sono visibili durante un’acquisizione una tantum.

![pianificazione](../../../images/tutorials/dataflow/table-based/scheduling.png)

Se imposti la frequenza di acquisizione su `Minute`, `Hour`, `Day` o `Week`, devi impostare un intervallo per stabilire un intervallo di tempo impostato tra ogni acquisizione. Ad esempio, se la frequenza di acquisizione è impostata su `Day` e l&#39;intervallo è impostato su `15`, il flusso di dati verrà pianificato in modo da acquisire i dati ogni 15 giorni.

Durante questo passaggio, puoi anche abilitare **backfill** e definire una colonna per l&#39;acquisizione incrementale dei dati. La retrocompilazione viene utilizzata per acquisire i dati storici, mentre la colonna definita per l’acquisizione incrementale consente di distinguere i nuovi dati dai dati esistenti.

Per ulteriori informazioni sulle configurazioni di pianificazione, consulta la tabella seguente.

| Configurazione pianificazione | Descrizione |
| --- | --- |
| Frequenza | Configura la frequenza per indicare la frequenza con cui deve essere eseguito il flusso di dati. Puoi impostare la frequenza su: <ul><li>**Una volta**: imposta la frequenza su `once` per creare un&#39;acquisizione unica. Le configurazioni di intervallo e backfill non sono disponibili quando crei un flusso di dati di acquisizione una tantum. Per impostazione predefinita, la frequenza di pianificazione è impostata su una volta.</li><li>**Minuti**: imposta la frequenza su `minute` per pianificare il flusso di dati in modo da acquisire i dati al minuto.</li><li>**Ora**: imposta la frequenza su `hour` per pianificare il flusso di dati per acquisire i dati su base oraria.</li><li>**Giorno**: imposta la frequenza su `day` per pianificare il flusso di dati in modo da acquisire i dati su base giornaliera.</li><li>**Settimana**: imposta la frequenza su `week` per pianificare il flusso di dati in modo da acquisire i dati su base settimanale. Per ulteriori informazioni, consulta la sezione su [informazioni sulla pianificazione dell’acquisizione settimanale] (#weekly).</li></ul> |
| Intervallo | Dopo aver selezionato una frequenza, puoi configurare l’impostazione dell’intervallo per stabilire l’intervallo di tempo tra ogni acquisizione. Ad esempio, se imposti la frequenza su giorno e configuri l’intervallo su 15, il flusso di dati verrà eseguito ogni 15 giorni. Impossibile impostare l&#39;intervallo su zero. Il valore dell&#39;intervallo minimo accettato per ciascuna frequenza è il seguente:<ul><li>**Una volta**: n/d</li><li>**Minuto**: 15</li><li>**Ora**: 1</li><li>**Giorno**: 1</li><li>**Settimana**: 1</li></ul> |
| Ora di inizio | La marca temporale per l’esecuzione prevista, presentata in fuso orario UTC. |
| Retrocompilazione | La retrocompilazione determina quali dati vengono inizialmente acquisiti. Se la retrocompilazione è abilitata, tutti i file correnti nel percorso specificato verranno acquisiti durante la prima acquisizione pianificata. Se la retrocompilazione è disattivata, verranno acquisiti solo i file caricati tra la prima esecuzione dell’acquisizione e l’ora di inizio. I file caricati prima dell’ora di inizio non verranno acquisiti. |
| Carica dati incrementali per | Opzione con un set filtrato di campi dello schema di origine di tipo, data o ora. Il campo selezionato per **[!UICONTROL Load incremental data by]** deve avere i valori data-ora nel fuso orario UTC per caricare correttamente i dati incrementali. Tutte le origini batch basate su tabelle selezionano i dati incrementali confrontando un valore di timestamp della colonna delta con il tempo UTC della finestra di esecuzione del flusso corrispondente e quindi copiando i dati dall&#39;origine, se vengono trovati nuovi dati all&#39;interno della finestra di tempo UTC. |

![backfill](../../../images/tutorials/dataflow/table-based/backfill.png)

### Informazioni sulla pianificazione dell’acquisizione settimanale {#weekly}

Quando scegli di impostare il flusso di dati in modo che venga eseguito secondo una pianificazione settimanale, il flusso di dati viene eseguito in base a uno dei seguenti scenari:

* Se l’origine dati è stata creata ma non sono ancora stati acquisiti dati, il primo flusso di dati settimanale verrà eseguito 7 giorni dopo la data di creazione dell’origine. Questo intervallo di 7 giorni inizia sempre da quando è stata creata l’origine, indipendentemente da quando hai impostato la pianificazione. Dopo l’esecuzione iniziale, il flusso di dati continuerà a essere eseguito settimanalmente in base alla pianificazione configurata.
* Se i dati dell’origine sono stati precedentemente acquisiti e li pianifichi di nuovo per l’acquisizione settimanale, il flusso di dati successivo verrà eseguito 7 giorni dopo l’acquisizione riuscita più recente.

## Verifica il flusso di dati

Viene visualizzato il passaggio **[!UICONTROL Review]**, che consente di rivedere il nuovo flusso di dati prima che venga creato. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connection]**: mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all&#39;interno di tale file di origine.
* **[!UICONTROL Assign dataset & map fields]**: visualizza il set di dati in cui verranno acquisiti i dati di origine, insieme allo schema associato. Se utilizzi uno schema relazionale, verifica che i campi obbligatori, come la chiave primaria e l’identificatore di versione, siano mappati correttamente. Inoltre, assicurati che tutte le colonne di controllo dell’acquisizione dati di modifica siano configurate correttamente. I set di dati che utilizzano schemi relazionali supportano più modelli di dati e abilitano [flussi di lavoro di acquisizione dati di modifica](../../api/change-data-capture.md).
* **[!UICONTROL Scheduling]**: mostra il periodo attivo, la frequenza e l&#39;intervallo della pianificazione di acquisizione.

Dopo aver rivisto il flusso di dati, seleziona **[!UICONTROL Finish]** e lascia un po&#39; di tempo per la creazione del flusso di dati.

![revisione](../../../images/tutorials/dataflow/table-based/review.png)

## Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni su tassi di acquisizione, successo ed errori. Per ulteriori informazioni su come monitorare il flusso di dati, consulta l&#39;esercitazione su [account di monitoraggio e flussi di dati nell&#39;interfaccia utente](../monitor.md).

## Eliminare il flusso di dati

È possibile eliminare i flussi di dati non più necessari o creati in modo errato utilizzando la funzione **[!UICONTROL Delete]** disponibile nell&#39;area di lavoro **[!UICONTROL Dataflows]**. Per ulteriori informazioni su come eliminare i flussi di dati, vedere l&#39;esercitazione sull&#39;eliminazione di [flussi di dati nell&#39;interfaccia utente](../delete.md).

## Passaggi successivi

Seguendo questa esercitazione, è stato creato un flusso di dati per portare dati dall’origine del database ad Experience Platform. I dati in arrivo possono ora essere utilizzati da servizi [!DNL Experience Platform] downstream come [!DNL Real-Time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica di [!DNL Real-Time Customer Profile]](../../../../profile/home.md)
* [Panoramica di [!DNL Data Science Workspace]](../../../../data-science-workspace/home.md)
