---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;postico;postico;connettersi al servizio query;
solution: Experience Platform
title: Connetti Postico a Query Service
description: Questo documento contiene il collegamento per l’installazione del client di backup Postico per Adobe Experience Platform Query Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 9fe7e618d251867c90c88f8bee6ef5863ae78f60
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Connetti [!DNL Postico] a Query Service (Mac)

Questo documento descrive i passaggi per la connessione di [!DNL Postico] a Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL Postico] e che tu abbia familiarità con le modalità di navigazione nella relativa interfaccia. Ulteriori informazioni su [!DNL Postico] sono disponibili nella [documentazione [!DNL Postico] ufficiale](https://eggerapps.at/postico/docs).
> 
> Inoltre, [!DNL Postico] è **only** disponibile sui dispositivi macOS.

Per connettere [!DNL Postico] a Query Service, apri [!DNL Postico] e seleziona **[!DNL New Favorite]**. Viene visualizzata la finestra di dialogo per le impostazioni di connessione. Da qui è possibile immettere i valori dei parametri per la connessione a Adobe Experience Platform. Immettere le impostazioni di connessione elencate di seguito. Le istruzioni su come [connettersi a un server PostgreSQL con Postico](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) sono disponibili anche sul sito ufficiale di Postico.

| Parametro di connessione | Descrizione |
|---|---|
| **[!DNL Host]:** | Nome host del server PostgreSQL. |
| **[!DNL Port]:** | Porta per [!DNL Query Service]. Per connettersi a [!DNL Query Service], è necessario utilizzare la porta **80** o **5432**. |
| **[!DNL User]** | Crea un nome per la connessione specifica. Lascia vuoto il campo per usare il nome di accesso di Mac. |
| **[!DNL Password]** | Questa stringa alfanumerica è la credenziale **[!UICONTROL Password]** di Experience Platform. Se si desidera utilizzare credenziali senza scadenza, questo valore corrisponde agli argomenti concatenati di `technicalAccountID` e `credential` scaricati nel file JSON di configurazione. Il valore della password assume la forma: {technicalAccountId}:{credential}. Il file JSON di configurazione per le credenziali senza scadenza è un download una tantum durante l’inizializzazione di, Adobe di cui non conserva una copia. |
| **[!DNL Database]** | Utilizza il valore delle credenziali dell&#39;Experience Platform **[!UICONTROL Database]**: `prod:all`. |

Per ulteriori informazioni su come trovare il nome del database, l&#39;host, la porta e le credenziali di accesso, leggere la [guida delle credenziali](../ui/credentials.md). Per trovare le credenziali, accedi a [!DNL Platform], quindi seleziona **[!UICONTROL Query]**, seguito da **[!UICONTROL Credenziali]**.

Dopo aver inserito le credenziali, selezionare **[!DNL Connect]** per connettersi a Query Service.

Dopo la connessione a Platform, potrai visualizzare un elenco di tutte le relazioni precedentemente stabilite con Query Service.

## Creare istruzioni SQL

Per creare una nuova query SQL, selezionare **[!DNL SQL Query]** dalla barra laterale. In alternativa, utilizzare la scelta rapida da tastiera (⇧⌘T) per passare alla visualizzazione della query e immettere la query che si desidera eseguire. Al termine, selezionare **[!DNL Execute Statement]** per eseguire la query. Viene visualizzata una tabella con i risultati dell’esecuzione della query completata.

Per ulteriori informazioni su [utilizzo della visualizzazione query](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html), vedere la documentazione ufficiale di Postico.

## Passaggi successivi

Dopo aver stabilito la connessione con [!DNL Query Service], è possibile utilizzare [!DNL Postico] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire query, leggere la [guida alle query in esecuzione](../best-practices/writing-queries.md).
