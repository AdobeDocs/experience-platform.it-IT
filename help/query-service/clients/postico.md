---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;postico;Postico;connessione al servizio query;
solution: Experience Platform
title: Connetti Postico a Query Service
topic-legacy: connect
description: Questo documento contiene il collegamento per l'installazione del client di backup Postico per Adobe Experience Platform Query Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# Connetti [!DNL Postico] a Query Service (Mac)

Questo documento descrive i passaggi per la connessione di [!DNL Postico] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL Postico] e che tu abbia familiarità con come navigare nella relativa interfaccia. Ulteriori informazioni su [!DNL Postico] sono disponibili nella [documentazione [!DNL Postico] ufficiale](https://eggerapps.at/postico/docs).
> 
> Inoltre, [!DNL Postico] è **disponibile solo** su dispositivi macOS.

Per connettersi a [!DNL Postico] Query Service, apri [!DNL Postico] e seleziona **[!DNL New Favorite]**.

![](../images/clients/postico/open-postico.png)

È ora possibile immettere i valori per la connessione con Adobe Experience Platform.

Per ulteriori informazioni su come trovare il nome del database, l&#39;host, la porta e le credenziali di accesso, visita la pagina delle credenziali [su Platform](https://platform.adobe.com/query/configuration). Per trovare le tue credenziali, accedi a [!DNL Platform], quindi seleziona **[!UICONTROL Queries]**, seguito da **[!UICONTROL Credentials]**.

Dopo aver inserito le credenziali, selezionare **[!DNL Connect]** per connettersi al servizio query.

![](../images/clients/postico/authentication-details.png)

Dopo la connessione a Platform, potrai visualizzare un elenco di tutte le relazioni precedentemente effettuate con Query Service.

![](../images/clients/postico/show-queries.png)

## Creare istruzioni SQL

Per creare una nuova query SQL, selezionare e aprire &quot;Query SQL&quot;.

![](../images/clients/postico/create-query.png)

Viene visualizzata una casella in cui è possibile digitare la query da eseguire. Al termine, seleziona **[!DNL Execute Statement]** per eseguire la query.

![](../images/clients/postico/run-statement.png)

Viene visualizzata una tabella che mostra i risultati dell’esecuzione della query completata.

![](../images/clients/postico/query-results.png)

## Passaggi successivi

Dopo aver effettuato la connessione con [!DNL Query Service], è possibile utilizzare [!DNL Postico] per scrivere le query. Per ulteriori informazioni su come scrivere ed eseguire le query, leggere la [guida all&#39;esecuzione delle query](../best-practices/writing-queries.md).
