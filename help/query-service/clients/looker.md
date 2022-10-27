---
keywords: Experience Platform;home;argomenti popolari;Query service;query service;Looker;looker;connect to query service;
solution: Experience Platform
title: Connetti Looker al servizio query
topic-legacy: connect
description: Questo documento descrive i passaggi necessari per la connessione di Looker con Adobe Experience Platform Query Service.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Connetti [!DNL Looker] al servizio query

Questo documento descrive i passaggi per la connessione [!DNL Looker] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL Looker] e conoscono bene come navigare nella relativa interfaccia. Ulteriori informazioni [!DNL Looker] si trova nella [ufficiale [!DNL Looker] documentazione](https://docs.looker.com/).

Dopo aver effettuato l’accesso a [!DNL Looker], seleziona **[!DNL Admin]**, seguita da **[!DNL Connections]**.

![La [!DNL Looker] dashboard con connessioni evidenziate dal menu a discesa Amministrazione.](../images/clients/looker/click-admin-connections.png)

In questa pagina, seleziona **[!DNL New Connection]**.

![Area di lavoro Connessioni con nuova connessione evidenziata.](../images/clients/looker/click-new-connection.png)

Da qui è possibile compilare i dettagli delle impostazioni di connessione.

![Pagina delle impostazioni delle connessioni per una nuova connessione.](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** Nome della connessione.
- **[!DNL Dialect]:** Il dialetto utilizzato per il database SQL. [!DNL Query Service] utilizza **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** L&#39;endpoint host e la relativa porta per [!DNL Query Service].
- **[!DNL Database]:** Database che verrà utilizzato.
- **[!DNL Username and Password]:** Le credenziali di accesso che verranno utilizzate. Il nome utente sarà sotto forma di `ORG_ID@AdobeOrg`.
- **SSL**: Abilita SSL per garantire una connessione sicura attraverso la rete.

>[!IMPORTANT]
>
>Consulta la sezione [[!DNL Query Service] Documentazione SSL](./ssl-modes.md) per informazioni sul supporto SSL per le connessioni di terze parti a Adobe Experience Platform Query Service e su come connettersi utilizzando `verify-full` Modalità SSL.

Per ulteriori informazioni su come trovare l&#39;host e la porta, il nome del database e le credenziali di accesso, leggere il [guida alle credenziali](../ui/credentials.md). Per trovare le tue credenziali, accedi a [!DNL Platform], quindi seleziona **[!UICONTROL Query]**, seguita da **[!UICONTROL Credenziali]**.

Dopo aver inserito i dettagli della connessione, seleziona **[!DNL Test These Settings]** per garantire il corretto funzionamento delle credenziali. In caso affermativo, di seguito verrà visualizzato un messaggio che indica che è possibile connettersi. Se la connessione ha esito positivo, seleziona **[!DNL Add Connection]** per creare la connessione.

![È evidenziata la pagina delle impostazioni Connessioni per una nuova connessione con il test di queste impostazioni.](../images/clients/looker/click-test-connection.png)

## Passaggi successivi

Ora che ti sei connesso [!DNL Query Service], puoi utilizzare [!DNL Looker] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire le query, leggere il [guida all’esecuzione delle query](../best-practices/writing-queries.md).
