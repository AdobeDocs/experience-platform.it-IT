---
title: Monitorare le query pianificate
description: Scopri come monitorare le query tramite l’interfaccia utente di Query Service.
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: 87b530c0ee509d9f24fc7af63507ff0567779d26
workflow-type: tm+mt
source-wordcount: '1252'
ht-degree: 0%

---

# Monitorare le query pianificate

Adobe Experience Platform fornisce una migliore visibilità dello stato di tutti i processi di query tramite l’interfaccia utente. Da [!UICONTROL Query pianificate] scheda ora puoi trovare informazioni importanti sulle esecuzioni della query, tra cui lo stato, i dettagli della pianificazione e i messaggi/codici di errore in caso di esito negativo. È inoltre possibile abbonarsi agli avvisi per le query basate sul loro stato tramite l’interfaccia utente per una di queste query tramite [!UICONTROL Query pianificate] scheda.

## [!UICONTROL Query pianificate]

Il [!UICONTROL Query pianificate] fornisce una panoramica di tutte le query CTAS e ITAS pianificate. È possibile trovare i dettagli di esecuzione per tutte le query pianificate, nonché i codici di errore e i messaggi per eventuali query non riuscite.

Per passare al [!UICONTROL Query pianificate] , seleziona **[!UICONTROL Query]** dalla barra di navigazione a sinistra seguita da **[!UICONTROL Query pianificate]**

![La scheda Query pianificate nell’area di lavoro Query.](../images/ui/monitor-queries/scheduled-queries.png)

La tabella seguente descrive ogni colonna disponibile.

>[!NOTE]
>
>L’icona di avviso delle sottoscrizioni è contenuta in ogni riga di una colonna senza titolo. Consulta la [avvisi abbonamenti](#alert-subscription) per ulteriori informazioni.

| Colonna | Descrizione |
|---|---|
| **[!UICONTROL Nome]** | Il campo del nome corrisponde al nome del modello o ai primi caratteri della query SQL. Tutte le query create tramite l’interfaccia utente con l’editor delle query sono denominate all’inizio. Se la query è stata creata tramite l’API, il suo nome diventa un frammento dell’istruzione SQL iniziale utilizzata per creare la query. Seleziona un elemento dal [!UICONTROL Nome] per visualizzare un elenco di tutte le esecuzioni associate alla query. Per ulteriori informazioni, consulta [la query esegue i dettagli della pianificazione](#query-runs) sezione. |
| **[!UICONTROL Modello]** | Nome del modello della query. Selezionate un nome di modello per passare all&#39;editor di query. Il modello di query viene visualizzato nell’editor delle query per comodità. Se non è presente alcun nome di modello, la riga viene contrassegnata con un trattino e non è possibile reindirizzare all’editor delle query per visualizzare la query. |
| **[!UICONTROL SQL]** | Frammento della query SQL. |
| **[!UICONTROL Frequenza di esecuzione]** | Questa è la frequenza con cui la query è impostata per l&#39;esecuzione. I valori disponibili sono `Run once` e `Scheduled`. Le query possono essere filtrate in base alla loro frequenza di esecuzione. |
| **[!UICONTROL Creato da]** | Nome dell&#39;utente che ha creato la query. |
| **[!UICONTROL Creato]** | La marca temporale in formato UTC in cui è stata creata la query. |
| **[!UICONTROL Timestamp dell’ultima esecuzione]** | Il timestamp più recente in cui è stata eseguita la query. In questa colonna viene evidenziato se una query è stata eseguita in base alla pianificazione corrente. |
| **[!UICONTROL Stato ultima esecuzione]** | Stato dell’esecuzione della query più recente. I valori dello stato sono: `Success`, `Failed`, `In progress`, e `No runs`. |

>[!TIP]
>
>Se si passa all&#39;editor delle query, è possibile selezionare **[!UICONTROL Query]** per tornare al [!UICONTROL Modelli] scheda.

### Personalizzare le impostazioni della tabella per le query pianificate

È possibile regolare le colonne nel [!UICONTROL Query pianificate] in base alle tue esigenze. Seleziona l’icona delle impostazioni (![Un&#39;icona delle impostazioni.](../images/ui/monitor-queries/settings-icon.png)) per aprire [!UICONTROL Personalizza tabella] impostazioni e modificare le colonne disponibili.

![Icona Personalizza impostazioni tabella.](../images/ui/monitor-queries/customze-table-settings-icon.png)

Per rimuovere o aggiungere una colonna di tabella, attiva o disattiva le caselle di controllo corrispondenti. Quindi, seleziona **[!UICONTROL Applica]** per confermare le scelte effettuate.

>[!NOTE]
>
>Qualsiasi query creata tramite l’interfaccia utente diventa un modello denominato come parte del processo di creazione. Il nome del modello viene visualizzato nella colonna del modello. Se la query è stata creata tramite l’API, la colonna del modello è vuota.

![Finestra di dialogo Personalizza impostazioni tabella.](../images/ui/monitor-queries/customize-table-dialog.png)

### Iscriviti agli avvisi {#alert-subscription}

È possibile abbonarsi agli avvisi dal [!UICONTROL Query pianificate] scheda. Seleziona l’icona di notifica dell’avviso (![Un&#39;icona di avviso.](../images/ui/monitor-queries/alerts-icon.png)) accanto al nome di una query per aprire [!UICONTROL Avvisi] . Il [!UICONTROL Avvisi] La finestra di dialogo si abbona sia alle notifiche dell’interfaccia utente che agli avvisi e-mail. Gli avvisi si basano sullo stato della query. Sono disponibili tre opzioni: `start`, `success`, e `failure`. Seleziona la casella o le caselle appropriate e seleziona **[!UICONTROL Salva]** per iscriversi.

![Finestra di dialogo Sottoscrizioni avvisi.](../images/ui/monitor-queries/alert-subscription-dialog.png)

Consulta la [documentazione API per le sottoscrizioni di avvisi](../api/alert-subscriptions.md) per ulteriori informazioni.

### Filtrare le query {#filter}

Puoi filtrare le query in base alla frequenza di esecuzione. Dalla sezione [!UICONTROL Query pianificate] , seleziona l’icona del filtro (![Icona filtro](../images/ui/monitor-queries/filter-icon.png)) per aprire la barra laterale del filtro.

![Scheda Query pianificate con l’icona del filtro evidenziata.](../images/ui/monitor-queries/filter-queries.png)

Seleziona una delle seguenti opzioni **[!UICONTROL Pianificato]** o **[!UICONTROL Esegui una volta]** per filtrare l’elenco delle query, esegui le caselle di controllo relative ai filtri di frequenza.

>[!NOTE]
>
>Qualsiasi query eseguita ma non pianificata può essere considerata [!UICONTROL Esegui una volta].

![Scheda Query pianificate con la barra laterale dei filtri evidenziata.](../images/ui/monitor-queries/filter-sidebar.png)

Dopo aver abilitato i criteri di filtro, seleziona **[!UICONTROL Nascondi filtri]** per chiudere il pannello dei filtri.

## La query esegue i dettagli della pianificazione {#query-runs}

Selezionare un nome di query per passare alla pagina dei dettagli della pianificazione. Questa vista fornisce un elenco di tutte le esecuzioni eseguite come parte della query pianificata. Le informazioni fornite includono l’ora di inizio e di fine, lo stato e il set di dati utilizzati.

![La pagina dei dettagli della pianificazione.](../images/ui/monitor-queries/schedule-details.png)

Queste informazioni sono fornite in una tabella a cinque colonne. Ogni riga indica un’esecuzione di query.

| Nome colonna | Descrizione |
|---|---|
| **[!UICONTROL ID esecuzione query]** | ID esecuzione query per l’esecuzione giornaliera. Seleziona la **[!UICONTROL ID esecuzione query]** per passare al [!UICONTROL Panoramica sull’esecuzione delle query]. |
| **[!UICONTROL Inizio esecuzione query]** | Il timestamp in cui è stata eseguita la query. In formato UTC. |
| **[!UICONTROL Esecuzione query completata]** | La marca temporale in cui è stata completata la query. In formato UTC. |
| **[!UICONTROL Stato]** | Stato dell’esecuzione della query più recente. I tre valori di stato sono: `successful` `failed` o `in progress`. |
| **[!UICONTROL Set di dati]** | Il set di dati coinvolto nell’esecuzione. |

I dettagli della query pianificata sono disponibili nella sezione [!UICONTROL Proprietà] pannello. Questo pannello include l’ID della query iniziale, il tipo di client, il nome del modello, l’SQL della query e la frequenza della pianificazione.

![La pagina dei dettagli della pianificazione con il pannello delle proprietà evidenziato.](../images/ui/monitor-queries/properties-panel.png)

Selezionare un ID esecuzione query per passare alla pagina dei dettagli esecuzione e visualizzare le informazioni sulla query.

![La schermata dei dettagli della pianificazione con un ID esecuzione evidenziato.](../images/ui/monitor-queries/navigate-to-run-details.png)

## Panoramica sull’esecuzione delle query {#query-run-overview}

Il [!UICONTROL Panoramica sull’esecuzione delle query] fornisce informazioni sulle singole esecuzioni per questa query pianificata e un raggruppamento più dettagliato dello stato di esecuzione. Questa pagina include anche le informazioni sul client e i dettagli di eventuali errori che potrebbero aver causato l’esito negativo della query.

![La schermata dei dettagli dell’esecuzione con la sezione panoramica evidenziata.](../images/ui/monitor-queries/query-run-details.png)

La sezione sullo stato della query fornisce il codice di errore e il messaggio di errore in caso di errore della query.

![La schermata dei dettagli dell’esecuzione con la sezione errori evidenziata.](../images/ui/monitor-queries/failed-query.png)

Da questa vista è possibile copiare l&#39;istruzione SQL per query negli Appunti. Selezionare l&#39;icona Copia in alto a destra dello snippet SQL per copiare la query. Un messaggio a comparsa conferma che il codice è stato copiato.

![La schermata dei dettagli dell&#39;esecuzione con l&#39;icona Copia SQL evidenziata.](../images/ui/monitor-queries/copy-sql.png)

### Eseguire i dettagli per le query con blocco anonimo {#anonymous-block-queries}

Le query che utilizzano blocchi anonimi per comporre le istruzioni SQL vengono separate nelle singole sottoquery. Questo consente di esaminare i dettagli di esecuzione per ogni blocco di query singolarmente.

>[!NOTE]
>
>I dettagli di esecuzione di un blocco anonimo che utilizza il comando DROP **non** essere segnalato come sottoquery separata. Sono disponibili dettagli di esecuzione separati per le query CTAS, le query ITAS e le istruzioni COPY utilizzate come sottoquery di blocco anonime. I dettagli di esecuzione del comando DROP non sono attualmente supportati.

I blocchi anonimi sono identificati mediante l’uso di un `$$` prima della query. Consulta la [documento blocco anonimo](../essential-concepts/anonymous-block.md) per ulteriori informazioni sui blocchi anonimi in query service.

Le sottoquery di blocco anonime dispongono di schede a sinistra dello stato di esecuzione. Selezionare una scheda per visualizzare i dettagli dell&#39;esecuzione.

![Panoramica dell’esecuzione della query con una query di blocco anonima. Vengono evidenziate più schede di query.](../images/ui/monitor-queries/anonymous-block-overview.png)

Nel caso in cui una query di blocco anonimo non riesca, puoi trovare il codice di errore per quel particolare blocco tramite questa interfaccia utente.

![Nella panoramica dell’esecuzione della query viene visualizzata una query di blocco anonima con il codice di errore per un singolo blocco evidenziato.](../images/ui/monitor-queries/anonymous-block-failed-query.png)

Seleziona **[!UICONTROL Query]** per tornare alla schermata dettagli pianificazione, oppure **[!UICONTROL Query pianificate]** per tornare al [!UICONTROL Query pianificate] scheda.

![La schermata dei dettagli dell’esecuzione con Query evidenziata.](../images/ui/monitor-queries/return-navigation.png)

<!-- Details required to complete this section below:
### Run details for queries with parameterized queries {#parameterized-queries}

Queries that use parameterized values to make up the SQL statement are ... 
-->
