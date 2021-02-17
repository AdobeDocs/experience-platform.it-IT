---
keywords: ' Experience Platform;home;argomenti più comuni;collegamento in streaming;creare una connessione in streaming;ui guide;tutorial;creare una connessione in streaming;streaming, assimilazione;assimilazione;'
solution: Experience Platform
title: Creare una connessione in streaming utilizzando l'interfaccia utente
topic: tutorial
type: Tutorial
description: Questa guida all'interfaccia utente consente di creare una connessione in streaming utilizzando Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: a4019227abaddd9dbe143899d273580ebf21849e
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---


# Creare una connessione in streaming utilizzando l&#39;interfaccia utente

Questa guida all&#39;interfaccia utente consente di creare una connessione in streaming utilizzando Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standard con cui  [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza dei clienti.
   - [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Creare una connessione in streaming

Dopo aver effettuato l&#39;accesso all&#39;interfaccia utente [!DNL Experience Platform], selezionare **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Sources]**. Nella schermata **[!UICONTROL Catalog]** sono visualizzate diverse sorgenti con le quali è possibile creare un account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la categoria **[!UICONTROL Streaming]**, selezionare **[!UICONTROL HTTP API]**. Se si tratta della prima volta che si utilizza questo connettore, selezionare **[!UICONTROL Configure]**. In caso contrario, selezionare **[!UICONTROL Add data]** per creare un nuovo connettore di streaming HTTP.

![](../../../../images/tutorials/create/http/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect HTTP API account]**. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome account e una descrizione facoltativa. Potrete inoltre fornire le seguenti proprietà di configurazione:

- **[!UICONTROL Authentication]:** Questa proprietà determina se la connessione di streaming richiede o meno l&#39;autenticazione. L&#39;autenticazione assicura che i dati vengano raccolti da fonti attendibili. Se hai a che fare con Informazioni personali (PII), questa proprietà deve essere attivata. Per impostazione predefinita, questa proprietà è disattivata.
- **[!UICONTROL XDM Schema Compatibility]:** Questa proprietà indica se la connessione di streaming invierà eventi compatibili con gli schemi XDM. Per impostazione predefinita, questa proprietà è attivata.

Al termine, selezionare **[!UICONTROL Connect to source]**, seguito da **[!UICONTROL Next]** per proseguire.

![](../../../../images/tutorials/create/http/new-account.png)

### Account esistente

Per connettersi utilizzando le credenziali esistenti, selezionare la connessione API HTTP che si desidera utilizzare, quindi selezionare **[!UICONTROL Next]** per continuare.

![](../../../../images/tutorials/create/http/existing-account.png)

## Seleziona dati

Dopo aver creato la connessione API HTTP, viene visualizzato il passaggio **[!UICONTROL Select data]**, che fornisce un&#39;interfaccia per scegliere il set di dati con cui connettersi. È possibile creare un nuovo set di dati o connettersi a un set di dati esistente.

### Creare un nuovo dataset

Per creare un nuovo dataset, selezionare **[!UICONTROL New dataset]**. Nel modulo visualizzato, fornite il nome, una descrizione facoltativa, nonché lo schema di destinazione per il dataset. Se selezionate uno schema abilitato per il profilo, potete scegliere se anche il set di dati deve essere abilitato per il profilo.

![](../../../../images/tutorials/create/http/new-dataset.png)

### Utilizzare un dataset esistente

Per utilizzare un dataset esistente, selezionare **[!UICONTROL Existing dataset]**. Nel modulo visualizzato, selezionare il set di dati che si desidera utilizzare. Dopo aver selezionato un set di dati, potete scegliere se il set di dati deve essere abilitato per il profilo.

![](../../../../images/tutorials/create/http/existing-dataset.png)

## Dettaglio flusso di dati

Viene visualizzato il passaggio **[!UICONTROL Dataflow detail]**. In questa pagina, puoi fornire i dettagli per il flusso di dati creato assegnando un nome e una descrizione facoltativa.

Dopo aver fornito i dettagli per il flusso di dati, selezionare **[!UICONTROL Next]**.

![](../../../../images/tutorials/create/http/dataflow-detail.png)

## Review

Viene visualizzato il passaggio **[!UICONTROL Review]**, che consente di controllare i dettagli del flusso di dati prima che venga creato. I dettagli sono raggruppati nelle seguenti categorie:

- **[!UICONTROL Connection]**: Mostra il nome account, la piattaforma di origine e il nome di origine.
- **[!UICONTROL Assign dataset and map fields]**: Mostra il set di dati di destinazione e lo schema a cui il set di dati aderisce.

Dopo aver confermato che i dettagli sono corretti, selezionare **[!UICONTROL Finish]**.

![](../../../../images/tutorials/create/http/review.png)

## Ottieni URL endpoint di streaming

Con la connessione creata, viene visualizzata la pagina di dettaglio delle origini. Questa pagina mostra i dettagli della nuova connessione creata, inclusi i flussi di dati eseguiti in precedenza, l’ID e l’URL dell’endpoint di streaming.

![](../../../../images/tutorials/create/http/get-streaming-url.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione HTTP in streaming che consente di utilizzare l&#39;endpoint in streaming per accedere a diverse API [!DNL Data Ingestion]. Per istruzioni su come creare una connessione in streaming nell&#39;API, leggete l&#39; [creazione di un&#39;esercitazione sulla connessione in streaming](../../../api/create/streaming/http.md).

Per informazioni su come eseguire lo streaming dei dati sulla piattaforma, leggere l&#39;esercitazione su [streaming time series data](../../../../../ingestion/tutorials/streaming-time-series-data.md) o l&#39;esercitazione su [streaming record data](../../../../../ingestion/tutorials/streaming-record-data.md).
