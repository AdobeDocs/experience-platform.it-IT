---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;Power BI;power bi;connessione al servizio query;
solution: Experience Platform
title: Connetti Power BI a Query Service
topic-legacy: connect
description: Questo documento descrive i passaggi necessari per la connessione di Power BI con Adobe Experience Platform Query Service.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 69f57a0e2293e438a0e5c986d888027892cc6359
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 1%

---

# Connetti Power BI a Query Service

Questo documento descrive i passaggi per la connessione di Power BI Desktop con Adobe Experience Platform Query Service.

## Introduzione

Questa guida richiede di avere già accesso all’app desktop Power BI e di avere familiarità con la modalità di navigazione all’interno della relativa interfaccia. Per scaricare Power BI Desktop o per ulteriori informazioni, consulta la [documentazione ufficiale di Power BI](https://docs.microsoft.com/it-IT/power-bi/).

>[!IMPORTANT]
>
> L&#39;applicazione desktop Power BI è **only** disponibile su dispositivi Windows.

Per acquisire le credenziali necessarie per la connessione di Power BI ad Experience Platform, è necessario disporre dell’accesso all’area di lavoro Query nell’interfaccia utente di Platform. Se al momento non disponi dell’accesso all’area di lavoro Query, contatta il tuo amministratore dell’organizzazione IMS.

Dopo aver installato Power BI, sarà necessario installare `Npgsql`, un pacchetto di driver .NET per PostgreSQL. Ulteriori informazioni su Npgsql sono disponibili nella sezione [Documentazione di Npgsql](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>È necessario scaricare v4.0.10 o versioni precedenti, in quanto le versioni più recenti generano errori.

Sotto &quot;[!DNL Npgsql GAC Installation]&quot; nella schermata di configurazione personalizzata, seleziona **[!DNL Will be installed on local hard drive]**.

Per verificare che Npgsql sia stato installato correttamente, riavviare il computer prima di procedere ai passaggi successivi.

## Connetti Power BI a Query Service {#connect-power-bi}

Per collegare Power BI a Query Service, apri Power BI e seleziona **[!DNL Get Data]** nella barra multifunzione del menu principale.

![](../images/clients/power-bi/open-power-bi.png)

Immettere &quot;PostgreSQL&quot; nella barra di ricerca per restringere l&#39;elenco delle origini dati. Sotto i risultati visualizzati, seleziona **[!DNL PostgreSQL database]**, seguita da **[!DNL Connect]**.

![](../images/clients/power-bi/get-data.png)

Viene visualizzata la finestra di dialogo del database PostgreSQl che richiede valori per il server e il database. Questi valori vengono ricavati dalle tue credenziali Adobe Experience Platform. Per trovare le tue credenziali, accedi all’interfaccia utente di Platform e seleziona **[!UICONTROL Query]** dalla navigazione a sinistra, seguita da **[!UICONTROL Credenziali]**. Per ulteriori informazioni su come trovare il nome del database, l&#39;host, la porta e le credenziali di accesso, leggere il [guida alle credenziali](../ui/credentials.md).

![Experience Platform Query Credenziali Dashboard con credenziali evidenziate.](../images/clients/power-bi/query-service-credentials-page.png)

Per **[!DNL Server]** in Power BI, immettere il valore per l&#39;host presente nella sezione Credenziali del servizio query. Per la produzione, aggiungi la porta `:80` alla fine della stringa host. Ad esempio, `made-up.platform-query.adobe.io:80`.

La **[!DNL Database]** può essere &quot;all&quot; o un nome di tabella di set di dati. Ad esempio, `prod:all`.

![Dashboard di Power BI con i campi di input del server e del database evidenziati.](../images/clients/power-bi/postgresql-database-dialog.png)

### Modalità di connessione dati

Successivamente, puoi selezionare il tuo **[!DNL Data Connectivity mode]**. Seleziona **[!DNL Import]** seguito da **[!DNL OK]** per visualizzare un elenco di tutte le tabelle disponibili oppure selezionare **[!DNL DirectQuery]** eseguire query direttamente sull’origine dati senza importare o copiare i dati direttamente in Power BI.

Per ulteriori informazioni **[!DNL Import]** in modalità, leggere la sezione [importazione di una tabella](#import). Per ulteriori informazioni **[!DNL DirectQuery]** in modalità, leggere la sezione [eseguire query su un set di dati senza importare dati](#direct-query).

Seleziona **[!DNL OK]** dopo aver confermato i dettagli del database.

![](../images/clients/power-bi/connectivity-mode.png)

### Autenticazione

Viene visualizzata una richiesta per richiedere il nome utente, la password e le impostazioni dell&#39;applicazione. Il nome utente in questo caso è il tuo ID organizzazione e la password è il tuo token di autenticazione. Entrambi sono disponibili nella pagina delle credenziali del servizio query.

Inserisci questi dettagli, quindi seleziona **[!DNL Connect]** per passare al passaggio successivo.

![](../images/clients/power-bi/import-mode.png)

## Importare una tabella {#import}

Selezionando la **[!DNL Import]** [!DNL Data Connectivity mode], viene importato il set di dati completo che consente di utilizzare le tabelle e le colonne selezionate all’interno dell’applicazione desktop Power BI così com’è.

>[!IMPORTANT]
>
>Per visualizzare le modifiche ai dati che si sono verificate dopo l’importazione iniziale, è necessario aggiornare i dati in Power BI importando nuovamente l’intero set di dati.

Per importare una tabella, immettere i dettagli del server e del database [come descritto sopra](#connect-power-bi) e seleziona la **[!DNL Import]** [!DNL Data Connectivity mode], seguita da **[!DNL OK]**. Viene visualizzata una finestra di dialogo contenente un elenco di tutte le tabelle disponibili. Selezionare la tabella da visualizzare in anteprima, seguita da **[!DNL Load]** per inserire il set di dati in Power BI.

![](../images/clients/power-bi/preview-table.png)

La tabella viene ora importata in Power BI.

![](../images/clients/power-bi/import-table.png)

### Importa tabelle utilizzando SQL personalizzato

Power BI e altri strumenti di terze parti come Tableau attualmente non consentono agli utenti di importare oggetti nidificati, come gli oggetti XDM in Platform. Per tenere conto di ciò, Power BI consente di utilizzare SQL personalizzato per accedere a questi campi nidificati e creare una visualizzazione appiattita dei dati. Power BI carica quindi questa visualizzazione appiattita dei dati precedentemente nidificati come una tabella normale.

Dal repository del database PostgreSQL, selezionare **[!DNL Advanced options]** per immettere una query SQL personalizzata nel **[!DNL SQL statement]** sezione . Questa query personalizzata deve essere utilizzata per appiattire le coppie nome-valore JSON in un formato tabella.

![Opzioni avanzate della modalità di connettività dei dati per creare un&#39;istruzione SQL personalizzata.](../images/clients/power-bi/custom-sql-statement.png)

Dopo aver inserito la query personalizzata, seleziona **[!DNL OK]** per continuare con la connessione al database. Consulta la sezione [autenticazione](#authentication) sezione precedente per informazioni sulla connessione di un database da questa parte del flusso di lavoro.

Una volta completata l&#39;autenticazione, viene visualizzata un&#39;anteprima dei dati appiattiti nel dashboard Power BI Desktop come tabella. Il nome del server e del database è elencato nella parte superiore della finestra di dialogo. Seleziona **[!DNL Load]** per completare il processo di importazione.

![Tabella importata appiattita nel dashboard Power BI.](../images/clients/power-bi/imported-table-preview.png)

Le visualizzazioni sono ora disponibili per la modifica e l’esportazione dall’app Power BI Desktop.

## Query del set di dati senza importare dati {#direct-query}

La **[!DNL DirectQuery]** [!DNL Data Connectivity mode] esegue la query dell&#39;origine dati direttamente senza importare o copiare i dati in Power BI Desktop. Utilizzando questa modalità di connessione, puoi aggiornare tutte le visualizzazioni con dati correnti tramite l’interfaccia utente. Tuttavia, il tempo necessario per produrre o aggiornare la visualizzazione varia a seconda delle prestazioni dell’origine dati sottostante.

Per utilizzare questo [!DNL Data Connectivity mode], seleziona **[!DNL DirectQuery]** attivare/disattivare **[!DNL Advanced options]** per immettere una query SQL personalizzata nel **[!DNL SQL statement]** sezione . Assicurati che **[!DNL Include relationship columns]** è selezionato. Una volta completata la query, seleziona **[!DNL OK]** per continuare.

![](../images/clients/power-bi/direct-query-mode.png)

Viene visualizzata un’anteprima della query. Seleziona **[!DNL Load]** per visualizzare i risultati della query.

![](../images/clients/power-bi/preview-direct-query.png)

## Passaggi successivi

Leggendo questo documento, è ora necessario comprendere come connettersi all&#39;app Power BI Desktop e alle diverse modalità di connessione dati disponibili. Per ulteriori informazioni su come scrivere ed eseguire le query, consulta [guida per l’esecuzione delle query](../best-practices/writing-queries.md).
