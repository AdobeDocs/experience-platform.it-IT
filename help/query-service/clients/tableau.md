---
keywords: Experience Platform;home;argomenti popolari;tableau;Tableau;servizio query;servizio query;connessione al servizio query;
solution: Experience Platform
title: Connettere Tableau a Query Service
topic-legacy: connect
description: Questo documento descrive i passaggi necessari per la connessione di Tableau con Adobe Experience Platform Query Service.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 0c20b19c4c34b29c46964d5d87a8646c61055b06
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 2%

---

# Connetti [!DNL Tableau] al servizio query

Questo documento descrive i passaggi per la connessione di Tableau con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL Tableau] e conoscono bene come navigare nella relativa interfaccia. Ulteriori informazioni [!DNL Tableau] si trova nella [ufficiale [!DNL Tableau] documentazione](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Connessione [!DNL Tableau] a [!DNL Query Service], apri [!DNL Tableau]e nella **[!DNL To a Server]** selezione della sezione **[!DNL More]** seguito da **[!DNL PostgreSQL]**

![](../images/clients/tableau/open-connection.png)

È ora possibile immettere i valori per la connessione con Adobe Experience Platform. Per ulteriori informazioni su come trovare il nome del database, l&#39;host, la porta e le credenziali di accesso, leggere il [guida alle credenziali](../ui/credentials.md). Per trovare le tue credenziali, accedi a [!DNL Platform], quindi seleziona **[!UICONTROL Query]**, seguita da **[!UICONTROL Credenziali]**.

Verifica di aver selezionato il **[!UICONTROL SSL richiesto]** prima di provare a connettersi.

>[!IMPORTANT]
>
>Consulta la sezione [[!DNL Query Service] Documentazione SSL](./ssl-modes.md) per informazioni sul supporto SSL per le connessioni di terze parti a Adobe Experience Platform Query Service e su come connettersi utilizzando `verify-full` Modalità SSL.

![](../images/clients/tableau/sign-in.png)

>[!IMPORTANT]
>
>Le strutture di dati nidificate negli strumenti BI di terze parti possono essere appiattite per migliorarne l’usabilità e ridurre il carico di lavoro necessario per recuperare, analizzare, trasformare e segnalare i dati. Consulta la documentazione sul[`FLATTEN` caratteristica](../best-practices/flatten-nested-data.md) per istruzioni su come attivare questa impostazione durante la connessione a un database.

Dopo aver compilato tutte le credenziali, seleziona **[!DNL Sign In]** per continuare.

Ora ti sei connesso a Adobe Experience Platform con un elenco delle tabelle visualizzato sul lato.

![](../images/clients/tableau/connected.png)

## Passaggi successivi

Ora che ti sei connesso [!DNL Query Service], puoi utilizzare [!DNL Tableau] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire le query, leggere la guida in [query in esecuzione](../best-practices/writing-queries.md).
