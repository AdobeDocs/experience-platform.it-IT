---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;editor query;editor query;editor query;editor query;editor query;editor query;
solution: Experience Platform
title: Guida all’interfaccia utente del servizio query
description: Adobe Experience Platform Query Service fornisce un’interfaccia utente che può essere utilizzata per scrivere ed eseguire query, visualizzare query eseguite in precedenza e accedere alle query salvate dagli utenti all’interno dell’organizzazione IMS.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 1%

---

# [!DNL Query Service] Guida all’interfaccia utente

Adobe Experience Platform [!DNL Query Service] fornisce un’interfaccia utente che può essere utilizzata per scrivere ed eseguire query, visualizzare query eseguite in precedenza e accedere alle query salvate dagli utenti all’interno dell’organizzazione IMS. Per accedere all’interfaccia in [Adobe Experience Platform](https://platform.adobe.com), seleziona **[!UICONTROL Query]** nella navigazione a sinistra.

## [!DNL Query Editor]

La [!DNL Query Editor] consente di scrivere ed eseguire query senza utilizzare un client esterno. Seleziona **[!UICONTROL Crea query]** per aprire [!DNL Query Editor] e crea una nuova query. Puoi anche accedere al [!DNL Query Editor] selezionando una query dal **[!UICONTROL Registro]** o **[!UICONTROL Modelli]** schede. Quando si seleziona una query eseguita o salvata in precedenza, viene aperta la [!DNL Query Editor] e visualizza l&#39;istruzione SQL per la query selezionata.

![Il dashboard Query con Crea query evidenziato.](../images/ui/overview/overview.png)

[!DNL Query Editor] fornisce uno spazio di modifica in cui iniziare a digitare una query. Mentre si digita, l&#39;editor completa automaticamente le parole riservate SQL, le tabelle e i nomi di campo all&#39;interno delle tabelle. Al termine della scrittura della query, seleziona la **Play** per eseguire la query. La **[!UICONTROL Console]** la scheda sotto l’editor mostra cosa [!DNL Query Service] è in corso, per indicare quando è stata restituita una query. La **[!UICONTROL Risultato]** accanto alla console vengono visualizzati i risultati delle query. Consulta la sezione [Guida all’editor delle query](./user-guide.md) per ulteriori informazioni sull&#39;utilizzo di [!DNL Query Editor].

![Uno zoom in vista del [!DNL Query Editor].](../images/ui/overview/query-editor.png)

## Query pianificate {#scheduled-queries}

Le query già salvate come modello possono essere programmate per essere eseguite con cadenza regolare. Quando pianifichi una query, puoi scegliere la frequenza delle esecuzioni, la data di inizio e di fine, il giorno della settimana in cui viene eseguita la query pianificata e il set di dati in cui esportare la query. Le pianificazioni delle query vengono impostate utilizzando l’Editor query.

Per informazioni su come pianificare una query tramite l’interfaccia utente, consulta [guida alle query pianificate](./user-guide.md#scheduled-queries). Per informazioni su come aggiungere le pianificazioni utilizzando l’API, leggi la [guida all’endpoint delle query pianificate](../api/scheduled-queries.md).

Una volta pianificata una query, questa viene visualizzata nell’elenco delle query pianificate nella [!UICONTROL Query pianificate] scheda . Per informazioni complete sulla query, le esecuzioni, il creatore e gli intervalli, seleziona una query pianificata dall’elenco.

![Area di lavoro Query con la scheda Query pianificate evidenziata e visualizzazione delle righe delle pianificazioni delle query.](../images/ui/overview/scheduled-queries.png)

| Colonna | Descrizione |
| --- | --- |
| **[!UICONTROL Nome]** | Il campo nome è il nome del modello o i primi caratteri della query SQL. All’inizio viene denominato qualsiasi query creata tramite l’interfaccia utente con l’Editor query. Se la query è stata creata tramite l’API, il nome della query è uno snippet dell’SQL iniziale utilizzato per creare la query. |
| **[!UICONTROL Modello]** | Nome del modello della query. Selezionare un nome di modello per passare all’Editor query. Il modello di query viene visualizzato nell’Editor query per comodità. Se non è presente un nome di modello, la riga viene contrassegnata con un trattino e non è possibile reindirizzare all’Editor query per visualizzare la query. |
| **[!UICONTROL SQL]** | Frammento della query SQL. |
| **[!UICONTROL Frequenza di esecuzione]** | Questa è la cadenza alla quale la query è impostata per essere eseguita. I valori disponibili sono `Run once` e `Scheduled`. Le query possono essere filtrate in base alla loro frequenza di esecuzione. |
| **[!UICONTROL Creato da]** | Nome dell’utente che ha creato la query. |
| **[!UICONTROL Creato]** | La marca temporale alla creazione della query, in formato UTC. |
| **[!UICONTROL Timestamp ultima esecuzione]** | La marca temporale più recente all’esecuzione della query. Questa colonna evidenzia se una query è stata eseguita in base alla pianificazione corrente. |
| **[!UICONTROL Stato dell&#39;ultima esecuzione]** | Lo stato dell’esecuzione della query più recente. I tre valori di stato sono: `successful` `failed` o `in progress`. |

Consulta la documentazione per ulteriori informazioni su come [monitorare le query tramite l’interfaccia utente del servizio query](../monitor-queries.md).

## Modelli {#browse}

La **[!UICONTROL Modelli]** mostra le query salvate dagli utenti dell’organizzazione. È utile considerarli come progetti di query, in quanto le query salvate qui potrebbero essere ancora in costruzione. Query visualizzate nel **[!UICONTROL Modelli]** viene visualizzata anche come query di esecuzione nella scheda **[!UICONTROL Registro]** se sono stati eseguiti in precedenza da [!DNL Query Service].

![Una visualizzazione ingrandita della scheda Modelli dashboard Query che mostra diverse query salvate.](../images/ui/overview/templates.png)

| Colonna | Descrizione |
| --- | --- |
| **[!UICONTROL Nome]** | Il campo nome è il nome della query creato dall&#39;utente o i primi caratteri della query SQL. All’inizio viene denominato qualsiasi query creata tramite l’interfaccia utente con l’Editor query. Se la query è stata creata tramite l’API, il nome della query è uno snippet dell’SQL iniziale utilizzato per creare la query. Puoi selezionare il nome della query per aprire la query nella [!DNL Query Editor]. È inoltre possibile utilizzare la barra di ricerca per cercare [!UICONTROL Nome] di una query. Le ricerche sono sensibili all’uso di maiuscole e minuscole. |
| **[!UICONTROL SQL]** | I primi caratteri della query SQL. Passando il puntatore del mouse sul codice viene visualizzata la query completa. |
| **[!UICONTROL Modificato da]** | Ultimo utente che ha modificato la query. Qualsiasi utente della tua organizzazione con accesso a [!DNL Query Service] può modificare le query. |
| **[!UICONTROL Ultima modifica]** | La data e l’ora dell’ultima modifica alla query, nel fuso orario del browser. |

## Registro

La **[!UICONTROL Registro]** fornisce un elenco delle query che sono state eseguite in precedenza. Per impostazione predefinita, il registro elenca le query nella cronologia inversa.

![Una visualizzazione ingrandita della scheda Registro dashboard Query che visualizza un elenco di query in ordine cronologico inverso.](../images/ui/overview/log.png)

| Colonna | Descrizione |
| --- | --- |
| **[!UICONTROL Nome]** | Nome della query, costituito dai primi caratteri della query SQL. Selezionando il nome si apre la [!DNL Query Editor], che consente di modificare la query. È possibile utilizzare la barra di ricerca per cercare il nome di una query. Le ricerche sono sensibili all’uso di maiuscole e minuscole. |
| **[!UICONTROL Creato da]** | Nome della persona che ha creato la query. |
| **[!UICONTROL Client]** | Client utilizzato per la query. |
| **[!UICONTROL Set di dati]** | Il set di dati di input utilizzato dalla query. Seleziona il set di dati da passare alla schermata dei dettagli del set di dati di input. |
| **[!UICONTROL Stato]** | Lo stato corrente della query. |
| **[!UICONTROL Ultima esecuzione]** | Quando la query è stata eseguita per ultima. Puoi ordinare l’elenco in ordine crescente o decrescente selezionando la freccia su questa colonna. |
| **[!UICONTROL Tempo di esecuzione]** | Il tempo necessario per eseguire la query. |

## Credenziali 

La **[!UICONTROL Credenziali]** visualizza le credenziali in scadenza e non in scadenza. Per ulteriori informazioni su come utilizzare queste credenziali per la connessione con client esterni, leggere il [guida alle credenziali](../clients/overview.md).

![Dashboard Query con la scheda Credenziali evidenziata.](../images/ui/overview/credentials.png)

## Passaggi successivi

Ora che hai familiarità con [!DNL Query Service] interfaccia utente attiva [!DNL Platform], puoi accedere a [!DNL Query Editor] per iniziare a creare progetti di query personalizzati da condividere con altri utenti dell’organizzazione. Per ulteriori informazioni sull’authoring e l’esecuzione di query in [!DNL Query Editor], vedi [[!DNL Query Editor] guida utente](./user-guide.md).