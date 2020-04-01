---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida all'interfaccia utente di Adobe Experience Platform Query Service
topic: guide
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce

---


# Guida al servizio query

Adobe Experience Platform Query Service fornisce un&#39;interfaccia utente che può essere utilizzata per scrivere ed eseguire query, visualizzare query eseguite in precedenza e query di accesso salvate dagli utenti all&#39;interno dell&#39;organizzazione IMS. Per accedere all&#39;interfaccia utente in [Adobe Experience Platform][platform-ui], seleziona **Query** nel menu di navigazione a sinistra.

## Editor query

L&#39;Editor query consente di scrivere ed eseguire query senza utilizzare un client esterno. Fate clic su **Crea query** per aprire l&#39;Editor query e creare una nuova query. È inoltre possibile accedere all&#39;Editor query selezionando una query dalle schede *Registro* o *Sfoglia* . Se si seleziona una query precedentemente eseguita o salvata, verrà aperto l&#39;Editor query e verrà visualizzato l&#39;SQL per la query selezionata.

![Immagine](../images/queries/ui-overview/overview.png)

Editor query fornisce spazio di modifica in cui è possibile iniziare a digitare una query. Durante la digitazione, l&#39;editor completa automaticamente le parole riservate, le tabelle e i nomi di campo SQL all&#39;interno delle tabelle. Al termine, fate clic su **Riproduci** per eseguire la query. La scheda *Console* sotto l&#39;editor mostra le operazioni eseguite dal servizio Query, indicando quando è stata restituita una query. Nella scheda *Risultato* , accanto alla console, sono visualizzati i risultati della query. Per ulteriori informazioni sull&#39;utilizzo dell&#39;editor di query, vedere la guida [all&#39;editor di][query-editor] query.

![Immagine](../images/queries/ui-overview/query-editor.png)

## Sfoglia

La scheda *Sfoglia* mostra le query salvate dagli utenti nell&#39;organizzazione. È utile considerarli come progetti di query, in quanto le query salvate qui potrebbero essere ancora in costruzione. Le query visualizzate nella scheda *Sfoglia* vengono visualizzate anche come query di esecuzione nella scheda *Registro* , se sono state eseguite in precedenza da Servizio query.

![Immagine](../images/queries/ui-overview/browse.png)

| Colonna | Descrizione |
| --- | --- |
| Nome | Nome della query creata dall&#39;utente. È possibile fare clic sul nome per aprire la query nell&#39;Editor query. È inoltre possibile utilizzare la barra di ricerca per effettuare ricerche in base al nome di una query. Le ricerche sono con distinzione tra maiuscole e minuscole. |
| SQL | I primi caratteri della query SQL. Quando passi il puntatore del mouse sul codice viene visualizzata la query completa. |
| Modificato da | Ultimo utente che ha modificato la query. Qualsiasi utente dell&#39;organizzazione con accesso a Query Service può modificare le query. |
| Ultima modifica | Data e ora dell’ultima modifica apportata alla query, nel fuso orario del browser. |

## Registro

La scheda *Registro* fornisce un elenco delle query che sono state eseguite in precedenza. Per impostazione predefinita, il registro elenca le query nella cronologia inversa.

![Immagine](../images/queries/ui-overview/log.png)

| Colonna | Descrizione |
| --- | --- |
| Nome | Il nome della query, costituito dai primi caratteri della query SQL. Facendo clic sul nome si apre l&#39;Editor query, che consente di modificare la query. È possibile utilizzare la barra di ricerca per effettuare ricerche in base al nome di una query. Le ricerche sono con distinzione tra maiuscole e minuscole. |
| Creato da | Nome della persona che ha creato la query. |
| Client | Client utilizzato per la query. |
| Set di dati | Set di dati di input utilizzato dalla query. Fare clic sul set di dati per passare alla schermata dei dettagli del set di dati di input. |
| Stato | Stato corrente della query. |
| Ultima esecuzione | Quando la query è stata eseguita per ultima. Potete ordinare l’elenco in ordine crescente o decrescente facendo clic sulla freccia su questa colonna. |
| Tempo di esecuzione | Il tempo necessario per eseguire la query. |

## Credenziali

Nella scheda *Credenziali* sono visualizzate le credenziali Post. Fare clic sull&#39;icona **Copia** accanto a un campo per memorizzarne il contenuto nel buffer della tastiera. Per ulteriori informazioni sull&#39;utilizzo di queste credenziali per la connessione con client esterni, consultare la guida [alla][connect-clients]connessione con i client.

![Immagine](../images/queries/ui-overview/credentials.png)

## Passaggi successivi

Ora che si ha familiarità con l&#39;interfaccia utente di Query Service sulla piattaforma, è possibile accedere a Query Editor per iniziare a creare i propri progetti di query da condividere con altri utenti dell&#39;organizzazione. Per ulteriori informazioni sull&#39;authoring e l&#39;esecuzione di query in Editor query, consultare la guida [utente dell&#39;Editor][query-editor]query.

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
