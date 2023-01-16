---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;postico;Postico;connessione al servizio query;
solution: Experience Platform
title: Connetti Postico a Query Service
description: Questo documento contiene il collegamento per l'installazione del client di backup Postico per Adobe Experience Platform Query Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 9fe7e618d251867c90c88f8bee6ef5863ae78f60
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Connetti [!DNL Postico] al servizio query (Mac)

Questo documento descrive i passaggi per la connessione [!DNL Postico] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL Postico] e conoscono bene come navigare nella relativa interfaccia. Ulteriori informazioni [!DNL Postico] si trova nella [ufficiale [!DNL Postico] documentazione](https://eggerapps.at/postico/docs).
> 
> Inoltre, [!DNL Postico] è **only** disponibile su dispositivi macOS.

Connessione [!DNL Postico] al servizio query, apri [!DNL Postico] e seleziona **[!DNL New Favorite]**. Viene visualizzata la finestra di dialogo relativa alle impostazioni di connessione. Da qui, puoi immettere i valori dei parametri per la connessione con Adobe Experience Platform. Immettere le impostazioni di connessione elencate di seguito. Istruzioni su come [connettersi a un server PostgreSQL con Postico](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) sono disponibili anche sul sito ufficiale di Postico.

| Parametro di connessione | Descrizione |
|---|---|
| **[!DNL Host]:** | Nome host del server PostgreSQL. |
| **[!DNL Port]:** | La porta [!DNL Query Service]. È necessario utilizzare la porta **80** o **5432** per connettersi con [!DNL Query Service]. |
| **[!DNL User]** | Crea un nome per la connessione specifica. Lascia vuoto il campo per utilizzare il nome di accesso di Mac. |
| **[!DNL Password]** | Questa stringa alfanumerica è il tuo Experience Platform **[!UICONTROL Password]** credenziale. Se desideri utilizzare credenziali non in scadenza, questo valore è costituito dagli argomenti concatenati della variabile `technicalAccountID` e `credential` scaricato nel file JSON di configurazione. Il valore della password assume la forma di: {technicalAccountId}:{credential}. Il file JSON di configurazione per le credenziali non in scadenza è un download una tantum durante l&#39;inizializzazione di cui l&#39;Adobe non conserva una copia. |
| **[!DNL Database]** | Utilizza il tuo Experience Platform **[!UICONTROL Database]** valore credenziale: `prod:all`. |

Per ulteriori informazioni su come trovare il nome del database, l&#39;host, la porta e le credenziali di accesso, leggere il [guida alle credenziali](../ui/credentials.md). Per trovare le tue credenziali, accedi a [!DNL Platform], quindi seleziona **[!UICONTROL Query]**, seguita da **[!UICONTROL Credenziali]**.

Dopo aver inserito le credenziali, seleziona **[!DNL Connect]** per la connessione con Query Service.

Dopo la connessione a Platform, potrai visualizzare un elenco di tutte le relazioni precedentemente effettuate con Query Service.

## Creare istruzioni SQL

Per creare una nuova query SQL, selezionare **[!DNL SQL Query]** dalla barra laterale. In alternativa, utilizza la scelta rapida da tastiera ( ⇧ ⌘ T) per passare alla visualizzazione della query e immettere la query da eseguire. Al termine, seleziona **[!DNL Execute Statement]** per eseguire la query. Viene visualizzata una tabella con i risultati dell’esecuzione della query completata.

Vedi la documentazione ufficiale di Postico per maggiori informazioni su [utilizzo della visualizzazione query](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html).

## Passaggi successivi

Ora che ti sei connesso [!DNL Query Service], puoi utilizzare [!DNL Postico] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire le query, leggere il [guida all’esecuzione delle query](../best-practices/writing-queries.md).
