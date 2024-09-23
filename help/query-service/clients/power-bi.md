---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;Power BI;power bi;connettersi al servizio query;
solution: Experience Platform
title: Connetti Power BI a Query Service
description: Questo documento illustra i passaggi necessari per la connessione di Power BI con Adobe Experience Platform Query Service.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 2b76b99d1e22d75faf8d758edd6cf08acdec7c21
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 0%

---

# Connetti [!DNL Power BI] a Query Service

Questo documento descrive i passaggi per la connessione di [!DNL Power BI] Desktop a Adobe Experience Platform Query Service.

## Introduzione

Questa guida richiede che tu abbia già accesso all&#39;app desktop [!DNL Power BI] e che tu abbia familiarità con le modalità di navigazione nella relativa interfaccia. Per scaricare il desktop [!DNL Power BI] o per ulteriori informazioni, consulta la [documentazione [!DNL Power BI] ufficiale](https://docs.microsoft.com/en-us/power-bi/).

>[!IMPORTANT]
>
> L&#39;applicazione desktop [!DNL Power BI] è **only** disponibile sui dispositivi Windows.

Per acquisire le credenziali necessarie per la connessione di [!DNL Power BI] a Experience Platform, è necessario avere accesso all&#39;area di lavoro Query nell&#39;interfaccia utente di Platform. Se al momento non disponi dell’accesso all’area di lavoro query, contatta l’amministratore dell’organizzazione.

## Connetti [!DNL Power BI] a Query Service {#connect-power-bi}

Per connettere [!DNL Power BI] a Query Service, apri [!DNL Power BI] e seleziona **[!DNL Get Data]** nella barra multifunzione del menu superiore. Quindi, immettere &quot;[!DNL PostgreSQL]&quot; nella barra di ricerca per limitare l&#39;elenco delle origini dati. Dai risultati visualizzati, selezionare **[!DNL PostgreSQL database]**, seguito da **[!DNL Connect]**.

Viene visualizzata la finestra di dialogo del database [!DNL PostgreSQL] in cui vengono richiesti i valori per il server e il database. Ulteriori istruzioni su come [connettersi a un database PostgreSQL da Power Query Desktop](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop) sono disponibili nella documentazione ufficiale di [!DNL PowerBI].

Questi valori richiesti vengono ricavati dalle credenziali Adobe Experience Platform. Per trovare le credenziali, accedi all&#39;interfaccia utente di Platform e seleziona **[!UICONTROL Query]** dal menu di navigazione a sinistra, seguito da **[!UICONTROL Credenziali]**. Per ulteriori informazioni su come trovare il nome del database, l&#39;host, la porta e le credenziali di accesso, leggere la [guida delle credenziali](../ui/credentials.md).

>[!IMPORTANT]
>
>In qualità di utente Power BI o Tableau, puoi collegare il Customer Journey Analytics agli strumenti di business intelligence dalla scheda Credenziali di Query Service. Consulta la documentazione sulle credenziali per istruzioni su come [collegare gli strumenti di business intelligence al Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics).

![L&#39;area di lavoro Query di Experience Platform con la scheda Credenziali e le credenziali in scadenza evidenziate.](../images/clients/power-bi/query-service-credentials-page.png)

Nel campo **[!DNL Server]** della finestra di dialogo [!DNL PostgreSQL database], immettere il valore per l&#39;host trovato nella sezione [!UICONTROL Credenziali] del servizio query. Per la produzione, aggiungere la porta `:80` alla fine della stringa host. Ad esempio, `made-up.platform-query.adobe.io:80`.

Il campo **[!DNL Database]** può essere &quot;all&quot; o un nome di tabella di set di dati. Ad esempio, `prod:all`.

>[!IMPORTANT]
>
>Le strutture di dati nidificate negli strumenti di BI di terze parti possono essere appiattite per migliorarne l’usabilità e ridurre il carico di lavoro necessario per recuperare, analizzare, trasformare e generare rapporti sui dati. Per istruzioni su come attivare questa impostazione durante la connessione a un database, vedere la documentazione della funzionalità [`FLATTEN`](../key-concepts/flatten-nested-data.md).

### Modalità di connettività dati {#data-connectivity-mode}

Quindi, puoi selezionare **[!DNL Data Connectivity mode]**. Nella finestra di dialogo [!DNL PostgreSQL database], selezionare **[!DNL Import]** seguito da **[!DNL OK]** per visualizzare un elenco di tutte le tabelle disponibili oppure selezionare **[!DNL DirectQuery]** per eseguire direttamente query sull&#39;origine dati senza importare o copiare dati direttamente in [!DNL Power BI].

Per ulteriori informazioni sulla modalità **[!DNL Import]**, leggere la sezione su [importazione di una tabella](#import). Per ulteriori informazioni sulla modalità **[!DNL DirectQuery]**, leggere la sezione relativa a [query su un set di dati senza importazione di dati](#direct-query).

Seleziona **[!DNL OK]** dopo aver confermato i dettagli del database.

### Autenticazione {#authentication}

Dopo aver confermato la modalità di connettività dati, viene visualizzato un messaggio in cui viene richiesto di specificare il nome utente, la password e le impostazioni dell’applicazione. Il nome utente in questo caso è l&#39;ID organizzazione e la password è il token di autenticazione. Entrambi sono disponibili nella pagina Credenziali di Query Service.

Compila questi dettagli, quindi seleziona **[!DNL Connect]** per continuare con il passaggio successivo.

## Importare una tabella {#import}

Selezionando **[!DNL Import]** [!DNL Data Connectivity mode], viene importato l&#39;intero set di dati che consente di utilizzare le tabelle e le colonne selezionate nell&#39;applicazione desktop [!DNL Power BI] così come sono.

>[!IMPORTANT]
>
>Per visualizzare le modifiche apportate ai dati dopo l&#39;importazione iniziale, è necessario aggiornare i dati in [!DNL Power BI] importando nuovamente l&#39;intero set di dati.

Per importare una tabella, immettere i dettagli del server e del database [come descritto in precedenza](#connect-power-bi) e selezionare **[!DNL Import]** [!DNL Data Connectivity mode], seguito da **[!DNL OK]**. Viene visualizzata la finestra di dialogo [!DNL Navigator] in cui viene visualizzato un elenco di tutte le tabelle disponibili. Selezionare la tabella da visualizzare in anteprima, seguita da **[!DNL Load]** per portare il set di dati in Power BI. La tabella è ora importata in [!DNL Power BI].

[Informazioni generali sulla connessione ai dati nell&#39;app PowerBi desktop](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data) sono disponibili nella documentazione ufficiale.

### Importare tabelle utilizzando SQL personalizzato

[!DNL Power BI] e altri strumenti di terze parti come [!DNL Tableau] non consentono attualmente agli utenti di importare oggetti nidificati, ad esempio oggetti XDM in Platform. Per tenere conto di ciò, [!DNL Power BI] consente di utilizzare SQL personalizzato per accedere a questi campi nidificati e creare una visualizzazione semplificata dei dati. [!DNL Power BI] carica quindi questa vista appiattita dei dati precedentemente nidificati come una normale tabella.

Dalla finestra di dialogo [!DNL PostgreSQL database], selezionare **[!DNL Advanced options]** per immettere una query SQL personalizzata nella sezione **[!DNL SQL statement]**. Questa query personalizzata deve essere utilizzata per &quot;appiattire&quot; le coppie nome-valore JSON in un formato di tabella. La documentazione ufficiale fornisce inoltre informazioni su come [connettere PowerBI utilizzando un&#39;istruzione SQL nelle opzioni avanzate](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-using-advanced-options).

Dopo aver immesso la query personalizzata, selezionare **[!DNL OK]** per continuare con la connessione al database. Consulta la sezione [authentication](#authentication) qui sopra per istruzioni sulla connessione di un database da questa parte del flusso di lavoro.

Al termine dell&#39;autenticazione, nel dashboard desktop [!DNL Power BI] verrà visualizzata un&#39;anteprima dei dati appiattiti sotto forma di tabella. Il nome del server e del database sono elencati nella parte superiore della finestra di dialogo. Selezionare **[!DNL Load]** per completare il processo di importazione.

Le visualizzazioni sono ora disponibili per la modifica e l&#39;esportazione dall&#39;app desktop [!DNL Power BI].

## Eseguire una query sul set di dati senza importare dati {#direct-query}

**[!DNL DirectQuery]** [!DNL Data Connectivity mode] esegue query direttamente sull&#39;origine dati senza importare o copiare dati nel desktop [!DNL Power BI]. Utilizzando questa modalità di connessione, puoi aggiornare tutte le visualizzazioni con i dati correnti tramite l’interfaccia utente. Tuttavia, il tempo necessario per produrre o aggiornare la visualizzazione varia a seconda delle prestazioni dell’origine dati sottostante.

Ulteriori informazioni sull&#39;[utilizzo di [!DNL DirectQuery]](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-use-directquery) e una discussione completa sulle [opzioni di connettività, sui casi d&#39;uso e sulle limitazioni](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-about) sono disponibili nella documentazione ufficiale di [!DNL PowerBI].

Per utilizzare [!DNL Data Connectivity mode], selezionare l&#39;interruttore **[!DNL DirectQuery]** e quindi **[!DNL Advanced options]** per immettere una query SQL personalizzata nella sezione **[!DNL SQL statement]**. Assicurarsi che **[!DNL Include relationship columns]** sia selezionato. Dopo aver completato la query, selezionare **[!DNL OK]** per continuare.

Viene visualizzata un’anteprima della query. Selezionare **[!DNL Load]** per visualizzare i risultati della query.

## Passaggi successivi

Dopo aver letto questo documento, sarai in grado di capire come connettersi all&#39;app desktop [!DNL Power BI] e alle diverse modalità di connessione dati disponibili. Per ulteriori informazioni su come scrivere ed eseguire query, consultare la [guida per l&#39;esecuzione delle query](../best-practices/writing-queries.md).
