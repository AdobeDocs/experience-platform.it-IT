---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Configurare un flusso di dati per un connettore pubblicitario nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 91bc87a6dcaf5c2d58da429712f010643c400a7a

---


# Configurare un flusso di dati per un connettore pubblicitario nell&#39;interfaccia utente

Un flusso di dati è un&#39;attività pianificata che recupera e trasferisce dati da un&#39;origine a un set di dati Adobe Experience Platform. Questa esercitazione fornisce i passaggi per configurare un nuovo flusso di dati utilizzando l&#39;account pubblicitario.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Sistema](../../../../xdm/home.md)XDM (Experience Data Model): Il framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   - [Nozioni di base sulla composizione](../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [Profilo](../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Inoltre, questa esercitazione richiede che sia già stato creato un account pubblicitario. Un elenco di esercitazioni per la creazione di diversi connettori di pagamento nell&#39;interfaccia utente è disponibile nella panoramica [dei connettori](../../../home.md)sorgente.

## Seleziona dati

Dopo aver creato l&#39;account pubblicitario, viene visualizzato il passaggio *Seleziona dati* , che fornisce un&#39;interfaccia interattiva per esplorare la gerarchia dei file.

- La metà sinistra dell&#39;interfaccia è un browser di directory che visualizza i file e le directory del server.
- La metà destra dell&#39;interfaccia consente di visualizzare in anteprima fino a 100 righe di dati da un file compatibile.

Selezionate la directory da utilizzare, quindi selezionate **Avanti**.

![add-data](../../../images/tutorials/dataflow/advertising/add-data.png)

## Mappatura dei campi dati su uno schema XDM

Viene visualizzato il passaggio *Mapping* , che fornisce un&#39;interfaccia interattiva per mappare i dati di origine a un set di dati della piattaforma.

Scegliere un set di dati in entrata in cui assimilare i dati. È possibile utilizzare un set di dati esistente o crearne uno nuovo.

### Utilizzare un dataset esistente

Per assimilare i dati in un set di dati esistente, selezionare **Usa set di dati** esistente, quindi fare clic sull&#39;icona del set di dati.

![use-existing-dataset](../../../images/tutorials/dataflow/advertising/use-existing-target-dataset.png)

Viene visualizzata la finestra di dialogo *Seleziona set di dati* . Individuate il set di dati da utilizzare, selezionatelo, quindi fate clic su **Continue (Continua)**.

![select-existing-dataset](../../../images/tutorials/dataflow/advertising/select-existing-dataset.png)

### Utilizza un nuovo set di dati

Per inserire i dati in un nuovo dataset, selezionare **Crea nuovo dataset** e immettere un nome e una descrizione per il dataset nei campi forniti.

Durante questo processo, potete anche abilitare l&#39;assimilazione *parziale* e la diagnostica ** degli errori. L&#39;abilitazione dell&#39;inserimento ** parziale consente di assimilare i dati contenenti errori, fino a un determinato limite che è possibile impostare. L&#39;attivazione della diagnostica degli errori fornisce dettagli su eventuali dati errati che vengono inseriti separatamente in batch. Per ulteriori informazioni, consultate la panoramica sull’assimilazione [parziale dei](../../../../ingestion/batch-ingestion/partial.md)batch.

Al termine, fare clic sull&#39;icona dello schema.

![create-new-dataset](../../../images/tutorials/dataflow/advertising/new-target-dataset.png)

Viene visualizzata la finestra di dialogo *Seleziona schema* . Selezionare lo schema da applicare al nuovo dataset, quindi fare clic su **Fine**.

![select-schema](../../../images/tutorials/dataflow/advertising/select-existing-schema.png)

In base alle esigenze, è possibile scegliere di mappare direttamente i campi oppure utilizzare le funzioni di mappatura per trasformare i dati di origine in modo da derivare i valori calcolati o calcolati. Per ulteriori informazioni sulla mappatura dei dati e sulle funzioni di mappatura, consulta l’esercitazione sulla [mappatura dei dati CSV ai campi](../../../../ingestion/tutorials/map-a-csv-file.md)dello schema XDM.

La schermata *Mapping* consente inoltre di impostare la colonna ** Delta. Quando si crea il flusso di dati, è possibile impostare qualsiasi campo di marca temporale come base per decidere quali record acquisire nelle assimilazioni incrementali pianificate.

Una volta mappati i dati di origine, fare clic su **Avanti**.

![](../../../images/tutorials/dataflow/advertising/mapping.png)

## Pianificare le esecuzioni dell&#39;assimilazione

Viene visualizzato il passaggio *Pianificazione* , che consente di configurare una pianificazione di assimilazione per l&#39;acquisizione automatica dei dati di origine selezionati tramite le mappature configurate. Nella tabella seguente sono riportati i diversi campi configurabili per la pianificazione:

| Field | Descrizione |
| --- | --- |
| Frequenza | Le frequenze selezionabili sono: Minuto, Ora, Giorno e Settimana. |
| Intervallo | Un numero intero che imposta l&#39;intervallo per la frequenza selezionata. |
| Ora di inizio | Una marca temporale UTC per la quale si verificherà la prima assimilazione. |
| Backfill | Un valore booleano che determina i dati inizialmente acquisiti. Se *Backfill* è abilitato, tutti i file correnti nel percorso specificato verranno acquisiti durante la prima assimilazione pianificata. Se *Backfill* è disattivato, verranno acquisiti solo i file caricati tra la prima esecuzione dell&#39;assimilazione e l&#39;ora *di* inizio. I file caricati prima dell&#39;ora *di* inizio non vengono acquisiti. |

I flussi di dati sono progettati per l&#39;acquisizione automatica dei dati su base programmata. Se desiderate effettuare il caricamento solo una volta in questo flusso di lavoro, potete farlo configurando la **Frequenza** su &quot;Giorno&quot; e applicando un numero molto elevato per l&#39; **Intervallo**, ad esempio 10000 o simile.

Immettete i valori per la pianificazione e fate clic su **Avanti**.

![programmazione](../../../images/tutorials/dataflow/advertising/schedule.png)

## Denominate il flusso di dati

Viene visualizzato il passaggio Dettaglio *flusso* DataSet, in cui è necessario specificare un nome e una descrizione facoltativa per il flusso di dataset. Al termine, selezionate **Avanti** .

![dataset-flow-details](../../../images/tutorials/dataflow/advertising/dataset-flow-detail.png)

## Controlla il flusso dei dataset

Viene visualizzato il passaggio *Revisione* , che consente di rivedere il nuovo flusso di dati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

- *Connessione*: Mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all&#39;interno del file di origine.
- *Assegna campi* dataset e mappa: Mostra il set di dati in cui vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati aderisce.
- *Pianificazione*: Mostra il periodo, la frequenza e l’intervallo attivi della pianificazione di assimilazione.

Dopo aver rivisto il flusso di dati, fai clic su **Fine** e concedi un po&#39; di tempo per la creazione del flusso di dati.

![review](../../../images/tutorials/dataflow/advertising/review.png)

## Monitorare il flusso dei dataset

Una volta creato il flusso di set di dati, è possibile monitorare i dati che vengono acquisiti attraverso di esso. Per ulteriori informazioni su come monitorare i flussi di dataset, vedere l&#39;esercitazione sugli [account e sui flussi](../monitor.md)di dataset.

## Passaggi successivi

Seguendo questa esercitazione, hai creato con successo un flusso di dataset per inserire i dati da un sistema di automazione marketing e hai acquisito informazioni sul monitoraggio dei set di dati. I dati in entrata possono ora essere utilizzati dai servizi della piattaforma a valle, come Profilo cliente in tempo reale e Data Science Workspace. Per ulteriori informazioni, consulta i documenti seguenti:

- [Panoramica del profilo cliente in tempo reale](../../../../profile/home.md)
- [Panoramica di Analysis Workspace](../../../../data-science-workspace/home.md)

## Appendice

Le sezioni seguenti forniscono informazioni aggiuntive sull&#39;utilizzo dei connettori di origine.

### Disattivazione di un flusso di dati

Quando viene creato un flusso di dati, esso diventa immediatamente attivo e acquisisce i dati in base alla pianificazione assegnata. È possibile disattivare un flusso di dataset attivo in qualsiasi momento seguendo le istruzioni riportate di seguito.

Nella schermata *Flussi* di dati, selezionare il nome del flusso di dati da disattivare.

![browse-dataset-flow](../../../images/tutorials/dataflow/advertising/view-dataset-flows.png)

La colonna *Proprietà* viene visualizzata sul lato destro della schermata. Questo pannello contiene un pulsante di attivazione **abilitata** . Fate clic sull’interruttore per disattivare il flusso di dati. La stessa opzione può essere utilizzata per riattivare un flusso di dati dopo che è stato disabilitato.

![disable](../../../images/tutorials/dataflow/advertising/disable.png)

### Attivare i dati in entrata per la popolazione del profilo

I dati in entrata provenienti dal connettore di origine possono essere utilizzati per arricchire e compilare i dati del profilo cliente in tempo reale. Per ulteriori informazioni sulla compilazione dei dati del profilo del cliente reale, consulta l’esercitazione sulla popolazione [del](../profile.md)profilo.
