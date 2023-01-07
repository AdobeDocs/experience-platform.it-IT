---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;Aqua Data Studio;studio dati Aqua;connettersi al servizio query;
solution: Experience Platform
title: Connettere Aqua Data Studio al servizio query
description: Questo documento descrive i passaggi necessari per la connessione di Aqua Data Studio con Adobe Experience Platform Query Service.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Connetti [!DNL Aqua Data Studio] al servizio query

Questo documento descrive i passaggi per la connessione [!DNL Aqua Data Studio] con Adobe Experience Platform [!DNL Query Service].

## Introduzione

Questa guida richiede l’accesso a [!DNL Aqua Data Studio] e scopri come navigare nella relativa interfaccia. Ulteriori informazioni [!DNL Aqua Data Studio] si trova nella [ufficiale [!DNL Aqua Data Studio] documentazione](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>Ci sono [!DNL Windows] e [!DNL macOS] versioni di [!DNL Aqua Data Studio]. Le schermate di questa guida sono state scattate utilizzando [!DNL macOS] app desktop. Possono esserci lievi discrepanze nell’interfaccia utente tra le versioni.

Acquisizione delle credenziali necessarie per la connessione [!DNL Aqua Data Studio] ad Experience Platform, devi avere accesso al [!UICONTROL Query] nell’interfaccia utente di Platform. Se al momento non disponi dell’accesso a [!UICONTROL Query] workspace.

## Registrare il server {#register-server}

Dopo l&#39;installazione [!DNL Aqua Data Studio], è innanzitutto necessario registrare il server. Dal menu principale, seleziona **[!DNL Server]**, seguita da **[!DNL Register Server]**.

![Menu a discesa Server con Register Server (Registro server) evidenziato.](../images/clients/aqua-data-studio/register-server.png)

La **[!DNL Register Server]** viene visualizzata la finestra di dialogo . Sotto la **[!DNL General]** scheda , seleziona **[!DNL PostgreSQL]** dall&#39;elenco a sinistra. Nella finestra di dialogo visualizzata, fornisci i seguenti dettagli per le impostazioni del server.

- **[!DNL Name]**: Nome della connessione. Si consiglia di fornire un nome descrittivo per riconoscere la connessione.
- **[!DNL Login Name]**: Il nome di accesso è l’ID organizzazione della piattaforma. Si presenta sotto forma di `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: Questa è una stringa alfanumerica trovata nel [!DNL Query Service] dashboard delle credenziali.
- **[!DNL Host and Port]**: L&#39;endpoint host e la relativa porta per [!DNL Query Service]. Per connettersi a è necessario utilizzare la porta 80 [!DNL Query Service].
- **[!DNL Database]:** Database che verrà utilizzato. Utilizzare il valore per la credenziale dell’interfaccia utente di Platform `dbname`: `prod:all`.

![La [!DNL Aqua Data Studio] Scheda Generale con i campi di input richiesti evidenziati.](../images/clients/aqua-data-studio/register-server-general-tab.png)

### [!DNL Query Service] credenziali

Per trovare le tue credenziali, accedi al [!DNL Platform] Interfaccia utente e seleziona **[!UICONTROL Query]** dalla navigazione a sinistra, seguita da **[!UICONTROL Credenziali]**. Per istruzioni complete per trovare le credenziali di accesso, l&#39;host, la porta e il nome del database, leggere il [guida alle credenziali](../ui/credentials.md).

[!DNL Query Service] offre inoltre credenziali non in scadenza per consentire una configurazione unica con client di terze parti. Consulta la documentazione per [istruzioni complete su come generare e utilizzare le credenziali non in scadenza](../ui/credentials.md#non-expiring-credentials).

### Impostazione della modalità SSL

Quindi, seleziona la **[!DNL Driver]** scheda . Sotto **[!DNL Parameters]**, imposta il valore come `?sslmode=require`

>[!IMPORTANT]
>
>Consulta la sezione [[!DNL Query Service] Documentazione SSL](./ssl-modes.md) per informazioni sul supporto SSL per le connessioni di terze parti a Adobe Experience Platform Query Service e su come connettersi utilizzando `verify-full` Modalità SSL.

![La [!DNL Aqua Data Studio] Scheda Driver con il campo Parametri evidenziato.](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Dopo aver inserito i dettagli della connessione, seleziona **[!DNL Test Connection]** per garantire il corretto funzionamento delle credenziali. Se il test di connessione ha esito positivo, seleziona **[!DNL Save]** per registrare il server. Viene visualizzata una finestra di dialogo di conferma della connessione e la connessione viene visualizzata sul dashboard. È ora possibile connettersi al server e visualizzare i relativi oggetti schema.

## Passaggi successivi

Ora che ti sei connesso a [!DNL Query Service], puoi utilizzare la **[!DNL Query Analyzer]** entro [!DNL Aqua Data Studio] per eseguire e modificare le istruzioni SQL. Per ulteriori informazioni su come scrivere ed eseguire le query, leggere il [guida all’esecuzione delle query](../best-practices/writing-queries.md).
