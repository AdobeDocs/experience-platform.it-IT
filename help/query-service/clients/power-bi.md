---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;Power BI;power bi;connessione al servizio query;
solution: Experience Platform
title: Connetti Power BI a Query Service
topic-legacy: connect
description: Questo documento descrive i passaggi necessari per la connessione di Power BI con Adobe Experience Platform Query Service.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---

# Connetti [!DNL Power BI] a Query Service (PC)

Questo documento descrive i passaggi per la connessione di Power BI con Adobe Experience Platform Query Service.

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL Power BI] e che tu abbia familiarità con come navigare nella relativa interfaccia. Ulteriori informazioni su [!DNL Power BI] sono disponibili nella [documentazione [!DNL Power BI] ufficiale](https://docs.microsoft.com/it-it/power-bi/).
>
> Inoltre, Power BI è disponibile **solo** sui dispositivi Windows.

Dopo aver installato Power BI, sarà necessario installare `Npgsql`, un pacchetto di driver .NET per PostgreSQL. Ulteriori informazioni su Npgsql sono disponibili nella [Documentazione Npgsql](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>È necessario scaricare v4.0.10 o versioni precedenti, in quanto le versioni più recenti generano errori.

In &quot;[!DNL Npgsql GAC Installation]&quot; nella schermata di configurazione personalizzata, seleziona **[!DNL Will be installed on local hard drive]**.

Per verificare che npgsql sia stato installato correttamente, riavviare il computer prima di procedere ai passaggi successivi.

## Connetti [!DNL Power BI] a [!DNL Query Service]

Per collegare [!DNL Power BI] a [!DNL Query Service], apri [!DNL Power BI] e seleziona **[!DNL Get Data]** nella barra multifunzione del menu principale.

![](../images/clients/power-bi/open-power-bi.png)

Selezionare **[!DNL PostgreSQL database]**, seguito da **[!DNL Connect]**.

![](../images/clients/power-bi/get-data.png)

È ora possibile immettere i valori per il server e il database. Per ulteriori informazioni su come trovare il nome del database, l&#39;host, la porta e le credenziali di accesso, leggere la [guida alle credenziali](../ui/credentials.md). Per trovare le tue credenziali, accedi a [!DNL Platform], quindi seleziona **[!UICONTROL Query]**, seguito da **[!UICONTROL Credenziali]**.

**[!DNL Server]** è l&#39;host trovato nei dettagli della connessione. Per la produzione, aggiungi la porta `:80` alla fine della stringa host. **[!DNL Database]** può essere &quot;all&quot; o un nome di tabella di set di dati.

Inoltre, puoi selezionare il tuo **[!DNL Data Connectivity mode]**. Selezionare **[!DNL Import]** per visualizzare un elenco di tutte le tabelle disponibili oppure selezionare **[!DNL DirectQuery]** per creare direttamente una query.

Per ulteriori informazioni sulla modalità **[!DNL Import]**, consulta la sezione relativa all’ [anteprima e importazione di una tabella](#preview). Per ulteriori informazioni sulla modalità **[!DNL DirectQuery]**, leggere la sezione relativa alla [creazione di istruzioni SQL](#create). Seleziona **[!DNL OK]** dopo aver confermato i dettagli del database.

![](../images/clients/power-bi/connectivity-mode.png)

Viene visualizzata una richiesta per richiedere il nome utente, la password e le impostazioni dell&#39;applicazione. Compila questi dettagli, quindi seleziona **[!DNL Connect]** per continuare con il passaggio successivo.

![](../images/clients/power-bi/import-mode.png)

## Anteprima e importazione di una tabella {#preview}

Se è stata selezionata la modalità **[!DNL Import]**, viene visualizzata una finestra di dialogo contenente un elenco di tutte le tabelle disponibili. Seleziona la tabella da visualizzare in anteprima, seguita da **[!DNL Load]** per inserire il set di dati in [!DNL Power BI].

![](../images/clients/power-bi/preview-table.png)

La tabella viene ora importata in Power BI.

![](../images/clients/power-bi/import-table.png)

## Creare istruzioni SQL {#create}

Se è stata selezionata la modalità **[!DNL DirectQuery]**, è necessario compilare la sezione Opzioni avanzate con la query SQL che si desidera creare.

In **[!DNL SQL statement]**, inserire la query SQL che si desidera creare. Assicurati che la casella di controllo denominata **[!DNL Include relationship columns]** sia selezionata. Dopo aver scritto la query, seleziona **[!DNL OK]** per continuare.

![](../images/clients/power-bi/direct-query-mode.png)

Viene visualizzata un’anteprima della query. Seleziona **[!DNL Load]** per visualizzare i risultati della query.

![](../images/clients/power-bi/preview-direct-query.png)

## Passaggi successivi

Dopo aver effettuato la connessione con [!DNL Query Service], è possibile utilizzare [!DNL Power BI] per scrivere le query. Per ulteriori informazioni su come scrivere ed eseguire le query, leggere la guida sull&#39; [esecuzione delle query](../best-practices/writing-queries.md).
