---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;editor query;editor query;editor query;editor query;editor query;editor query;
solution: Experience Platform
title: Guida all’interfaccia utente del servizio query
topic-legacy: guide
description: Adobe Experience Platform Query Service fornisce un’interfaccia utente che può essere utilizzata per scrivere ed eseguire query, visualizzare query eseguite in precedenza e accedere alle query salvate dagli utenti all’interno dell’organizzazione IMS.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
translation-type: tm+mt
source-git-commit: d2f19cc97082f75e66cf38e54b5bdb89482930ed
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 2%

---

# [!DNL Query Service] guida

Adobe Experience Platform [!DNL Query Service] fornisce un&#39;interfaccia utente che può essere utilizzata per scrivere ed eseguire query, visualizzare query eseguite in precedenza e accedere alle query salvate dagli utenti all&#39;interno dell&#39;organizzazione IMS. Per accedere all&#39;interfaccia utente di [Adobe Experience Platform][platform-ui], seleziona **[!UICONTROL Queries]** nel menu di navigazione a sinistra.

## [!DNL Query Editor]

[!DNL Query Editor] consente di scrivere ed eseguire query senza utilizzare un client esterno. Seleziona **[!UICONTROL Create Query]** per aprire [!DNL Query Editor] e creare una nuova query. Puoi anche accedere a [!DNL Query Editor] selezionando una query dalle schede **[!UICONTROL Log]** o **[!UICONTROL Browse]** . Quando si seleziona una query eseguita o salvata in precedenza, viene aperto il [!DNL Query Editor] e viene visualizzato il SQL per la query selezionata.

![Immagine](../images/ui/overview/overview.png)

[!DNL Query Editor] fornisce uno spazio di modifica in cui iniziare a digitare una query. Mentre si digita, l&#39;editor completa automaticamente le parole riservate SQL, le tabelle e i nomi di campo all&#39;interno delle tabelle. Al termine della scrittura della query, selezionare il pulsante **Play** per eseguire la query. La scheda **[!UICONTROL Console]** sotto l&#39;editor mostra le operazioni correnti di [!DNL Query Service], indicando quando è stata restituita una query. La scheda **[!UICONTROL Result]**, accanto alla console, visualizza i risultati della query. Per ulteriori informazioni sull&#39;utilizzo di [!DNL Query Editor], consulta la [Guida all&#39;editor delle query][query-editor] .

![Immagine](../images/ui/overview/query-editor.png)

## Sfoglia

La scheda **[!UICONTROL Browse]** mostra le query salvate dagli utenti dell’organizzazione. È utile considerarli come progetti di query, in quanto le query salvate qui potrebbero essere ancora in costruzione. Le query visualizzate nella scheda **[!UICONTROL Browse]** vengono visualizzate anche come query di esecuzione nella scheda **[!UICONTROL Log]** se sono state eseguite in precedenza da [!DNL Query Service].

![Immagine](../images/ui/overview/browse.png)

| Colonna | Descrizione |
| --- | --- |
| Nome | Nome della query creata dall&#39;utente. Puoi selezionare il nome per aprire la query in [!DNL Query Editor]. È inoltre possibile utilizzare la barra di ricerca per cercare il Nome di una query. Le ricerche sono sensibili all’uso di maiuscole e minuscole. |
| SQL | I primi caratteri della query SQL. Passando il puntatore del mouse sul codice viene visualizzata la query completa. |
| Modificato da | Ultimo utente che ha modificato la query. Qualsiasi utente della tua organizzazione con accesso a [!DNL Query Service] può modificare le query. |
| Ultima modifica | La data e l’ora dell’ultima modifica alla query, nel fuso orario del browser. |

## Registro

La scheda **[!UICONTROL Log]** fornisce un elenco delle query eseguite in precedenza. Per impostazione predefinita, il registro elenca le query nella cronologia inversa.

![Immagine](../images/ui/overview/log.png)

| Colonna | Descrizione |
| --- | --- |
| **[!UICONTROL Name]** | Nome della query, costituito dai primi caratteri della query SQL. Selezionando il nome si apre il [!DNL Query Editor], che consente di modificare la query. È possibile utilizzare la barra di ricerca per cercare il nome di una query. Le ricerche sono sensibili all’uso di maiuscole e minuscole. |
| **[!UICONTROL Created By]** | Nome della persona che ha creato la query. |
| **[!UICONTROL Client]** | Client utilizzato per la query. |
| **[!UICONTROL Dataset]** | Il set di dati di input utilizzato dalla query. Seleziona il set di dati da passare alla schermata dei dettagli del set di dati di input. |
| **[!UICONTROL Status]** | Lo stato corrente della query. |
| **[!UICONTROL Last Run]** | Quando la query è stata eseguita per ultima. Puoi ordinare l’elenco in ordine crescente o decrescente selezionando la freccia su questa colonna. |
| **[!UICONTROL Run Time]** | Il tempo necessario per eseguire la query. |

## Credenziali

La scheda **[!UICONTROL Credentials]** visualizza le credenziali [!DNL Postgres]. Seleziona l’icona **[!UICONTROL Copy]** accanto a qualsiasi campo per memorizzarne il contenuto nel buffer della tastiera. Per ulteriori informazioni su come utilizzare queste credenziali per connettersi con client esterni, leggere la [guida alla connessione con i client][connect-clients].

![Immagine](../images/ui/overview/credentials.png)

## Passaggi successivi

Ora che hai familiarità con l’ [!DNL Query Service] interfaccia utente su [!DNL Platform], puoi accedere a [!DNL Query Editor] per iniziare a creare progetti di query personalizzati da condividere con altri utenti dell’organizzazione. Per ulteriori informazioni sull’authoring e l’esecuzione di query in [!DNL Query Editor], consulta la [Guida utente dell’editor delle query][query-editor].

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
