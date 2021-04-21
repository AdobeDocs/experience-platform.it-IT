---
keywords: Experience Platform;home;argomenti popolari;tableau;Tableau;servizio query;servizio query;connessione al servizio query;
solution: Experience Platform
title: Connetti Tableau a Query Service
topic-legacy: connect
description: Questo documento descrive i passaggi necessari per la connessione di Tableau con Adobe Experience Platform Query Service.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# Connetti [!DNL Tableau] al servizio query

Questo documento descrive i passaggi per la connessione di Tableau con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL Tableau] e che tu abbia familiarità con come navigare nella relativa interfaccia. Ulteriori informazioni su [!DNL Tableau] sono disponibili nella [documentazione [!DNL Tableau] ufficiale](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Per collegare [!DNL Tableau] a [!DNL Query Service], apri [!DNL Tableau] e nella sezione **[!DNL To a Server]** seleziona **[!DNL More]** seguito da **[!DNL PostgreSQL]**

![](../images/clients/tableau/open-connection.png)

È ora possibile immettere i valori per la connessione con Adobe Experience Platform. Per ulteriori informazioni su come trovare il nome del database, l&#39;host, la porta e le credenziali di accesso, visita la pagina delle credenziali [su Platform](https://platform.adobe.com/query/configuration). Per trovare le tue credenziali, accedi a [!DNL Platform], quindi seleziona **[!UICONTROL Queries]**, seguito da **[!UICONTROL Credentials]**.

Assicurati di aver selezionato la casella **[!UICONTROL SSL Required]** prima di provare a connetterti.

Dopo aver compilato tutte le credenziali, seleziona **[!DNL Sign In]** per continuare.

![](../images/clients/tableau/sign-in.png)

Ora ti sei connesso a Adobe Experience Platform con un elenco delle tabelle visualizzato sul lato.

![](../images/clients/tableau/connected.png)

## Passaggi successivi

Dopo aver effettuato la connessione con [!DNL Query Service], è possibile utilizzare [!DNL Tableau] per scrivere le query. Per ulteriori informazioni su come scrivere ed eseguire le query, leggere la guida sull&#39; [esecuzione delle query](../best-practices/writing-queries.md).
