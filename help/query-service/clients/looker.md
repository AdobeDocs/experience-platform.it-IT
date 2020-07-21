---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connetti con Looker
topic: connect
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 1%

---


# Connetti con [!DNL Looker]

Per collegarsi [!DNL Looker] con [!DNL Query Service] il Adobe Experience Platform , attenetevi alla procedura seguente:

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
>Per ulteriori informazioni su come trovare l&#39;host e la porta, il nome del database e le credenziali di accesso, visitare la pagina delle [credenziali su Platform](https://platform.adobe.com/query/configuration). Per trovare le credenziali, accedi a [!DNL Platform], fai clic su **[!UICONTROL Queries]**, quindi fai clic su **[!UICONTROL Credentials]**.

Dopo aver inserito i dettagli di connessione, fate clic su **[!UICONTROL Test These Settings]** per verificare che le credenziali funzionino correttamente. In caso affermativo, di seguito verrà visualizzato un messaggio in cui si informa che è possibile connettersi. Se la connessione ha esito positivo, fare clic su **[!UICONTROL Add Connection]** per creare la connessione.

![](../images/clients/looker/click-test-connection.png)

## Passaggi successivi

Ora che siete connessi [!DNL Query Service], potete usare [!DNL Looker] per scrivere delle query. Per ulteriori informazioni su come scrivere ed eseguire query, consultare la guida [alle query](../creating-queries/creating-queries.md)in esecuzione.