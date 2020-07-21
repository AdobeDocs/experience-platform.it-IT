---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare una connessione in streaming utilizzando l'interfaccia utente
topic: tutorial
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# Creare una connessione in streaming utilizzando l&#39;interfaccia utente

Questa guida all&#39;interfaccia utente consente di creare una connessione in streaming utilizzando  Adobe Experience Platform.

## Introduzione

Per avviare lo streaming dei dati su [!DNL Experience Platform], è innanzitutto necessario creare una connessione HTTP in streaming. Durante la creazione di una connessione di streaming, è necessario fornire dettagli chiave come l&#39;origine dei dati di streaming e specificare se si intende inviare o meno dati da un&#39;origine attendibile (autenticata) o non attendibile (non autenticata).

Dopo aver registrato una connessione in streaming, si dispone di un URL univoco che può essere utilizzato per lo streaming dei dati [!DNL Platform].

Per completare questa guida, è necessario accedere al Adobe Experience Platform . Se non avete accesso a [!DNL Platform], contattate l&#39;amministratore di sistema prima di continuare.

## Creare una connessione in streaming

Dopo aver effettuato l’accesso all’ [!DNL Experience Platform] interfaccia utente, fate clic **[!UICONTROL Sources]** per aprire la *[!UICONTROL Catalog]* scheda. In questa pagina vengono visualizzati i tipi di origine disponibili come singole schede, con ciascuna scheda contenente una bolla che mostra il numero di flussi di dati creati dalle connessioni di streaming ai dataset.

![](../images/streaming-ingestion/ui/click-sources.png)

Sulla *[!UICONTROL Sources]* pagina fare clic su **[!UICONTROL HTTP API]**, quindi **[!UICONTROL Connect source]**.

![](../images/streaming-ingestion/ui/click-connect-source.png)

Viene *[!UICONTROL Connect to HTTP]* visualizzata la schermata. In *[!UICONTROL Service details]*, fornite sia l&#39; **[!UICONTROL name]** e una **[!UICONTROL description]** per la nuova connessione di streaming.

In *[!UICONTROL Account Authentication]*, seleziona le seguenti proprietà di configurazione per la connessione in streaming:

- **[!UICONTROL Authentication]:**Indica se la connessione di streaming richiede o meno l&#39;autenticazione. L&#39;autenticazione assicura che i dati vengano raccolti da fonti attendibili. Si consiglia di attivarlo se si tratta di informazioni personali (PII).
- **[!UICONTROL XDM Schema Compatibility]:**Indica se questa connessione di streaming invierà o meno eventi compatibili con gli schemi XDM. Per impostazione predefinita, questa proprietà è attivata****.

Dopo aver selezionato le proprietà di configurazione, fate clic su **[!UICONTROL Connect]**. La connessione HTTP in streaming è stata creata e ora può essere visualizzata nella *[!UICONTROL Browse]* scheda nell’ *[!UICONTROL Sources]* area di lavoro.

![](../images/streaming-ingestion/ui/http-sources-details.png)

Dalla *[!UICONTROL Browse]* scheda, è possibile fare clic sulla nuova connessione Streaming HTTP e visualizzare i dettagli della connessione.

![](../images/streaming-ingestion/ui/browse-sources.png)

Facendo clic sul collegamento ipertestuale del nome della connessione, è possibile selezionare i dati da visualizzare configurando il set di dati connesso facendo clic su *[!UICONTROL Select data]*.

![](../images/streaming-ingestion/ui/select-data.png)

È possibile [creare un nuovo dataset](#create-a-new-dataset) o [utilizzare un dataset](#use-an-existing-dataset)esistente.

### Creare un nuovo dataset

Per creare un nuovo set di dati, fornire **[!UICONTROL Name]**, **[!UICONTROL Description]** e la destinazione **[!UICONTROL Schema]** del set di dati.

![](../images/streaming-ingestion/ui/create-new-dataset.png)

Dopo aver inserito tutti i dettagli e aver fatto clic su **[!UICONTROL Next]**, è possibile rivedere i dettagli forniti prima di fare clic **[!UICONTROL Finish]** per connettere il dataset alla connessione HTTP in streaming.

![](../images/streaming-ingestion/ui/review-create-new-dataset.png)

### Utilizzare un dataset esistente

Per utilizzare un set di dati esistente, selezionare il **[!UICONTROL Output dataset name]**.

![](../images/streaming-ingestion/ui/use-existing-dataset.png)

Dopo aver fatto clic su **[!UICONTROL Next]**, è possibile esaminare i dettagli prima di fare clic **[!UICONTROL Finish]** per collegare il set di dati selezionato alla connessione HTTP in streaming.

![](../images/streaming-ingestion/ui/review-existing-dataset.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione HTTP in streaming che consente di utilizzare l&#39;endpoint in streaming per accedere a diverse [!DNL Data Ingestion] API. Per istruzioni su come creare una connessione in streaming nell&#39;API, leggete l&#39;esercitazione sulla [creazione di una connessione in streaming](../tutorials/create-streaming-connection.md).
