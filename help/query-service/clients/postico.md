---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;postico;Postico;connessione al servizio query;
solution: Experience Platform
title: Connetti Postico a Query Service
description: Questo documento contiene il collegamento per l'installazione del client di backup Postico per Adobe Experience Platform Query Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# Connetti [!DNL Postico] al servizio query (Mac)

Questo documento descrive i passaggi per la connessione [!DNL Postico] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL Postico] e conoscono bene come navigare nella relativa interfaccia. Ulteriori informazioni [!DNL Postico] si trova nella [ufficiale [!DNL Postico] documentazione](https://eggerapps.at/postico/docs).
> 
> Inoltre, [!DNL Postico] è **only** disponibile su dispositivi macOS.

Connessione [!DNL Postico] al servizio query, apri [!DNL Postico] e seleziona **[!DNL New Favorite]**.

![La [!DNL Postico] Interfaccia utente con nuovo preferito evidenziato.](../images/clients/postico/open-postico.png)

È ora possibile immettere i valori per la connessione con Adobe Experience Platform.

Per ulteriori informazioni su come trovare il nome del database, l&#39;host, la porta e le credenziali di accesso, leggere il [guida alle credenziali](../ui/credentials.md). Per trovare le tue credenziali, accedi a [!DNL Platform], quindi seleziona **[!UICONTROL Query]**, seguita da **[!UICONTROL Credenziali]**.

Dopo aver inserito le credenziali, seleziona **[!DNL Connect]** per la connessione con Query Service.

![Finestra di dialogo Nuovo preferito con connessione evidenziata.](../images/clients/postico/authentication-details.png)

Dopo la connessione a Platform, potrai visualizzare un elenco di tutte le relazioni precedentemente effettuate con Query Service.

![Un elenco di connessioni nel [!DNL Postico] Interfaccia utente.](../images/clients/postico/show-queries.png)

## Creare istruzioni SQL

Per creare una nuova query SQL, selezionare e aprire &quot;Query SQL&quot;.

![La [!DNL Postico] Interfaccia utente con il collegamento a query SQL evidenziato.](../images/clients/postico/create-query.png)

Viene visualizzata una casella in cui è possibile digitare la query da eseguire. Al termine, seleziona **[!DNL Execute Statement]** per eseguire la query.

![Editor SQL con istruzione Execute evidenziato.](../images/clients/postico/run-statement.png)

Viene visualizzata una tabella che mostra i risultati dell’esecuzione della query completata.

![Tabella dei risultati della query di esempio.](../images/clients/postico/query-results.png)

## Passaggi successivi

Ora che ti sei connesso [!DNL Query Service], puoi utilizzare [!DNL Postico] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire le query, leggere il [guida all’esecuzione delle query](../best-practices/writing-queries.md).
