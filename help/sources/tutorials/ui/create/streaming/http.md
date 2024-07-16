---
title: Creare una connessione in streaming API HTTP tramite l’interfaccia utente
description: Questa guida dell’interfaccia utente ti aiuterà a creare una connessione in streaming utilizzando Adobe Experience Platform.
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
source-git-commit: de721d204cda8e55c72ac5f530b89b2275d94306
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 1%

---


# Crea una connessione in streaming [!DNL HTTP API] tramite l&#39;interfaccia utente

Questa esercitazione fornisce i passaggi per la creazione di una connessione a un&#39;origine di streaming utilizzando l&#39;area di lavoro [!UICONTROL Sources].

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   - [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Creare una connessione in streaming

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria **[!UICONTROL Streaming]**, selezionare **[!UICONTROL API HTTP]**, quindi **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/http/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti account API HTTP]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona l&#39;account API HTTP con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Avanti]** per continuare.

![account-esistente](../../../../images/tutorials/create/http/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome account e una descrizione facoltativa. È inoltre possibile specificare le seguenti proprietà di configurazione:

- **[!UICONTROL Autenticazione]:** Questa proprietà determina se la connessione streaming richiede o meno l&#39;autenticazione. L’autenticazione garantisce che i dati vengano raccolti da fonti attendibili. Se hai a che fare con informazioni personali (PII, Personally Identifiable Information), devi attivare questa proprietà. Per impostazione predefinita, questa proprietà è disattivata.
- **[!UICONTROL Compatibile con XDM]:** Questa proprietà indica se la connessione di streaming invierà eventi compatibili con gli schemi XDM. Per impostazione predefinita, questa proprietà è disattivata.

Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]**, quindi selezionare **[!UICONTROL Avanti]** per continuare.

![nuovo-account](../../../../images/tutorials/create/http/new.png)

## Selezionare i dati

Dopo aver creato la connessione API HTTP, viene visualizzato il passaggio **[!UICONTROL Seleziona dati]** che fornisce un&#39;interfaccia per caricare e visualizzare in anteprima i dati.

Seleziona **[!UICONTROL Carica file]** per caricare i dati. In alternativa, è possibile trascinare e rilasciare i dati nella sezione [!UICONTROL Trascinare i file] dell&#39;interfaccia.

![add-data](../../../../images/tutorials/create/http/add-data.png)

Con i dati caricati, puoi utilizzare il lato destro dell’interfaccia per visualizzare in anteprima la gerarchia dei file. Seleziona **[!UICONTROL Avanti]** per procedere.

![preview-sample-data](../../../../images/tutorials/create/http/preview-sample-data.png)

## Mappare i campi dati su uno schema XDM

Viene visualizzato il passaggio [!UICONTROL Mappatura] che fornisce un&#39;interfaccia per mappare i dati di origine su un set di dati di Platform.

L&#39;origine [!DNL HTTP API] supporta l&#39;acquisizione di file JSON. I file JSON non richiedono la configurazione manuale se sono contrassegnati come XDM-complaints. In caso contrario, devi configurare esplicitamente la mappatura.

Scegli un set di dati per i dati in entrata da acquisire in. Puoi utilizzare un set di dati esistente o crearne uno nuovo.

### Creare un nuovo set di dati

Per creare un nuovo set di dati, selezionare **[!UICONTROL Nuovo set di dati]**. Nel modulo visualizzato, fornisci il nome, una descrizione facoltativa e lo schema di destinazione per il set di dati. Se si seleziona uno schema abilitato per [!DNL Profile], è possibile scegliere se anche il set di dati deve essere abilitato per [!DNL Profile].

![nuovo-set di dati](../../../../images/tutorials/create/http/new-dataset.png)

### Usa un set di dati esistente

Per utilizzare un set di dati esistente, selezionare **[!UICONTROL Set di dati esistente]**. Nella maschera visualizzata selezionare il set di dati che si desidera utilizzare. Dopo aver selezionato un set di dati, puoi scegliere se il set di dati deve essere abilitato per [!DNL Profile].

![set di dati esistente](../../../../images/tutorials/create/http/existing-dataset.png)

### Mappa campi standard

In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull&#39;utilizzo dell&#39;interfaccia mapper e dei campi calcolati, consulta la [guida dell&#39;interfaccia utente della preparazione dati](../../../../../data-prep/ui/mapping.md).

Per aggiungere un nuovo campo di origine, selezionare **[!UICONTROL Aggiungi nuova mappatura]**.

![aggiungi-nuovo-mapping](../../../../images/tutorials/create/http/add-new-mapping.png)

Viene visualizzata una nuova coppia di campi sorgente e di destinazione. Per aggiungere un nuovo campo di origine, selezionare l&#39;icona freccia accanto alla barra di input [!UICONTROL Seleziona campo di origine].

![select-source-field](../../../../images/tutorials/create/http/select-source-field.png)

Il pannello [!UICONTROL Seleziona attributi] consente di esplorare la gerarchia dei file e selezionare un campo di origine specifico da mappare a un campo XDM di destinazione. Dopo aver selezionato il campo di origine da mappare, seleziona **[!UICONTROL Seleziona]** per continuare.

![select-attributes](../../../../images/tutorials/create/http/select-attributes.png)

Con un campo sorgente selezionato, ora puoi identificare il campo XDM di destinazione appropriato a cui eseguire il mapping. Seleziona l’icona schema nella sezione del campo di destinazione.

![select-target-field](../../../../images/tutorials/create/http/select-target-field.png)

Viene visualizzata la finestra [!UICONTROL Mappa il campo di origine al campo di destinazione], che fornisce un&#39;interfaccia per esplorare lo schema del set di dati di destinazione. Seleziona il campo di destinazione che corrisponde al campo di origine, quindi seleziona **[!UICONTROL Seleziona]** per continuare.

![mappa-campo-destinazione](../../../../images/tutorials/create/http/map-to-target-field.png)

Una volta mappati tutti i campi sorgente ai campi XDM di destinazione appropriati, seleziona **[!UICONTROL Successivo]**

![preparazione dati-completata](../../../../images/tutorials/create/http/data-prep-complete.png)

## Dettaglio del flusso di dati

Viene visualizzato il passaggio **[!UICONTROL Dettagli flusso di dati]**. In questa pagina puoi fornire dettagli per il flusso di dati creato assegnando un nome e una descrizione facoltativa.

Dopo aver fornito i dettagli per il flusso di dati, seleziona **[!UICONTROL Avanti]**.

![dettagli flusso di dati](../../../../images/tutorials/create/http/dataflow-detail.png)

## Controlla

Viene visualizzato il passaggio **[!UICONTROL Rivedi]**, che consente di rivedere i dettagli del flusso di dati prima che venga creato. I dettagli sono raggruppati nelle seguenti categorie:

- **[!UICONTROL Connessione]**: mostra il nome dell&#39;account, la piattaforma di origine e il nome dell&#39;origine.
- **[!UICONTROL Assegna set di dati e mappa campi]**: mostra il set di dati di destinazione e lo schema a cui il set di dati è conforme.

Dopo aver confermato che i dettagli sono corretti, selezionare **[!UICONTROL Fine]**.

![revisione](../../../../images/tutorials/create/http/review.png)

## Ottieni URL endpoint di streaming

Una volta creata la connessione, viene visualizzata la pagina dei dettagli delle origini. Questa pagina mostra i dettagli della connessione appena creata, inclusi i flussi di dati, l’ID e l’URL dell’endpoint di streaming eseguiti in precedenza.

![endpoint](../../../../images/tutorials/create/http/endpoint.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione HTTP di streaming che consente di utilizzare l&#39;endpoint di streaming per accedere a diverse API [!DNL Data Ingestion]. Per istruzioni su come creare una connessione in streaming nell&#39;API, consulta l&#39;[esercitazione sulla creazione di una connessione in streaming](../../../api/create/streaming/http.md).

Per informazioni su come inviare dati a Platform in streaming, leggi l&#39;esercitazione su [dati di streaming serie temporale](../../../../../ingestion/tutorials/streaming-time-series-data.md) o l&#39;esercitazione su [dati di streaming record](../../../../../ingestion/tutorials/streaming-record-data.md).
