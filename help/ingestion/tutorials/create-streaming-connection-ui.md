---
keywords: ' Experience Platform;home;argomenti più comuni;collegamento in streaming;creare una connessione in streaming;ui guide;tutorial;creare una connessione in streaming;streaming, assimilazione;assimilazione;'
solution: Experience Platform
title: Creare una connessione in streaming utilizzando l'interfaccia utente
topic: tutorial
type: Tutorial
description: Questa guida all'interfaccia utente consente di creare una connessione in streaming utilizzando Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---


# Creare una connessione in streaming utilizzando l&#39;interfaccia utente

Questa guida all&#39;interfaccia utente consente di creare una connessione in streaming utilizzando Adobe Experience Platform.

## Introduzione

Per avviare lo streaming dei dati su [!DNL Experience Platform], è innanzitutto necessario creare una connessione HTTP in streaming. Durante la creazione di una connessione di streaming, è necessario fornire dettagli chiave come l&#39;origine dei dati di streaming e specificare se si intende inviare o meno dati da un&#39;origine attendibile (autenticata) o non attendibile (non autenticata).

Dopo aver registrato una connessione in streaming, si dispone di un URL univoco che può essere utilizzato per lo streaming dei dati in [!DNL Platform].

Per completare questa guida, è necessario accedere ad Adobe Experience Platform. Se non disponete dell&#39;accesso a [!DNL Platform], contattate l&#39;amministratore di sistema prima di continuare.

## Creare una connessione in streaming

Dopo aver effettuato l&#39;accesso all&#39;interfaccia utente [!DNL Experience Platform], fare clic su **[!UICONTROL Sources]** per aprire la scheda **[!UICONTROL Catalog]**. In questa pagina vengono visualizzati i tipi di origine disponibili come singole schede, con ciascuna scheda contenente una bolla che mostra il numero di flussi di dati creati dalle connessioni di streaming ai dataset.

![](../images/streaming-ingestion/ui/click-sources.png)

Nella pagina **[!UICONTROL Sources]** fare clic su **[!UICONTROL HTTP API]**, quindi su **[!UICONTROL Connect source]**.

![](../images/streaming-ingestion/ui/click-connect-source.png)

Viene visualizzata la schermata **[!UICONTROL Connect to HTTP]**. In **[!UICONTROL Service details]**, fornite sia il nome che una descrizione per la nuova connessione di streaming.

In **[!UICONTROL Account Authentication]**, selezionate le seguenti proprietà di configurazione per la connessione di streaming:

- **[!UICONTROL Authentication]:** Indica se la connessione di streaming richiede o meno l&#39;autenticazione. L&#39;autenticazione assicura che i dati vengano raccolti da fonti attendibili. Si consiglia di attivarlo se si tratta di informazioni personali (PII).
- **[!UICONTROL XDM Schema Compatibility]:** Indica se questa connessione di streaming invierà o meno eventi compatibili con gli schemi XDM. Per impostazione predefinita, questa proprietà è attivata **su**.

Dopo aver selezionato le proprietà di configurazione, fare clic su **[!UICONTROL Connect]**. La connessione HTTP in streaming è stata creata e ora può essere visualizzata nella scheda **[!UICONTROL Browse]** nell&#39;area di lavoro **[!UICONTROL Sources]**.

![](../images/streaming-ingestion/ui/http-sources-details.png)

Dalla scheda **[!UICONTROL Browse]**, potete fare clic sulla connessione HTTP in streaming appena creata e visualizzare i dettagli della connessione.

![](../images/streaming-ingestion/ui/browse-sources.png)

Facendo clic sul collegamento ipertestuale del nome della connessione, è possibile selezionare i dati da visualizzare configurando il set di dati connesso, facendo clic su **[!UICONTROL Select data]**.

![](../images/streaming-ingestion/ui/select-data.png)

È possibile [creare un nuovo dataset](#create-a-new-dataset) o [utilizzare un dataset esistente](#use-an-existing-dataset).

### Creare un nuovo dataset

Per creare un nuovo dataset, fornire il nome, la descrizione e lo schema di destinazione per il dataset.

![](../images/streaming-ingestion/ui/create-new-dataset.png)

Dopo aver inserito tutti i dettagli e aver fatto clic su **[!UICONTROL Next]**, è possibile esaminare i dettagli forniti prima di fare clic su **[!UICONTROL Finish]** per collegare il dataset alla connessione HTTP in streaming.

![](../images/streaming-ingestion/ui/review-create-new-dataset.png)

### Utilizzare un dataset esistente

Per utilizzare un set di dati esistente, selezionare **[!UICONTROL Output dataset name]**.

![](../images/streaming-ingestion/ui/use-existing-dataset.png)

Dopo aver fatto clic su **[!UICONTROL Next]**, è possibile esaminare i dettagli prima di fare clic su **[!UICONTROL Finish]** per collegare il set di dati selezionato alla connessione HTTP in streaming.

![](../images/streaming-ingestion/ui/review-existing-dataset.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione HTTP in streaming che consente di utilizzare l&#39;endpoint in streaming per accedere a diverse API [!DNL Data Ingestion]. Per istruzioni su come creare una connessione in streaming nell&#39;API, leggete l&#39; [creazione di un&#39;esercitazione sulla connessione in streaming](../tutorials/create-streaming-connection.md).
