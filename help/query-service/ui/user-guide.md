---
keywords: Experience Platform;home;argomenti popolari;editor query;editor query;servizio query;servizio query;
solution: Experience Platform
title: Guida all’interfaccia utente dell’editor delle query
topic-legacy: query editor
description: Query Editor è uno strumento interattivo fornito da Adobe Experience Platform Query Service che consente di scrivere, convalidare ed eseguire query per i dati sulla customer experience all’interno dell’interfaccia utente di Experience Platform. L’editor delle query supporta lo sviluppo di query per l’analisi e l’esplorazione dei dati e consente di eseguire query interattive a scopo di sviluppo, nonché query non interattive per popolare i set di dati in Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: c8b3b22b678622c31462ba0baa2f50fbe89b00d5
workflow-type: tm+mt
source-wordcount: '1625'
ht-degree: 1%

---

# [!DNL Query Editor] Guida all’interfaccia utente

[!DNL Query Editor] è uno strumento interattivo fornito da Adobe Experience Platform [!DNL Query Service], che consente di scrivere, convalidare ed eseguire query per i dati sulla customer experience all’interno dell’ [!DNL Experience Platform] interfaccia utente. [!DNL Query Editor] supporta lo sviluppo di query per l’analisi e l’esplorazione dei dati e consente di eseguire query interattive a scopo di sviluppo, nonché query non interattive per compilare i set di dati in [!DNL Experience Platform].

Per ulteriori informazioni sui concetti e le funzionalità di [!DNL Query Service], vedi [Panoramica del servizio query](../home.md). Per ulteriori informazioni su come navigare nell’interfaccia utente del servizio query su [!DNL Platform], vedi [Panoramica dell’interfaccia utente del servizio query](./overview.md).

## Introduzione {#getting-started}

[!DNL Query Editor] fornisce un&#39;esecuzione flessibile delle query tramite la connessione a [!DNL Query Service], e le query verranno eseguite solo quando la connessione è attiva.

### Connessione a [!DNL Query Service] {#connecting-to-query-service}

[!DNL Query Editor] L&#39;inizializzazione e la connessione richiedono alcuni secondi [!DNL Query Service] quando viene aperto. La console indica quando è connessa, come illustrato di seguito. Se tenti di eseguire una query prima che l’editor si sia connesso, l’esecuzione ritarda fino al completamento della connessione.

![Immagine](../images/ui/query-editor/connect.png)

### Esecuzione delle query da [!DNL Query Editor] {#run-a-query}

Query eseguite da [!DNL Query Editor] esegui in modo interattivo. Ciò significa che se chiudi il browser o se ti allontani, la query viene annullata. Questo vale anche per le query create per generare set di dati dagli output delle query.

## Creazione di query tramite [!DNL Query Editor] {#query-authoring}

Utilizzo [!DNL Query Editor], puoi scrivere, eseguire e salvare query per i dati sulla customer experience. Tutte le query eseguite o salvate in [!DNL Query Editor] sono disponibili per tutti gli utenti dell’organizzazione con accesso a [!DNL Query Service].

### Accesso al [!DNL Query Editor] {#accessing-query-editor}

In [!DNL Experience Platform] Interfaccia utente, seleziona **[!UICONTROL Query]** nel menu di navigazione a sinistra per aprire [!DNL Query Service] workspace. Quindi, seleziona **[!UICONTROL Crea query]** in alto a destra della schermata per iniziare a scrivere query. Questo collegamento è disponibile da una qualsiasi delle pagine nel [!DNL Query Service] workspace.

![Immagine](../images/ui/query-editor/create-query.png)

### Scrittura di query {#writing-queries}

[!UICONTROL Editor query] è organizzato in modo da rendere la scrittura di query il più semplice possibile. La schermata seguente mostra come l’editor appare nell’interfaccia utente, con **Play** campo voce pulsante e SQL evidenziato.

![Immagine](../images/ui/query-editor/editor.png)

Per ridurre al minimo il tempo di sviluppo, è consigliabile sviluppare le query con limiti sulle righe restituite. Ad esempio, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Dopo aver verificato che la query produca l’output previsto, rimuovi i limiti ed esegui la query con `CREATE TABLE tablename AS SELECT` per generare un set di dati con l’output.

### Strumenti di scrittura in [!DNL Query Editor] {#writing-tools}

- **Evidenziazione automatica della sintassi:** Semplifica la lettura e l&#39;organizzazione di SQL.

![Immagine](../images/ui/query-editor/syntax-highlight.png)

- **Completamento automatico parola chiave SQL:** Inizia a digitare la query e utilizza i tasti freccia per passare al termine desiderato e premi **Invio**.

![Immagine](../images/ui/query-editor/syntax-auto.png)

- **Completamento automatico tabella e campo:** Inizia a digitare il nome della tabella che desideri `SELECT` da, quindi utilizzare i tasti freccia per passare alla tabella desiderata e premere **Invio**. Una volta selezionata una tabella, la funzione di completamento automatico riconoscerà i campi presenti nella tabella.

![Immagine](../images/ui/query-editor/tables-auto.png)

### Rilevamento degli errori {#error-detection}

[!DNL Query Editor] convalida automaticamente una query durante la scrittura, fornendo una convalida SQL generica e una convalida di esecuzione specifica. Se sotto la query viene visualizzata una sottolineatura rossa (come illustrato nell’immagine seguente), la query presenta un errore.

![Immagine](../images/ui/query-editor/syntax-error-highlight.png)

Quando vengono rilevati errori, è possibile visualizzare i messaggi di errore specifici passando il mouse sul codice SQL.

![Immagine](../images/ui/query-editor/linting-error.png)

### Dettagli query {#query-details}

Durante la visualizzazione di una query in [!DNL Query Editor], **[!UICONTROL Dettagli query]** Il pannello fornisce gli strumenti per gestire la query selezionata.

![Immagine](../images/ui/query-editor/query-details.png)

Questo pannello consente di generare un set di dati di output direttamente dall’interfaccia utente, eliminare o denominare la query visualizzata e aggiungere una pianificazione alla query.

Questo pannello mostra anche metadati utili, come l’ultima volta che la query è stata modificata e chi l’ha modificata, se applicabile. Per generare un set di dati, seleziona **[!UICONTROL Set di dati di output]**. La **[!UICONTROL Set di dati di output]** viene visualizzata la finestra di dialogo . Immetti un nome e una descrizione, quindi seleziona **[!UICONTROL Esegui query]**. Il nuovo set di dati viene visualizzato nel **[!UICONTROL Set di dati]** nella scheda [!DNL Query Service] interfaccia utente attiva [!DNL Platform].

### Query pianificate {#scheduled-queries}

>[!IMPORTANT]
>
>Di seguito è riportato un elenco di limitazioni per le query pianificate quando si utilizza l’editor delle query. Non si applicano al [!DNL Query Service] API:<br/>È possibile aggiungere una pianificazione solo a una query già creata, salvata ed eseguita.<br/>You **impossibile** aggiungi una pianificazione a una query con parametri.<br/>Query pianificate **impossibile** contiene un blocco anonimo.

Per aggiungere una pianificazione a una query, seleziona **[!UICONTROL Aggiungi pianificazione]**.

![Immagine](../images/ui/query-editor/add-schedule.png)

La **[!UICONTROL Dettagli della pianificazione]** viene visualizzata la pagina . In questa pagina puoi scegliere la frequenza della query pianificata, le date di esecuzione della query pianificata e il set di dati in cui esportare la query.

![Immagine](../images/ui/query-editor/schedule-details.png)

Puoi scegliere le seguenti opzioni per **[!UICONTROL Frequenza]**:

- **[!UICONTROL Orario]**: La query pianificata viene eseguita ogni ora per il periodo di data selezionato.
- **[!UICONTROL Giornaliero]**: La query pianificata verrà eseguita ogni X giorni all’ora e al periodo di data selezionato. Tieni presente che l’ora selezionata è in **UTC** e non il fuso orario locale.
- **[!UICONTROL Settimanale]**: La query selezionata verrà eseguita nei giorni della settimana, dell’ora e del periodo di data selezionati. Tieni presente che l’ora selezionata è in **UTC** e non il fuso orario locale.
- **[!UICONTROL Mensile]**: La query selezionata viene eseguita ogni mese al giorno, all’ora e al periodo di data selezionato. Tieni presente che l’ora selezionata è in **UTC** e non il fuso orario locale.
- **[!UICONTROL Annuale]**: La query selezionata viene eseguita ogni anno al giorno, al mese, all’ora e al periodo di data selezionato. Tieni presente che l’ora selezionata è in **UTC** e non il fuso orario locale.

Per il set di dati, puoi utilizzare un set di dati esistente o crearne uno nuovo.

>[!IMPORTANT]
>
> Poiché utilizzi un set di dati esistente o crei un nuovo, lo fai **not** devono includere `INSERT INTO` o `CREATE TABLE AS SELECT` come parte della query, poiché i set di dati sono già impostati. Includere `INSERT INTO` o `CREATE TABLE AS SELECT` come parte delle query pianificate si verifica un errore.

Dopo aver confermato tutti questi dettagli, seleziona **[!UICONTROL Salva]** per creare una pianificazione.

La pagina dei dettagli della query viene visualizzata nuovamente e ora mostra i dettagli della nuova pianificazione creata, inclusi l’ID pianificazione, la pianificazione stessa e il set di dati di output della pianificazione. Puoi utilizzare l’ID pianificazione per cercare ulteriori informazioni sulle esecuzioni della query pianificata stessa. Per saperne di più, leggere il [guida agli endpoint di esecuzione delle query programmate](../api/runs-scheduled-queries.md).

>[!NOTE]
>
> È possibile pianificare solo **uno** modello di query utilizzando l’interfaccia utente. Se desideri aggiungere ulteriori pianificazioni a un modello di query, dovrai utilizzare l’API . Se una pianificazione è già stata aggiunta utilizzando l’API, **not** puoi aggiungere altre pianificazioni utilizzando l’interfaccia utente . Se più pianificazioni sono già collegate a un modello di query, verrà visualizzata solo la pianificazione meno recente. Per informazioni su come aggiungere le pianificazioni utilizzando l’API, leggi la [guida all’endpoint delle query pianificate](../api/scheduled-queries.md).
>
> Inoltre, devi aggiornare la pagina se desideri avere lo stato più recente della pianificazione che stai visualizzando.

#### Eliminare una pianificazione {#delete-schedule}

Per eliminare una pianificazione, seleziona **[!UICONTROL Eliminare una pianificazione]**.

![Immagine](../images/ui/query-editor/delete-schedule.png)

>[!IMPORTANT]
>
> Se si desidera eliminare una pianificazione per una query, è necessario prima disattivare la pianificazione.

### Salvataggio delle query {#saving-queries}

[!DNL Query Editor] fornisce una funzione di salvataggio che ti consente di salvare una query e lavorarci in un secondo momento. Per salvare una query, seleziona **[!UICONTROL Salva]** nell&#39;angolo in alto a destra di [!DNL Query Editor]. Prima di salvare una query, è necessario specificare un nome per la query utilizzando **[!UICONTROL Dettagli query]** pannello.

>[!NOTE]
>
>Le query denominate e salvate con l’Editor query sono disponibili come modelli all’interno del dashboard Query [!UICONTROL Sfoglia] scheda . Consulta la sezione [documentazione dei modelli](./query-templates.md) per ulteriori informazioni.

### Come trovare le query precedenti {#previous-queries}

Tutte le query eseguite da [!DNL Query Editor] vengono acquisiti nella tabella Registro. Puoi utilizzare la funzionalità di ricerca nella sezione **[!UICONTROL Registro]** per trovare le esecuzioni delle query. Le query salvate sono elencate nella **[!UICONTROL Sfoglia]** scheda .

Consulta la sezione [Panoramica dell’interfaccia utente del servizio query](./overview.md) per ulteriori informazioni.

>[!NOTE]
>
>Le query non eseguite non vengono salvate dal registro. Affinché la query sia disponibile in [!DNL Query Service], deve essere eseguito o salvato in [!DNL Query Editor].

## Esecuzione di query tramite Editor query {#executing-queries}

Per eseguire una query in [!DNL Query Editor], è possibile immettere SQL nell&#39;editor o caricare una query precedente dal **[!UICONTROL Registro]** o **[!UICONTROL Sfoglia]** e seleziona **Play**. Lo stato dell’esecuzione della query viene visualizzato nel **[!UICONTROL Console]** , e i dati di output sono visualizzati nella **[!UICONTROL Risultati]** scheda .

### Console {#console}

La console fornisce informazioni sullo stato e sul funzionamento di [!DNL Query Service]. Nella console viene visualizzato lo stato della connessione a [!DNL Query Service], le operazioni di query in esecuzione ed eventuali messaggi di errore risultanti da tali query.

![Immagine](../images/ui/query-editor/console.png)

>[!NOTE]
>
>La console mostra solo gli errori derivanti dall’esecuzione di una query. Non mostra gli errori di convalida delle query prima dell’esecuzione di una query.

### Risultati della query {#query-results}

Al termine di una query, i risultati vengono visualizzati nella **[!UICONTROL Risultati]** accanto alla scheda **[!UICONTROL Console]** scheda . Questa visualizzazione mostra l’output tabulare della query, visualizzando fino a 100 righe. Questa visualizzazione ti consente di verificare che la query produca l’output previsto. Per generare un set di dati con la query, rimuovi i limiti sulle righe restituite ed esegui la query con `CREATE TABLE tablename AS SELECT` per generare un set di dati con l’output. Consulta la sezione [esercitazione sulla generazione di set di dati](./create-datasets.md) per istruzioni su come generare un set di dati dai risultati della query in [!DNL Query Editor].

![Immagine](../images/ui/query-editor/query-results.png)

## Eseguire query con [!DNL Query Service] video tutorial {#query-tutorial-video}

Il video seguente mostra come eseguire le query nell’interfaccia Adobe Experience Platform e in un client PSQL. Inoltre, vengono dimostrate l’utilizzo di singole proprietà in un oggetto XDM, di funzioni definite in Adobe e di CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Passaggi successivi

Ora sai quali funzioni sono disponibili in [!DNL Query Editor] e come navigare nell’applicazione, puoi iniziare a creare query personalizzate direttamente in [!DNL Platform]. Per ulteriori informazioni sull&#39;esecuzione di query SQL rispetto ai set di dati in [!DNL Data Lake], consulta la guida su [query in esecuzione](../best-practices/writing-queries.md).
