---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;Aqua Data Studio;Aqua data studio;connettersi al servizio query;
solution: Experience Platform
title: Connettere Aqua Data Studio a Query Service
description: Questo documento illustra i passaggi per la connessione di Aqua Data Studio con Adobe Experience Platform Query Service.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: 3ffb535e9a6648f037678acebba0de5f2088e79e
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Connetti [!DNL Aqua Data Studio] a Query Service

Questo documento descrive i passaggi per la connessione [!DNL Aqua Data Studio] con Adobe Experience Platform [!DNL Query Service].

## Introduzione

Questa guida richiede di avere già accesso a [!DNL Aqua Data Studio] e avere familiarità con le modalità di navigazione nell’interfaccia. Ulteriori informazioni su [!DNL Aqua Data Studio] si trova nella sezione [ufficiale [!DNL Aqua Data Studio] documentazione](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>Ci sono [!DNL Windows] e [!DNL macOS] versioni di [!DNL Aqua Data Studio]. Le schermate di questa guida sono state scattate utilizzando [!DNL macOS] app desktop. Potrebbero esserci discrepanze minori nell’interfaccia utente tra le versioni.

Per acquisire le credenziali necessarie per la connessione [!DNL Aqua Data Studio] ad Experience Platform, devi avere accesso al [!UICONTROL Query] nell’interfaccia utente di Platform. Se al momento non disponi dell’accesso a, contatta l’amministratore dell’organizzazione IMS [!UICONTROL Query] Workspace.

## Registra il server {#register-server}

Dopo l’installazione [!DNL Aqua Data Studio], è necessario innanzitutto registrare il server. Per istruzioni su come eseguire questa operazione, consulta la documentazione ufficiale di Aqua Data Studio. [avviare il [!DNL Register Server] finestra di dialogo](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) e [registrare il server](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

Una volta **[!DNL Register Server]** viene visualizzata una finestra di dialogo per un server PostgresSQL. Fornire i dettagli seguenti per le impostazioni del server.

- **[!DNL Name]**: nome della connessione. Si consiglia di fornire un nome descrittivo per riconoscere la connessione.
- **[!DNL Login Name]**: il nome di accesso corrisponde all’ID organizzazione della piattaforma. Si presenta sotto forma di `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: stringa alfanumerica trovata sul [!DNL Query Service] dashboard delle credenziali.
- **[!DNL Host and Port]**: l’endpoint host e la relativa porta per [!DNL Query Service]. È necessario utilizzare la porta 80 per connettersi con [!DNL Query Service].
- **[!DNL Database]:** Il database che verrà utilizzato. Usa il valore per le credenziali dell’interfaccia utente di Platform `dbname`: `prod:all`.

### [!DNL Query Service] credenziali

Per trovare le credenziali, accedi a [!DNL Platform] Interfaccia utente e selezione **[!UICONTROL Query]** dal menu di navigazione a sinistra, seguito da **[!UICONTROL Credenziali]**. Per informazioni complete su come trovare le credenziali di accesso, l&#39;host, la porta e il nome del database, leggere [guida alle credenziali](../ui/credentials.md).

[!DNL Query Service] offre anche credenziali senza scadenza per consentire una configurazione una tantum con client di terze parti. Consulta la documentazione per [istruzioni complete su come generare e utilizzare credenziali senza scadenza](../ui/credentials.md#non-expiring-credentials).

### Impostazione della modalità SSL

Successivamente, devi impostare il valore della modalità SSL come `?sslmode=require`. Questa operazione viene eseguita dal [!DNL Driver] scheda di [!DNL Edit Server Properties] . Per istruzioni su come eseguire questa operazione, consulta la documentazione ufficiale di Aqua Data Studio. [modifica proprietà driver](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) e [configurare SSL per [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). Utilizza la barra di ricerca per trovare `sslmode` proprietà.

>[!IMPORTANT]
>
>Consulta la [[!DNL Query Service] Documentazione SSL](./ssl-modes.md) per informazioni sul supporto SSL per le connessioni di terze parti a Adobe Experience Platform Query Service e su come connettersi utilizzando `verify-full` Modalità SSL.

Dopo aver inserito i dettagli di connessione, dalla stessa scheda, seleziona **[!DNL Test Connection]** per garantire il corretto funzionamento delle credenziali. Se il test di connessione ha esito positivo, seleziona **[!DNL Save]** per registrare il server. Viene visualizzata una finestra di dialogo di conferma che conferma la connessione e l’icona di connessione viene visualizzata sul dashboard. È ora possibile connettersi al server e visualizzarne gli oggetti schema.

## Passaggi successivi

Ora che ti sei connesso a [!DNL Query Service], è possibile utilizzare **[!DNL Query Analyzer]** entro [!DNL Aqua Data Studio] per eseguire e modificare le istruzioni SQL. Per ulteriori informazioni su come scrivere ed eseguire query, leggere [guida all’esecuzione delle query](../best-practices/writing-queries.md).
