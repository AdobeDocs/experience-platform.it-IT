---
keywords: Experience Platform;home;argomenti popolari;connessione streaming;creare una connessione streaming;guida interfaccia utente;tutorial;creare una connessione streaming;acquisizione streaming;acquisizione;
solution: Experience Platform
title: Creare una connessione di streaming API HTTP utilizzando l’interfaccia utente
topic-legacy: tutorial
type: Tutorial
description: Questa guida all’interfaccia utente facilita la creazione di una connessione in streaming tramite Adobe Experience Platform.
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
source-git-commit: f5d341daffd7d4d77ee816cc7537b0d0c52ca636
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 0%

---


# Crea un [!DNL HTTP API] connessione in streaming tramite l’interfaccia utente

Questa esercitazione descrive i passaggi necessari per creare una connessione sorgente in streaming utilizzando [!UICONTROL Origini] workspace.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   - [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Creare una connessione in streaming

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in questa schermata vengono visualizzate diverse sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la **[!UICONTROL Streaming]** categoria, seleziona **[!UICONTROL API HTTP]** quindi seleziona **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/http/catalog.png)

La **[!UICONTROL Connetti account API HTTP]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona l’account API HTTP con cui desideri creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![account esistente](../../../../images/tutorials/create/http/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, specificare un nome account e una descrizione facoltativa. Otterrai anche la possibilità di fornire le seguenti proprietà di configurazione:

- **[!UICONTROL Autenticazione]:** Questa proprietà determina se la connessione in streaming richiede o meno l’autenticazione. L&#39;autenticazione assicura che i dati vengano raccolti da fonti attendibili. Se hai a che fare con Informazioni personali (PII, Personally Identifiable Information), devi attivare questa proprietà. Per impostazione predefinita, questa proprietà è disattivata.
- **[!UICONTROL Compatibilità XDM]:** Questa proprietà indica se questa connessione streaming invierà eventi compatibili con gli schemi XDM. Per impostazione predefinita, questa proprietà è disattivata.

Al termine, seleziona **[!UICONTROL Connetti alla sorgente]** quindi seleziona **[!UICONTROL Successivo]** per procedere.

![nuovo account](../../../../images/tutorials/create/http/new.png)

## Seleziona dati

Dopo aver creato la connessione API HTTP, la **[!UICONTROL Seleziona dati]** viene visualizzato un passaggio che fornisce un’interfaccia per caricare e visualizzare in anteprima i dati.

Seleziona **[!UICONTROL Caricare file]** per caricare i dati. In alternativa, puoi trascinare e rilasciare i dati nella [!UICONTROL Trascinamento di file] della sezione dell&#39;interfaccia.

![add-data](../../../../images/tutorials/create/http/add-data.png)

Con i dati caricati, puoi utilizzare il lato destro dell’interfaccia per visualizzare un’anteprima della gerarchia dei file. Seleziona **[!UICONTROL Successivo]** per procedere.

![preview-sample-data](../../../../images/tutorials/create/http/preview-sample-data.png)

## Mappatura di campi dati su uno schema XDM

La [!UICONTROL Mappatura] viene visualizzato un passaggio che fornisce un’interfaccia per mappare i dati di origine a un set di dati di Platform.

I file di parquet devono essere conformi a XDM e non richiedono la configurazione manuale della mappatura, mentre i file CSV richiedono la configurazione esplicita della mappatura, ma consentono di scegliere quali campi di dati di origine mappare. I file JSON, se contrassegnati come reclamo XDM, non richiedono la configurazione manuale. Tuttavia, se non è contrassegnato come conforme a XDM, sarà necessario configurare esplicitamente la mappatura.

Scegli un set di dati in entrata in cui acquisire i dati. Puoi utilizzare un set di dati esistente o crearne uno nuovo.

### Creare un nuovo set di dati

Per creare un nuovo set di dati, seleziona **[!UICONTROL Nuovo set di dati]**. Nel modulo visualizzato, fornisci il nome, una descrizione facoltativa e lo schema di destinazione per il set di dati. Se selezioni un [!DNL Profile]Schema abilitato, puoi scegliere se anche il set di dati deve essere [!DNL Profile]-abilitato.

![nuovo set di dati](../../../../images/tutorials/create/http/new-dataset.png)

### Utilizzare un set di dati esistente

Per utilizzare un set di dati esistente, seleziona **[!UICONTROL Set di dati esistente]**. Nel modulo visualizzato, selezionare il set di dati da utilizzare. Una volta selezionato un set di dati, puoi scegliere se il set di dati deve essere [!DNL Profile]-abilitato.

![set di dati esistente](../../../../images/tutorials/create/http/existing-dataset.png)

### Mappa campi standard


In base alle tue esigenze, puoi scegliere di mappare direttamente i campi oppure utilizzare le funzioni di preparazione dei dati per trasformare i dati di origine in valori calcolati o calcolati. Per i passaggi completi sull’utilizzo dell’interfaccia di mappatura e dei campi calcolati, consulta la sezione [Guida all’interfaccia utente della preparazione dei dati](../../../../../data-prep/ui/mapping.md).

Per aggiungere un nuovo campo di origine, selezionare **[!UICONTROL Aggiungi nuova mappatura]**.

![add-new-mapping](../../../../images/tutorials/create/http/add-new-mapping.png)

Viene visualizzata una nuova associazione di campi di origine e campo di destinazione. Per aggiungere un nuovo campo di origine, seleziona l’icona a forma di freccia accanto al campo [!UICONTROL Selezionare il campo di origine] barra di ingresso.

![select-source-field](../../../../images/tutorials/create/http/select-source-field.png)

La [!UICONTROL Seleziona attributi] Il pannello ti consente di esplorare la gerarchia dei file e selezionare un campo sorgente specifico da mappare a un campo XDM di destinazione. Dopo aver selezionato il campo sorgente da mappare, seleziona **[!UICONTROL Seleziona]** per procedere.

![select-attributes](../../../../images/tutorials/create/http/select-attributes.png)

Selezionando un campo di origine, ora è possibile identificare il campo XDM di destinazione appropriato da mappare. Seleziona l’icona dello schema nella sezione del campo di destinazione.

![select-target-field](../../../../images/tutorials/create/http/select-target-field.png)

La [!UICONTROL Mappatura del campo sorgente su un campo di destinazione] viene visualizzata una finestra che fornisce un’interfaccia per esplorare lo schema del set di dati di destinazione. Selezionare il campo di destinazione corrispondente al campo di origine, quindi selezionare **[!UICONTROL Seleziona]** per procedere.

![map-to-target-field](../../../../images/tutorials/create/http/map-to-target-field.png)

Una volta mappati i campi di origine ai campi XDM di destinazione appropriati, seleziona **[!UICONTROL Successivo]**

![data-prep-complete](../../../../images/tutorials/create/http/data-prep-complete.png)

## Dettaglio flusso di dati

La **[!UICONTROL Dettaglio flusso di dati]** viene visualizzato il passaggio . In questa pagina puoi fornire i dettagli del flusso di dati creato assegnando un nome e una descrizione facoltativa.

Dopo aver fornito i dettagli per il flusso di dati, seleziona **[!UICONTROL Successivo]**.

![dettaglio del flusso di dati](../../../../images/tutorials/create/http/dataflow-detail.png)

## Revisione

La **[!UICONTROL Revisione]** viene visualizzato un passaggio che ti consente di rivedere i dettagli del flusso di dati prima che venga creato. I dettagli sono raggruppati nelle seguenti categorie:

- **[!UICONTROL Connessione]**: Mostra il nome dell’account, la piattaforma di origine e il nome dell’origine.
- **[!UICONTROL Assegna set di dati e mappa campi]**: Mostra il set di dati di destinazione e lo schema a cui il set di dati aderisce.

Dopo aver confermato la correttezza dei dettagli, seleziona **[!UICONTROL Fine]**.

![revisione](../../../../images/tutorials/create/http/review.png)

## Ottieni URL endpoint di streaming

Con la connessione creata, viene visualizzata la pagina dei dettagli delle sorgenti. Questa pagina mostra i dettagli della nuova connessione appena creata, inclusi i flussi di dati, l’ID e l’URL dell’endpoint di streaming precedentemente eseguiti.

![endpoint](../../../../images/tutorials/create/http/endpoint.png)

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione HTTP in streaming, consentendoti di utilizzare l’endpoint di streaming per accedere a una varietà di [!DNL Data Ingestion] API. Per istruzioni su come creare una connessione in streaming nell’API, leggi la [creazione di un&#39;esercitazione sulla connessione in streaming](../../../api/create/streaming/http.md).

Per informazioni su come inviare dati a Platform, consulta l’esercitazione su [dati in streaming](../../../../../ingestion/tutorials/streaming-time-series-data.md) o l&#39;esercitazione su [dati di registrazione in streaming](../../../../../ingestion/tutorials/streaming-record-data.md).
