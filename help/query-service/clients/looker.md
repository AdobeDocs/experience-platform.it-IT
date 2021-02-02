---
keywords: ' Experience Platform;home;argomenti popolari;servizio query;servizio query;Looker;looker;connect to query service;'
solution: Experience Platform
title: Connetti con Looker
topic: connect
description: Questo documento descrive i passaggi necessari per la connessione di Looker con Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: bc1bbdddd75b11ac180b5e6faa391fd74e5f7e02
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# [!DNL Looker]

Questo documento descrive i passaggi per la connessione di [!DNL Looker] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che abbiate già accesso a [!DNL Looker] e che abbiate familiarità con come navigare all&#39;interfaccia. Ulteriori informazioni su [!DNL Looker] sono disponibili nella [documentazione  [!DNL Looker] ufficiale](https://docs.looker.com/).

## Connetti [!DNL Looker] con la piattaforma

Dopo aver eseguito l&#39;accesso in [!DNL Looker], selezionare **[!DNL Admin]**, seguito da **[!DNL Connections]**.

![](../images/clients/looker/click-admin-connections.png)

In questa pagina, selezionare **[!DNL New Connection]**.

![](../images/clients/looker/click-new-connection.png)

Da qui è possibile compilare i dettagli delle impostazioni di connessione.

![](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** Il nome della connessione.
- **[!DNL Dialect]:** Il dialetto utilizzato per il database SQL. [!DNL Query Service] use  **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** L&#39;endpoint host e la relativa porta per  [!DNL Query Service].
- **[!DNL Database]:** Il database che verrà utilizzato.
- **[!DNL Username and Password]:** Le credenziali di accesso che verranno utilizzate. Il nome utente sarà in forma di `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Per ulteriori informazioni su come trovare l&#39;host e la porta, il nome del database e le credenziali di accesso, visitare la pagina delle [credenziali sulla piattaforma](https://platform.adobe.com/query/configuration). Per trovare le credenziali, accedere a [!DNL Platform], quindi selezionare **[!UICONTROL Queries]**, seguito da **[!UICONTROL Credentials]**.

Dopo aver inserito i dettagli di connessione, selezionare **[!DNL Test These Settings]** per assicurarsi che le credenziali funzionino correttamente. In caso affermativo, di seguito verrà visualizzato un messaggio che indica che è possibile connettersi. Se la connessione ha esito positivo, selezionare **[!DNL Add Connection]** per creare la connessione.

![](../images/clients/looker/click-test-connection.png)

## Passaggi successivi

Ora che si è connessi con [!DNL Query Service], è possibile utilizzare [!DNL Looker] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire query, consultare la [guida alle query in esecuzione](../best-practices/writing-queries.md).