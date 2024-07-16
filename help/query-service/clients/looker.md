---
keywords: Experience Platform;home;argomenti popolari;Query service;servizio query;Looker;looker;connect to query service;
solution: Experience Platform
title: Connetti Looker a Query Service
description: Questo documento illustra i passaggi per la connessione di Looker con Adobe Experience Platform Query Service.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Connetti [!DNL Looker] a Query Service

Questo documento descrive i passaggi per la connessione di [!DNL Looker] a Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL Looker] e che tu abbia familiarità con le modalità di navigazione nella relativa interfaccia. Ulteriori informazioni su [!DNL Looker] sono disponibili nella [documentazione [!DNL Looker] ufficiale](https://docs.looker.com/).

## Crea una nuova connessione al database {#create-connection}

Dopo aver effettuato l&#39;accesso a [!DNL Looker], selezionare **[!DNL Admin]**, seguito da **[!DNL Connections]**. Verrà aperta la pagina [!DNL Connections]. Nella pagina [!DNL Connections], selezionare **[!DNL Add Connection]**.

Da qui immettere i dettagli delle impostazioni di connessione elencate di seguito. Per [istruzioni per creare una nuova connessione al database e descrizioni delle proprietà disponibili](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection), vedere la documentazione di Looker ufficiale.

- **[!DNL Name]:** Il nome della connessione.
- **[!DNL Dialect]:** Il dialetto utilizzato per il database SQL. [!DNL Query Service] utilizza **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** L&#39;endpoint host e la relativa porta per [!DNL Query Service].
- **[!DNL Database]:** Il database che verrà utilizzato.
- **[!DNL Username and Password]:** Le credenziali di accesso che verranno utilizzate. Il nome utente sarà nel formato `ORG_ID@AdobeOrg`.
- **SSL**: abilitare SSL per garantire una connessione protetta in rete.

Per trovare le credenziali necessarie per connettere Looker con Query Service, accedi all&#39;interfaccia utente di Platform e seleziona **[!UICONTROL Query]** dalla barra di navigazione a sinistra, seguita da **[!UICONTROL Credenziali]**. Per ulteriori informazioni su come trovare le credenziali di **host**, **porta**, **database**, **nome utente** e **password**, leggere la [guida delle credenziali](../ui/credentials.md).

![Pagina Credenziali dell&#39;area di lavoro Query Experience Platform con le credenziali evidenziate e le credenziali in scadenza.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] offre anche credenziali senza scadenza per consentire una configurazione una tantum con client di terze parti. Consulta la documentazione per [istruzioni complete su come generare e utilizzare credenziali senza scadenza](../ui/credentials.md#non-expiring-credentials). È necessario completare questo processo se si desidera connettere Looker come configurazione unica. I valori `credential` e `technicalAccountId` acquisiti comprendono il valore per il parametro `password` Looker.

Per informazioni sul supporto SSL per le connessioni di terze parti in Adobe Experience Platform, consulta la [[!DNL Query Service] documentazione SSL](./ssl-modes.md). In questo documento vengono fornite istruzioni su come connettersi utilizzando la modalità SSL `verify-full`.

Dopo aver immesso i dettagli di connessione, selezionare **[!DNL Test These Settings]** per verificare che le credenziali funzionino correttamente. Ulteriori informazioni sulla [verifica delle impostazioni di connessione](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) sono fornite nella documentazione ufficiale di Looker. Una volta stabilita la connessione, sullo schermo viene visualizzato un messaggio che indica che è possibile connettersi. Una volta stabilita la connessione, selezionare **[!DNL Add Connection]** per creare la connessione.

## Passaggi successivi

Dopo aver stabilito la connessione con [!DNL Query Service], è possibile utilizzare [!DNL Looker] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire query, leggere la [guida alle query in esecuzione](../best-practices/writing-queries.md).
