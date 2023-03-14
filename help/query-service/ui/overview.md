---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;query;editor query;editor query;editor query;
solution: Experience Platform
title: Guida dell’interfaccia utente di Query Service
description: Adobe Experience Platform Query Service fornisce un’interfaccia utente che può essere utilizzata per scrivere ed eseguire query, visualizzare le query eseguite in precedenza e accedere a quelle salvate dagli utenti della tua organizzazione IMS.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: 5a027200efc22051cca6d4c041e857b2abc7d96f
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 1%

---

# [!DNL Query Service] Guida all’interfaccia utente

Adobe Experience Platform [!DNL Query Service] fornisce un’interfaccia utente che può essere utilizzata per scrivere ed eseguire query, visualizzare le query eseguite in precedenza e accedere a quelle salvate dagli utenti della tua organizzazione IMS. Per accedere all’interfaccia utente in [Adobe Experience Platform](https://platform.adobe.com), seleziona **[!UICONTROL Query]** nel menu di navigazione a sinistra.

## [!DNL Query Editor]

Il [!DNL Query Editor] consente di scrivere ed eseguire query senza utilizzare un client esterno. Seleziona **[!UICONTROL Crea query]** per aprire [!DNL Query Editor] e crea una nuova query. È inoltre possibile accedere al [!DNL Query Editor] selezionando una query dalla **[!UICONTROL Log]** o **[!UICONTROL Modelli]** schede. Selezionando una query eseguita o salvata in precedenza si aprirà la [!DNL Query Editor] e visualizza l&#39;istruzione SQL per la query selezionata.

![Dashboard delle query con Crea query evidenziato.](../images/ui/overview/overview.png)

[!DNL Query Editor] fornisce uno spazio di modifica in cui è possibile iniziare a digitare una query. Durante la digitazione, l&#39;editor completa automaticamente le parole riservate SQL, le tabelle e i nomi dei campi all&#39;interno delle tabelle. Al termine della scrittura della query, selezionare **Play** per eseguire la query. Il **[!UICONTROL Console]** sotto l’editor mostra ciò che [!DNL Query Service] , che indica quando è stata restituita una query. Il **[!UICONTROL Risultato]** accanto alla Console, visualizza i risultati della query. Consulta la [Guida all’editor delle query](./user-guide.md) per ulteriori informazioni sull&#39;utilizzo di [!DNL Query Editor].

![Zoom in visualizzazione della [!DNL Query Editor].](../images/ui/overview/query-editor.png)

## Query pianificate {#scheduled-queries}

È possibile pianificare l&#39;esecuzione di query già salvate come modello con una frequenza regolare. Quando pianifichi una query, puoi scegliere la frequenza delle esecuzioni, la data di inizio e di fine, il giorno della settimana in cui viene eseguita la query pianificata e il set di dati in cui esportare la query. Le pianificazioni delle query vengono impostate mediante l&#39;Editor query.

Per informazioni su come pianificare una query tramite l’interfaccia utente, consulta [guida alle query pianificate](./user-guide.md#scheduled-queries). Per informazioni su come aggiungere pianificazioni utilizzando l’API, leggi la [guida dell’endpoint &quot;scheduled queries&quot;](../api/scheduled-queries.md).

Una volta pianificata, la query viene visualizzata nell’elenco delle query pianificate nel [!UICONTROL Query pianificate] scheda. Per informazioni dettagliate sulla query, sulle esecuzioni, sul creatore e sugli intervalli, seleziona una query pianificata dall’elenco.

![L’area di lavoro Query, con la scheda Query pianificate evidenziata, mostra le righe delle pianificazioni delle query.](../images/ui/overview/scheduled-queries.png)

| Colonna | Descrizione |
| --- | --- |
| **[!UICONTROL Nome]** | Il campo del nome corrisponde al nome del modello o ai primi caratteri della query SQL. Tutte le query create tramite l’interfaccia utente con l’editor delle query sono denominate all’inizio. Se la query è stata creata tramite l’API, il nome della query è un frammento dell’istruzione SQL iniziale utilizzata per creare la query. |
| **[!UICONTROL Modello]** | Nome del modello della query. Selezionate un nome di modello per passare all&#39;editor di query. Il modello di query viene visualizzato nell’editor delle query per comodità. Se non è presente alcun nome di modello, la riga viene contrassegnata con un trattino e non è possibile reindirizzare all’editor delle query per visualizzare la query. |
| **[!UICONTROL SQL]** | Frammento della query SQL. |
| **[!UICONTROL Frequenza di esecuzione]** | Questa è la frequenza con cui la query è impostata per l&#39;esecuzione. I valori disponibili sono `Run once` e `Scheduled`. Le query possono essere filtrate in base alla loro frequenza di esecuzione. |
| **[!UICONTROL Creato da]** | Nome dell&#39;utente che ha creato la query. |
| **[!UICONTROL Creato]** | La marca temporale in formato UTC in cui è stata creata la query. |
| **[!UICONTROL Timestamp dell’ultima esecuzione]** | Il timestamp più recente in cui è stata eseguita la query. In questa colonna viene evidenziato se una query è stata eseguita in base alla pianificazione corrente. |
| **[!UICONTROL Stato ultima esecuzione]** | Stato dell’esecuzione della query più recente. I tre valori di stato sono: `successful` `failed` o `in progress`. |

Consulta la documentazione per ulteriori informazioni su come [monitorare le query tramite l’interfaccia utente di Query Service](./monitor-queries.md).

## Modelli {#browse}

Il **[!UICONTROL Modelli]** Questa scheda mostra le query salvate dagli utenti dell’organizzazione. È utile considerarli come progetti di query, in quanto le query salvate qui potrebbero essere ancora in fase di costruzione. Query visualizzate nel **[!UICONTROL Modelli]** viene visualizzata anche come query di esecuzione nel **[!UICONTROL Log]** , se sono state precedentemente eseguite da [!DNL Query Service].

![Visualizzazione ingrandita della scheda Modelli del dashboard Query che visualizza diverse query salvate.](../images/ui/overview/templates.png)

| Colonna | Descrizione |
| --- | --- |
| **[!UICONTROL Nome]** | Il campo del nome è il nome della query creato dall&#39;utente o i primi caratteri della query SQL. Tutte le query create tramite l’interfaccia utente con l’editor delle query sono denominate all’inizio. Se la query è stata creata tramite l’API, il nome della query è un frammento dell’istruzione SQL iniziale utilizzata per creare la query. È possibile selezionare il nome della query per aprirla in [!DNL Query Editor]. È inoltre possibile utilizzare la barra di ricerca per cercare [!UICONTROL Nome] di una query. Le ricerche distinguono tra maiuscole e minuscole. |
| **[!UICONTROL SQL]** | I primi caratteri della query SQL. Passando il puntatore del mouse sul codice viene visualizzata la query completa. |
| **[!UICONTROL Modificato da]** | Ultimo utente che ha modificato la query. Qualsiasi utente dell’organizzazione con accesso a [!DNL Query Service] può modificare le query. |
| **[!UICONTROL Ultima modifica]** | La data e l’ora dell’ultima modifica alla query, nel fuso orario del browser. |

Consulta la [modelli di query](./query-templates.md) per ulteriori informazioni sui modelli nell’interfaccia utente di Platform.

## Registro {#log}

Il **[!UICONTROL Log]** fornisce un elenco delle query eseguite in precedenza. Per impostazione predefinita, il registro elenca le query in ordine cronologico inverso.

![Visualizzazione ingrandita della scheda Registro del dashboard Query che visualizza un elenco di query in ordine cronologico inverso.](../images/ui/overview/log.png)

| Colonna | Descrizione |
| --- | --- |
| **[!UICONTROL Nome]** | Il nome della query, costituito dai primi caratteri della query SQL. Seleziona il nome del modello per aprire [!UICONTROL Dettagli registro query] vista per l&#39;esecuzione. È possibile utilizzare la barra di ricerca per eseguire una ricerca in base al nome di una query. Le ricerche distinguono tra maiuscole e minuscole. |
| **[!UICONTROL Ora di inizio]** | L’ora in cui è stata eseguita la query. |
| **[!UICONTROL Tempo di completamento]** | L’ora in cui è stata completata la query. |
| **[!UICONTROL Stato]** | Stato corrente della query. |
| **[!UICONTROL Set di dati]** | Set di dati di input utilizzato dalla query. Seleziona il set di dati per passare alla schermata dei dettagli del set di dati di input. |
| **[!UICONTROL Client]** | Client utilizzato per la query. |
| **[!UICONTROL Creato da]** | Nome della persona che ha creato la query. |

>!![Note]
Seleziona l’icona della matita (![Un’icona a forma di matita.](../images/ui/overview/edit-icon.png)) da una riga qualsiasi del registro query per passare al [!DNL Query Editor]. La query è precompilata per facilitarne la modifica.

Consulta la [documentazione dei registri di query](./query-logs.md) per ulteriori informazioni sui file di registro generati automaticamente da un evento di query.

## Credenziali 

Il **[!UICONTROL Credenziali]** nella scheda vengono visualizzate sia le credenziali in scadenza che quelle senza scadenza. Per ulteriori informazioni su come utilizzare queste credenziali per connettersi con client esterni, leggere [guida alle credenziali](../clients/overview.md).

![Il dashboard Query con la scheda Credenziali evidenziata.](../images/ui/overview/credentials.png)

## Passaggi successivi

Ora che conosci [!DNL Query Service] interfaccia utente su [!DNL Platform], puoi accedere a [!DNL Query Editor] per iniziare a creare progetti di query personalizzati da condividere con altri utenti dell’organizzazione. Per ulteriori informazioni sull’authoring e l’esecuzione di query in [!DNL Query Editor], vedere [[!DNL Query Editor] guida utente](./user-guide.md).
