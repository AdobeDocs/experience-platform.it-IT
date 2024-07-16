---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;Aqua Data Studio;Aqua data studio;connettersi al servizio query;
solution: Experience Platform
title: Connettere Aqua Data Studio a Query Service
description: Questo documento illustra i passaggi per la connessione di Aqua Data Studio con Adobe Experience Platform Query Service.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# Connetti [!DNL Aqua Data Studio] a Query Service

Questo documento descrive i passaggi per la connessione di [!DNL Aqua Data Studio] a Adobe Experience Platform [!DNL Query Service].

## Introduzione

Questa guida richiede di avere già accesso a [!DNL Aqua Data Studio] e di avere familiarità con le modalità di navigazione nell&#39;interfaccia. Ulteriori informazioni su [!DNL Aqua Data Studio] sono disponibili nella [documentazione [!DNL Aqua Data Studio] ufficiale](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>Sono presenti [!DNL Windows] e [!DNL macOS] versioni di [!DNL Aqua Data Studio]. Le schermate di questa guida sono state scattate utilizzando l&#39;app desktop [!DNL macOS]. Potrebbero esserci discrepanze minori nell’interfaccia utente tra le versioni.

Per acquisire le credenziali necessarie per la connessione di [!DNL Aqua Data Studio] a Experience Platform, è necessario avere accesso all&#39;area di lavoro [!UICONTROL Query] nell&#39;interfaccia utente di Platform. Contatta l&#39;amministratore dell&#39;organizzazione se al momento non hai accesso all&#39;area di lavoro [!UICONTROL Query].

## Registra il server {#register-server}

Dopo aver installato [!DNL Aqua Data Studio], è necessario prima registrare il server. Consulta la documentazione ufficiale di Aqua Data Studio per istruzioni su come [avviare la [!DNL Register Server] finestra di dialogo](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) e [registrare il server](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

Quando viene visualizzata la finestra di dialogo **[!DNL Register Server]** per un server PostgresSQL, specificare i dettagli seguenti per le impostazioni del server.

- **[!DNL Name]**: nome della connessione. Si consiglia di fornire un nome descrittivo per riconoscere la connessione.
- **[!DNL Login Name]**: il nome di accesso è l&#39;ID organizzazione della piattaforma. Si presenta come `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: stringa alfanumerica trovata nel dashboard delle credenziali [!DNL Query Service].
- **[!DNL Host and Port]**: endpoint host e relativa porta per [!DNL Query Service]. Per connettersi a [!DNL Query Service], è necessario utilizzare la porta 80.
- **[!DNL Database]:** Il database che verrà utilizzato. Utilizzare il valore per le credenziali dell&#39;interfaccia utente di Platform `dbname`: `prod:all`.

### [!DNL Query Service] credenziali

Per trovare le credenziali, accedi all&#39;interfaccia utente [!DNL Platform] e seleziona **[!UICONTROL Query]** dal menu di navigazione a sinistra, seguito da **[!UICONTROL Credenziali]**. Per informazioni complete su come trovare le credenziali di accesso, l&#39;host, la porta e il nome del database, leggere la [guida delle credenziali](../ui/credentials.md).

[!DNL Query Service] offre anche credenziali senza scadenza per consentire una configurazione una tantum con client di terze parti. Consulta la documentazione per [istruzioni complete su come generare e utilizzare credenziali senza scadenza](../ui/credentials.md#non-expiring-credentials).

### Impostazione della modalità SSL

Impostare quindi il valore della modalità SSL come `?sslmode=require`. Operazione eseguita dalla scheda [!DNL Driver] della finestra di dialogo [!DNL Edit Server Properties]. Per istruzioni su come [modificare le proprietà del driver](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) e [configurare SSL per [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration), vedere la documentazione ufficiale di Aqua Data Studio. Utilizzare la barra di ricerca per trovare la proprietà `sslmode`.

>[!IMPORTANT]
>
>Consulta la [[!DNL Query Service] documentazione SSL](./ssl-modes.md) per informazioni sul supporto SSL per le connessioni di terze parti a Adobe Experience Platform Query Service e su come connettersi utilizzando la modalità SSL `verify-full`.

Dopo aver immesso i dettagli di connessione, dalla stessa scheda, seleziona **[!DNL Test Connection]** per verificare che le credenziali funzionino correttamente. Se il test di connessione ha esito positivo, selezionare **[!DNL Save]** per registrare il server. Viene visualizzata una finestra di dialogo di conferma che conferma la connessione e l’icona di connessione viene visualizzata sul dashboard. È ora possibile connettersi al server e visualizzarne gli oggetti schema.

## Passaggi successivi

Dopo aver stabilito la connessione a [!DNL Query Service], è possibile utilizzare **[!DNL Query Analyzer]** in [!DNL Aqua Data Studio] per eseguire e modificare le istruzioni SQL. Per ulteriori informazioni su come scrivere ed eseguire query, leggere la [guida alle query in esecuzione](../best-practices/writing-queries.md).
