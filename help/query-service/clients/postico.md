---
keywords: ' Experience Platform;home;argomenti popolari;Query service;query service;postico;Postico;connect;connect to query service;'
solution: Experience Platform
title: Connect Postico to Query Service
topic: connect
description: Questo documento contiene il collegamento per l'installazione del client di backup Postico per Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# Connessione di [!DNL Postico] a Query Service (Mac)

Questo documento descrive i passaggi per la connessione di [!DNL Postico] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che abbiate già accesso a [!DNL Postico] e che abbiate familiarità con come navigare all&#39;interfaccia. Ulteriori informazioni su [!DNL Postico] sono disponibili nella [documentazione  [!DNL Postico] ufficiale](https://eggerapps.at/postico/docs).
> 
> Inoltre, [!DNL Postico] è disponibile solo **su dispositivi MacOS.**

Per connettere [!DNL Postico] a Query Service, aprire [!DNL Postico] e selezionare **[!DNL New Favorite]**.

![](../images/clients/postico/open-postico.png)

Ora potete immettere i valori per la connessione con Adobe Experience Platform.

Per ulteriori informazioni su come trovare il nome del database, l&#39;host, la porta e le credenziali di accesso, visitare la pagina delle [credenziali sulla piattaforma](https://platform.adobe.com/query/configuration). Per trovare le credenziali, accedere a [!DNL Platform], quindi selezionare **[!UICONTROL Queries]**, seguito da **[!UICONTROL Credentials]**.

Dopo aver inserito le credenziali, selezionare **[!DNL Connect]** per connettersi a Query Service.

![](../images/clients/postico/authentication-details.png)

Dopo la connessione alla piattaforma, potrai visualizzare un elenco di tutte le relazioni precedentemente effettuate con il servizio Query.

![](../images/clients/postico/show-queries.png)

## Creazione di istruzioni SQL

Per creare una nuova query SQL, selezionate e aprite &quot;Query SQL&quot;.

![](../images/clients/postico/create-query.png)

Viene visualizzata una casella e da qui è possibile digitare la query da eseguire. Al termine, selezionare **[!DNL Execute Statement]** per eseguire la query.

![](../images/clients/postico/run-statement.png)

Viene visualizzata una tabella che mostra i risultati dell&#39;esecuzione della query completata.

![](../images/clients/postico/query-results.png)

## Passaggi successivi

Ora che si è connessi con [!DNL Query Service], è possibile utilizzare [!DNL Postico] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire query, consultare la [guida alle query in esecuzione](../best-practices/writing-queries.md).