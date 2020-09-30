---
keywords: Experience Platform;home;popular topics;Query service;query service;Looker;looker;connect to query service;
solution: Experience Platform
title: Connetti con Looker
topic: connect
description: Questo documento descrive i passaggi necessari per la connessione di Looker con Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Connetti con [!DNL Looker]

Per connettersi [!DNL Looker] con [!DNL Query Service] Adobe Experience Platform, attenetevi alla procedura seguente:

Dopo aver effettuato l’accesso [!DNL Looker], fate clic su **[!UICONTROL Admin]**, quindi su **[!UICONTROL Connections]**.

![](../images/clients/looker/click-admin-connections.png)

In questa pagina, fate clic su **Nuova connessione**.

![](../images/clients/looker/click-new-connection.png)

Da qui, potete compilare i dettagli per le Impostazioni di connessione.

![](../images/clients/looker/new-connection.png)

- **Nome:** Nome della connessione.
- **Dialetto:** Il dialetto utilizzato per il database SQL. [!DNL Query Service] use **[!DNL PostgreSQL]**.
- **Host e porta:** L&#39;endpoint host e la relativa porta per [!DNL Query Service].
- **Database:** Il database che verrà utilizzato.
- **Nome utente e password:** Le credenziali di accesso che verranno utilizzate. Il nome utente sarà in forma di `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Per ulteriori informazioni su come trovare l&#39;host e la porta, il nome del database e le credenziali di accesso, visitare la pagina delle [credenziali sulla piattaforma](https://platform.adobe.com/query/configuration). Per trovare le credenziali, accedi a [!DNL Platform], fai clic su **[!UICONTROL Queries]**, quindi fai clic su **[!UICONTROL Credentials]**.

Dopo aver inserito i dettagli di connessione, fate clic su **[!UICONTROL Test These Settings]** per verificare che le credenziali funzionino correttamente. In caso affermativo, di seguito verrà visualizzato un messaggio in cui si informa che è possibile connettersi. Se la connessione ha esito positivo, fare clic su **[!UICONTROL Add Connection]** per creare la connessione.

![](../images/clients/looker/click-test-connection.png)

## Passaggi successivi

Ora che siete connessi [!DNL Query Service], potete usare [!DNL Looker] per scrivere delle query. Per ulteriori informazioni su come scrivere ed eseguire query, consultare la guida [alle query](../creating-queries/creating-queries.md)in esecuzione.