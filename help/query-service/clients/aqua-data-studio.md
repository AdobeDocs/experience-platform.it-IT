---
keywords: ' Experience Platform;home;argomenti popolari;servizio query;servizio query;Aqua Data Studio;Aqua data studio;collegarsi al servizio query;'
solution: Experience Platform
title: Connetti con Aqua Data Studio
topic: connect
description: Questo documento descrive i passaggi necessari per la connessione di Aqua Data Studio con Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: eac93f3465fa6ce4af7a6aa783cf5f8fb4ac9b9b
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 1%

---


# [!DNL Aqua Data Studio]

Questo documento descrive i passaggi per la connessione di [!DNL Aqua Data Studio] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che abbiate già accesso a [!DNL Aqua Data Studio] e che abbiate familiarità con come navigare all&#39;interfaccia. Ulteriori informazioni su [!DNL Aqua Data Studio] sono disponibili nella [documentazione  [!DNL Aqua Data Studio] ufficiale](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

## Connetti [!DNL Aqua Data Studio] con la piattaforma

Dopo aver installato [!DNL Aqua Data Studio], è prima necessario registrare il server. Dal menu principale, selezionare **[!DNL Server]**, seguito da **[!DNL Register Server]**.

![](../images/clients/aqua-data-studio/register-server.png)

Viene visualizzata la finestra di dialogo **[!DNL Register Server]**. Nella scheda **[!DNL General]**, selezionare **[!DNL PostgreSQL]** dall&#39;elenco a sinistra. Nella finestra di dialogo visualizzata, fornite i seguenti dettagli per le impostazioni del server.

- **[!DNL Name]**: Nome della connessione.
- **[!DNL Login Name and Password]**: Le credenziali di accesso che verranno utilizzate. Il nome utente assume la forma di `ORG_ID@AdobeOrg`.
- **[!DNL Host and Port]**: L&#39;endpoint host e la relativa porta per  [!DNL Query Service]. È necessario utilizzare la porta 80 per connettersi con [!DNL Query Service].
- **[!DNL Database]:** Il database che verrà utilizzato.

>[!NOTE]
>
>Per ulteriori informazioni su come trovare le credenziali di accesso, l&#39;host, la porta e il nome del database, visitare la pagina delle credenziali [su Platform](https://platform.adobe.com/query/configuration). Per trovare le credenziali, accedere a [!DNL Platform], quindi selezionare **[!UICONTROL Queries]**, seguito da **[!UICONTROL Credentials]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Seleziona la scheda **[!DNL Driver]**. In **[!DNL Parameters]**, impostare il valore come `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Dopo aver inserito i dettagli di connessione, selezionare **[!DNL Test Connection]** per assicurarsi che le credenziali funzionino correttamente. Se la connessione ha esito positivo, selezionare **[!DNL Save]** per registrare il server. La connessione viene visualizzata sul dashboard dopo la registrazione, confermando che è ora possibile connettersi al server e visualizzare i relativi oggetti schema.

## Passaggi successivi

Ora che si è connessi a [!DNL Query Service], è possibile utilizzare **[!DNL Query Analyzer]** all&#39;interno di [!DNL Aqua Data Studio] per eseguire e modificare le istruzioni SQL. Per ulteriori informazioni su come scrivere ed eseguire query, consultare la [guida alle query in esecuzione](../best-practices/writing-queries.md).