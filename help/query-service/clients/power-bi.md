---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;Power BI;power bi;connessione al servizio query;
solution: Experience Platform
title: Connetti Power BI a Query Service
description: Questo documento descrive i passaggi necessari per la connessione di Power BI con Adobe Experience Platform Query Service.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 1af89160cbf5b689396921869fec6c30a5bcfff0
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 1%

---

# Connetti [!DNL Power BI] al servizio query

Questo documento descrive i passaggi per la connessione [!DNL Power BI] Desktop con Adobe Experience Platform Query Service.

## Introduzione

Questa guida richiede l’accesso a [!DNL Power BI] app desktop e scopri come navigare nella relativa interfaccia. Per scaricare [!DNL Power BI] Desktop o per ulteriori informazioni, consulta [ufficiale [!DNL Power BI] documentazione](https://docs.microsoft.com/it-IT/power-bi/).

>[!IMPORTANT]
>
> La [!DNL Power BI] applicazione desktop **only** disponibile su dispositivi Windows.

Acquisizione delle credenziali necessarie per la connessione [!DNL Power BI] ad Experience Platform, devi disporre dell’accesso all’area di lavoro Query nell’interfaccia utente di Platform. Se al momento non disponi dell’accesso all’area di lavoro query, contatta l’amministratore dell’organizzazione.

Dopo l&#39;installazione [!DNL Power BI], sarà necessario installare `Npgsql`, un pacchetto di driver .NET per PostgreSQL. Ulteriori informazioni su Npgsql sono disponibili nella sezione [Documentazione di Npgsql](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>È necessario scaricare v4.0.10 o versioni precedenti, in quanto le versioni più recenti generano errori.

Sotto &quot;[!DNL Npgsql GAC Installation]&quot; nella schermata di configurazione personalizzata, seleziona **[!DNL Will be installed on local hard drive]**.

Per verificare che Npgsql sia stato installato correttamente, riavviare il computer prima di procedere ai passaggi successivi.

## Connetti [!DNL Power BI] al servizio query {#connect-power-bi}

Connessione [!DNL Power BI] al servizio query, apri [!DNL Power BI] e seleziona **[!DNL Get Data]** nella barra multifunzione del menu principale. Quindi, immetti &quot;[!DNL PostgreSQL]&quot; nella barra di ricerca per limitare l’elenco delle origini dati. Dai risultati visualizzati, seleziona **[!DNL PostgreSQL database]**, seguita da **[!DNL Connect]**.

La [!DNL PostgreSQL] viene visualizzata la finestra di dialogo del database che richiede valori per il server e il database. Istruzioni aggiuntive su come [connettersi a un database PostgreSQL da Power Query Desktop](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop) può essere trovato nel [!DNL PowerBI] documentazione.

Questi valori richiesti vengono ricavati dalle tue credenziali Adobe Experience Platform. Per trovare le tue credenziali, accedi all’interfaccia utente di Platform e seleziona **[!UICONTROL Query]** dalla navigazione a sinistra, seguita da **[!UICONTROL Credenziali]**. Per ulteriori informazioni su come trovare il nome del database, l&#39;host, la porta e le credenziali di accesso, leggere il [guida alle credenziali](../ui/credentials.md).

![Area di lavoro Query di Experience Platform con la scheda Credenziali e credenziali in scadenza evidenziate.](../images/clients/power-bi/query-service-credentials-page.png)

In **[!DNL Server]** campo [!DNL PostgreSQL database] immettere il valore dell&#39;host trovato nel servizio query [!UICONTROL Credenziali] sezione . Per la produzione, aggiungi la porta `:80` alla fine della stringa host. Ad esempio, `made-up.platform-query.adobe.io:80`.

La **[!DNL Database]** può essere &quot;all&quot; o un nome di tabella di set di dati. Ad esempio, `prod:all`.

>[!IMPORTANT]
>
>Le strutture di dati nidificate negli strumenti BI di terze parti possono essere appiattite per migliorarne l’usabilità e ridurre il carico di lavoro necessario per recuperare, analizzare, trasformare e segnalare i dati. Consulta la documentazione sul[`FLATTEN` caratteristica](../best-practices/flatten-nested-data.md) per istruzioni su come attivare questa impostazione durante la connessione a un database.

### Modalità di connessione dati {#data-connectivity-mode}

Successivamente, puoi selezionare il tuo **[!DNL Data Connectivity mode]**. In [!DNL PostgreSQL database] finestra di dialogo, seleziona **[!DNL Import]** seguito da **[!DNL OK]** per visualizzare un elenco di tutte le tabelle disponibili oppure selezionare **[!DNL DirectQuery]** per eseguire query direttamente sull’origine dati senza importare o copiare i dati direttamente in [!DNL Power BI].

Per ulteriori informazioni sulle **[!DNL Import]** in modalità, leggere la sezione [importazione di una tabella](#import). Per ulteriori informazioni **[!DNL DirectQuery]** in modalità, leggere la sezione [eseguire query su un set di dati senza importare dati](#direct-query).

Seleziona **[!DNL OK]** dopo aver confermato i dettagli del database.

### Autenticazione {#authentication}

Dopo aver confermato la modalità di connettività dei dati, viene visualizzato un messaggio per richiedere il nome utente, la password e le impostazioni dell’applicazione. Il nome utente in questo caso è il tuo ID organizzazione e la password è il tuo token di autenticazione. Entrambi sono disponibili nella pagina delle credenziali del servizio query.

Inserisci questi dettagli, quindi seleziona **[!DNL Connect]** per passare al passaggio successivo.

## Importare una tabella {#import}

Selezionando la **[!DNL Import]** [!DNL Data Connectivity mode], viene importato il set di dati completo che consente di utilizzare le tabelle e le colonne selezionate all’interno di [!DNL Power BI] l&#39;applicazione desktop così com&#39;è.

>[!IMPORTANT]
>
>Per visualizzare le modifiche ai dati che si sono verificate dopo l’importazione iniziale, devi aggiornare i dati all’interno di [!DNL Power BI] importando nuovamente il set di dati completo.

Per importare una tabella, immettere i dettagli del server e del database [come descritto sopra](#connect-power-bi) e seleziona la **[!DNL Import]** [!DNL Data Connectivity mode], seguita da **[!DNL OK]**. La [!DNL Navigator] viene visualizzata una finestra di dialogo in cui viene visualizzato un elenco di tutte le tabelle disponibili. Selezionare la tabella da visualizzare in anteprima, seguita da **[!DNL Load]** per inserire il set di dati in Power BI. La tabella viene ora importata in [!DNL Power BI].

[Informazioni generali sulla connessione ai dati nel desktop PowerBi](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data) l&#39;app è disponibile nella documentazione ufficiale.

### Importa tabelle utilizzando SQL personalizzato

[!DNL Power BI] e altri strumenti di terze parti come [!DNL Tableau] attualmente non consentono agli utenti di importare oggetti nidificati, ad esempio oggetti XDM in Platform. Per questo motivo, [!DNL Power BI] consente di utilizzare SQL personalizzato per accedere a questi campi nidificati e creare una visualizzazione appiattita dei dati. [!DNL Power BI] carica quindi questa visualizzazione appiattita dei dati precedentemente nidificati come una tabella normale.

Da [!DNL PostgreSQL database] finestra di dialogo, seleziona **[!DNL Advanced options]** per immettere una query SQL personalizzata nel **[!DNL SQL statement]** sezione . Questa query personalizzata deve essere utilizzata per appiattire le coppie nome-valore JSON in un formato tabella. La documentazione ufficiale fornisce anche informazioni su come [collegare PowerBI utilizzando un&#39;istruzione SQL nelle opzioni avanzate](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-using-advanced-options).

Dopo aver inserito la query personalizzata, seleziona **[!DNL OK]** per continuare con la connessione al database. Consulta la sezione [autenticazione](#authentication) sezione precedente per informazioni sulla connessione di un database da questa parte del flusso di lavoro.

Una volta completata l’autenticazione, viene visualizzata un’anteprima dei dati appiattiti nel [!DNL Power BI] Dashboard desktop come tabella. Il nome del server e del database è elencato nella parte superiore della finestra di dialogo. Seleziona **[!DNL Load]** per completare il processo di importazione.

Le visualizzazioni sono ora disponibili per la modifica e l’esportazione dal [!DNL Power BI] App desktop.

## Query del set di dati senza importare dati {#direct-query}

La **[!DNL DirectQuery]** [!DNL Data Connectivity mode] esegue direttamente la query dell&#39;origine dati senza importare o copiare i dati in [!DNL Power BI] Desktop. Utilizzando questa modalità di connessione, puoi aggiornare tutte le visualizzazioni con dati correnti tramite l’interfaccia utente. Tuttavia, il tempo necessario per produrre o aggiornare la visualizzazione varia a seconda delle prestazioni dell’origine dati sottostante.

Ulteriori informazioni [l&#39;uso di [!DNL DirectQuery]](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-use-directquery) nonché una discussione approfondita sulla sua [opzioni di connettività, casi d’uso e limitazioni](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-about) può essere trovato nel [!DNL PowerBI] documentazione.

Per utilizzare questo [!DNL Data Connectivity mode], seleziona **[!DNL DirectQuery]** attivare/disattivare **[!DNL Advanced options]** per immettere una query SQL personalizzata nel **[!DNL SQL statement]** sezione . Assicurati che **[!DNL Include relationship columns]** è selezionato. Una volta completata la query, seleziona **[!DNL OK]** per continuare.

Viene visualizzata un’anteprima della query. Seleziona **[!DNL Load]** per visualizzare i risultati della query.

## Passaggi successivi

Leggendo questo documento, è ora necessario comprendere come connettersi al [!DNL Power BI] App desktop e le diverse modalità di connessione dati disponibili. Per ulteriori informazioni su come scrivere ed eseguire le query, consulta [guida per l’esecuzione delle query](../best-practices/writing-queries.md).
