---
keywords: Experience Platform;home;argomenti popolari;Query service;query service;Looker;looker;connect to query service;
solution: Experience Platform
title: Connetti Looker al servizio query
topic-legacy: connect
description: Questo documento descrive i passaggi necessari per la connessione di Looker con Adobe Experience Platform Query Service.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Connetti [!DNL Looker] al servizio query

Questo documento descrive i passaggi per la connessione di [!DNL Looker] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL Looker] e che tu abbia familiarità con come navigare nella relativa interfaccia. Ulteriori informazioni su [!DNL Looker] sono disponibili nella [documentazione [!DNL Looker] ufficiale](https://docs.looker.com/).

Dopo aver effettuato l&#39;accesso a [!DNL Looker], seleziona **[!DNL Admin]**, seguito da **[!DNL Connections]**.

![](../images/clients/looker/click-admin-connections.png)

In questa pagina, seleziona **[!DNL New Connection]**.

![](../images/clients/looker/click-new-connection.png)

Da qui è possibile compilare i dettagli delle impostazioni di connessione.

![](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** Il nome della connessione.
- **[!DNL Dialect]:** Il dialetto utilizzato per il database SQL. [!DNL Query Service] utilizza  **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** l’endpoint host e la relativa porta per  [!DNL Query Service].
- **[!DNL Database]:** Il database che verrà utilizzato.
- **[!DNL Username and Password]:** Le credenziali di accesso che verranno utilizzate. Il nome utente sarà in forma di `ORG_ID@AdobeOrg`.

>[!NOTE]
>
>Per ulteriori informazioni su come trovare l&#39;host e la porta, il nome del database e le credenziali di accesso, visita la pagina delle credenziali [su Platform](https://platform.adobe.com/query/configuration). Per trovare le tue credenziali, accedi a [!DNL Platform], quindi seleziona **[!UICONTROL Queries]**, seguito da **[!UICONTROL Credentials]**.

Dopo aver inserito i dettagli di connessione, seleziona **[!DNL Test These Settings]** per garantire il corretto funzionamento delle credenziali. In caso affermativo, di seguito verrà visualizzato un messaggio che indica che è possibile connettersi. Se la connessione ha esito positivo, selezionare **[!DNL Add Connection]** per creare la connessione.

![](../images/clients/looker/click-test-connection.png)

## Passaggi successivi

Dopo aver effettuato la connessione con [!DNL Query Service], è possibile utilizzare [!DNL Looker] per scrivere le query. Per ulteriori informazioni su come scrivere ed eseguire le query, leggere la [guida all&#39;esecuzione delle query](../best-practices/writing-queries.md).
