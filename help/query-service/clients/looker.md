---
keywords: Experience Platform;home;popular topics;Query service;query service;Looker;looker;connect to query service;
solution: Experience Platform
title: Connetti con Looker
topic: connect
description: Questo documento descrive i passaggi necessari per la connessione di Looker con Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 9fbb6b829cd9ddec30f22b0de66874be7710e465
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Connetti con [!DNL Looker]

Per collegare [!DNL Looker] con [!DNL Query Service] su Adobe Experience Platform, procedere come segue:

Dopo aver eseguito l&#39;accesso in [!DNL Looker], fare clic su **[!UICONTROL Admin]**, seguito da **[!UICONTROL Connections]**.

![](../images/clients/looker/click-admin-connections.png)

In questa pagina, fare clic su **Nuova connessione**.

![](../images/clients/looker/click-new-connection.png)

Da qui, potete compilare i dettagli per le Impostazioni di connessione.

![](../images/clients/looker/new-connection.png)

- **Nome:** il nome della connessione.
- **Dialetto:** dialetto utilizzato per il database SQL. [!DNL Query Service] use  **[!DNL PostgreSQL]**.
- **Host e porta:** l&#39;endpoint host e la relativa porta per  [!DNL Query Service].
- **Database:** il database che verrà utilizzato.
- **Nome utente e password:** le credenziali di accesso che verranno utilizzate. Il nome utente sarà in forma di `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Per ulteriori informazioni su come trovare l&#39;host e la porta, il nome del database e le credenziali di accesso, visitare la pagina delle [credenziali sulla piattaforma](https://platform.adobe.com/query/configuration). Per trovare le credenziali, accedere a [!DNL Platform], fare clic su **[!UICONTROL Queries]**, quindi su **[!UICONTROL Credentials]**.

Dopo aver inserito i dettagli di connessione, fate clic su **[!UICONTROL Test These Settings]** per verificare il corretto funzionamento delle credenziali. In caso affermativo, di seguito verrà visualizzato un messaggio in cui si informa che è possibile connettersi. Se la connessione ha esito positivo, fare clic su **[!UICONTROL Add Connection]** per creare la connessione.

![](../images/clients/looker/click-test-connection.png)

## Passaggi successivi

Ora che si è connessi con [!DNL Query Service], è possibile utilizzare [!DNL Looker] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire query, consultare la [guida alle query in esecuzione](../best-practices/writing-queries.md).