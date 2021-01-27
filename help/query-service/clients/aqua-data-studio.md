---
keywords: Experience Platform;home;popular topics;query service;Query service;Aqua Data Studio;Aqua data studio;connect to query service;
solution: Experience Platform
title: Connetti con Aqua Data Studio
topic: connect
description: Questo documento descrive i passaggi necessari per la connessione di Aqua Data Studio con Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 9fbb6b829cd9ddec30f22b0de66874be7710e465
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 2%

---


# Connetti con [!DNL Aqua Data Studio]

Questo documento descrive i passaggi per la connessione di [!DNL Aqua Data Studio] con Adobe Experience Platform [!DNL Query Service].

Dopo aver installato [!DNL Aqua Data Studio], è prima necessario registrare il server. Dal menu principale, fare clic su **[!UICONTROL Server]**, quindi su **[!UICONTROL Register Server]**.

![](../images/clients/aqua-data-studio/register-server.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Register Server]**. Nella scheda **[!UICONTROL General]**, selezionare **[!UICONTROL PostgreSQL]** dall&#39;elenco a sinistra. Nella finestra di dialogo visualizzata, fornite i seguenti dettagli per le impostazioni del server.

- **[!UICONTROL Name]**: Nome della connessione.
- **[!UICONTROL Login Name and Password]**: Le credenziali di accesso che verranno utilizzate. Il nome utente assume la forma di `ORG_ID@AdobeOrg`.
- **[!UICONTROL Host and Port]**: L&#39;endpoint host e la relativa porta per  [!DNL Query Service]. È necessario utilizzare la porta 80 per connettersi con [!DNL Query Service].
- **[!UICONTROL Database]:** Il database che verrà utilizzato.

>[!NOTE]
>
>Per ulteriori informazioni su come trovare le credenziali di accesso, l&#39;host, la porta e il nome del database, visitare la pagina delle credenziali [su Platform](https://platform.adobe.com/query/configuration). Per trovare le credenziali, accedere a [!DNL Platform], fare clic su **[!UICONTROL Queries]**, quindi su **[!UICONTROL Credentials]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Seleziona la scheda **[!UICONTROL Driver]**. In **[!UICONTROL Parameters]**, impostare il valore come `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Dopo aver inserito i dettagli di connessione, fare clic su **[!UICONTROL Test Connection]** per verificare il corretto funzionamento delle credenziali. Se la connessione ha esito positivo, fare clic su **[!UICONTROL Save]** per registrare il server. La connessione viene visualizzata sul **dashboard** dopo la registrazione, confermando che è ora possibile connettersi al server e visualizzare i relativi oggetti schema.

## Passaggi successivi

Ora che si è connessi a [!DNL Query Service], è possibile utilizzare **[!UICONTROL Query Analyzer]** all&#39;interno di [!DNL Aqua Data Studio] per eseguire e modificare le istruzioni SQL. Per ulteriori informazioni su come scrivere ed eseguire query, consultare la [guida alle query in esecuzione](../best-practices/writing-queries.md).