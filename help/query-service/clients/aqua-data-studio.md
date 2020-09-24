---
keywords: Experience Platform;home;popular topics;query service;Query service;Aqua Data Studio;Aqua data studio;connect to query service;
solution: Experience Platform
title: Connetti con Aqua Data Studio
topic: connect
translation-type: tm+mt
source-git-commit: 106d5150371a890e2d4c295bf5d12c110c593568
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 2%

---


# Connetti con [!DNL Aqua Data Studio]

Questo documento descrive i passaggi necessari per connettersi [!DNL Aqua Data Studio] con Adobe Experience Platform [!DNL Query Service].

Dopo l&#39;installazione [!DNL Aqua Data Studio], dovete prima registrare il server. Dal menu principale, fare clic **[!UICONTROL Server]**, quindi fare clic su **[!UICONTROL Register Server]**.

![](../images/clients/aqua-data-studio/register-server.png)

Viene visualizzata **[!UICONTROL Register Server]** la finestra di dialogo. Sotto la **[!UICONTROL General]** scheda, selezionare **[!UICONTROL PostgreSQL]** dall&#39;elenco a sinistra. Nella finestra di dialogo visualizzata, fornite i seguenti dettagli per le impostazioni del server.

- **[!UICONTROL Name]**: Nome della connessione.
- **[!UICONTROL Login Name and Password]**: Le credenziali di accesso che verranno utilizzate. Il nome utente assume la forma di `ORG_ID@AdobeOrg`.
- **[!UICONTROL Host and Port]**: L&#39;endpoint host e la relativa porta per [!DNL Query Service]. È necessario utilizzare la porta 80 per connettersi con [!DNL Query Service].
- **[!UICONTROL Database]:** Il database che verrà utilizzato.

>[!NOTE]
>
>Per ulteriori informazioni su come trovare le credenziali di accesso, l&#39;host, la porta e il nome del database, visitare la pagina delle [credenziali sulla piattaforma](https://platform.adobe.com/query/configuration). Per trovare le credenziali, accedi a [!DNL Platform], fai clic su **[!UICONTROL Queries]**, quindi fai clic su **[!UICONTROL Credentials]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Seleziona la scheda **[!UICONTROL Driver]**. In **[!UICONTROL Parameters]**, imposta il valore come `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Dopo aver inserito i dettagli di connessione, fate clic **[!UICONTROL Test Connection]** per verificare che le credenziali funzionino correttamente. Se la connessione ha esito positivo, fate clic **[!UICONTROL Save]** per registrare il server. La connessione viene visualizzata sul *dashboard* dopo la registrazione, confermando che è ora possibile connettersi al server e visualizzare i relativi oggetti schema.

## Passaggi successivi

Ora che si è connessi a [!DNL Query Service], è possibile utilizzare l&#39; **[!UICONTROL Query Analyzer]** interno [!DNL Aqua Data Studio] per eseguire e modificare le istruzioni SQL. Per ulteriori informazioni su come scrivere ed eseguire query, consultare la guida [alle query](../creating-queries/creating-queries.md)in esecuzione.