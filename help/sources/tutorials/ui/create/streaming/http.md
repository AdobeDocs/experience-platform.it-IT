---
keywords: Experience Platform;home;argomenti popolari;connessione streaming;creare una connessione streaming;guida interfaccia utente;tutorial;creare una connessione streaming;acquisizione streaming;acquisizione;
solution: Experience Platform
title: Creare una connessione in streaming tramite l’interfaccia utente
topic-legacy: tutorial
type: Tutorial
description: Questa guida all’interfaccia utente facilita la creazione di una connessione in streaming tramite Adobe Experience Platform.
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
source-git-commit: df6ddf52f5cab7e5faae591594f060d641977783
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 0%

---


# Creare una connessione in streaming tramite l’interfaccia utente

Questa esercitazione fornisce passaggi per la creazione di una connessione sorgente in streaming utilizzando l&#39;area di lavoro [!UICONTROL Sorgenti].

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   - [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Creare una connessione in streaming

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all’area di lavoro [!UICONTROL Origini]. La schermata [!UICONTROL Catalogo] visualizza una varietà di sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la categoria **[!UICONTROL Streaming]**, seleziona **[!UICONTROL API HTTP]**, quindi seleziona **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/http/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti account API HTTP]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona l’account API HTTP con cui desideri creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Avanti]** per continuare.

![account esistente](../../../../images/tutorials/create/http/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, specificare un nome account e una descrizione facoltativa. Otterrai anche la possibilità di fornire le seguenti proprietà di configurazione:

- **[!UICONTROL Autenticazione]:** questa proprietà determina se la connessione in streaming richiede o meno l’autenticazione. L&#39;autenticazione assicura che i dati vengano raccolti da fonti attendibili. Se hai a che fare con Informazioni personali (PII, Personally Identifiable Information), devi attivare questa proprietà. Per impostazione predefinita, questa proprietà è disattivata.
- **[!UICONTROL Compatibile con XDM]:** questa proprietà indica se questa connessione streaming invierà eventi compatibili con gli schemi XDM. Per impostazione predefinita, questa proprietà è disattivata.

Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]**, quindi selezionare **[!UICONTROL Avanti]** per continuare.

![nuovo account](../../../../images/tutorials/create/http/new.png)

## Seleziona dati

Dopo aver creato la connessione HTTP API, viene visualizzato il passaggio **[!UICONTROL Seleziona dati]** , che fornisce un&#39;interfaccia per caricare e visualizzare in anteprima i dati.

Seleziona **[!UICONTROL Carica file]** per caricare i dati. In alternativa, puoi trascinare e rilasciare i tuoi dati nella sezione [!UICONTROL Trascina e rilascia i file] dell&#39;interfaccia.

![add-data](../../../../images/tutorials/create/http/add-data.png)

Con i dati caricati, puoi utilizzare il lato destro dell’interfaccia per visualizzare un’anteprima della gerarchia dei file. Selezionare **[!UICONTROL Avanti]** per continuare.

![preview-sample-data](../../../../images/tutorials/create/http/preview-sample-data.png)

## Mappatura di campi dati su uno schema XDM

Viene visualizzato il passaggio [!UICONTROL Mapping] , che fornisce un’interfaccia per mappare i dati di origine a un set di dati della Platform.

I file di parquet devono essere conformi a XDM e non richiedono la configurazione manuale della mappatura, mentre i file CSV richiedono la configurazione esplicita della mappatura, ma consentono di scegliere quali campi di dati di origine mappare. I file JSON, se contrassegnati come reclamo XDM, non richiedono la configurazione manuale. Tuttavia, se non è contrassegnato come conforme a XDM, sarà necessario configurare esplicitamente la mappatura.

Scegli un set di dati in entrata in cui acquisire i dati. Puoi utilizzare un set di dati esistente o crearne uno nuovo.

### Creare un nuovo set di dati

Per creare un nuovo set di dati, seleziona **[!UICONTROL Nuovo set di dati]**. Nel modulo visualizzato, fornisci il nome, una descrizione facoltativa e lo schema di destinazione per il set di dati. Se selezioni uno schema abilitato [!DNL Profile], puoi scegliere se il set di dati deve essere abilitato anche [!DNL Profile].

![nuovo set di dati](../../../../images/tutorials/create/http/new-dataset.png)

### Utilizzare un set di dati esistente

Per utilizzare un set di dati esistente, seleziona **[!UICONTROL Set di dati esistente]**. Nel modulo visualizzato, selezionare il set di dati da utilizzare. Dopo aver selezionato un set di dati, puoi scegliere se il set di dati deve essere abilitato [!DNL Profile].

![set di dati esistente](../../../../images/tutorials/create/http/existing-dataset.png)

### Mappa campi standard

In base alle tue esigenze, puoi scegliere di mappare direttamente i campi oppure utilizzare le funzioni di preparazione dei dati per trasformare i dati di origine in valori calcolati o calcolati. Per ulteriori informazioni sulle funzioni di mappatura e sui campi calcolati, consulta la [Guida alle funzioni di preparazione dei dati](../../../../../data-prep/functions.md) o la [guida ai campi calcolati](../../../../../data-prep/calculated-fields.md).

Per aggiungere un nuovo campo di origine, selezionare **[!UICONTROL Aggiungi nuova mappatura]**.

![add-new-mapping](../../../../images/tutorials/create/http/add-new-mapping.png)

Viene visualizzata una nuova associazione di campi di origine e campo di destinazione. Per aggiungere un nuovo campo sorgente, seleziona l’icona a forma di freccia accanto alla barra di input [!UICONTROL Seleziona campo sorgente].

![select-source-field](../../../../images/tutorials/create/http/select-source-field.png)

Il pannello [!UICONTROL Seleziona attributi] ti consente di esplorare la gerarchia dei file e selezionare un campo di origine specifico da mappare a un campo XDM di destinazione. Dopo aver selezionato il campo di origine da mappare, selezionare **[!UICONTROL Seleziona]** per continuare.

![select-attributes](../../../../images/tutorials/create/http/select-attributes.png)

Selezionando un campo di origine, ora è possibile identificare il campo XDM di destinazione appropriato da mappare. Seleziona l’icona dello schema nella sezione del campo di destinazione.

![select-target-field](../../../../images/tutorials/create/http/select-target-field.png)

Viene visualizzata la finestra [!UICONTROL Mappa campo di origine sul campo di destinazione] , che offre un’interfaccia per esplorare lo schema del set di dati di destinazione. Seleziona il campo di destinazione che corrisponde al campo di origine, quindi seleziona **[!UICONTROL Seleziona]** per continuare.

![map-to-target-field](../../../../images/tutorials/create/http/map-to-target-field.png)

Una volta mappati i campi di origine sui campi XDM di destinazione appropriati, seleziona **[!UICONTROL Avanti]**

![data-prep-complete](../../../../images/tutorials/create/http/data-prep-complete.png)

## Dettaglio flusso di dati

Viene visualizzato il passaggio **[!UICONTROL Dettaglio flusso di dati]** . In questa pagina puoi fornire i dettagli del flusso di dati creato assegnando un nome e una descrizione facoltativa.

Dopo aver fornito i dettagli per il flusso di dati, seleziona **[!UICONTROL Avanti]**.

![dettaglio del flusso di dati](../../../../images/tutorials/create/http/dataflow-detail.png)

## Revisione

Viene visualizzato il passaggio **[!UICONTROL Rivedi]** , che consente di esaminare i dettagli del flusso di dati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

- **[!UICONTROL Connessione]**: Mostra il nome dell’account, la piattaforma di origine e il nome dell’origine.
- **[!UICONTROL Assegna set di dati e campi]** mappa: Mostra il set di dati di destinazione e lo schema a cui il set di dati aderisce.

Dopo aver confermato che i dettagli sono corretti, selezionare **[!UICONTROL Fine]**.

![revisione](../../../../images/tutorials/create/http/review.png)

## Ottieni URL endpoint di streaming

Con la connessione creata, viene visualizzata la pagina dei dettagli delle sorgenti. Questa pagina mostra i dettagli della nuova connessione appena creata, inclusi i flussi di dati, l’ID e l’URL dell’endpoint di streaming precedentemente eseguiti.

![endpoint](../../../../images/tutorials/create/http/endpoint.png)

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione HTTP in streaming che ti consente di utilizzare l’endpoint di streaming per accedere a una varietà di API [!DNL Data Ingestion]. Per istruzioni su come creare una connessione in streaming nell&#39;API, leggi l&#39; [esercitazione sulla creazione di una connessione in streaming](../../../api/create/streaming/http.md).

Per informazioni su come eseguire lo streaming dei dati su Platform, leggi l’esercitazione su [dati in streaming della serie temporale](../../../../../ingestion/tutorials/streaming-time-series-data.md) o l’esercitazione su [dati in streaming record](../../../../../ingestion/tutorials/streaming-record-data.md).
