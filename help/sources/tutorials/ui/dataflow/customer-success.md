---
keywords: Experience Platform;home;argomenti comuni;configurare un flusso di dati;connettore di successo del cliente
solution: Experience Platform
title: Configurare un flusso di dati per una connessione sorgente con successo cliente nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Un flusso di dati è un’attività pianificata che recupera e acquisisce dati da un’origine a un set di dati [!DNL Platform] . Questa esercitazione fornisce i passaggi per configurare un nuovo flusso di dati utilizzando l’account di successo del cliente.
exl-id: d348a7f8-6302-45f1-9961-bab56ad0407e
source-git-commit: 46fb08a10bc05dc758bdcb025693f819b980b41a
workflow-type: tm+mt
source-wordcount: '1491'
ht-degree: 0%

---

# Configurare un flusso di dati per una connessione del cliente nell’interfaccia utente

Un flusso di dati è un’attività pianificata che recupera e acquisisce dati da un’origine a un set di dati [!DNL Platform]. Questa esercitazione fornisce i passaggi per configurare un nuovo flusso di dati utilizzando l’account di successo del cliente.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   - [Nozioni di base sulla composizione](../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione](../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-time Customer Profile]](../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Inoltre, questa esercitazione richiede che tu abbia già creato un account di successo del cliente. Un elenco di esercitazioni per la creazione di diversi connettori di successo dei clienti nell’interfaccia utente è disponibile nella [panoramica dei connettori sorgente](../../../home.md).

## Seleziona dati

Dopo aver creato il connettore di successo del cliente, viene visualizzato il passaggio **[!UICONTROL Seleziona dati]** , che fornisce un&#39;interfaccia interattiva per esplorare la gerarchia dei file.

- La metà sinistra dell&#39;interfaccia è un browser di directory che visualizza i file e le directory del server.
- La metà destra dell’interfaccia consente di visualizzare in anteprima fino a 100 righe di dati da un file compatibile.

Puoi utilizzare l&#39;opzione **[!UICONTROL Cerca]** nella parte superiore della pagina per identificare rapidamente i dati di origine che intendi utilizzare.

>[!NOTE]
>
>L’opzione per i dati dell’origine di ricerca è disponibile per tutti i connettori sorgente basati su tabelle, esclusi i connettori Analytics, Classificazioni, Hubs evento e Kinesis.

Una volta trovati i dati di origine, seleziona la directory, quindi fai clic su **[!UICONTROL Avanti]**.

![select-data](../../../images/tutorials/dataflow/all-tabular/select-data.png)

## Mappatura di campi dati su uno schema XDM

Viene visualizzato il passaggio **[!UICONTROL Mapping]** , che fornisce un&#39;interfaccia interattiva per mappare i dati di origine a un set di dati [!DNL Platform].

Scegli un set di dati in entrata in cui acquisire i dati. Puoi utilizzare un set di dati esistente o crearne uno nuovo.

### Utilizzare un set di dati esistente

Per acquisire dati in un set di dati esistente, seleziona **[!UICONTROL Utilizza set di dati esistenti]**, quindi fai clic sull’icona del set di dati.

![use-existing-dataset](../../../images/tutorials/dataflow/customer-success/use-existing-dataset.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Seleziona set di dati]** . Trova il set di dati che desideri utilizzare, selezionalo, quindi fai clic su **[!UICONTROL Continua]**.

![select-existing-dataset](../../../images/tutorials/dataflow/customer-success/select-dataset.png)

### Utilizzare un nuovo set di dati

Per acquisire dati in un nuovo set di dati, seleziona **[!UICONTROL Crea nuovo set di dati]** e inserisci un nome e una descrizione per il set di dati nei campi forniti.

È possibile allegare un campo schema immettendo un nome schema nella barra di ricerca **[!UICONTROL Seleziona schema]**. Puoi anche selezionare l’icona a discesa per visualizzare un elenco degli schemi esistenti. In alternativa, puoi selezionare **[!UICONTROL Ricerca avanzata]** per accedere alla schermata degli schemi esistenti, inclusi i rispettivi dettagli.

Durante questo passaggio, puoi abilitare il set di dati per [!DNL Real-time Customer Profile] e creare una visualizzazione olistica degli attributi e dei comportamenti di un’entità. I dati di tutti i set di dati abilitati verranno inclusi in [!DNL Profile] e le modifiche vengono applicate al salvataggio del flusso di dati.

Attiva il pulsante **[!UICONTROL Set di dati di profilo]** per abilitare il set di dati di destinazione per [!DNL Profile].

![create-new-dataset](../../../images/tutorials/dataflow/crm/new-dataset.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Seleziona schema]**. Seleziona lo schema da applicare al nuovo set di dati, quindi fai clic su **[!UICONTROL Fine]**.

![select-schema](../../../images/tutorials/dataflow/customer-success/select-schema.png)

In base alle tue esigenze, puoi scegliere di mappare direttamente i campi oppure utilizzare le funzioni di preparazione dei dati per trasformare i dati di origine in valori calcolati o calcolati. Per ulteriori informazioni sulle funzioni di mappatura e sui campi calcolati, consulta la [Guida alle funzioni di preparazione dei dati](../../../../data-prep/functions.md) o la [guida ai campi calcolati](../../../../data-prep/calculated-fields.md).

>[!TIP]
>
>[!DNL Platform] fornisce consigli intelligenti per i campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso.

![](../../../images/tutorials/dataflow/all-tabular/mapping.png)

Seleziona **[!UICONTROL Anteprima dati]** per visualizzare i risultati della mappatura di fino a 100 righe di dati di esempio dal set di dati selezionato.

Durante l’anteprima, la colonna Identity ha la priorità come primo campo, in quanto rappresenta le informazioni chiave necessarie per la convalida dei risultati della mappatura.

![](../../../images/tutorials/dataflow/all-tabular/mapping-preview.png)

Una volta mappati i dati di origine, seleziona **[!UICONTROL Chiudi]**.

## Pianifica esecuzioni di acquisizione

Viene visualizzato il passaggio **[!UICONTROL Pianificazione]** , che consente di configurare una pianificazione dell’acquisizione per acquisire automaticamente i dati di origine selezionati utilizzando le mappature configurate. La tabella seguente illustra i diversi campi configurabili per la pianificazione:

| Campo | Descrizione |
| --- | --- |
| Frequenza | Le frequenze selezionabili sono `Once`, `Minute`, `Hour`, `Day` e `Week`. |
| Intervallo | Un numero intero che imposta l&#39;intervallo per la frequenza selezionata. |
| Ora di inizio | Una marca temporale UTC che indica quando è impostata la prima acquisizione. |
| Backfill | Un valore booleano che determina i dati inizialmente acquisiti. Se è abilitato **[!UICONTROL Backfill]**, tutti i file correnti nel percorso specificato verranno acquisiti durante la prima acquisizione pianificata. Se **[!UICONTROL Backfill]** è disattivato, verranno acquisiti solo i file caricati tra la prima esecuzione dell’acquisizione e l’ora di inizio. I file caricati prima dell’ora di inizio non vengono acquisiti. |
| Colonna Delta | Opzione con un set filtrato di campi dello schema di origine di tipo, data o ora. Questo campo viene utilizzato per distinguere tra dati nuovi ed esistenti. I dati incrementali verranno acquisiti in base al timestamp della colonna selezionata. |

I flussi di dati sono progettati per acquisire automaticamente i dati su base pianificata. Inizia selezionando la frequenza di acquisizione. Quindi, impostare l&#39;intervallo per indicare il periodo tra due esecuzioni di flusso. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero e deve essere impostato su maggiore o uguale a 15.

Per impostare l’ora di inizio per l’acquisizione, regola la data e l’ora visualizzate nella casella dell’ora di inizio. In alternativa, puoi selezionare l’icona del calendario per modificare il valore dell’ora di inizio. L’ora di inizio deve essere maggiore o uguale all’ora UTC corrente.

Seleziona **[!UICONTROL Carica dati incrementali per]** per assegnare la colonna delta. Questo campo distingue tra dati nuovi ed esistenti.

![](../../../images/tutorials/dataflow/databases/schedule-interval-on.png)

### Configurare un flusso di dati di acquisizione una tantum

Per impostare l’acquisizione una tantum, seleziona la freccia a discesa della frequenza e seleziona **[!UICONTROL Una volta]**.

>[!TIP]
>
>**** Intervaland  **** Backfillare non sono visibili durante un’acquisizione una tantum.

Dopo aver fornito i valori appropriati alla pianificazione, selezionare **[!UICONTROL Avanti]**.

![](../../../images/tutorials/dataflow/databases/schedule-once.png)

## Fornire i dettagli del flusso di dati

Viene visualizzato il passaggio **[!UICONTROL Dettaglio flusso di dati]** , che consente di assegnare un nome e una breve descrizione del nuovo flusso di dati.

Durante questo processo, puoi anche abilitare **[!UICONTROL Acquisizione parziale]** e **[!UICONTROL Diagnostica errori]**. L’abilitazione di **[!UICONTROL Acquisizione parziale]** consente di acquisire dati contenenti errori fino a una determinata soglia. Una volta abilitato **[!UICONTROL Partial ingestion]**, trascina il comando **[!UICONTROL Error soglia %]** per regolare la soglia di errore del batch. In alternativa, è possibile regolare manualmente la soglia selezionando la casella di input. Per ulteriori informazioni, consulta la [panoramica sull’acquisizione parziale dei batch](../../../../ingestion/batch-ingestion/partial.md).

Immetti i valori per il flusso di dati e seleziona **[!UICONTROL Avanti]**.

![dataflow-details](../../../images/tutorials/dataflow/all-tabular/dataflow-detail.png)

## Controlla il tuo flusso di dati

Viene visualizzato il passaggio **[!UICONTROL Rivedi]**, che consente di rivedere il nuovo flusso di dati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

- **[!UICONTROL Dettagli]** di connessione: Mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all&#39;interno del file di origine.
- **[!UICONTROL Dettagli]** mappatura: Mostra il set di dati in cui vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati aderisce.
- **[!UICONTROL Dettagli]** pianificazione: Mostra il periodo, la frequenza e l’intervallo attivi della pianificazione dell’acquisizione.

Dopo aver esaminato il flusso di dati, fai clic su **[!UICONTROL Fine]** e consenti la creazione del flusso di dati.

![revisione](../../../images/tutorials/dataflow/customer-success/review.png)

## Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni sui tassi di acquisizione, sul successo e sugli errori. Per ulteriori informazioni su come monitorare il flusso di dati, consulta l’esercitazione su [monitoraggio di account e flussi di dati nell’interfaccia utente](../monitor.md).

## Elimina il flusso di dati

È possibile eliminare i flussi di dati che non sono più necessari o che sono stati creati in modo errato utilizzando la funzione **[!UICONTROL Elimina]** disponibile nell&#39;area di lavoro **[!UICONTROL Dataflows]**. Per ulteriori informazioni su come eliminare i flussi di dati, consulta l’esercitazione sull’ [eliminazione dei flussi di dati nell’interfaccia utente](../delete.md).

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente un flusso di dati per inserire i dati da un’origine di successo del cliente e hai acquisito informazioni sul monitoraggio dei set di dati. I dati in entrata possono ora essere utilizzati dai servizi a valle [!DNL Platform] come [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i seguenti documenti:

- [Panoramica del profilo cliente in tempo reale](../../../../profile/home.md)
- [Panoramica di Data Science Workspace](../../../../data-science-workspace/home.md)

## Appendice

Le sezioni seguenti forniscono informazioni aggiuntive per l’utilizzo dei connettori sorgente.

### Disattiva un flusso di dati

Quando un flusso di dati viene creato, diventa immediatamente attivo e acquisisce i dati in base alla pianificazione specificata. Puoi disattivare un flusso di dati attivo in qualsiasi momento seguendo le istruzioni riportate di seguito.

Nella schermata **[!UICONTROL Autenticazione]** , seleziona il nome dell’account associato al flusso di dati che desideri disattivare.

![](../../../images/tutorials/dataflow/customer-success/monitor.png)

Viene visualizzata la pagina **[!UICONTROL Attività sorgente]** . Seleziona il flusso di dati attivo dall’elenco per aprire la relativa colonna **[!UICONTROL Proprietà]** sul lato destro dello schermo, che contiene un pulsante di attivazione/disattivazione **[!UICONTROL Attivato]**. Fai clic sull’interruttore per disattivare il flusso di dati. La stessa opzione può essere utilizzata per riattivare un flusso di dati dopo che è stato disabilitato.

![disable](../../../images/tutorials/dataflow/customer-success/disable.png)

### Attivare i dati in entrata per la popolazione [!DNL Profile]

I dati in entrata provenienti dal connettore di origine possono essere utilizzati per arricchire e popolare i dati [!DNL Real-time Customer Profile]. Per ulteriori informazioni sulla compilazione dei dati [!DNL Real-time Customer Profile], consulta l’esercitazione su [Popolazione di profili](../profile.md).
