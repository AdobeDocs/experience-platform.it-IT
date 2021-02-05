---
keywords: ' Experience Platform;home;argomenti popolari;editor query;editor query;servizio query;servizio query;'
solution: Experience Platform
title: Guida all’interfaccia utente dell’editor di query
topic: query editor
description: Query Editor è uno strumento interattivo fornito da Adobe Experience Platform Query Service che consente di scrivere, convalidare ed eseguire query per i dati relativi all'esperienza cliente all'interno dell'interfaccia utente del Experience Platform . Query Editor supporta lo sviluppo di query per analisi e esplorazione dati e consente di eseguire query interattive a scopo di sviluppo, nonché query non interattive per compilare set di dati in  Experience Platform.
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 1%

---


# [!DNL Query Editor] Guida all&#39;interfaccia

[!DNL Query Editor] è uno strumento interattivo fornito da Adobe Experience Platform  [!DNL Query Service], che consente di scrivere, convalidare ed eseguire query per i dati relativi all&#39;esperienza cliente all&#39;interno dell&#39;interfaccia  [!DNL Experience Platform] utente. [!DNL Query Editor] supporta lo sviluppo di query per l&#39;analisi e l&#39;esplorazione dei dati e consente di eseguire query interattive a scopo di sviluppo, nonché query non interattive per la compilazione dei set di dati in  [!DNL Experience Platform].

Per ulteriori informazioni sui concetti e sulle funzionalità di [!DNL Query Service], vedere la [Panoramica del servizio query][query-service-overview]. Per ulteriori informazioni su come navigare nell&#39;interfaccia utente del servizio query su [!DNL Platform], vedere la [Panoramica dell&#39;interfaccia utente del servizio query][query-service-ui].

## Introduzione

[!DNL Query Editor] consente l&#39;esecuzione flessibile delle query connettendosi a  [!DNL Query Service], e le query verranno eseguite solo quando la connessione è attiva.

### Connessione a [!DNL Query Service]

[!DNL Query Editor] l&#39;inizializzazione e la connessione  [!DNL Query Service] quando viene aperta richiedono alcuni secondi. Console indica quando è connesso, come mostrato di seguito. Se si tenta di eseguire una query prima che l&#39;editor si sia connesso, l&#39;esecuzione ritarda fino al completamento della connessione.

![Immagine](../images/queries/query-editor-overview/initializing-connection.png)

### Esecuzione delle query da [!DNL Query Editor]

Le query eseguite da [!DNL Query Editor] vengono eseguite in modo interattivo. Questo significa che se chiudete il browser o se vi allontanate, la query viene annullata. Ciò è vero anche per le query effettuate per generare set di dati dagli output delle query.

## Creazione di query con [!DNL Query Editor]

[!DNL Query Editor] consente di scrivere, eseguire e salvare query per i dati relativi all&#39;esperienza cliente. Tutte le query eseguite in [!DNL Query Editor], o salvate, sono disponibili per tutti gli utenti dell&#39;organizzazione con accesso a [!DNL Query Service].

### Accesso al [!DNL Query Editor]

Nell&#39;interfaccia di [!DNL Experience Platform], fare clic su **[!UICONTROL Queries]** nel menu di navigazione a sinistra per aprire l&#39;area di lavoro [!DNL Query Service]. Fare clic su **[!UICONTROL Create Query]** in alto a destra della schermata per iniziare a scrivere query. Questo collegamento è disponibile da una qualsiasi delle pagine nell&#39;area di lavoro di [!DNL Query Service].

![Immagine](../images/queries/query-editor-overview/create-query.png)

### Scrittura di query

[!UICONTROL Query Editor] è organizzato in modo da rendere più semplice la scrittura di query. La schermata seguente mostra come l&#39;editor viene visualizzato nell&#39;interfaccia utente, con il pulsante **Play** e il campo di immissione SQL evidenziato.

![Immagine](../images/queries/query-editor-overview/editor.png)

Per ridurre al minimo il tempo di sviluppo, si consiglia di sviluppare le query con limiti sulle righe restituite. Ad esempio, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Dopo aver verificato che la query produca l&#39;output previsto, rimuovere i limiti ed eseguire la query con `CREATE TABLE tablename AS SELECT` per generare un dataset con l&#39;output.

### Strumenti di scrittura in [!DNL Query Editor]

- **Evidenziazione automatica della sintassi:** semplifica la lettura e l&#39;organizzazione di SQL.

![Immagine](../images/queries/query-editor-overview/syntax-highlight.png)

- **Completamento automatico della parola chiave SQL:** iniziate a digitare la query, quindi utilizzate i tasti freccia per passare al termine desiderato e premete  **Invio**.

![Immagine](../images/queries/query-editor-overview/syntax-auto.png)

- **Tabella e campo con completamento automatico:** Inizia a digitare il nome della tabella  `SELECT` da cui vuoi uscire, quindi utilizza i tasti freccia per passare alla tabella che stai cercando e premi  **Invio**. Dopo aver selezionato una tabella, la funzione di completamento automatico riconoscerà i campi nella tabella.

![Immagine](../images/queries/query-editor-overview/tables-auto.png)

### Rilevamento errori

[!DNL Query Editor] convalida automaticamente una query durante la scrittura, fornendo la convalida SQL generica e la convalida dell&#39;esecuzione specifica. Se sotto la query viene visualizzata una sottolineatura rossa (come illustrato nell&#39;immagine seguente), all&#39;interno della query viene visualizzato un errore.

![Immagine](../images/queries/query-editor-overview/syntax-error-highlight.png)

Quando vengono rilevati degli errori, è possibile visualizzare i messaggi di errore specifici posizionando il puntatore del mouse sul codice SQL.

![Immagine](../images/queries/query-editor-overview/linting-error.png)

### Dettagli query

Durante la visualizzazione di una query in [!DNL Query Editor], il pannello **[!UICONTROL Query Details]** fornisce gli strumenti per gestire la query selezionata.

![Immagine](../images/queries/query-editor-overview/query-details.png)

Questo pannello consente di generare un set di dati di output direttamente dall&#39;interfaccia utente, eliminare o assegnare un nome alla query visualizzata e visualizzare il codice SQL in un formato di semplice copia nella scheda **[!UICONTROL SQL Query]**. Questo pannello mostra anche utili metadati, ad esempio l’ultima volta che la query è stata modificata e l’utente che l’ha modificata, se applicabile. Per generare un set di dati, fare clic su **[!UICONTROL Output Dataset]**. Viene visualizzata la finestra di dialogo **[!UICONTROL Output Dataset]**. Immettete un nome e una descrizione, quindi fate clic su **[!UICONTROL Run Query]**. Il nuovo dataset viene visualizzato nella scheda **[!UICONTROL Datasets]** dell&#39;interfaccia utente [!DNL Query Service] in [!DNL Platform].

### Salvataggio delle query

[!DNL Query Editor] fornisce una funzione save che consente di salvare una query e di lavorarci in un secondo momento. Per salvare una query, fare clic su **[!UICONTROL Save]** nell&#39;angolo superiore destro di [!DNL Query Editor]. Prima di salvare una query, è necessario specificare un nome per la query utilizzando il pannello **[!UICONTROL Query Details]**.

### Come trovare le query precedenti

Tutte le query eseguite da [!DNL Query Editor] vengono acquisite nella tabella Log. È possibile utilizzare la funzionalità di ricerca nella scheda **[!UICONTROL Log]** per trovare le esecuzioni delle query. Le query salvate sono elencate nella scheda **[!UICONTROL Browse]**.

Per ulteriori informazioni, vedere [Panoramica dell&#39;interfaccia utente del servizio query][query-service-ui].

>[!NOTE]
>
>Le query non eseguite non vengono salvate dal registro. Affinché la query sia disponibile in [!DNL Query Service], è necessario eseguirla o salvarla in [!DNL Query Editor].

## Esecuzione di query con l&#39;Editor query

Per eseguire una query in [!DNL Query Editor], è possibile immettere SQL nell&#39;editor o caricare una query precedente dalla scheda **[!UICONTROL Log]** o **[!UICONTROL Browse]**, quindi fare clic su **Play**. Lo stato dell&#39;esecuzione della query viene visualizzato nella scheda **[!UICONTROL Console]** riportata di seguito e i dati di output sono visualizzati nella scheda **[!UICONTROL Results]**.

### Console

La console fornisce informazioni sullo stato e il funzionamento di [!DNL Query Service]. La console visualizza lo stato della connessione su [!DNL Query Service], le operazioni di query in esecuzione ed eventuali messaggi di errore risultanti da tali query.

![Immagine](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>Nella console sono visualizzati solo gli errori risultanti dall’esecuzione di una query. Non vengono visualizzati errori di convalida delle query prima dell&#39;esecuzione di una query.

### Risultati query

Al termine di una query, i risultati vengono visualizzati nella scheda **[!UICONTROL Results]**, accanto alla scheda **[!UICONTROL Console]**. Questa visualizzazione mostra l’output tabulare della query, visualizzando fino a 100 righe. Questa visualizzazione consente di verificare che la query produca l&#39;output previsto. Per generare un dataset con la query, rimuovere i limiti sulle righe restituite ed eseguire la query con `CREATE TABLE tablename AS SELECT` per generare un dataset con l&#39;output. Per istruzioni su come generare un set di dati dai risultati della query in [!DNL Query Editor], vedere l&#39; [esercitazione sulla generazione di set di dati][query-service-create-datasets].

![Immagine](../images/queries/query-editor-overview/query-results.png)

## Eseguire query con video di esercitazione [!DNL Query Service]

Il seguente video mostra come eseguire le query nell&#39;interfaccia Adobe Experience Platform e in un client PSQL. Inoltre, viene illustrato l&#39;utilizzo di singole proprietà in un oggetto XDM, utilizzando  funzioni definite dal Adobe e utilizzando CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Passaggi successivi

Ora che sai quali funzioni sono disponibili in [!DNL Query Editor] e come navigare nell&#39;applicazione, puoi iniziare a creare query personalizzate direttamente in [!DNL Platform]. Per ulteriori informazioni sull&#39;esecuzione di query SQL rispetto ai set di dati in [!DNL Data Lake], vedere la guida sull&#39;esecuzione di query [query][query-service-running-queries].

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../best-practices/writing-queries.md
[query-service-create-datasets]: ./create-datasets.md
