---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;query;editor query;editor query;editor query;
solution: Experience Platform
title: Guida dell’interfaccia utente di Query Service
description: Adobe Experience Platform Query Service fornisce un’interfaccia utente che può essere utilizzata per scrivere ed eseguire query, visualizzare le query eseguite in precedenza e accedere a quelle salvate dagli utenti della tua organizzazione.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 1%

---

# Guida dell&#39;interfaccia utente di [!DNL Query Service]

In Adobe Experience Platform [!DNL Query Service] è disponibile un&#39;interfaccia utente che può essere utilizzata per scrivere ed eseguire query, visualizzare le query eseguite in precedenza e accedere a quelle salvate dagli utenti dell&#39;organizzazione. Per accedere all&#39;interfaccia utente in [Adobe Experience Platform](https://platform.adobe.com), seleziona **[!UICONTROL Query]** nell&#39;area di navigazione a sinistra.

## [!DNL Query Editor]

[!DNL Query Editor] consente di scrivere ed eseguire query senza utilizzare un client esterno. Selezionare **[!UICONTROL Crea query]** per aprire [!DNL Query Editor] e creare una nuova query. Puoi anche accedere a [!DNL Query Editor] selezionando una query dalle schede **[!UICONTROL Registro]** o **[!UICONTROL Modelli]**. Se si seleziona una query salvata o eseguita in precedenza, verrà aperto [!DNL Query Editor] e verrà visualizzato il codice SQL per la query selezionata.

![Dashboard delle query con l&#39;opzione Crea query evidenziata.](../images/ui/overview/overview.png)

[!DNL Query Editor] fornisce uno spazio di modifica in cui è possibile iniziare a digitare una query. Durante la digitazione, l&#39;editor completa automaticamente le parole riservate SQL, le tabelle e i nomi dei campi all&#39;interno delle tabelle. Al termine della scrittura della query, selezionare il pulsante **Riproduci** per eseguire la query. La scheda **[!UICONTROL Console]** sotto l&#39;editor mostra ciò che [!DNL Query Service] sta facendo, indicando quando è stata restituita una query. Nella scheda **[!UICONTROL Risultato]** accanto alla console vengono visualizzati i risultati della query. Per ulteriori informazioni sull&#39;utilizzo di [!DNL Query Editor], vedere la [Guida dell&#39;editor di query](./user-guide.md).

![Visualizzazione ingrandita di [!DNL Query Editor].](../images/ui/overview/query-editor.png)

## Query pianificate {#scheduled-queries}

È possibile pianificare l&#39;esecuzione di query già salvate come modello con una frequenza regolare. Quando pianifichi una query, puoi scegliere la frequenza delle esecuzioni, la data di inizio e di fine, il giorno della settimana in cui viene eseguita la query pianificata e il set di dati in cui esportare la query. Le pianificazioni delle query vengono impostate mediante l&#39;Editor query.

Per informazioni su come pianificare una query tramite l&#39;interfaccia utente, consulta la [guida delle query pianificate](./user-guide.md#scheduled-queries). Per informazioni su come aggiungere pianificazioni utilizzando l&#39;API, leggere la [guida dell&#39;endpoint per le query pianificate](../api/scheduled-queries.md).

Una volta pianificata, la query viene visualizzata nell&#39;elenco delle query pianificate nella scheda [!UICONTROL Query pianificate]. Per informazioni dettagliate sulla query, sulle esecuzioni, sul creatore e sugli intervalli, seleziona una query pianificata dall’elenco.

![Area di lavoro Query con la scheda Query pianificate evidenziata e visualizzazione delle righe delle pianificazioni delle query.](../images/ui/overview/scheduled-queries.png)

| Colonna | Descrizione |
| --- | --- |
| **[!UICONTROL Nome]** | Il campo del nome corrisponde al nome del modello o ai primi caratteri della query SQL. Tutte le query create tramite l’interfaccia utente con l’editor delle query sono denominate all’inizio. Se la query è stata creata tramite l’API, il nome della query è un frammento dell’istruzione SQL iniziale utilizzata per creare la query. |
| **[!UICONTROL Modello]** | Nome del modello della query. Selezionate un nome di modello per passare all&#39;editor di query. Il modello di query viene visualizzato nell’editor delle query per comodità. Se non è presente alcun nome di modello, la riga viene contrassegnata con un trattino e non è possibile reindirizzare all’editor delle query per visualizzare la query. |
| **[!UICONTROL SQL]** | Frammento della query SQL. |
| **[!UICONTROL Frequenza di esecuzione]** | Questa è la frequenza con cui la query è impostata per l&#39;esecuzione. I valori disponibili sono `Run once` e `Scheduled`. Le query possono essere filtrate in base alla loro frequenza di esecuzione. |
| **[!UICONTROL Creato da]** | Nome dell&#39;utente che ha creato la query. |
| **[!UICONTROL Creato]** | La marca temporale in formato UTC in cui è stata creata la query. |
| **[!UICONTROL Timestamp ultima esecuzione]** | Il timestamp più recente in cui è stata eseguita la query. In questa colonna viene evidenziato se una query è stata eseguita in base alla pianificazione corrente. |
| **[!UICONTROL Stato ultima esecuzione]** | Stato dell’esecuzione della query più recente. I tre valori di stato sono: `successful` `failed` o `in progress`. |

Per ulteriori informazioni su come [monitorare le query tramite l&#39;interfaccia utente di Query Service](./monitor-queries.md), vedere la documentazione.

## Modelli {#browse}

La scheda **[!UICONTROL Modelli]** mostra le query salvate dagli utenti dell&#39;organizzazione. È utile considerarli come progetti di query, in quanto le query salvate qui potrebbero essere ancora in fase di costruzione. Le query visualizzate nella scheda **[!UICONTROL Modelli]** vengono visualizzate anche come query di esecuzione nella scheda **[!UICONTROL Registro]** se sono state precedentemente eseguite da [!DNL Query Service].

![Visualizzazione ingrandita della scheda Modelli del dashboard delle query che visualizza diverse query salvate.](../images/ui/overview/templates.png)

| Colonna | Descrizione |
| --- | --- |
| **[!UICONTROL Nome]** | Il campo del nome è il nome della query creato dall&#39;utente o i primi caratteri della query SQL. Tutte le query create tramite l’interfaccia utente con l’editor delle query sono denominate all’inizio. Se la query è stata creata tramite l’API, il nome della query è un frammento dell’istruzione SQL iniziale utilizzata per creare la query. È possibile selezionare il nome della query per aprire la query in [!DNL Query Editor]. È inoltre possibile utilizzare la barra di ricerca per cercare il [!UICONTROL Nome] di una query. Le ricerche distinguono tra maiuscole e minuscole. |
| **[!UICONTROL SQL]** | I primi caratteri della query SQL. Passando il puntatore del mouse sul codice viene visualizzata la query completa. |
| **[!UICONTROL Modificato da]** | Ultimo utente che ha modificato la query. Qualsiasi utente dell&#39;organizzazione con accesso a [!DNL Query Service] può modificare le query. |
| **[!UICONTROL Ultima modifica]** | La data e l’ora dell’ultima modifica alla query, nel fuso orario del browser. |

Per ulteriori informazioni sui modelli nell&#39;interfaccia utente di Platform, consulta la documentazione dei [modelli di query](./query-templates.md).

## Registro {#log}

La scheda **[!UICONTROL Registro]** fornisce un elenco delle query eseguite in precedenza. Per impostazione predefinita, il registro elenca le query in ordine cronologico inverso.

![Visualizzazione ingrandita della scheda Registro del dashboard delle query con un elenco delle query in ordine cronologico inverso.](../images/ui/overview/log.png)

| Colonna | Descrizione |
| --- | --- |
| **[!UICONTROL Nome]** | Il nome della query, costituito dai primi caratteri della query SQL. Selezionare il nome del modello per aprire la visualizzazione [!UICONTROL Dettagli registro query] per l&#39;esecuzione. È possibile utilizzare la barra di ricerca per eseguire una ricerca in base al nome di una query. Le ricerche distinguono tra maiuscole e minuscole. |
| **[!UICONTROL Ora di inizio]** | L’ora in cui è stata eseguita la query. |
| **[!UICONTROL Ora di completamento]** | L’ora in cui è stata completata la query. |
| **[!UICONTROL Stato]** | Stato corrente della query. |
| **[!UICONTROL Set di dati]** | Set di dati di input utilizzato dalla query. Seleziona il set di dati per passare alla schermata dei dettagli del set di dati di input. |
| **[!UICONTROL Client]** | Client utilizzato per la query. |
| **[!UICONTROL Creato da]** | Nome della persona che ha creato la query. |

>
>
>Selezionare l&#39;icona della matita (![Un&#39;icona della matita.](/help/images/icons/edit.png)) da qualsiasi riga del registro query per passare a [!DNL Query Editor]. La query è precompilata per facilitarne la modifica.

Per ulteriori informazioni sui file di registro generati automaticamente da un evento di query, consulta la [documentazione dei registri di query](./query-logs.md).

## Credenziali

Nella scheda **[!UICONTROL Credenziali]** vengono visualizzate le credenziali sia in scadenza che non in scadenza. Per ulteriori informazioni su come utilizzare queste credenziali per connettersi con client esterni, leggere la [guida delle credenziali](../clients/overview.md).

![Dashboard delle query con la scheda Credenziali evidenziata.](../images/ui/overview/credentials.png)

## Passaggi successivi

Ora che hai familiarità con l&#39;interfaccia utente di [!DNL Query Service] su [!DNL Platform], puoi accedere a [!DNL Query Editor] per iniziare a creare progetti di query personalizzati da condividere con altri utenti dell&#39;organizzazione. Per ulteriori informazioni sull&#39;authoring e l&#39;esecuzione di query in [!DNL Query Editor], vedere la [[!DNL Query Editor] guida utente](./user-guide.md).
