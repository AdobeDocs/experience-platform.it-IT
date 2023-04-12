---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;Aqua Data Studio;studio dati Aqua;connettersi al servizio query;
solution: Experience Platform
title: Connettere Aqua Data Studio al servizio query
description: Questo documento descrive i passaggi necessari per la connessione di Aqua Data Studio con Adobe Experience Platform Query Service.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Connetti [!DNL Aqua Data Studio] al servizio query

Questo documento descrive i passaggi per la connessione [!DNL Aqua Data Studio] con Adobe Experience Platform [!DNL Query Service].

## Introduzione

Questa guida richiede l’accesso a [!DNL Aqua Data Studio] e scopri come navigare nella relativa interfaccia. Ulteriori informazioni [!DNL Aqua Data Studio] si trova nella [ufficiale [!DNL Aqua Data Studio] documentazione](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>Ci sono [!DNL Windows] e [!DNL macOS] versioni di [!DNL Aqua Data Studio]. Le schermate di questa guida sono state scattate utilizzando [!DNL macOS] app desktop. Possono esserci lievi discrepanze nell’interfaccia utente tra le versioni.

Acquisizione delle credenziali necessarie per la connessione [!DNL Aqua Data Studio] ad Experience Platform, devi avere accesso al [!UICONTROL Query] nell’interfaccia utente di Platform. Contatta l’amministratore dell’organizzazione se al momento non disponi dell’accesso a [!UICONTROL Query] workspace.

## Registrare il server {#register-server}

Dopo l&#39;installazione [!DNL Aqua Data Studio], è innanzitutto necessario registrare il server. Consulta la documentazione ufficiale di Aqua Data Studio per istruzioni su come [lanciare [!DNL Register Server] dialogo](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) e [registra il server](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

Una volta che **[!DNL Register Server]** viene visualizzata la finestra di dialogo per un server PostgresSQL, fornire i seguenti dettagli per le impostazioni del server.

- **[!DNL Name]**: Nome della connessione. Si consiglia di fornire un nome descrittivo per riconoscere la connessione.
- **[!DNL Login Name]**: Il nome di accesso è l’ID organizzazione della piattaforma. Si presenta sotto forma di `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: Questa è una stringa alfanumerica trovata nel [!DNL Query Service] dashboard delle credenziali.
- **[!DNL Host and Port]**: L&#39;endpoint host e la relativa porta per [!DNL Query Service]. Per connettersi a è necessario utilizzare la porta 80 [!DNL Query Service].
- **[!DNL Database]:** Database che verrà utilizzato. Utilizzare il valore per la credenziale dell’interfaccia utente di Platform `dbname`: `prod:all`.

### [!DNL Query Service] credenziali

Per trovare le tue credenziali, accedi al [!DNL Platform] Interfaccia utente e seleziona **[!UICONTROL Query]** dalla navigazione a sinistra, seguita da **[!UICONTROL Credenziali]**. Per istruzioni complete per trovare le credenziali di accesso, l&#39;host, la porta e il nome del database, leggere il [guida alle credenziali](../ui/credentials.md).

[!DNL Query Service] offre inoltre credenziali non in scadenza per consentire una configurazione unica con client di terze parti. Consulta la documentazione per [istruzioni complete su come generare e utilizzare le credenziali non in scadenza](../ui/credentials.md#non-expiring-credentials).

### Impostazione della modalità SSL

Successivamente, devi impostare il valore della modalità SSL come `?sslmode=require`. Questa operazione viene eseguita dal [!DNL Driver] della scheda [!DNL Edit Server Properties] finestra di dialogo. Consulta la documentazione ufficiale di Aqua Data Studio per istruzioni su come [modificare le proprietà del driver](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) e [configura SSL per [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). Utilizza la barra di ricerca per trovare il `sslmode` proprietà.

>[!IMPORTANT]
>
>Consulta la sezione [[!DNL Query Service] Documentazione SSL](./ssl-modes.md) per informazioni sul supporto SSL per le connessioni di terze parti a Adobe Experience Platform Query Service e su come connettersi utilizzando `verify-full` Modalità SSL.

Dopo aver inserito i dettagli di connessione, dalla stessa scheda, seleziona **[!DNL Test Connection]** per garantire il corretto funzionamento delle credenziali. Se il test di connessione ha esito positivo, seleziona **[!DNL Save]** per registrare il server. Viene visualizzata una finestra di dialogo di conferma che conferma la connessione e l’icona di connessione sul dashboard. È ora possibile connettersi al server e visualizzare i relativi oggetti schema.

## Passaggi successivi

Ora che ti sei connesso a [!DNL Query Service], puoi utilizzare la **[!DNL Query Analyzer]** entro [!DNL Aqua Data Studio] per eseguire e modificare le istruzioni SQL. Per ulteriori informazioni su come scrivere ed eseguire le query, leggere il [guida all’esecuzione delle query](../best-practices/writing-queries.md).
