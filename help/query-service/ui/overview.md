---
keywords: ' Experience Platform;home;argomenti popolari;servizio query;servizio query;query;editor query;editor query;editor query;editor query;'
solution: Experience Platform
title: Guida all'interfaccia utente del servizio query
topic: guide
description: Adobe Experience Platform Query Service fornisce un'interfaccia utente che può essere utilizzata per scrivere ed eseguire query, visualizzare query eseguite in precedenza e query di accesso salvate dagli utenti all'interno dell'organizzazione IMS.
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 2%

---


# [!DNL Query Service] guida

Adobe Experience Platform [!DNL Query Service] fornisce un&#39;interfaccia utente che può essere utilizzata per scrivere ed eseguire query, visualizzare query eseguite in precedenza e query di accesso salvate dagli utenti all&#39;interno dell&#39;organizzazione IMS. Per accedere all&#39;interfaccia utente in [Adobe Experience Platform][platform-ui], selezionare **[!UICONTROL Queries]** nel menu di navigazione a sinistra.

## [!DNL Query Editor]

[!DNL Query Editor] consente di scrivere ed eseguire query senza utilizzare un client esterno. Fare clic su **[!UICONTROL Create Query]** per aprire la [!DNL Query Editor] e creare una nuova query. È inoltre possibile accedere a [!DNL Query Editor] selezionando una query dalle schede **[!UICONTROL Log]** o **[!UICONTROL Browse]**. Selezionando una query eseguita in precedenza o salvata, si aprirà la [!DNL Query Editor] e si visualizzerà l&#39;SQL per la query selezionata.

![Immagine](../images/queries/ui-overview/overview.png)

[!DNL Query Editor] fornisce uno spazio di modifica in cui è possibile iniziare a digitare una query. Durante la digitazione, l&#39;editor completa automaticamente le parole riservate, le tabelle e i nomi di campo SQL all&#39;interno delle tabelle. Al termine della scrittura della query, fare clic sul pulsante **Play** per eseguire la query. La scheda **[!UICONTROL Console]** sotto l&#39;editor mostra le operazioni eseguite attualmente da [!DNL Query Service], indicando quando è stata restituita una query. La scheda **[!UICONTROL Result]**, accanto alla console, mostra i risultati della query. Per ulteriori informazioni sull&#39;utilizzo di [!DNL Query Editor], vedere la [Guida per l&#39;editor di query][query-editor].

![Immagine](../images/queries/ui-overview/query-editor.png)

## Sfoglia

La scheda **[!UICONTROL Browse]** mostra le query salvate dagli utenti nell&#39;organizzazione. È utile considerarli come progetti di query, in quanto le query salvate qui potrebbero essere ancora in costruzione. Le query visualizzate nella scheda **[!UICONTROL Browse]** vengono visualizzate anche come query di esecuzione nella scheda **[!UICONTROL Log]** se sono state eseguite in precedenza da [!DNL Query Service].

![Immagine](../images/queries/ui-overview/browse.png)

| Colonna | Descrizione |
| --- | --- |
| Nome | Nome della query creata dall&#39;utente. È possibile fare clic sul nome per aprire la query in [!DNL Query Editor]. È inoltre possibile utilizzare la barra di ricerca per effettuare ricerche in base al nome di una query. Le ricerche sono con distinzione tra maiuscole e minuscole. |
| SQL | I primi caratteri della query SQL. Quando passi il puntatore del mouse sul codice viene visualizzata la query completa. |
| Modificato da | Ultimo utente che ha modificato la query. Qualsiasi utente dell&#39;organizzazione che ha accesso a [!DNL Query Service] può modificare le query. |
| Ultima modifica | Data e ora dell’ultima modifica apportata alla query, nel fuso orario del browser. |

## Registro

La scheda **[!UICONTROL Log]** fornisce un elenco delle query che sono state eseguite in precedenza. Per impostazione predefinita, il registro elenca le query nella cronologia inversa.

![Immagine](../images/queries/ui-overview/log.png)

| Colonna | Descrizione |
| --- | --- |
| **[!UICONTROL Name]** | Il nome della query, costituito dai primi caratteri della query SQL. Facendo clic sul nome si apre la [!DNL Query Editor], consentendo di modificare la query. È possibile utilizzare la barra di ricerca per effettuare ricerche in base al nome di una query. Le ricerche sono con distinzione tra maiuscole e minuscole. |
| **[!UICONTROL Created By]** | Nome della persona che ha creato la query. |
| **[!UICONTROL Client]** | Client utilizzato per la query. |
| **[!UICONTROL Dataset]** | Set di dati di input utilizzato dalla query. Fare clic sul set di dati per passare alla schermata dei dettagli del set di dati di input. |
| **[!UICONTROL Status]** | Stato corrente della query. |
| **[!UICONTROL Last Run]** | Quando la query è stata eseguita per ultima. Potete ordinare l’elenco in ordine crescente o decrescente facendo clic sulla freccia su questa colonna. |
| **[!UICONTROL Run Time]** | Il tempo necessario per eseguire la query. |

## Credenziali

La scheda **[!UICONTROL Credentials]** visualizza le credenziali [!DNL Postgres]. Fare clic sull&#39;icona **[!UICONTROL Copy]** accanto a qualsiasi campo per memorizzarne il contenuto nel buffer della tastiera. Per ulteriori informazioni sull&#39;utilizzo di queste credenziali per la connessione con client esterni, consultare la [guida alla connessione con i client][connect-clients].

![Immagine](../images/queries/ui-overview/credentials.png)

## Passaggi successivi

Ora che si ha familiarità con l&#39;interfaccia utente [!DNL Query Service] in [!DNL Platform], è possibile accedere a [!DNL Query Editor] per iniziare a creare progetti di query personali da condividere con altri utenti dell&#39;organizzazione. Per ulteriori informazioni sull&#39;authoring e l&#39;esecuzione di query in [!DNL Query Editor], consultare la [Guida utente dell&#39;editor di query][query-editor].

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
