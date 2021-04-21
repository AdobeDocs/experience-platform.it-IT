---
keywords: Experience Platform;home;argomenti popolari;editor query;editor query;servizio query;servizio query;
solution: Experience Platform
title: Guida all’interfaccia utente dell’editor delle query
topic-legacy: query editor
description: Query Editor è uno strumento interattivo fornito da Adobe Experience Platform Query Service che consente di scrivere, convalidare ed eseguire query per i dati sulla customer experience all’interno dell’interfaccia utente di Experience Platform. L’editor delle query supporta lo sviluppo di query per l’analisi e l’esplorazione dei dati e consente di eseguire query interattive a scopo di sviluppo, nonché query non interattive per popolare i set di dati in Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 1%

---

# [!DNL Query Editor] Guida all’interfaccia utente

[!DNL Query Editor] è uno strumento interattivo fornito da Adobe Experience Platform  [!DNL Query Service], che consente di scrivere, convalidare ed eseguire query per dati sulla customer experience all’interno dell’interfaccia  [!DNL Experience Platform] utente. [!DNL Query Editor] supporta lo sviluppo di query per l’analisi e l’esplorazione dei dati e consente di eseguire query interattive a scopo di sviluppo, nonché query non interattive per compilare i set di dati in  [!DNL Experience Platform].

Per ulteriori informazioni sui concetti e le funzionalità di [!DNL Query Service], consulta la [Panoramica del servizio query][query-service-overview]. Per ulteriori informazioni su come navigare nell’interfaccia utente del servizio query su [!DNL Platform], consulta la [Panoramica dell’interfaccia utente del servizio query][query-service-ui].

## Introduzione

[!DNL Query Editor] fornisce un’esecuzione flessibile delle query tramite la connessione a  [!DNL Query Service] e le query vengono eseguite solo mentre questa connessione è attiva.

### Connessione a [!DNL Query Service]

[!DNL Query Editor] l&#39;inizializzazione e la connessione richiedono alcuni secondi all&#39; [!DNL Query Service] apertura. La console indica quando è connessa, come illustrato di seguito. Se tenti di eseguire una query prima che l’editor si sia connesso, l’esecuzione ritarda fino al completamento della connessione.

![Immagine](../images/queries/query-editor-overview/initializing-connection.png)

### Esecuzione delle query da [!DNL Query Editor]

Le query eseguite da [!DNL Query Editor] vengono eseguite in modo interattivo. Ciò significa che se chiudi il browser o se ti allontani, la query viene annullata. Questo vale anche per le query create per generare set di dati dagli output delle query.

## Creazione di query utilizzando [!DNL Query Editor]

Utilizzando [!DNL Query Editor], puoi scrivere, eseguire e salvare query per i dati sulla customer experience. Tutte le query eseguite in [!DNL Query Editor] o salvate sono disponibili per tutti gli utenti dell’organizzazione con accesso a [!DNL Query Service].

### Accesso al [!DNL Query Editor]

Nell&#39;interfaccia utente [!DNL Experience Platform], fai clic su **[!UICONTROL Queries]** nel menu di navigazione a sinistra per aprire l&#39;area di lavoro [!DNL Query Service]. Quindi, fai clic su **[!UICONTROL Create Query]** in alto a destra dello schermo per iniziare a scrivere le query. Questo collegamento è disponibile da una qualsiasi delle pagine nell’ area di lavoro [!DNL Query Service] .

![Immagine](../images/queries/query-editor-overview/create-query.png)

### Scrittura di query

[!UICONTROL Query Editor] è organizzato in modo da rendere la scrittura di query il più semplice possibile. La schermata seguente mostra come l&#39;editor appare nell&#39;interfaccia utente, con il pulsante **Play** e il campo di immissione SQL evidenziato.

![Immagine](../images/queries/query-editor-overview/editor.png)

Per ridurre al minimo il tempo di sviluppo, è consigliabile sviluppare le query con limiti sulle righe restituite. Ad esempio, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Dopo aver verificato che la query produca l’output previsto, rimuovi i limiti ed esegui la query con `CREATE TABLE tablename AS SELECT` per generare un set di dati con l’output.

### Strumenti di scrittura in [!DNL Query Editor]

- **Evidenziazione automatica della sintassi:** semplifica la lettura e l&#39;organizzazione di SQL.

![Immagine](../images/queries/query-editor-overview/syntax-highlight.png)

- **Completamento automatico della parola chiave SQL:** inizia a digitare la query e utilizza i tasti freccia per passare al termine desiderato e premi  **Invio**.

![Immagine](../images/queries/query-editor-overview/syntax-auto.png)

- **Completamento automatico tabella e campo:** inizia a digitare il nome della tabella  `SELECT` da cui desideri eseguire l’operazione, quindi utilizza i tasti freccia per passare alla tabella che stai cercando e premi  **Invio**. Una volta selezionata una tabella, la funzione di completamento automatico riconoscerà i campi presenti nella tabella.

![Immagine](../images/queries/query-editor-overview/tables-auto.png)

### Rilevamento degli errori

[!DNL Query Editor] convalida automaticamente una query durante la scrittura, fornendo una convalida SQL generica e una convalida di esecuzione specifica. Se sotto la query viene visualizzata una sottolineatura rossa (come illustrato nell’immagine seguente), la query presenta un errore.

![Immagine](../images/queries/query-editor-overview/syntax-error-highlight.png)

Quando vengono rilevati errori, è possibile visualizzare i messaggi di errore specifici passando il mouse sul codice SQL.

![Immagine](../images/queries/query-editor-overview/linting-error.png)

### Dettagli query

Durante la visualizzazione di una query in [!DNL Query Editor], il pannello **[!UICONTROL Query Details]** fornisce gli strumenti per gestire la query selezionata.

![Immagine](../images/queries/query-editor-overview/query-details.png)

Questo pannello consente di generare un set di dati di output direttamente dall’interfaccia utente, eliminare o denominare la query visualizzata e visualizzare il codice SQL in un formato di semplice copia nella scheda **[!UICONTROL SQL Query]** . Questo pannello mostra anche metadati utili, come l’ultima volta che la query è stata modificata e chi l’ha modificata, se applicabile. Per generare un set di dati, fai clic su **[!UICONTROL Output Dataset]**. Viene visualizzata la finestra di dialogo **[!UICONTROL Output Dataset]**. Immetti un nome e una descrizione, quindi fai clic su **[!UICONTROL Run Query]**. Il nuovo set di dati viene visualizzato nella scheda **[!UICONTROL Datasets]** dell’interfaccia utente [!DNL Query Service] in [!DNL Platform].

### Salvataggio delle query

[!DNL Query Editor] fornisce una funzione di salvataggio che ti consente di salvare una query e lavorarci in un secondo momento. Per salvare una query, fai clic su **[!UICONTROL Save]** nell’angolo in alto a destra di [!DNL Query Editor]. Prima di salvare una query, è necessario specificare un nome per la query utilizzando il pannello **[!UICONTROL Query Details]** .

### Come trovare le query precedenti

Tutte le query eseguite da [!DNL Query Editor] vengono acquisite nella tabella Registro. Puoi utilizzare la funzionalità di ricerca nella scheda **[!UICONTROL Log]** per trovare le esecuzioni delle query. Le query salvate sono elencate nella scheda **[!UICONTROL Browse]** .

Per ulteriori informazioni, consulta la [Panoramica dell’interfaccia utente del servizio query][query-service-ui] .

>[!NOTE]
>
>Le query non eseguite non vengono salvate dal registro. Affinché la query sia disponibile in [!DNL Query Service], deve essere eseguita o salvata in [!DNL Query Editor].

## Esecuzione di query tramite Editor query

Per eseguire una query in [!DNL Query Editor], è possibile immettere SQL nell&#39;editor o caricare una query precedente dalla scheda **[!UICONTROL Log]** o **[!UICONTROL Browse]** e fare clic su **Play**. Lo stato di esecuzione della query viene visualizzato nella scheda **[!UICONTROL Console]** qui sotto, mentre i dati di output sono visualizzati nella scheda **[!UICONTROL Results]**.

### Console

La console fornisce informazioni sullo stato e il funzionamento di [!DNL Query Service]. Nella console viene visualizzato lo stato della connessione a [!DNL Query Service], le operazioni di query eseguite ed eventuali messaggi di errore risultanti da tali query.

![Immagine](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>La console mostra solo gli errori derivanti dall’esecuzione di una query. Non mostra gli errori di convalida delle query prima dell’esecuzione di una query.

### Risultati della query

Al termine di una query, i risultati vengono visualizzati nella scheda **[!UICONTROL Results]**, accanto alla scheda **[!UICONTROL Console]** . Questa visualizzazione mostra l’output tabulare della query, visualizzando fino a 100 righe. Questa visualizzazione ti consente di verificare che la query produca l’output previsto. Per generare un set di dati con la query, rimuovi i limiti sulle righe restituite ed esegui la query con `CREATE TABLE tablename AS SELECT` per generare un set di dati con l’output. Per istruzioni su come generare un set di dati dai risultati della query in [!DNL Query Editor], consulta l’ [esercitazione sulla generazione di set di dati][query-service-create-datasets] .

![Immagine](../images/queries/query-editor-overview/query-results.png)

## Eseguire query con il video tutorial [!DNL Query Service]

Il video seguente mostra come eseguire le query nell’interfaccia Adobe Experience Platform e in un client PSQL. Inoltre, vengono dimostrate l’utilizzo di singole proprietà in un oggetto XDM, di funzioni definite in Adobe e di CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Passaggi successivi

Ora che sai quali funzioni sono disponibili in [!DNL Query Editor] e come navigare nell’applicazione, puoi iniziare a creare query personalizzate direttamente in [!DNL Platform]. Per ulteriori informazioni sull&#39;esecuzione di query SQL rispetto ai set di dati in [!DNL Data Lake], vedere la guida sull&#39;esecuzione di query [a2/>.][query-service-running-queries]

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../best-practices/writing-queries.md
[query-service-create-datasets]: ./create-datasets.md
