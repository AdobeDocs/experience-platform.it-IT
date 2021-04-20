---
keywords: Experience Platform;home;argomenti popolari;connessione streaming;creare una connessione streaming;guida interfaccia utente;tutorial;creare una connessione streaming;acquisizione streaming;acquisizione;
solution: Experience Platform
title: Creare una connessione in streaming tramite l’interfaccia utente
topic: tutorial
type: Tutorial
description: Questa guida all’interfaccia utente facilita la creazione di una connessione in streaming tramite Adobe Experience Platform.
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
translation-type: tm+mt
source-git-commit: 3b71f1399a770e097cf75827e626d6d4e289ab77
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---


# Creare una connessione in streaming tramite l’interfaccia utente

Questa esercitazione descrive i passaggi necessari per creare una connessione sorgente in streaming utilizzando l’area di lavoro [!UICONTROL Sources].

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   - [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Creare una connessione in streaming

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sources]** dal menu di navigazione a sinistra per accedere all’area di lavoro [!UICONTROL Sources]. Nella schermata [!UICONTROL Catalog] sono visualizzate diverse sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la categoria **[!UICONTROL Streaming]**, selezionare **[!UICONTROL HTTP API]**, quindi selezionare **[!UICONTROL Add data]**.

![catalogo](../../../../images/tutorials/create/http/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect HTTP API account]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona l’account API HTTP con cui desideri creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Next]** per procedere.

![account esistente](../../../../images/tutorials/create/http/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome account e una descrizione facoltativa. Otterrai anche la possibilità di fornire le seguenti proprietà di configurazione:

- **[!UICONTROL Authentication]:** questa proprietà determina se la connessione in streaming richiede o meno l’autenticazione. L&#39;autenticazione assicura che i dati vengano raccolti da fonti attendibili. Se hai a che fare con Informazioni personali (PII, Personally Identifiable Information), devi attivare questa proprietà. Per impostazione predefinita, questa proprietà è disattivata.
- **[!UICONTROL XDM compatible]:** Questa proprietà indica se questa connessione streaming invierà eventi compatibili con gli schemi XDM. Per impostazione predefinita, questa proprietà è disattivata.

Al termine, selezionare **[!UICONTROL Connect to source]**, quindi selezionare **[!UICONTROL Next]** per continuare.

![nuovo account](../../../../images/tutorials/create/http/new.png)

## Seleziona dati

Dopo aver creato la connessione HTTP API, viene visualizzato il passaggio **[!UICONTROL Select data]** , che fornisce un’interfaccia per caricare e visualizzare in anteprima i dati.

Seleziona **[!UICONTROL Upload files]** per caricare i dati. In alternativa, puoi trascinare i dati nella sezione [!UICONTROL Drag and drop files] dell’interfaccia.

![add-data](../../../../images/tutorials/create/http/add-data.png)

Con i dati caricati, puoi utilizzare il lato destro dell’interfaccia per visualizzare un’anteprima della gerarchia dei file. Selezionare **[!UICONTROL Next]** per continuare.

![preview-sample-data](../../../../images/tutorials/create/http/preview-sample-data.png)

## Mappatura di campi dati su uno schema XDM

Viene visualizzato il passaggio [!UICONTROL Mapping] , che fornisce un’interfaccia per mappare i dati di origine a un set di dati di Platform.

I file di parquet devono essere conformi a XDM e non richiedono la configurazione manuale della mappatura, mentre i file CSV richiedono la configurazione esplicita della mappatura, ma consentono di scegliere quali campi di dati di origine mappare. I file JSON, se contrassegnati come reclamo XDM, non richiedono la configurazione manuale. Tuttavia, se non è contrassegnato come conforme a XDM, sarà necessario configurare esplicitamente la mappatura.

Scegli un set di dati in entrata in cui acquisire i dati. Puoi utilizzare un set di dati esistente o crearne uno nuovo.

### Creare un nuovo set di dati

Per creare un nuovo set di dati, seleziona **[!UICONTROL New dataset]**. Nel modulo visualizzato, fornisci il nome, una descrizione facoltativa e lo schema di destinazione per il set di dati. Se selezioni uno schema abilitato [!DNL Profile], puoi scegliere se il set di dati deve essere abilitato anche [!DNL Profile].

![nuovo set di dati](../../../../images/tutorials/create/http/new-dataset.png)

### Utilizzare un set di dati esistente

Per utilizzare un set di dati esistente, seleziona **[!UICONTROL Existing dataset]**. Nel modulo visualizzato, selezionare il set di dati da utilizzare. Dopo aver selezionato un set di dati, puoi scegliere se il set di dati deve essere abilitato [!DNL Profile].

![set di dati esistente](../../../../images/tutorials/create/http/existing-dataset.png)

### Mappa campi standard

In base alle tue esigenze, puoi scegliere di mappare direttamente i campi oppure utilizzare le funzioni di preparazione dei dati per trasformare i dati di origine in valori calcolati o calcolati. Per ulteriori informazioni sulla mappatura dei dati e sulle funzioni di mappatura, consulta l’esercitazione sulla [mappatura dei dati CSV nei campi dello schema XDM](../../../../../ingestion/tutorials/map-a-csv-file.md).

Per aggiungere un nuovo campo di origine, selezionare **[!UICONTROL Add new mapping]**.

![add-new-mapping](../../../../images/tutorials/create/http/add-new-mapping.png)

Viene visualizzata una nuova associazione di campi di origine e campo di destinazione. Per aggiungere un nuovo campo sorgente, seleziona l’icona a forma di freccia accanto alla barra di input [!UICONTROL Select source field].

![select-source-field](../../../../images/tutorials/create/http/select-source-field.png)

Il pannello [!UICONTROL Select attributes] ti consente di esplorare la gerarchia dei file e selezionare un campo di origine specifico da mappare a un campo XDM di destinazione. Dopo aver selezionato il campo di origine da mappare, selezionare **[!UICONTROL Select]** per continuare.

![select-attributes](../../../../images/tutorials/create/http/select-attributes.png)

Selezionando un campo di origine, ora è possibile identificare il campo XDM di destinazione appropriato da mappare. Seleziona l’icona dello schema nella sezione del campo di destinazione.

![select-target-field](../../../../images/tutorials/create/http/select-target-field.png)

Viene visualizzata la finestra [!UICONTROL Map source field to target field] che fornisce un’interfaccia per esplorare lo schema del set di dati di destinazione. Selezionare il campo di destinazione corrispondente al campo di origine, quindi selezionare **[!UICONTROL Select]** per continuare.

![map-to-target-field](../../../../images/tutorials/create/http/map-to-target-field.png)

Una volta mappati i campi di origine sui campi XDM di destinazione appropriati, seleziona **[!UICONTROL Next]**

![data-prep-complete](../../../../images/tutorials/create/http/data-prep-complete.png)

## Dettaglio flusso di dati

Viene visualizzato il passaggio **[!UICONTROL Dataflow detail]** . In questa pagina puoi fornire i dettagli del flusso di dati creato assegnando un nome e una descrizione facoltativa.

Dopo aver fornito i dettagli per il flusso di dati, seleziona **[!UICONTROL Next]**.

![dettaglio del flusso di dati](../../../../images/tutorials/create/http/dataflow-detail.png)

## Revisione

Viene visualizzato il passaggio **[!UICONTROL Review]** , che consente di controllare i dettagli del flusso di dati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

- **[!UICONTROL Connection]**: Mostra il nome dell’account, la piattaforma di origine e il nome dell’origine.
- **[!UICONTROL Assign dataset and map fields]**: Mostra il set di dati di destinazione e lo schema a cui il set di dati aderisce.

Dopo aver confermato che i dettagli sono corretti, seleziona **[!UICONTROL Finish]**.

![revisione](../../../../images/tutorials/create/http/review.png)

## Ottieni URL endpoint di streaming

Con la connessione creata, viene visualizzata la pagina dei dettagli delle sorgenti. Questa pagina mostra i dettagli della nuova connessione appena creata, inclusi i flussi di dati, l’ID e l’URL dell’endpoint di streaming precedentemente eseguiti.

![endpoint](../../../../images/tutorials/create/http/endpoint.png)

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione HTTP in streaming che ti consente di utilizzare l’endpoint di streaming per accedere a una varietà di API [!DNL Data Ingestion]. Per istruzioni su come creare una connessione in streaming nell&#39;API, leggi l&#39; [esercitazione sulla creazione di una connessione in streaming](../../../api/create/streaming/http.md).

Per informazioni su come eseguire lo streaming dei dati su Platform, leggi l’esercitazione su [dati in streaming della serie temporale](../../../../../ingestion/tutorials/streaming-time-series-data.md) o l’esercitazione su [dati in streaming record](../../../../../ingestion/tutorials/streaming-record-data.md).
