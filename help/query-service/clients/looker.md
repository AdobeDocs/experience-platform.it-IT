---
keywords: Experience Platform;home;argomenti popolari;Query service;servizio query;Looker;looker;connect to query service;
solution: Experience Platform
title: Connetti Looker a Query Service
description: Questo documento illustra i passaggi per la connessione di Looker con Adobe Experience Platform Query Service.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# Connetti [!DNL Looker] a Query Service

Questo documento descrive i passaggi per la connessione [!DNL Looker] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL Looker] e hanno familiarità con le modalità di navigazione nell’interfaccia. Ulteriori informazioni su [!DNL Looker] si trova nella sezione [ufficiale [!DNL Looker] documentazione](https://docs.looker.com/).

## Crea una nuova connessione al database {#create-connection}

Dopo l’accesso a [!DNL Looker], seleziona **[!DNL Admin]**, seguito da **[!DNL Connections]**. Il [!DNL Connections] viene visualizzata la pagina. Il giorno [!DNL Connections] pagina, seleziona **[!DNL Add Connection]**.

Da qui immettere i dettagli delle impostazioni di connessione elencate di seguito. Consulta la documentazione ufficiale di Looker per [istruzioni per creare una nuova connessione al database e descrizioni delle proprietà disponibili](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]:** Nome della connessione.
- **[!DNL Dialect]:** Il dialetto utilizzato per il database SQL. [!DNL Query Service] utilizza **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** L&#39;endpoint host e la relativa porta per [!DNL Query Service].
- **[!DNL Database]:** Il database che verrà utilizzato.
- **[!DNL Username and Password]:** Le credenziali di accesso che verranno utilizzate. Il nome utente assumerà la forma di `ORG_ID@AdobeOrg`.
- **SSL**: abilita SSL per garantire una connessione sicura in rete.

Per trovare le credenziali necessarie per connettere Looker con Query Service, accedi all’interfaccia utente di Platform e seleziona **[!UICONTROL Query]** dal menu di navigazione a sinistra, seguito da **[!UICONTROL Credenziali]**. Per ulteriori informazioni su come trovare **host**, **porta**, **database**, **nome utente**, e **password** , leggere le [guida alle credenziali](../ui/credentials.md).

![Pagina Credenziali dell’area di lavoro Query di Experience Platform con le credenziali ed evidenziate Credenziali in scadenza.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] offre anche credenziali senza scadenza per consentire una configurazione una tantum con client di terze parti. Consulta la documentazione per [istruzioni complete su come generare e utilizzare credenziali senza scadenza](../ui/credentials.md#non-expiring-credentials). È necessario completare questo processo se si desidera connettere Looker come configurazione unica. Il `credential` e `technicalAccountId` i valori acquisiti comprendono il valore per Looker `password` parametro.

Per informazioni sul supporto SSL per le connessioni di terze parti in Adobe Experience Platform, consulta [[!DNL Query Service] Documentazione SSL](./ssl-modes.md). Questo documento fornisce istruzioni su come connettersi utilizzando `verify-full` Modalità SSL.

Dopo aver inserito i dettagli di connessione, seleziona **[!DNL Test These Settings]** per garantire il corretto funzionamento delle credenziali. Ulteriori informazioni su [verifica delle impostazioni di connessione](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) sono fornite nella documentazione ufficiale di Looker. Una volta stabilita la connessione, sullo schermo viene visualizzato un messaggio che indica che è possibile connettersi. Una volta stabilita la connessione, seleziona **[!DNL Add Connection]** per creare la connessione.

## Passaggi successivi

Ora che hai stabilito una connessione con [!DNL Query Service], è possibile utilizzare [!DNL Looker] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire query, leggere [guida all’esecuzione delle query](../best-practices/writing-queries.md).
