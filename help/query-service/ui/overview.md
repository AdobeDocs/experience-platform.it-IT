---
keywords: Experience Platform;home;popular topics;query service;Query service;query
solution: Experience Platform
title: Guida all'interfaccia utente di Adobe Experience Platform Query Service
topic: guide
description: Adobe Experience Platform Query Service fornisce un'interfaccia utente che può essere utilizzata per scrivere ed eseguire query, visualizzare query eseguite in precedenza e query di accesso salvate dagli utenti all'interno dell'organizzazione IMS.
translation-type: tm+mt
source-git-commit: 23516c66a67ae5663dcf90a40ccba98bfd266ab0
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 2%

---


# [!DNL Query Service] guida

Adobe Experience Platform [!DNL Query Service] fornisce un&#39;interfaccia utente che può essere utilizzata per scrivere ed eseguire query, visualizzare query eseguite in precedenza e query di accesso salvate dagli utenti all&#39;interno dell&#39;organizzazione IMS. Per accedere all’interfaccia utente in [Adobe Experience Platform][platform-ui], selezionate **[!UICONTROL Queries]** nella barra di navigazione a sinistra.

## [!DNL Query Editor]

Consente di [!DNL Query Editor] scrivere ed eseguire query senza utilizzare un client esterno. Fate clic **[!UICONTROL Create Query]** per aprire la query [!DNL Query Editor] e creare una nuova query. È inoltre possibile accedere al modulo [!DNL Query Editor] selezionando una query dalle *[!UICONTROL Log]* o *[!UICONTROL Browse]* schede. Se si seleziona una query eseguita in precedenza o salvata, verrà aperto [!DNL Query Editor] e visualizzato l&#39;SQL per la query selezionata.

![Immagine](../images/queries/ui-overview/overview.png)

[!DNL Query Editor] fornisce uno spazio di modifica in cui è possibile iniziare a digitare una query. Durante la digitazione, l&#39;editor completa automaticamente le parole riservate, le tabelle e i nomi di campo SQL all&#39;interno delle tabelle. Al termine, fate clic sul pulsante **Riproduci** per eseguire la query. La *[!UICONTROL Console]* scheda sotto l&#39;editor mostra le operazioni [!DNL Query Service] in corso, indicando quando è stata restituita una query. Nella *[!UICONTROL Result]* scheda accanto alla console sono visualizzati i risultati della query. Per ulteriori informazioni sull&#39;utilizzo di [Query Editor, consultate la guida][query-editor] all&#39;editor di query [!DNL Query Editor].

![Immagine](../images/queries/ui-overview/query-editor.png)

## Sfoglia

La *[!UICONTROL Browse]* scheda mostra le query salvate dagli utenti nell&#39;organizzazione. È utile considerarli come progetti di query, in quanto le query salvate qui potrebbero essere ancora in costruzione. Le query visualizzate nella *[!UICONTROL Browse]* scheda vengono visualizzate anche come query di esecuzione nella *[!UICONTROL Log]* scheda se sono state eseguite in precedenza da [!DNL Query Service].

![Immagine](../images/queries/ui-overview/browse.png)

| Colonna | Descrizione |
| --- | --- |
| Nome | Nome della query creata dall&#39;utente. È possibile fare clic sul nome per aprire la query nel [!DNL Query Editor]. È inoltre possibile utilizzare la barra di ricerca per effettuare ricerche in base al nome di una query. Le ricerche sono con distinzione tra maiuscole e minuscole. |
| SQL | I primi caratteri della query SQL. Quando passi il puntatore del mouse sul codice viene visualizzata la query completa. |
| Modificato da | Ultimo utente che ha modificato la query. Qualsiasi utente dell’organizzazione con accesso a [!DNL Query Service] può modificare le query. |
| Ultima modifica | Data e ora dell’ultima modifica apportata alla query, nel fuso orario del browser. |

## Registro

La *[!UICONTROL Log]* scheda fornisce un elenco delle query che sono state eseguite in precedenza. Per impostazione predefinita, il registro elenca le query nella cronologia inversa.

![Immagine](../images/queries/ui-overview/log.png)

| Colonna | Descrizione |
| --- | --- |
| **[!UICONTROL Name]** | Il nome della query, costituito dai primi caratteri della query SQL. Facendo clic sul nome si apre il [!DNL Query Editor], consentendo di modificare la query. È possibile utilizzare la barra di ricerca per effettuare ricerche in base al nome di una query. Le ricerche sono con distinzione tra maiuscole e minuscole. |
| **[!UICONTROL Created By]** | Nome della persona che ha creato la query. |
| **[!UICONTROL Client]** | Client utilizzato per la query. |
| **[!UICONTROL Dataset]** | Set di dati di input utilizzato dalla query. Fare clic sul set di dati per passare alla schermata dei dettagli del set di dati di input. |
| **[!UICONTROL Status]** | Stato corrente della query. |
| **[!UICONTROL Last Run]** | Quando la query è stata eseguita per ultima. Potete ordinare l’elenco in ordine crescente o decrescente facendo clic sulla freccia su questa colonna. |
| **[!UICONTROL Run Time]** | Il tempo necessario per eseguire la query. |

## Credenziali

Nella *[!UICONTROL Credentials]* scheda vengono visualizzate [!DNL Postgres] le credenziali. Fare clic sull&#39; **[!UICONTROL Copy]** icona accanto a un campo per memorizzarne il contenuto nel buffer della tastiera. Per ulteriori informazioni sull&#39;utilizzo di queste credenziali per la connessione con client esterni, consultare la guida [alla][connect-clients]connessione con i client.

![Immagine](../images/queries/ui-overview/credentials.png)

## Passaggi successivi

Ora che avete familiarità con l&#39;interfaccia [!DNL Query Service] utente in [!DNL Platform], potete accedere [!DNL Query Editor] per iniziare a creare progetti di query personali da condividere con altri utenti dell&#39;organizzazione. Per ulteriori informazioni sull&#39;authoring e l&#39;esecuzione di query in [!DNL Query Editor], consultare la guida [utente dell&#39;Editor][query-editor]query.

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
