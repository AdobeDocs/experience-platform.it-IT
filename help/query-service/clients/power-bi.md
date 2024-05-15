---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;Power BI;power bi;connettersi al servizio query;
solution: Experience Platform
title: Connetti Power BI a Query Service
description: Questo documento illustra i passaggi necessari per la connessione di Power BI con Adobe Experience Platform Query Service.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 26f0725f0f239707bd719ed46929648f8d557155
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 0%

---

# Connetti [!DNL Power BI] a Query Service

Questo documento descrive i passaggi per la connessione [!DNL Power BI] Desktop con Adobe Experience Platform Query Service.

## Introduzione

Questa guida richiede che tu abbia già accesso al [!DNL Power BI] e hanno familiarità con le modalità di navigazione nell&#39;interfaccia. Per scaricare [!DNL Power BI] Desktop o per ulteriori informazioni, vedere [ufficiale [!DNL Power BI] documentazione](https://docs.microsoft.com/en-us/power-bi/).

>[!IMPORTANT]
>
> Il [!DNL Power BI] applicazione desktop è **solo** disponibile sui dispositivi Windows.

Per acquisire le credenziali necessarie per la connessione [!DNL Power BI] ad Experience Platform, devi avere accesso all’area di lavoro Query nell’interfaccia utente di Platform. Se al momento non disponi dell’accesso all’area di lavoro query, contatta l’amministratore dell’organizzazione.

Dopo l’installazione [!DNL Power BI], sarà necessario installare `Npgsql`, pacchetto driver .NET per PostgreSQL. Ulteriori informazioni su Npgsql sono disponibili nella sezione [Documentazione di Npgsql](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>È necessario scaricare la versione 4.0.10 o successiva, in quanto le versioni più recenti generano errori.

In &quot;[!DNL Npgsql GAC Installation]&quot; nella schermata di impostazione personalizzata, selezionare **[!DNL Will be installed on local hard drive]**.

Per verificare che Npgsql sia stato installato correttamente, riavviare il computer prima di procedere con i passaggi successivi.

## Connetti [!DNL Power BI] a Query Service {#connect-power-bi}

Per connettersi [!DNL Power BI] in Query Service, apri [!DNL Power BI] e seleziona **[!DNL Get Data]** sulla barra multifunzione del menu superiore. Quindi, immetti &quot;[!DNL PostgreSQL]&quot; nella barra di ricerca per restringere l’elenco delle origini dati. Dai risultati visualizzati, selezionare **[!DNL PostgreSQL database]**, seguito da **[!DNL Connect]**.

Il [!DNL PostgreSQL] viene visualizzata la finestra di dialogo database, in cui vengono richiesti i valori per il server e il database. Ulteriori istruzioni su come [connettersi a un database PostgreSQL da Power Query Desktop](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop) può essere trovato nella [!DNL PowerBI] documentazione.

Questi valori richiesti vengono ricavati dalle credenziali Adobe Experience Platform. Per trovare le credenziali, accedi all’interfaccia utente di Platform e seleziona **[!UICONTROL Query]** dal menu di navigazione a sinistra, seguito da **[!UICONTROL Credenziali]**. Per ulteriori informazioni su come trovare il nome del database, l&#39;host, la porta e le credenziali di accesso, leggere [guida alle credenziali](../ui/credentials.md).

>[!IMPORTANT]
>
>In qualità di utente Power BI o Tableau, puoi collegare il Customer Journey Analytics agli strumenti di business intelligence dalla scheda Credenziali di Query Service. Per istruzioni su come utilizzare, consulta la documentazione sulle credenziali. [collegare gli strumenti BI al Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics).

![L’area di lavoro Query di Experience Platform con la scheda Credenziali ed evidenziate le credenziali in Scadenza.](../images/clients/power-bi/query-service-credentials-page.png)

In **[!DNL Server]** campo del [!DNL PostgreSQL database] , immetti il valore per l’host trovato in Query Service [!UICONTROL Credenziali] sezione. Per la produzione, aggiungi porta `:80` alla fine della stringa host. Ad esempio, `made-up.platform-query.adobe.io:80`.

Il **[!DNL Database]** può essere &quot;all&quot; o un nome di tabella di un set di dati. Ad esempio, `prod:all`.

>[!IMPORTANT]
>
>Le strutture di dati nidificate negli strumenti di BI di terze parti possono essere appiattite per migliorarne l’usabilità e ridurre il carico di lavoro necessario per recuperare, analizzare, trasformare e generare rapporti sui dati. Consulta la documentazione su[`FLATTEN` funzionalità](../key-concepts/flatten-nested-data.md) per istruzioni su come attivare questa impostazione durante la connessione a un database.

### Modalità di connettività dati {#data-connectivity-mode}

Quindi, puoi selezionare il **[!DNL Data Connectivity mode]**. In [!DNL PostgreSQL database] finestra di dialogo, seleziona **[!DNL Import]** seguito da **[!DNL OK]** per visualizzare un elenco di tutte le tabelle disponibili, oppure selezionare **[!DNL DirectQuery]** per eseguire query direttamente sull&#39;origine dati senza importare o copiare i dati direttamente in [!DNL Power BI].

Per ulteriori informazioni su **[!DNL Import]** , leggi la sezione relativa a [importazione di una tabella](#import). Per ulteriori informazioni su **[!DNL DirectQuery]** , leggi la sezione relativa a [esecuzione di query su un set di dati senza importare dati](#direct-query).

Seleziona **[!DNL OK]** dopo aver confermato i dettagli del database.

### Autenticazione {#authentication}

Dopo aver confermato la modalità di connettività dati, viene visualizzato un messaggio in cui viene richiesto di specificare il nome utente, la password e le impostazioni dell’applicazione. Il nome utente in questo caso è l&#39;ID organizzazione e la password è il token di autenticazione. Entrambi sono disponibili nella pagina Credenziali di Query Service.

Compila questi dettagli, quindi seleziona **[!DNL Connect]** per procedere al passaggio successivo.

## Importare una tabella {#import}

Selezionando **[!DNL Import]** [!DNL Data Connectivity mode], viene importato l’intero set di dati che ti consente di utilizzare le tabelle e le colonne selezionate all’interno del [!DNL Power BI] applicazione desktop così com&#39;è.

>[!IMPORTANT]
>
>Per visualizzare le modifiche apportate ai dati dopo l&#39;importazione iniziale, è necessario aggiornare i dati in [!DNL Power BI] importando nuovamente l’intero set di dati.

Per importare una tabella, immettere i dettagli del server e del database [come descritto in precedenza](#connect-power-bi) e seleziona la **[!DNL Import]** [!DNL Data Connectivity mode], seguito da **[!DNL OK]**. Il [!DNL Navigator] viene visualizzata una finestra di dialogo in cui viene visualizzato un elenco di tutte le tabelle disponibili. Seleziona la tabella da visualizzare in anteprima, seguita da **[!DNL Load]** per portare il set di dati in Power BI. La tabella viene ora importata in [!DNL Power BI].

[Informazioni generali sulla connessione ai dati nel desktop PowerBi](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data) si trova nella documentazione ufficiale.

### Importare tabelle utilizzando SQL personalizzato

[!DNL Power BI] e altri strumenti di terze parti come [!DNL Tableau] non consentire attualmente agli utenti di importare oggetti nidificati, ad esempio oggetti XDM in Platform. Per rendere conto di ciò, [!DNL Power BI] consente di utilizzare codice SQL personalizzato per accedere a questi campi nidificati e creare una visualizzazione semplificata dei dati. [!DNL Power BI] quindi carica questa vista appiattita dei dati precedentemente nidificati come una normale tabella.

Dalla sezione [!DNL PostgreSQL database] finestra di dialogo, seleziona **[!DNL Advanced options]** per immettere una query SQL personalizzata in **[!DNL SQL statement]** sezione. Questa query personalizzata deve essere utilizzata per &quot;appiattire&quot; le coppie nome-valore JSON in un formato di tabella. La documentazione ufficiale fornisce anche informazioni su come [connettere Power BI utilizzando un&#39;istruzione SQL nelle opzioni avanzate](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-using-advanced-options).

Dopo aver inserito la query personalizzata, seleziona **[!DNL OK]** per continuare con la connessione al database. Consulta la [autenticazione](#authentication) per istruzioni sulla connessione di un database da questa parte del flusso di lavoro.

Una volta completata l’autenticazione, nella sezione viene visualizzata un’anteprima dei dati appiattiti. [!DNL Power BI] Dashboard desktop come tabella. Il nome del server e del database sono elencati nella parte superiore della finestra di dialogo. Seleziona **[!DNL Load]** per completare il processo di importazione.

Le visualizzazioni sono ora disponibili per la modifica e l’esportazione dal [!DNL Power BI] App desktop.

## Eseguire una query sul set di dati senza importare dati {#direct-query}

Il **[!DNL DirectQuery]** [!DNL Data Connectivity mode] esegue query direttamente sull’origine dati senza importare o copiare dati in [!DNL Power BI] Desktop. Utilizzando questa modalità di connessione, puoi aggiornare tutte le visualizzazioni con i dati correnti tramite l’interfaccia utente. Tuttavia, il tempo necessario per produrre o aggiornare la visualizzazione varia a seconda delle prestazioni dell’origine dati sottostante.

Ulteriori informazioni su [l&#39;uso di [!DNL DirectQuery]](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-use-directquery) nonché una discussione esauriente sulle sue [opzioni di connettività, casi d’uso e limitazioni](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-about) può essere trovato nella [!DNL PowerBI] documentazione.

Per utilizzare questo [!DNL Data Connectivity mode], seleziona la **[!DNL DirectQuery]** attiva e disattiva **[!DNL Advanced options]** per immettere una query SQL personalizzata in **[!DNL SQL statement]** sezione. Assicurati che **[!DNL Include relationship columns]** è selezionato. Dopo aver completato la query, seleziona **[!DNL OK]** per continuare.

Viene visualizzata un’anteprima della query. Seleziona **[!DNL Load]** per visualizzare i risultati della query.

## Passaggi successivi

Una volta letto questo documento, sarai in grado di capire come connetterti al [!DNL Power BI] L&#39;app desktop e le diverse modalità di connessione dati disponibili. Per ulteriori informazioni su come scrivere ed eseguire query, fare riferimento a [linee guida per l’esecuzione delle query](../best-practices/writing-queries.md).
