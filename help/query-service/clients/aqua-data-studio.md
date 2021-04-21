---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;Aqua Data Studio;studio dati Aqua;connettersi al servizio query;
solution: Experience Platform
title: Connettere Aqua Data Studio al servizio query
topic-legacy: connect
description: Questo documento descrive i passaggi necessari per la connessione di Aqua Data Studio con Adobe Experience Platform Query Service.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# Connetti [!DNL Aqua Data Studio] al servizio query

Questo documento descrive i passaggi per la connessione di [!DNL Aqua Data Studio] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL Aqua Data Studio] e che tu abbia familiarità con come navigare nella relativa interfaccia. Ulteriori informazioni su [!DNL Aqua Data Studio] sono disponibili nella [documentazione [!DNL Aqua Data Studio] ufficiale](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

Dopo aver installato [!DNL Aqua Data Studio], è necessario prima registrare il server. Dal menu principale, selezionare **[!DNL Server]**, seguito da **[!DNL Register Server]**.

![](../images/clients/aqua-data-studio/register-server.png)

Viene visualizzata la finestra di dialogo **[!DNL Register Server]**. Nella scheda **[!DNL General]** , seleziona **[!DNL PostgreSQL]** dall’elenco a sinistra. Nella finestra di dialogo visualizzata, fornisci i seguenti dettagli per le impostazioni del server.

- **[!DNL Name]**: Nome della connessione.
- **[!DNL Login Name and Password]**: Le credenziali di accesso che verranno utilizzate. Il nome utente assume la forma di `ORG_ID@AdobeOrg`.
- **[!DNL Host and Port]**: L&#39;endpoint host e la relativa porta per  [!DNL Query Service]. È necessario utilizzare la porta 80 per connettersi a [!DNL Query Service].
- **[!DNL Database]:** Il database che verrà utilizzato.

>[!NOTE]
>
>Per ulteriori informazioni su come trovare le credenziali di accesso, l&#39;host, la porta e il nome del database, visita la pagina delle credenziali [su Platform](https://platform.adobe.com/query/configuration). Per trovare le tue credenziali, accedi a [!DNL Platform], quindi seleziona **[!UICONTROL Queries]**, seguito da **[!UICONTROL Credentials]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Seleziona la scheda **[!DNL Driver]**. Sotto **[!DNL Parameters]**, imposta il valore come `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Dopo aver inserito i dettagli di connessione, seleziona **[!DNL Test Connection]** per garantire il corretto funzionamento delle credenziali. Se la connessione ha esito positivo, selezionare **[!DNL Save]** per registrare il server. La connessione viene visualizzata sul dashboard al termine della registrazione, confermando che è ora possibile connettersi al server e visualizzare i relativi oggetti schema.

## Passaggi successivi

Dopo aver effettuato la connessione a [!DNL Query Service], è possibile utilizzare **[!DNL Query Analyzer]** in [!DNL Aqua Data Studio] per eseguire e modificare le istruzioni SQL. Per ulteriori informazioni su come scrivere ed eseguire le query, leggere la [guida all&#39;esecuzione delle query](../best-practices/writing-queries.md).
