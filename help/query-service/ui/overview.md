---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;editor query;editor query;editor query;editor query;editor query;editor query;
solution: Experience Platform
title: Guida all’interfaccia utente del servizio query
topic-legacy: guide
description: Adobe Experience Platform Query Service fornisce un’interfaccia utente che può essere utilizzata per scrivere ed eseguire query, visualizzare query eseguite in precedenza e accedere alle query salvate dagli utenti all’interno dell’organizzazione IMS.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: 30c3ca4aa3e8f42140566c8fdf9fbc855ec72e1b
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 2%

---

# [!DNL Query Service] guida

Adobe Experience Platform [!DNL Query Service] fornisce un&#39;interfaccia utente che può essere utilizzata per scrivere ed eseguire query, visualizzare query eseguite in precedenza e accedere alle query salvate dagli utenti all&#39;interno dell&#39;organizzazione IMS. Per accedere all&#39;interfaccia utente di [Adobe Experience Platform](https://platform.adobe.com), seleziona **[!UICONTROL Query]** nel menu di navigazione a sinistra.

## [!DNL Query Editor]

[!DNL Query Editor] consente di scrivere ed eseguire query senza utilizzare un client esterno. Seleziona **[!UICONTROL Crea query]** per aprire [!DNL Query Editor] e creare una nuova query. Puoi anche accedere a [!DNL Query Editor] selezionando una query dalle schede **[!UICONTROL Log]** o **[!UICONTROL Sfoglia]**. Quando si seleziona una query eseguita o salvata in precedenza, viene aperto il [!DNL Query Editor] e viene visualizzato il SQL per la query selezionata.

![Immagine](../images/ui/overview/overview.png)

[!DNL Query Editor] fornisce uno spazio di modifica in cui iniziare a digitare una query. Mentre si digita, l&#39;editor completa automaticamente le parole riservate SQL, le tabelle e i nomi di campo all&#39;interno delle tabelle. Al termine della scrittura della query, selezionare il pulsante **Play** per eseguire la query. La scheda **[!UICONTROL Console]** sotto l&#39;editor mostra le operazioni attualmente eseguite da [!DNL Query Service], indicando quando è stata restituita una query. La scheda **[!UICONTROL Risultato]**, accanto alla console, visualizza i risultati della query. Per ulteriori informazioni sull&#39;utilizzo di [!DNL Query Editor], consulta la [Guida all&#39;editor delle query](./user-guide.md) .

![Immagine](../images/ui/overview/query-editor.png)

## Sfoglia

La scheda **[!UICONTROL Sfoglia]** mostra le query salvate dagli utenti dell’organizzazione. È utile considerarli come progetti di query, in quanto le query salvate qui potrebbero essere ancora in costruzione. Le query visualizzate nella scheda **[!UICONTROL Sfoglia]** vengono visualizzate anche come query di esecuzione nella scheda **[!UICONTROL Registro]** se sono state eseguite in precedenza da [!DNL Query Service].

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
| **[!UICONTROL Nome]** | Nome della query, costituito dai primi caratteri della query SQL. Selezionando il nome si apre il [!DNL Query Editor], che consente di modificare la query. È possibile utilizzare la barra di ricerca per cercare il nome di una query. Le ricerche sono sensibili all’uso di maiuscole e minuscole. |
| **[!UICONTROL Creato da]** | Nome della persona che ha creato la query. |
| **[!UICONTROL Client]** | Client utilizzato per la query. |
| **[!UICONTROL Set di dati]** | Il set di dati di input utilizzato dalla query. Seleziona il set di dati da passare alla schermata dei dettagli del set di dati di input. |
| **[!UICONTROL Stato]** | Lo stato corrente della query. |
| **[!UICONTROL Ultima esecuzione]** | Quando la query è stata eseguita per ultima. Puoi ordinare l’elenco in ordine crescente o decrescente selezionando la freccia su questa colonna. |
| **[!UICONTROL Tempo di esecuzione]** | Il tempo necessario per eseguire la query. |

## Credenziali

La scheda **[!UICONTROL Credenziali]** visualizza le credenziali in scadenza e non in scadenza. Per ulteriori informazioni su come utilizzare queste credenziali per connettersi con client esterni, consulta la [guida alle credenziali](../clients/overview.md).

![Immagine](../images/ui/overview/credentials.png)

## Passaggi successivi

Ora che hai familiarità con l’ [!DNL Query Service] interfaccia utente su [!DNL Platform], puoi accedere a [!DNL Query Editor] per iniziare a creare progetti di query personalizzati da condividere con altri utenti dell’organizzazione. Per ulteriori informazioni sull’authoring e l’esecuzione di query in [!DNL Query Editor], consulta la [Guida utente dell’editor delle query](./user-guide.md).