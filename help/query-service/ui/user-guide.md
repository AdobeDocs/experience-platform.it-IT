---
keywords: Experience Platform;home;argomenti popolari;editor query;editor query;servizio query;servizio query;
solution: Experience Platform
title: Guida dell’interfaccia utente di Query Editor
description: L’editor delle query è uno strumento interattivo fornito da Adobe Experience Platform Query Service che consente di scrivere, convalidare ed eseguire query per i dati sull’esperienza del cliente all’interno dell’interfaccia utente di Experienci Platform. Query Editor supporta lo sviluppo di query per l’analisi e l’esplorazione dei dati e consente di eseguire query interattive a scopo di sviluppo, nonché query non interattive per popolare i set di dati in Experienci Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: 8b6cd84a31f9cdccef9f342df7f7b8450c2405dc
workflow-type: tm+mt
source-wordcount: '2825'
ht-degree: 2%

---

# [!DNL Query Editor] Guida all’interfaccia utente

>[!NOTE]
>
>Al 30 aprile 2024 [Editor query avanzato](#enhanced-editor-toggle) è diventato l’editor predefinito per tutti gli utenti. L’editor legacy diventerà obsoleto il 30 maggio 2024 e non sarà più disponibile.

[!DNL Query Editor] è uno strumento interattivo fornito da Adobe Experience Platform [!DNL Query Service], che consente di scrivere, convalidare ed eseguire query per i dati sulla customer experience in [!DNL Experience Platform] dell&#39;utente. [!DNL Query Editor] supporta lo sviluppo di query per l’analisi e l’esplorazione dei dati e consente di eseguire query interattive a scopo di sviluppo, nonché query non interattive per popolare i set di dati in [!DNL Experience Platform].

Per ulteriori informazioni sui concetti e le funzionalità di [!DNL Query Service], vedere [Panoramica di Query Service](../home.md). Per ulteriori informazioni su come navigare nell’interfaccia utente di Query Service su [!DNL Platform], vedere [Panoramica dell’interfaccia utente di Query Service](./overview.md).

>[!NOTE]
>
>Alcune funzionalità di Query Service non sono fornite dalla versione precedente di Query Editor. Le schermate utilizzate in questo documento vengono acquisite utilizzando la versione migliorata dell’editor delle query, salvo diversa indicazione. Consulta la sezione sulla [Editor query avanzato](#enhanced-editor-toggle) per ulteriori dettagli.

## Introduzione {#getting-started}

[!DNL Query Editor] fornisce un’esecuzione flessibile delle query tramite la connessione a [!DNL Query Service]Le query, e vengono eseguite solo quando la connessione è attiva.

## Accesso [!DNL Query Editor] {#accessing-query-editor}

In [!DNL Experience Platform] UI, seleziona **[!UICONTROL Query]** nel menu di navigazione sinistro per aprire [!DNL Query Service] Workspace. Quindi, per iniziare a scrivere le query, seleziona **[!UICONTROL Crea query]** in alto a destra. Questo collegamento è disponibile da una qualsiasi delle pagine di [!DNL Query Service] Workspace.

![La scheda Panoramica dell’area di lavoro Query in cui è evidenziata l’opzione Crea query.](../images/ui/query-editor/create-query.png)

### Connessione a [!DNL Query Service] {#connecting-to-query-service}

L’editor delle query impiega alcuni secondi per inizializzare e connettersi a Query Service quando viene aperto. La console indica quando è collegata, come illustrato di seguito. Se tenti di eseguire una query prima che l’editor si sia connesso, l’esecuzione viene rimandata fino al completamento della connessione.

![L&#39;output della console dell&#39;editor di query al momento della connessione iniziale.](../images/ui/query-editor/connect.png)

### Esecuzione delle query da [!DNL Query Editor] {#run-a-query}

Query eseguite da [!DNL Query Editor] esegui in modo interattivo, il che significa che se chiudi il browser o esci, la query viene annullata. Lo stesso vale per le query eseguite per generare set di dati dagli output delle query.

L&#39;edizione avanzata dell&#39;editor di query consente di scrivere più query nell&#39;editor ed eseguirle in sequenza. Consulta la sezione su [esecuzione di più query sequenziali](#execute-multiple-sequential-queries) per ulteriori informazioni.

## Creazione di query tramite [!DNL Query Editor] {#query-authoring}

Utilizzo di [!DNL Query Editor], puoi scrivere, eseguire e salvare query per i dati sull’esperienza del cliente. Tutte le query eseguite o salvate in [!DNL Query Editor] sono disponibili per tutti gli utenti dell’organizzazione con accesso a [!DNL Query Service].

>[!IMPORTANT]
>
>Il 30 aprile 2024 l’Editor query avanzato sarà l’editor predefinito per tutti gli utenti. L’editor legacy diventerà obsoleto il 30 maggio 2024 e non sarà più disponibile.

## Opzione Editor di query ottimizzata {#enhanced-editor-toggle}

>[!CONTEXTUALHELP]
>id="platform_queryService_queryEditor_enhancedEditorToggle"
>title="Interruttore per editor avanzato"
>abstract="Puoi passare dall’editor di query precedente alla nuova versione avanzata. La versione precedente è abilitata per impostazione predefinita, ma la versione avanzata fornisce migliori funzioni per l’accessibilità e il supporto di più temi. Per ulteriori informazioni su queste modifiche, consulta la documentazione."

Un interruttore dell’interfaccia utente consente di passare dalla versione legacy alla versione avanzata dell’editor di query. La versione precedente è abilitata per impostazione predefinita, ma la versione avanzata fornisce migliori funzioni per l’accessibilità e il supporto di più temi. Abilita la versione avanzata per accedere alle impostazioni dell’editor di query.

![L’Editor query con l’Editor query avanzato è evidenziato.](../images/ui/query-editor/enhanced-query-editor-toggle.png)

Attivando l’interruttore, l’editor diventa leggero e migliora la leggibilità della sintassi. Sopra il campo di input dell’editor di query viene visualizzata un’icona delle impostazioni che incorpora l’interruttore di completamento automatico. Dall’icona delle impostazioni, puoi abilitare il tema scuro o disabilitare/abilitare il completamento automatico.

>[!TIP]
>
>L’editor di query avanzato consente di: [!UICONTROL Disabilita completamento automatico sintassi] durante l’authoring di una query senza perdere l’avanzamento. In genere, se si disattiva la funzione di completamento automatico durante la modifica, tutte le modifiche apportate alla query andranno perse.

Per attivare i temi scuri o chiari, selezionare l&#39;icona delle impostazioni (![Un&#39;icona delle impostazioni.](../images/ui/query-editor/settings-icon.png)) seguito dall&#39;opzione nel menu a discesa visualizzato.

![L’editor delle query con l’icona delle impostazioni e l’opzione del menu a discesa Abilita tema scuro sono evidenziate.](../images/ui/query-editor/query-editor-settings.png)

### Eseguire più query sequenziali {#execute-multiple-sequential-queries}

L&#39;edizione avanzata dell&#39;editor di query consente di scrivere più di una query nell&#39;editor ed eseguirle tutte in modo sequenziale.

L’esecuzione di più query in una sequenza genera ciascuna una voce di registro. Tuttavia, solo i risultati della prima query vengono visualizzati nella console dell’editor delle query. Se hai la necessità di risolvere i problemi o confermare le query eseguite, controlla il registro delle query. Consulta la [documentazione dei registri di query](./query-logs.md) per ulteriori informazioni.

>[!NOTE]
> 
>Se una query CTAS viene eseguita dopo la prima query nell’editor delle query, viene comunque creata una tabella, ma non è presente alcun output nella console dell’editor delle query.

### Esegui query selezionata {#execute-selected-query}

Se hai scritto più query ma devi eseguirne una sola, puoi evidenziare la query scelta e selezionare la
[!UICONTROL Esegui query selezionata] icona. Questa icona è disattivata per impostazione predefinita finché non selezioni la sintassi della query all’interno dell’editor.

![L’editor delle query con [!UICONTROL Esegui query selezionata] icona evidenziata.](../images/ui/query-editor/run-selected-query.png)

### Annulla sessione editor query {#cancel-query}

Controlla l’esecuzione delle query e migliora la produttività annullando le query con tempi di esecuzione lunghi. Questa azione cancella l&#39;Editor query durante l&#39;esecuzione di una query. Tieni presente che la query continua a essere eseguita in background. Se si tratta di una query CTAS, verrà comunque generato un set di dati di output. Per annullare l&#39;esecuzione nell&#39;editor e continuare a comporre un&#39;istruzione SQL, selezionare **[!UICONTROL Annulla query]** dopo l’esecuzione di una query.

![Editor query con [!UICONTROL Annulla query] evidenziato.](../images/ui/query-editor/cancel-query-run.png)

Viene visualizzata una finestra di dialogo di conferma. Seleziona **[!UICONTROL Conferma]** per annullare l&#39;esecuzione della query.

![La finestra di dialogo Annulla conferma query con Conferma è evidenziata.](../images/ui/query-editor/cancel-query-confirmation-dialog.png)

### Conteggio risultati {#result-count}

L’editor delle query può contenere un massimo di 50.000 righe. Puoi scegliere il numero di righe da visualizzare contemporaneamente nella console dell’editor delle query. Per modificare il numero di righe visualizzate nella console, seleziona la **[!UICONTROL Conteggio risultati]** e selezionare tra le opzioni 50, 100, 150, 300 e 500.

![L’editor delle query con il menu a discesa Conteggio risultati è evidenziato.](../images/ui/query-editor/result-count.png)

## Scrittura delle query {#writing-queries}

[!UICONTROL Editor query] è organizzato in modo da rendere la scrittura delle query il più semplice possibile. La schermata seguente mostra come viene visualizzato l’editor nell’interfaccia utente, con il campo di immissione SQL e **Play** evidenziato.

![Editor query con il campo di input SQL e Play evidenziati.](../images/ui/query-editor/editor.png)

Per ridurre al minimo il tempo di sviluppo, ti consigliamo di sviluppare le query con limiti al numero di righe restituite. Ad esempio, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Dopo aver verificato che la query produca l’output previsto, rimuovi i limiti ed esegui la query con `CREATE TABLE tablename AS SELECT` per generare un set di dati con l’output.

## Strumenti di scrittura in [!DNL Query Editor] {#writing-tools}

- **Evidenziazione automatica della sintassi:** Semplifica la lettura e l&#39;organizzazione di SQL.

![Istruzione SQL nell&#39;editor delle query che illustra l&#39;evidenziazione dei colori della sintassi.](../images/ui/query-editor/syntax-highlight.png)

- **Completamento automatico parola chiave SQL:** Inizia a digitare la query, quindi utilizza i tasti freccia per passare al termine desiderato e premi **Invio**.

![Alcuni caratteri di SQL con il menu a discesa di completamento automatico che fornisce le opzioni dall’editor delle query.](../images/ui/query-editor/syntax-auto.png)

- **Completamento automatico tabella e campo:** Inizia a digitare il nome della tabella che desideri `SELECT` da, quindi utilizzare i tasti freccia per passare alla tabella desiderata e premere **Invio**. Dopo aver selezionato una tabella, il completamento automatico riconosce i campi della tabella.

![L’input dell’editor delle query che visualizza i suggerimenti per i nomi delle tabelle a discesa.](../images/ui/query-editor/tables-auto.png)

### Formato testo {#format-text}

Il [!UICONTROL Formato testo] rende la query più leggibile aggiungendo uno stile di sintassi standardizzato. Seleziona **[!UICONTROL Formato testo]** per standardizzare tutto il testo all&#39;interno dell&#39;editor di query.

>[!NOTE]
>
>Il [!UICONTROL Formato testo] La funzionalità non funziona con blocchi anonimi. Per informazioni su come concatenare una o più istruzioni SQL in sequenza, vedere [documentazione di blocco anonimo](../key-concepts/anonymous-block.md).

![Editor query con [!UICONTROL Formato testo] e le istruzioni SQL evidenziate.](../images/ui/query-editor/format-text.png)

<!-- ### Undo text {#undo-text}

If you format your SQL in the Query Editor, you can undo the formatting applied by the [!UICONTROL Format text] feature. To return your SQL back to its original form, select **[!UICONTROL Undo text]**.

![The Query Editor with [!UICONTROL Undo text] and the SQL statements highlighted.](../images/ui/query-editor/undo-text.png) -->

### Copia SQL {#copy-sql}

Selezionare l&#39;icona Copia per copiare SQL dall&#39;editor di query negli Appunti. Questa funzione di copia è disponibile sia per i modelli di query che per le query appena create nell’Editor query.

![Nell’area di lavoro Query è presente un modello di query di esempio con l’icona Copia evidenziata.](../images/ui/query-editor/copy-sql.png)

### Attivazione/disattivazione della configurazione dell’interfaccia utente a completamento automatico {#auto-complete}

Il [!DNL Query Editor] suggerisce automaticamente parole chiave SQL potenziali insieme ai dettagli di tabella o colonna per la query durante la scrittura. La funzione di completamento automatico è abilitata per impostazione predefinita e può essere disabilitata o abilitata in qualsiasi momento selezionando [!UICONTROL Completamento automatico della sintassi] passa in alto a destra nell’editor di query.

L’impostazione di configurazione del completamento automatico è per utente e viene memorizzata per gli accessi consecutivi per tale utente.

>[!NOTE]
>
>L’opzione di completamento automatico della sintassi è disponibile solo per la versione precedente di Query Editor.

![Editor query con l&#39;opzione di completamento automatico della sintassi evidenziata.](../images/ui/query-editor/auto-complete-toggle.png)

La disattivazione di questa funzione interrompe l’elaborazione di diversi comandi di metadati e fornisce consigli che in genere migliorano la velocità dell’autore durante la modifica delle query.

Quando si utilizza l’interruttore per abilitare la funzione di completamento automatico, dopo una breve pausa diventano disponibili i suggerimenti consigliati per i nomi di tabelle e colonne e le parole chiave SQL. Un messaggio di operazione riuscita nella console sotto l’editor di query indica che la funzione è attiva.

Se disattivate la funzione di completamento automatico, è necessario aggiornare la pagina per rendere effettiva la funzione. Viene visualizzata una finestra di dialogo di conferma con tre opzioni quando disattivi il [!UICONTROL Completamento automatico della sintassi] toggle:

- [!UICONTROL Annulla]
- [!UICONTROL Salva modifiche e aggiorna]
- [!UICONTROL Aggiorna senza salvare le modifiche]

>[!IMPORTANT]
>
>Se si sta scrivendo o modificando una query quando si disabilita questa funzione, è necessario salvare le modifiche apportate alla query prima di aggiornare la pagina. In caso contrario, tutto l&#39;avanzamento andrà perduto.

![Finestra di dialogo di conferma per disattivare la funzione di completamento automatico.](../images/ui/query-editor/confirmation-dialog.png)

Per disattivare la funzione di completamento automatico, selezionare l&#39;opzione di conferma appropriata.

### Rilevamento di errori {#error-detection}

[!DNL Query Editor] convalida automaticamente una query durante la scrittura, fornendo una convalida SQL generica e una convalida di esecuzione specifica. Se sotto la query viene visualizzata una sottolineatura rossa (come illustrato nell&#39;immagine riportata di seguito), si verifica un errore all&#39;interno della query.

<!-- ... Image below needs updating couldn't replicate the effect -->

![L&#39;input dell&#39;editor delle query che visualizza SQL sottolineato in rosso indica un errore.](../images/ui/query-editor/syntax-error-highlight.png)

Quando vengono rilevati errori, è possibile visualizzare i messaggi di errore specifici passando il puntatore del mouse sul codice SQL.

<!-- ... Image below needs updating couldn't replicate the effect -->

![Finestra di dialogo con un messaggio di errore.](../images/ui/query-editor/linting-error.png)

### Dettagli query {#query-details}

Per visualizzare una query nell’editor delle query, seleziona un modello salvato dall’ [!UICONTROL Modelli] scheda. Il pannello Dettagli query fornisce ulteriori informazioni e strumenti per gestire la query selezionata. Mostra inoltre metadati utili, ad esempio l’ultima volta che la query è stata modificata e chi l’ha modificata, se applicabile.

>[!NOTE]
>
>Il [!UICONTROL Visualizza pianificazione], [!UICONTROL Aggiungi pianificazione] e [!UICONTROL Elimina query] le opzioni sono disponibili solo dopo il salvataggio della query come modello. Il [!UICONTROL Aggiungi pianificazione] consente di accedere direttamente al generatore di pianificazione dall’editor di query. Il [!UICONTROL Visualizza pianificazione] consente di passare direttamente all&#39;inventario di programmazione per tale query. Consulta la documentazione sulle pianificazioni delle query per scoprire come [creare pianificazioni di query nell’interfaccia utente](./query-schedules.md#create-schedule).

![Editor query con il pannello Dettagli query evidenziato.](../images/ui/query-editor/query-details.png)

Dal pannello dei dettagli puoi generare un set di dati di output direttamente dall’interfaccia utente, eliminare o denominare la query visualizzata, visualizzare la pianificazione di esecuzione della query e aggiungere la query a una pianificazione.

Per generare un set di dati di output, seleziona **[!UICONTROL Esegui come CTAS]**. Il **[!UICONTROL Immetti i dettagli del set di dati di output]** viene visualizzata. Inserisci un nome e una descrizione, quindi seleziona **[!UICONTROL Esegui come CTAS]**. Il nuovo set di dati viene visualizzato in **[!UICONTROL Set di dati]** Scheda Sfoglia. Consulta [la documentazione visualizza set di dati](../../catalog/datasets/user-guide.md#view-datasets) per ulteriori informazioni sui set di dati disponibili per la tua organizzazione.

>[!NOTE]
>
>Il [!UICONTROL Esegui come CTAS] è disponibile solo se la query ha **non** pianificata.

![Il [!UICONTROL Immetti i dettagli del set di dati di output] .](../images/ui/query-editor/output-dataset-details.png)

Dopo aver eseguito **[!UICONTROL Esegui come CTAS]** azione, viene visualizzato un messaggio di conferma per avvisarti dell’azione riuscita. Questo messaggio a comparsa contiene un collegamento che consente di accedere facilmente all’area di lavoro dei registri delle query. Consulta la [documentazione dei registri di query](./query-logs.md) per ulteriori informazioni sui registri delle query.

### Salvataggio delle query {#saving-queries}

Il [!DNL Query Editor] fornisce una funzione di salvataggio che consente di salvare una query e lavorarci in un secondo momento. Per salvare una query, seleziona **[!UICONTROL Salva]** nell’angolo in alto a destra di [!DNL Query Editor]. Prima di poter salvare una query, è necessario specificarne il nome utilizzando **[!UICONTROL Dettagli query]** pannello.

>[!NOTE]
>
>Le query denominate e salvate in mediante l&#39;Editor query sono disponibili come modelli nel dashboard Query [!UICONTROL Modelli] scheda. Consulta la [documentazione sui modelli](./query-templates.md) per ulteriori informazioni.

Quando salvi una query nell’editor delle query, viene visualizzato un messaggio di conferma per informarti dell’azione riuscita. Questo messaggio a comparsa contiene un collegamento che consente di accedere facilmente all’area di lavoro di pianificazione delle query. Consulta la [documentazione sulle query di pianificazione](./query-schedules.md) per scoprire come eseguire query su una cadenza personalizzata.

### Query pianificate {#scheduled-queries}

Le query salvate come modello possono essere pianificate dall&#39;Editor query. La pianificazione delle query consente di automatizzare l’esecuzione delle query su una cadenza personalizzata. Puoi pianificare le query in base a frequenza, data e ora e, se necessario, scegliere anche un set di dati di output per i risultati. Le pianificazioni delle query possono anche essere disabilitate o eliminate tramite l’interfaccia utente.

Le pianificazioni vengono impostate nell&#39;editor delle query. Quando si utilizza l&#39;editor delle query, è possibile aggiungere una pianificazione solo a una query già creata e salvata. La stessa limitazione non si applica al [!DNL Query Service] API.

>[!NOTE]
>
>Le query pianificate che non superano dieci esecuzioni consecutive vengono inserite automaticamente in un [!UICONTROL In quarantena] stato. Una query con questo stato richiede l’intervento dell’utente prima di poter eseguire ulteriori esecuzioni. Consulta la [query in quarantena](./monitor-queries.md#quarantined-queries) per ulteriori dettagli.

Consulta la documentazione sulle pianificazioni delle query per scoprire come [creare pianificazioni di query nell’interfaccia utente](./query-schedules.md). In alternativa, per scoprire come aggiungere pianificazioni utilizzando l’API, leggi [guida dell’endpoint &quot;scheduled queries&quot;](../api/scheduled-queries.md).

Tutte le query pianificate vengono aggiunte all’elenco in [!UICONTROL Query pianificate] scheda. Da tale area di lavoro è possibile monitorare lo stato di tutti i processi di query pianificati tramite l’interfaccia utente. Il giorno [!UICONTROL Query pianificate] , puoi trovare informazioni importanti sull’esecuzione della query e abbonarti agli avvisi. Le informazioni disponibili includono lo stato, i dettagli della pianificazione e i messaggi/codici di errore in caso di esecuzione non riuscita. Consulta la [Monitorare il documento delle query pianificate](./monitor-queries.md) per ulteriori informazioni.


### Come trovare le query precedenti {#previous-queries}

Tutte le query eseguite da [!DNL Query Editor] vengono acquisiti nella tabella Log. È possibile utilizzare la funzionalità di ricerca in **[!UICONTROL Log]** per trovare le esecuzioni della query. Le query salvate sono elencate in **[!UICONTROL Modelli]** scheda.

Se è stata pianificata una query, il [!UICONTROL Query pianificate] fornisce una migliore visibilità tramite l’interfaccia utente per tali processi di query. Consulta la [documentazione sul monitoraggio delle query](./monitor-queries.md) per ulteriori informazioni.

>[!NOTE]
>
>Le query non eseguite non vengono salvate dal registro. Affinché la query sia disponibile in [!DNL Query Service], deve essere eseguito o salvato in [!DNL Query Editor].

## Esecuzione di query tramite Editor query {#executing-queries}

Per eseguire una query in [!DNL Query Editor], è possibile immettere le istruzioni SQL nell&#39;editor o caricare una query precedente dal **[!UICONTROL Log]** o **[!UICONTROL Modelli]** e seleziona **Play**. Lo stato dell’esecuzione della query viene visualizzato nel **[!UICONTROL Console]** e i dati di output sono visualizzati nella scheda **[!UICONTROL Risultati]** scheda.

### Console {#console}

La console fornisce informazioni sullo stato e sul funzionamento di [!DNL Query Service]. Nella console viene visualizzato lo stato della connessione a [!DNL Query Service], le operazioni di query in esecuzione ed eventuali messaggi di errore derivanti da tali query.

![Scheda Console della console dell’editor delle query.](../images/ui/query-editor/console.png)

>[!NOTE]
>
>La console mostra solo gli errori derivanti dall’esecuzione di una query. Non mostra gli errori di convalida della query che si verificano prima dell’esecuzione di una query.

### Risultati della query {#query-results}

Al termine di una query, i risultati vengono visualizzati nella **[!UICONTROL Risultati]** accanto alla scheda **[!UICONTROL Console]** scheda. Questa vista mostra l’output tabulare della query, visualizzando tra 50 e 500 righe di risultati a seconda della scelta [conteggio dei risultati](#result-count). Questa vista consente di verificare che la query produca l’output previsto. Per generare un set di dati con la query, rimuovi i limiti sulle righe restituite ed esegui la query con `CREATE TABLE tablename AS SELECT` per generare un set di dati con l’output. Consulta la [esercitazione sulla generazione di set di dati](./create-datasets.md) per istruzioni su come generare un set di dati dai risultati della query in [!DNL Query Editor].

![La scheda Risultati della console Editor query che visualizza i risultati di un’esecuzione di query.](../images/ui/query-editor/query-results.png)

## Casi d’uso {#use-cases}

Query Service offre soluzioni per una varietà di casi d’uso in diversi settori e scenari aziendali. Questi esempi pratici dimostrano la flessibilità e l&#39;impatto del servizio nel soddisfare le diverse esigenze. A [scopri in che modo Query Service può apportare valore alle tue esigenze aziendali specifiche](../use-cases/overview.md), esplora la raccolta completa dei documenti dei casi d’uso. Scopri come utilizzare Query Service per fornire informazioni approfondite e soluzioni per migliorare l’efficienza operativa e il successo aziendale.

## Eseguire query con [!DNL Query Service] video tutorial {#query-tutorial-video}

Il video seguente illustra come eseguire query nell’interfaccia di Adobe Experience Platform e in un client PSQL. Il video illustra inoltre l’utilizzo di singole proprietà in un oggetto XDM, di funzioni definite dall’Adobe e di query CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Passaggi successivi

Ora che sai quali funzioni sono disponibili in [!DNL Query Editor] e come esplorare l’applicazione, puoi iniziare a creare query personalizzate direttamente in [!DNL Platform]. Per ulteriori informazioni sull’esecuzione di query SQL sui set di dati in [!DNL Data Lake], consulta la guida [esecuzione di query](../best-practices/writing-queries.md).
