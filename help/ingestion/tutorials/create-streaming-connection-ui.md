---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare una connessione in streaming utilizzando l'interfaccia utente
topic: tutorial
translation-type: tm+mt
source-git-commit: 181719e729748adcde62199c9406a97b7a807182

---


# Creare una connessione in streaming utilizzando l&#39;interfaccia utente

Questa guida all&#39;interfaccia utente è utile per creare una connessione in streaming tramite Adobe Experience Platform.

## Introduzione

Per avviare lo streaming dei dati in Experience Platform, è innanzitutto necessario creare una connessione HTTP in streaming. Durante la creazione di una connessione di streaming, è necessario fornire dettagli chiave come l&#39;origine dei dati di streaming e specificare se si intende inviare o meno dati da un&#39;origine attendibile (autenticata) o non attendibile (non autenticata).

Dopo aver registrato una connessione in streaming, si dispone di un URL univoco che può essere utilizzato per lo streaming dei dati su Platform.

Per completare questa guida, è necessario accedere ad Adobe Experience Platform. Se non disponete dell&#39;accesso a Piattaforma, contattate l&#39;amministratore di sistema prima di continuare.

## Creare una connessione in streaming

Dopo aver effettuato l&#39;accesso all&#39;interfaccia utente della piattaforma Experience, fai clic su **Origini** per aprire la scheda *Catalogo* . In questa pagina vengono visualizzati i tipi di origine disponibili come singole schede, con ciascuna scheda contenente una bolla che mostra il numero di flussi di dati creati dalle connessioni di streaming ai dataset.

![](../images/streaming-ingestion/ui/click-sources.png)

Nella pagina *Origini* , fai clic su **HTTP API**, quindi su **Connect source**.

![](../images/streaming-ingestion/ui/click-connect-source.png)

Viene visualizzata la schermata *Connetti a HTTP* . In Dettagli ** servizio, fornite sia il **nome** che una **descrizione** per la nuova connessione di streaming.

In Autenticazione ** account, selezionate le seguenti proprietà di configurazione per la connessione in streaming:

- **Autenticazione:** Indica se la connessione di streaming richiede o meno l&#39;autenticazione. L&#39;autenticazione assicura che i dati vengano raccolti da fonti attendibili. Si consiglia di attivarlo se si tratta di informazioni personali (PII).
- **Compatibilità schema XDM:** Indica se questa connessione di streaming invierà o meno eventi compatibili con gli schemi XDM. Per impostazione predefinita, questa proprietà è attivata ****.

Dopo aver selezionato le proprietà di configurazione, fate clic su **Connect**. La connessione HTTP in streaming è stata creata e ora può essere visualizzata nella scheda *Sfoglia* nell&#39;area di lavoro *Origini* .

![](../images/streaming-ingestion/ui/http-sources-details.png)

Dalla scheda *Sfoglia* , potete fare clic sulla nuova connessione HTTP Streaming e visualizzare i dettagli di tale connessione.

![](../images/streaming-ingestion/ui/browse-sources.png)

Facendo clic sul collegamento ipertestuale del nome della connessione, è possibile selezionare i dati da visualizzare configurando il set di dati connesso, facendo clic su *Seleziona dati*.

![](../images/streaming-ingestion/ui/select-data.png)

È possibile [creare un nuovo dataset](#create-a-new-dataset) o [utilizzare un dataset](#use-an-existing-dataset)esistente.

### Creare un nuovo dataset

Per creare un nuovo set di dati, fornire **Nome**, **Descrizione** e lo **schema** di destinazione per il set di dati.

![](../images/streaming-ingestion/ui/create-new-dataset.png)

Dopo aver inserito tutti i dettagli e aver fatto clic su **Avanti**, è possibile esaminare i dettagli forniti prima di fare clic su **Fine** per collegare il dataset alla connessione HTTP in streaming.

![](../images/streaming-ingestion/ui/review-create-new-dataset.png)

### Utilizzare un dataset esistente

Per utilizzare un set di dati esistente, selezionare il nome **del set di dati di** output.

![](../images/streaming-ingestion/ui/use-existing-dataset.png)

Dopo aver fatto clic su **Avanti**, è possibile esaminare i dettagli prima di fare clic su **Fine** per collegare il set di dati selezionato alla connessione HTTP in streaming.

![](../images/streaming-ingestion/ui/review-existing-dataset.png)

## Passaggi successivi

Seguendo questa esercitazione, avete creato una connessione HTTP in streaming che consente di utilizzare l&#39;endpoint in streaming per accedere a diverse API di inserimento dati. Per istruzioni su come creare una connessione in streaming nell&#39;API, leggete l&#39;esercitazione sulla [creazione di una connessione in streaming](../tutorials/create-streaming-connection.md).
