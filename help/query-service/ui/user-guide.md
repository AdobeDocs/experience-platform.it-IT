---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ' Guida all''Editor di query del servizio Query'
topic: query editor
translation-type: tm+mt
source-git-commit: cc101b1a439408861961c6fcd0899ca7c48bfa04
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 1%

---


# Guida utente per l’editor di query

Query Editor è uno strumento interattivo fornito da  Adobe Experience Platform Query Service che consente di scrivere, convalidare ed eseguire query per i dati relativi all&#39;esperienza cliente all&#39;interno dell&#39;interfaccia utente  Experience Platform. Query Editor supporta lo sviluppo di query per l&#39;analisi e l&#39;esplorazione dei dati e consente di eseguire query interattive a scopo di sviluppo, nonché query non interattive per compilare set di dati in  Experience Platform.

Per ulteriori informazioni sui concetti e sulle funzionalità di Query Service, consultate la panoramica [di][query-service-overview]Query Service. Per ulteriori informazioni su come navigare nell&#39;interfaccia utente di Servizio query su Platform, vedere la panoramica [dell&#39;interfaccia utente di Servizio][query-service-ui]query.

## Introduzione

L&#39;Editor query consente l&#39;esecuzione flessibile delle query collegandosi a Servizio query e le query verranno eseguite solo quando la connessione è attiva.

### Connessione a Query Service

L&#39;editor di query richiede alcuni secondi per l&#39;inizializzazione e la connessione al servizio di query quando viene aperto. Console indica quando è connesso, come mostrato di seguito. Se si tenta di eseguire una query prima che l&#39;editor si sia connesso, l&#39;esecuzione ritarda fino al completamento della connessione.

![Immagine](../images/queries/query-editor-overview/initializing-connection.png)

### Esecuzione delle query dall&#39;editor query

Le query eseguite dall&#39;Editor query vengono eseguite in modo interattivo. Questo significa che se chiudete il browser o se vi allontanate, la query viene annullata. Ciò è vero anche per le query effettuate per generare set di dati dagli output delle query.

## Authoring delle query con Editor query

Utilizzando l&#39;editor di query è possibile scrivere, eseguire e salvare query per i dati relativi all&#39;esperienza cliente. Tutte le query eseguite in Query Editor, o salvate, sono disponibili per tutti gli utenti dell&#39;organizzazione con accesso a Query Service.

### Accesso all&#39;Editor query

Nell’interfaccia  Experience Platform, fate clic su **Query** nel menu di navigazione a sinistra per aprire l’area di lavoro Servizio query. Fare clic su **Crea query** in alto a destra nella schermata per iniziare a scrivere query. Questo collegamento è disponibile da una qualsiasi delle pagine nell&#39;area di lavoro Servizio query.

![Immagine](../images/queries/query-editor-overview/create-query.png)

### Scrittura di query

Editor query è organizzato in modo da semplificare la scrittura delle query. La schermata seguente mostra l’aspetto dell’editor nell’interfaccia utente, con il pulsante **Riproduci** e il campo di immissione SQL evidenziati.

![Immagine](../images/queries/query-editor-overview/editor.png)

Per ridurre al minimo il tempo di sviluppo, si consiglia di sviluppare le query con limiti sulle righe restituite. Ad esempio, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Dopo aver verificato che la query produca l&#39;output previsto, rimuovere i limiti ed eseguire la query con `CREATE TABLE tablename AS SELECT` cui generare un dataset con l&#39;output.

### Strumenti di scrittura nell’Editor query

- **Evidenziazione automatica della sintassi:** Semplifica la lettura e l&#39;organizzazione di SQL.

![Immagine](../images/queries/query-editor-overview/syntax-highlight.png)

- **Completamento automatico parola chiave SQL:** Iniziate a digitare la query, quindi utilizzate i tasti freccia per passare al termine desiderato e premete **Invio**.

![Immagine](../images/queries/query-editor-overview/syntax-auto.png)

- **Tabella e campo con completamento automatico:** Iniziate a digitare il nome della tabella da cui desiderate `SELECT` uscire, quindi utilizzate i tasti freccia per passare alla tabella cercata e premete **Invio**. Dopo aver selezionato una tabella, la funzione di completamento automatico riconoscerà i campi nella tabella.

![Immagine](../images/queries/query-editor-overview/tables-auto.png)

### Rilevamento errori

Editor query convalida automaticamente una query durante la scrittura, fornendo la convalida SQL generica e la convalida dell&#39;esecuzione specifica. Se sotto la query viene visualizzata una sottolineatura rossa (come illustrato nell&#39;immagine seguente), all&#39;interno della query viene visualizzato un errore.

![Immagine](../images/queries/query-editor-overview/syntax-error-highlight.png)

Quando vengono rilevati degli errori, è possibile visualizzare i messaggi di errore specifici posizionando il puntatore del mouse sul codice SQL.

![Immagine](../images/queries/query-editor-overview/linting-error.png)

### Dettagli query

Durante la visualizzazione di una query in Editor query, il pannello Dettagli ** query fornisce gli strumenti per gestire la query selezionata.

![Immagine](../images/queries/query-editor-overview/query-details.png)

Questo pannello consente di generare un set di dati di output direttamente dall&#39;interfaccia utente, eliminare o assegnare un nome alla query visualizzata e visualizzare il codice SQL in un formato di semplice copia nella scheda Query ** SQL. Questo pannello mostra anche utili metadati, ad esempio l’ultima volta che la query è stata modificata e l’utente che l’ha modificata, se applicabile. Per generare un set di dati, fare clic su **Output Dataset**. Viene visualizzata la finestra di dialogo DataSet di *output* . Immettete un nome e una descrizione, quindi fate clic su **Esegui query**. Il nuovo set di dati viene visualizzato nella scheda *Set* di dati dell&#39;interfaccia utente Servizio query di Platform.

### Salvataggio delle query

L&#39;Editor query fornisce una funzione di salvataggio che consente di salvare una query e di lavorarci in un secondo momento. Per salvare una query, fate clic su **Salva** nell’angolo in alto a destra dell’Editor query. Prima di salvare una query, è necessario specificare un nome per la query utilizzando il pannello Dettagli ** query.

### Come trovare le query precedenti

Tutte le query eseguite dall&#39;Editor query vengono acquisite nella tabella Registro. È possibile utilizzare la funzionalità di ricerca nella scheda *Registro* per individuare le esecuzioni delle query. Le query salvate sono elencate nella scheda *Sfoglia* .

Per ulteriori informazioni, consulta la panoramica [dell’interfaccia utente del servizio][query-service-ui] query.

>[!NOTE]
>
>Le query non eseguite non vengono salvate dal registro. Affinché la query sia disponibile in Query Service, è necessario eseguirla o salvarla in Query Editor.

## Esecuzione di query con l&#39;Editor query

Per eseguire una query in Editor query, è possibile immettere SQL nell&#39;editor o caricare una query precedente dalla scheda *Registro* o *Sfoglia* , quindi fare clic su **Riproduci**. Lo stato dell&#39;esecuzione della query viene visualizzato nella scheda *Console* sottostante e i dati di output sono visualizzati nella scheda *Risultati* .

### Console

La console fornisce informazioni sullo stato e il funzionamento di Query Service. La console visualizza lo stato della connessione a Query Service, le operazioni di query in esecuzione ed eventuali messaggi di errore risultanti da tali query.

![Immagine](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>Nella console sono visualizzati solo gli errori risultanti dall’esecuzione di una query. Non vengono visualizzati errori di convalida delle query prima dell&#39;esecuzione di una query.

### Risultati query

Al termine di una query, i risultati vengono visualizzati nella scheda *Risultati* , accanto alla scheda *Console* . Questa visualizzazione mostra l’output tabulare della query, visualizzando fino a 100 righe. Questa visualizzazione consente di verificare che la query produca l&#39;output previsto. Per generare un dataset con la query, rimuovere i limiti sulle righe restituite ed eseguire la query con `CREATE TABLE tablename AS SELECT` cui generare un dataset con l&#39;output. Per istruzioni su come generare un set di dati dai risultati della query nell&#39;Editor query, vedere l&#39;esercitazione sulla [generazione][query-service-create-datasets] dei set di dati.

![Immagine](../images/queries/query-editor-overview/query-results.png)

## Eseguire query con il video di esercitazione del servizio query

Il seguente video mostra come eseguire le query nell&#39;interfaccia del Adobe Experience Platform  e in un client PSQL. Inoltre, viene illustrato l&#39;utilizzo di singole proprietà in un oggetto XDM, utilizzando funzioni definite da Adobe e utilizzando CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Passaggi successivi

Ora che si conoscono le funzionalità disponibili in Editor query e come navigare nell&#39;applicazione, è possibile iniziare a creare query personalizzate direttamente in Platform. Per ulteriori informazioni sull&#39;esecuzione di query SQL rispetto ai dataset in Data Lake, vedere la guida sull&#39; [esecuzione di query][query-service-running-queries]. Per query SQL di esempio per lavorare con Adobe  Analytics e dati  Adobe Target, consultate il riferimento [alle query di][query-service-sample-queries]esempio.

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../creating-queries/creating-queries.md
[query-service-sample-queries]: ../sample-queries/overview.md
[query-service-create-datasets]: ../creating-queries/create-datasets.md
