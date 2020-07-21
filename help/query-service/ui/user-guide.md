---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ' Guida all''Editor di query del servizio Query'
topic: query editor
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 1%

---


# [!DNL Query Editor] guida utente

[!DNL Query Editor] è uno strumento interattivo fornito da  Adobe Experience Platform [!DNL Query Service], che consente di scrivere, convalidare ed eseguire query per i dati relativi all&#39;esperienza cliente all&#39;interno dell&#39;interfaccia [!DNL Experience Platform] utente. [!DNL Query Editor] supporta lo sviluppo di query per l&#39;analisi e l&#39;esplorazione dei dati e consente di eseguire query interattive a scopo di sviluppo, nonché query non interattive per la compilazione dei set di dati in [!DNL Experience Platform].

Per ulteriori informazioni sui concetti e sulle funzionalità di [!DNL Query Service]Query Service, consultate la panoramica [di][query-service-overview]Query Service. Per ulteriori informazioni su come navigare nell&#39;interfaccia utente di Servizio query, [!DNL Platform]vedere la panoramica [dell&#39;interfaccia utente di Servizio][query-service-ui]query.

## Introduzione

[!DNL Query Editor] consente l&#39;esecuzione flessibile delle query connettendosi a [!DNL Query Service], e le query verranno eseguite solo quando la connessione è attiva.

### Collegamento a [!DNL Query Service]

[!DNL Query Editor] l&#39;inizializzazione e la connessione [!DNL Query Service] quando viene aperta richiedono alcuni secondi. Console indica quando è connesso, come mostrato di seguito. Se si tenta di eseguire una query prima che l&#39;editor si sia connesso, l&#39;esecuzione ritarda fino al completamento della connessione.

![Immagine](../images/queries/query-editor-overview/initializing-connection.png)

### Modalità di esecuzione delle query [!DNL Query Editor]

Query eseguite dall&#39; [!DNL Query Editor] esecuzione in modo interattivo. Questo significa che se chiudete il browser o se vi allontanate, la query viene annullata. Ciò è vero anche per le query effettuate per generare set di dati dagli output delle query.

## Creazione di query tramite [!DNL Query Editor]

Utilizzando [!DNL Query Editor]questa funzione, potete scrivere, eseguire e salvare le query per i dati relativi all&#39;esperienza cliente. Tutte le query eseguite [!DNL Query Editor]o salvate sono disponibili per tutti gli utenti dell&#39;organizzazione con accesso a [!DNL Query Service].

### Accesso [!DNL Query Editor]

Nell’ [!DNL Experience Platform] interfaccia utente, fate clic **[!UICONTROL Queries]** nel menu di navigazione a sinistra per aprire l’ [!DNL Query Service] area di lavoro. Fare clic **[!UICONTROL Create Query]** nella parte superiore destra della schermata per iniziare a scrivere le query. Questo collegamento è disponibile da una qualsiasi delle pagine nell’ [!DNL Query Service] area di lavoro.

![Immagine](../images/queries/query-editor-overview/create-query.png)

### Scrittura di query

[!UICONTROL Query Editor] è organizzato in modo da rendere più semplice la scrittura di query. La schermata seguente mostra l’aspetto dell’editor nell’interfaccia utente, con il pulsante **Riproduci** e il campo di immissione SQL evidenziati.

![Immagine](../images/queries/query-editor-overview/editor.png)

Per ridurre al minimo il tempo di sviluppo, si consiglia di sviluppare le query con limiti sulle righe restituite. Ad esempio, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Dopo aver verificato che la query produca l&#39;output previsto, rimuovere i limiti ed eseguire la query con `CREATE TABLE tablename AS SELECT` cui generare un dataset con l&#39;output.

### Strumenti di scrittura in [!DNL Query Editor]

- **Evidenziazione automatica della sintassi:** Semplifica la lettura e l&#39;organizzazione di SQL.

![Immagine](../images/queries/query-editor-overview/syntax-highlight.png)

- **Completamento automatico parola chiave SQL:** Iniziate a digitare la query, quindi utilizzate i tasti freccia per passare al termine desiderato e premete **Invio**.

![Immagine](../images/queries/query-editor-overview/syntax-auto.png)

- **Tabella e campo con completamento automatico:** Iniziate a digitare il nome della tabella da cui desiderate `SELECT` uscire, quindi utilizzate i tasti freccia per passare alla tabella cercata e premete **Invio**. Dopo aver selezionato una tabella, la funzione di completamento automatico riconoscerà i campi nella tabella.

![Immagine](../images/queries/query-editor-overview/tables-auto.png)

### Rilevamento errori

[!DNL Query Editor] convalida automaticamente una query durante la scrittura, fornendo la convalida SQL generica e la convalida dell&#39;esecuzione specifica. Se sotto la query viene visualizzata una sottolineatura rossa (come illustrato nell&#39;immagine seguente), all&#39;interno della query viene visualizzato un errore.

![Immagine](../images/queries/query-editor-overview/syntax-error-highlight.png)

Quando vengono rilevati degli errori, è possibile visualizzare i messaggi di errore specifici posizionando il puntatore del mouse sul codice SQL.

![Immagine](../images/queries/query-editor-overview/linting-error.png)

### Dettagli query

Durante la visualizzazione di una query in [!DNL Query Editor], il *[!UICONTROL Query Details]* pannello fornisce gli strumenti per gestire la query selezionata.

![Immagine](../images/queries/query-editor-overview/query-details.png)

Questo pannello consente di generare un set di dati di output direttamente dall’interfaccia utente, eliminare o assegnare un nome alla query visualizzata e visualizzare il codice SQL in un formato di facile copia nella *[!UICONTROL SQL Query]* scheda. Questo pannello mostra anche utili metadati, ad esempio l’ultima volta che la query è stata modificata e l’utente che l’ha modificata, se applicabile. Per generare un set di dati, fare clic su **[!UICONTROL Output Dataset]**. Viene visualizzata *[!UICONTROL Output Dataset]* la finestra di dialogo. Immettete un nome e una descrizione, quindi fate clic **[!UICONTROL Run Query]**. Il nuovo set di dati viene visualizzato nella *[!UICONTROL Datasets]* scheda dell&#39;interfaccia [!DNL Query Service] utente in [!DNL Platform].

### Salvataggio delle query

[!DNL Query Editor] fornisce una funzione save che consente di salvare una query e di lavorarci in un secondo momento. Per salvare una query, fate clic **[!UICONTROL Save]** nell’angolo in alto a destra di [!DNL Query Editor]. Prima di salvare una query, è necessario specificare un nome per la query utilizzando il *[!UICONTROL Query Details]* pannello.

### Come trovare le query precedenti

Tutte le query eseguite da [!DNL Query Editor] vengono acquisite nella tabella Log. È possibile utilizzare la funzionalità di ricerca nella *[!UICONTROL Log]* scheda per individuare le esecuzioni delle query. Le query salvate sono elencate nella *[!UICONTROL Browse]* scheda.

Per ulteriori informazioni, consulta la panoramica [dell’interfaccia utente del servizio][query-service-ui] query.

>[!NOTE]
>
>Le query non eseguite non vengono salvate dal registro. Affinché la query sia disponibile in [!DNL Query Service], è necessario eseguirla o salvarla in [!DNL Query Editor].

## Esecuzione di query con l&#39;Editor query

Per eseguire una query in [!DNL Query Editor], è possibile immettere SQL nell&#39;editor o caricare una query precedente dalla *scheda Registro* o *[!UICONTROL Browse]* scheda, quindi fare clic su **Riproduci**. Lo stato dell&#39;esecuzione della query viene visualizzato nella *[!UICONTROL Console]* scheda sottostante e i dati di output sono visualizzati nella *[!UICONTROL Results]* scheda.

### Console

La console fornisce informazioni sullo stato e il funzionamento di [!DNL Query Service]. Nella console viene visualizzato lo stato della connessione a [!DNL Query Service], le operazioni di query eseguite ed eventuali messaggi di errore risultanti da tali query.

![Immagine](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>Nella console sono visualizzati solo gli errori risultanti dall’esecuzione di una query. Non vengono visualizzati errori di convalida delle query prima dell&#39;esecuzione di una query.

### Risultati query

Al termine di una query, i risultati vengono visualizzati nella *[!UICONTROL Results]* scheda accanto alla *[!UICONTROL Console]* scheda. Questa visualizzazione mostra l’output tabulare della query, visualizzando fino a 100 righe. Questa visualizzazione consente di verificare che la query produca l&#39;output previsto. Per generare un dataset con la query, rimuovere i limiti sulle righe restituite ed eseguire la query con `CREATE TABLE tablename AS SELECT` cui generare un dataset con l&#39;output. Per istruzioni su come generare un set di dati dai risultati della query, vedere l&#39;esercitazione [sulla][query-service-create-datasets] generazione di set di dati in [!DNL Query Editor].

![Immagine](../images/queries/query-editor-overview/query-results.png)

## Esecuzione di query con video [!DNL Query Service] di esercitazione

Il seguente video mostra come eseguire le query nell&#39;interfaccia del Adobe Experience Platform  e in un client PSQL. Inoltre, viene illustrato l&#39;utilizzo di singole proprietà in un oggetto XDM, utilizzando funzioni definite da Adobe e utilizzando CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Passaggi successivi

Ora che sai quali funzioni sono disponibili [!DNL Query Editor] e come navigare nell’applicazione, puoi iniziare a creare query personalizzate direttamente in [!DNL Platform]. Per ulteriori informazioni sull&#39;esecuzione di query SQL rispetto ai dataset in [!DNL Data Lake], vedere la guida sull&#39; [esecuzione di query][query-service-running-queries]. Per query SQL di esempio per lavorare con Adobe  Analytics e dati  Adobe Target, consultate il riferimento [alle query di][query-service-sample-queries]esempio.

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../creating-queries/creating-queries.md
[query-service-sample-queries]: ../sample-queries/overview.md
[query-service-create-datasets]: ../creating-queries/create-datasets.md
