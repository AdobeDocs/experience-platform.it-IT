---
keywords: Experience Platform;home;argomenti popolari;Query service;query service;Looker;looker;connect to query service;
solution: Experience Platform
title: Connetti Looker al servizio query
description: Questo documento descrive i passaggi necessari per la connessione di Looker con Adobe Experience Platform Query Service.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# Connetti [!DNL Looker] al servizio query

Questo documento descrive i passaggi per la connessione [!DNL Looker] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL Looker] e conoscono bene come navigare nella relativa interfaccia. Ulteriori informazioni [!DNL Looker] si trova nella [ufficiale [!DNL Looker] documentazione](https://docs.looker.com/).

## Crea una nuova connessione al database {#create-connection}

Dopo aver effettuato l’accesso a [!DNL Looker], seleziona **[!DNL Admin]**, seguita da **[!DNL Connections]**. La [!DNL Connections] viene visualizzata la pagina . Sulla [!DNL Connections] pagina, seleziona **[!DNL Add Connection]**.

Da qui, immetti i dettagli delle impostazioni di connessione elencate di seguito. Consulta la documentazione ufficiale di Looker per [istruzioni per creare una nuova connessione al database e descrizioni delle proprietà disponibili](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]:** Nome della connessione.
- **[!DNL Dialect]:** Il dialetto utilizzato per il database SQL. [!DNL Query Service] utilizza **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** L&#39;endpoint host e la relativa porta per [!DNL Query Service].
- **[!DNL Database]:** Database che verrà utilizzato.
- **[!DNL Username and Password]:** Le credenziali di accesso che verranno utilizzate. Il nome utente sarà sotto forma di `ORG_ID@AdobeOrg`.
- **SSL**: Abilita SSL per garantire una connessione sicura attraverso la rete.

Per trovare le credenziali necessarie per collegare Looker a Query Service, accedi all’interfaccia utente di Platform e seleziona **[!UICONTROL Query]** dalla navigazione a sinistra, seguita da **[!UICONTROL Credenziali]**. Per ulteriori informazioni su come trovare le **host**, **porta**, **database**, **username** e **password** credenziali, leggere [guida alle credenziali](../ui/credentials.md).

![La pagina Credenziali dell&#39;area di lavoro Query Experienci Platform con credenziali e le credenziali in scadenza evidenziate.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] offre inoltre credenziali non in scadenza per consentire una configurazione unica con client di terze parti. Consulta la documentazione per [istruzioni complete su come generare e utilizzare le credenziali non in scadenza](../ui/credentials.md#non-expiring-credentials). È necessario completare questo processo se si desidera collegare Looker come una configurazione una tantum. La `credential` e `technicalAccountId` i valori acquisiti comprendono il valore del Looker `password` parametro .

Per informazioni sul supporto SSL per connessioni di terze parti in Adobe Experience Platform, consulta la [[!DNL Query Service] Documentazione SSL](./ssl-modes.md). Questo documento fornisce istruzioni su come connettersi utilizzando `verify-full` Modalità SSL.

Dopo aver inserito i dettagli di connessione, seleziona **[!DNL Test These Settings]** per garantire il corretto funzionamento delle credenziali. Ulteriori informazioni [verifica delle impostazioni di connessione](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) sono forniti nella documentazione ufficiale del Looker. Una volta stabilita la connessione, sullo schermo viene visualizzato un messaggio per indicare che è possibile connettersi. Una volta completata la connessione, seleziona **[!DNL Add Connection]** per creare la connessione.

## Passaggi successivi

Ora che ti sei connesso [!DNL Query Service], puoi utilizzare [!DNL Looker] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire le query, leggere il [guida all’esecuzione delle query](../best-practices/writing-queries.md).
