---
keywords: Experience Platform;home;argomenti popolari;tableau;Tableau;servizio query;servizio query;connessione al servizio query;
solution: Experience Platform
title: Connettere Tableau a Query Service
topic-legacy: connect
description: Questo documento descrive i passaggi necessari per la connessione di Tableau con Adobe Experience Platform Query Service.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: ad3e1b0de6dd3b82cc82f0dc3d0f36b12cd3899e
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 3%

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

Dopo aver compilato tutte le credenziali, seleziona **[!DNL Sign In]** per continuare.

![](../images/clients/tableau/sign-in.png)

Ora ti sei connesso a Adobe Experience Platform con un elenco delle tabelle visualizzato sul lato.

![](../images/clients/tableau/connected.png)

## Passaggi successivi

Ora che ti sei connesso [!DNL Query Service], puoi utilizzare [!DNL Tableau] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire le query, leggere la guida in [query in esecuzione](../best-practices/writing-queries.md).
