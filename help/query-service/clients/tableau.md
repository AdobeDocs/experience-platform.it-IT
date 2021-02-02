---
keywords: ' Experience Platform;home;argomenti popolari;tableau;Tableau;query service;Query service;connect to query service;'
solution: Experience Platform
title: Connetti con Tableau
topic: connect
description: Questo documento descrive i passaggi necessari per la connessione di Tableau con Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: eac93f3465fa6ce4af7a6aa783cf5f8fb4ac9b9b
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# [!DNL Tableau]

Questo documento descrive i passaggi per la connessione di Tableau con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che abbiate già accesso a [!DNL Tableau] e che abbiate familiarità con come navigare all&#39;interfaccia. Ulteriori informazioni su [!DNL Tableau] sono disponibili nella [documentazione  [!DNL Tableau] ufficiale](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

## Connetti [!DNL Tableau] con la piattaforma

Per collegare [!DNL Tableau] a [!DNL Query Service], aprire [!DNL Tableau] e, nella sezione **[!DNL To a Server]**, selezionare **[!DNL More]** seguito da **[!DNL PostgreSQL]**

![](../images/clients/tableau/open-connection.png)

Ora potete immettere i valori per la connessione con Adobe Experience Platform. Per ulteriori informazioni su come trovare il nome del database, l&#39;host, la porta e le credenziali di accesso, visitare la pagina delle [credenziali sulla piattaforma](https://platform.adobe.com/query/configuration). Per trovare le credenziali, accedere a [!DNL Platform], quindi selezionare **[!UICONTROL Queries]**, seguito da **[!UICONTROL Credentials]**.

Assicurarsi di aver selezionato la casella **[!UICONTROL SSL Required]** prima di provare a connettersi.

Dopo aver compilato tutte le credenziali, selezionare **[!DNL Sign In]** per continuare.

![](../images/clients/tableau/sign-in.png)

Ora si è connessi ad Adobe Experience Platform, con un elenco delle tabelle visualizzato sul lato.

![](../images/clients/tableau/connected.png)

## Passaggi successivi

Ora che si è connessi con [!DNL Query Service], è possibile utilizzare [!DNL Tableau] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire query, consultare la guida in [esecuzione query](../best-practices/writing-queries.md).