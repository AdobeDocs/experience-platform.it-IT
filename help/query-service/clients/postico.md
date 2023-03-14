---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;postico;postico;connettersi al servizio query;
solution: Experience Platform
title: Connetti Postico a Query Service
description: Questo documento contiene il collegamento per l’installazione del client di backup Postico per Adobe Experience Platform Query Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 9fe7e618d251867c90c88f8bee6ef5863ae78f60
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Connetti [!DNL Postico] a Query Service (Mac)

Questo documento descrive i passaggi per la connessione [!DNL Postico] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL Postico] e hanno familiarità con le modalità di navigazione nell’interfaccia. Ulteriori informazioni su [!DNL Postico] si trova nella sezione [ufficiale [!DNL Postico] documentazione](https://eggerapps.at/postico/docs).
> 
> Inoltre, [!DNL Postico] è **solo** disponibile sui dispositivi macOS.

Per connettersi [!DNL Postico] in Query Service, apri [!DNL Postico] e seleziona **[!DNL New Favorite]**. Viene visualizzata la finestra di dialogo per le impostazioni di connessione. Da qui è possibile immettere i valori dei parametri per la connessione a Adobe Experience Platform. Immettere le impostazioni di connessione elencate di seguito. Istruzioni su come [connettersi a un server PostgreSQL con Postico](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) sono disponibili anche sul sito ufficiale di Postico.

| Parametro di connessione | Descrizione |
|---|---|
| **[!DNL Host]:** | Nome host del server PostgreSQL. |
| **[!DNL Port]:** | La porta per [!DNL Query Service]. È necessario utilizzare la porta **80** o **5432** per connettersi con [!DNL Query Service]. |
| **[!DNL User]** | Crea un nome per la connessione specifica. Lascia vuoto il campo per usare il nome di accesso di Mac. |
| **[!DNL Password]** | Questa stringa alfanumerica è il tuo Experience Platform **[!UICONTROL Password]** credenziali. Se si desidera utilizzare credenziali senza scadenza, questo valore corrisponde agli argomenti concatenati del `technicalAccountID` e `credential` scaricato nel file JSON di configurazione. Il valore della password è il seguente: {technicalAccountId}:{credential}. Il file JSON di configurazione per le credenziali senza scadenza è un download una tantum durante l’inizializzazione di, Adobe di cui non conserva una copia. |
| **[!DNL Database]** | Utilizza il tuo Experience Platform **[!UICONTROL Database]** valore credenziali: `prod:all`. |

Per ulteriori informazioni su come trovare il nome del database, l&#39;host, la porta e le credenziali di accesso, leggere [guida alle credenziali](../ui/credentials.md). Per trovare le credenziali, accedi a [!DNL Platform], quindi seleziona **[!UICONTROL Query]**, seguito da **[!UICONTROL Credenziali]**.

Dopo aver inserito le credenziali, seleziona **[!DNL Connect]** per connettersi a Query Service.

Dopo la connessione a Platform, potrai visualizzare un elenco di tutte le relazioni precedentemente stabilite con Query Service.

## Creare istruzioni SQL

Per creare una nuova query SQL, selezionare **[!DNL SQL Query]** dalla barra laterale. In alternativa, utilizzare la scelta rapida da tastiera (⇧⌘T) per passare alla visualizzazione della query e immettere la query che si desidera eseguire. Al termine, seleziona **[!DNL Execute Statement]** per eseguire la query. Viene visualizzata una tabella con i risultati dell’esecuzione della query completata.

Per ulteriori informazioni, consulta la documentazione ufficiale di Postico. [utilizzo della visualizzazione query](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html).

## Passaggi successivi

Ora che hai stabilito una connessione con [!DNL Query Service], è possibile utilizzare [!DNL Postico] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire query, leggere [guida all’esecuzione delle query](../best-practices/writing-queries.md).
