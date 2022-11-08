---
title: Monitoraggio delle query
description: Scopri come monitorare le query tramite l’interfaccia utente del servizio query.
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: a9887535b12b8c4aeb39bb5a6646da88db4f0308
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 0%

---

# Monitorare le query

Adobe Experience Platform offre una migliore visibilità dello stato di tutti i processi di query tramite l’interfaccia utente. Da [!UICONTROL Query pianificate] è ora possibile trovare informazioni importanti sulle esecuzioni della query che includono lo stato, i dettagli della pianificazione e i messaggi/codici di errore in caso di errore. Puoi anche abbonarti agli avvisi per le query in base al loro stato tramite l’interfaccia utente per ognuna di queste query tramite [!UICONTROL Query pianificate] scheda .

## [!UICONTROL Query pianificate]

La [!UICONTROL Query pianificate] fornisce una panoramica delle query eseguite e pianificate. L&#39;area di lavoro contiene tutte le query CTAS e ITAS pianificate per l&#39;esecuzione o eseguite almeno una volta. È possibile trovare dettagli di esecuzione per tutte le query pianificate, nonché codici di errore e messaggi per le query non riuscite.

Per passare al [!UICONTROL Query pianificate] scheda , seleziona **[!UICONTROL Query]** dalla barra di navigazione a sinistra seguita da **[!UICONTROL Query pianificate]**

![Scheda Query pianificate nell’area di lavoro Query.](./images/monitor-queries/scheduled-queries.png)

La tabella seguente descrive ogni colonna disponibile.

>[!NOTE]
>
>L’icona delle sottoscrizioni di avvisi è contenuta in ogni riga di una colonna senza titolo. Consulta la sezione [sottoscrizioni di avvisi](#alert-subscription) per ulteriori informazioni.

| Colonna | Descrizione |
|---|---|
| Nome | Il campo nome è il nome del modello o i primi caratteri della query SQL. All’inizio viene denominato qualsiasi query creata tramite l’interfaccia utente con l’Editor query. Se la query è stata creata tramite l’API, il nome della query è uno snippet dell’SQL iniziale utilizzato per creare la query. |
| Modello | Nome del modello della query. Selezionare un nome di modello per passare all’Editor query. Il modello di query viene visualizzato nell’Editor query per comodità. Se non è presente un nome di modello, la riga viene contrassegnata con un trattino e non è possibile reindirizzare all’Editor query per visualizzare la query. |
| SQL | Frammento della query SQL. |
| Frequenza di esecuzione | Questa è la cadenza alla quale la query è impostata per essere eseguita. I valori disponibili sono `Run once` e `Scheduled`. Le query possono essere filtrate in base alla loro frequenza di esecuzione. |
| Creato da | Nome dell’utente che ha creato la query. |
| Creato | La marca temporale alla creazione della query, in formato UTC. |
| Timestamp ultima esecuzione | La marca temporale più recente all’esecuzione della query. Questa colonna evidenzia se una query è stata eseguita in base alla pianificazione corrente. |
| Stato dell&#39;ultima esecuzione | Lo stato dell’esecuzione della query più recente. I tre valori di stato sono: `successful` `failed` o `in progress`. |

>[!TIP]
>
>Se passi all’Editor query, puoi selezionare **[!UICONTROL Query]** per tornare al [!UICONTROL Modelli] scheda .

### Personalizzare le impostazioni della tabella per le query pianificate

È possibile regolare le colonne nel [!UICONTROL Query pianificate] in base alle tue esigenze. Seleziona l’icona delle impostazioni (![Icona delle impostazioni.](./images/monitor-queries/settings-icon.png)) per aprire [!UICONTROL Personalizzare la tabella] finestra di dialogo delle impostazioni e modifica le colonne disponibili.

![Icona Personalizza impostazioni tabella.](./images/monitor-queries/customze-table-settings-icon.png)

Selezionare le caselle di controllo desiderate per rimuovere o aggiungere una colonna di tabella. Quindi, seleziona **[!UICONTROL Applica]** per confermare le scelte.

>[!NOTE]
>
>Qualsiasi query creata tramite l’interfaccia utente diventa un modello denominato come parte del processo di creazione. Il nome del modello viene visualizzato nella colonna del modello. Se la query è stata creata tramite l’API, la colonna del modello è vuota.

![Finestra di dialogo Personalizza impostazioni tabella.](./images/monitor-queries/customize-table-dialog.png)

### Iscriviti agli avvisi {#alert-subscription}

Puoi abbonarti agli avvisi dal [!UICONTROL Query pianificate] scheda . Seleziona l’icona della notifica di avviso (![Icona di avviso.](./images/monitor-queries/alerts-icon.png)) accanto al nome di una query per aprire la [!UICONTROL Avvisi] finestra di dialogo. La [!UICONTROL Avvisi] La finestra di dialogo si abbona sia alle notifiche dell’interfaccia utente che agli avvisi e-mail. Gli avvisi si basano sullo stato della query. Sono disponibili tre opzioni: `start`, `success`e `failure`. Selezionare la casella o le caselle appropriate e selezionare **[!UICONTROL Salva]** per iscriversi.

<!-- This dialog will be updated before release. THe image below will need to be updated inline with these changes. -->

![Finestra di dialogo delle sottoscrizioni di avvisi.](./images/monitor-queries/alert-subscription-dialog.png)

<!-- Link to alert subscriptions doc when available -->

### Filtrare le query

È possibile filtrare le query in base alla frequenza di esecuzione. Da [!UICONTROL Query pianificate] , seleziona l’icona del filtro (![Icona filtro](./images/monitor-queries/filter-icon.png)) per aprire la barra laterale del filtro.

![La scheda Query pianificate con l’icona del filtro evidenziata.](./images/monitor-queries/filter-queries.png)

Seleziona la **[!UICONTROL Pianificato]** o **[!UICONTROL Esegui una volta]** esegui le caselle di controllo filtro di frequenza per filtrare l’elenco di query.

>[!NOTE]
>
>Qualsiasi query eseguita ma non pianificata si qualifica come [!UICONTROL Esegui una volta].

![La scheda Query pianificate con la barra laterale del filtro evidenziata.](./images/monitor-queries/filter-sidebar.png)

Dopo aver abilitato i criteri di filtro, seleziona **[!UICONTROL Nascondi filtri]** per chiudere il pannello del filtro.

## Query esegue i dettagli della pianificazione

Seleziona un nome di query per passare alla pagina dei dettagli della pianificazione. Questa visualizzazione fornisce un elenco di tutte le esecuzioni eseguite nell&#39;ambito di tale query pianificata. Le informazioni fornite includono l’ora di inizio e di fine, lo stato e il set di dati utilizzati.

![Pagina dei dettagli della pianificazione.](./images/monitor-queries/schedule-details.png)

Queste informazioni sono fornite in una tabella a cinque colonne. Ciascuna riga indica un’esecuzione della query.

| Nome colonna | Descrizione |
|---|---|
| ID esecuzione query | ID di esecuzione della query per l&#39;esecuzione giornaliera. |
| Avvio esecuzione query | La marca temporale in cui è stata eseguita la query. Questo è in formato UTC. |
| Esecuzione query completata | La marca temporale al completamento della query. Questo è in formato UTC. |
| Stato | Lo stato dell’esecuzione della query più recente. I tre valori di stato sono: `successful` `failed` o `in progress`. |
| Set di dati | Il set di dati coinvolto nell’esecuzione. |

I dettagli della query pianificata possono essere visualizzati nella [!UICONTROL Proprietà] pannello. Questo pannello include l&#39;ID della query iniziale, il tipo di client, il nome del modello, l&#39;SQL della query e la frequenza della pianificazione.

![La pagina dei dettagli della pianificazione con il pannello delle proprietà evidenziato.](./images/monitor-queries/properties-panel.png)

### Dettagli esecuzione

Seleziona un ID di esecuzione della query per passare alla pagina dei dettagli di esecuzione e visualizzare le informazioni sulla query.

![Schermata dei dettagli della pianificazione con un ID di esecuzione evidenziato.](./images/monitor-queries/navigate-to-run-details.png)

Questa visualizzazione fornisce informazioni sulle singole esecuzioni per questa query pianificata e una suddivisione più dettagliata dello stato di esecuzione. Questa pagina include anche le informazioni sul client e i dettagli di eventuali errori che hanno causato il mancato funzionamento della query.

![La schermata dei dettagli di esecuzione con la sezione panoramica evidenziata.](./images/monitor-queries/query-run-details.png)

La sezione relativa allo stato della query fornisce il codice di errore e il messaggio di errore in caso di errore della query.

![Schermata dei dettagli di esecuzione con la sezione degli errori evidenziata.](./images/monitor-queries/failed-query.png)

È possibile copiare l&#39;SQL della query negli Appunti da questa visualizzazione. Selezionare l&#39;icona di copia in alto a destra dello snippet SQL per copiare la query. Un messaggio popup conferma che il codice è stato copiato.

![Schermata dei dettagli di esecuzione con l&#39;icona di copia SQL evidenziata.](./images/monitor-queries/copy-sql.png)

Seleziona **[!UICONTROL Query]** per tornare alla schermata dei dettagli della pianificazione, oppure **[!UICONTROL Query pianificate]** per tornare al [!UICONTROL Query pianificate] scheda .

![Schermata dei dettagli di esecuzione con Query evidenziata.](./images/monitor-queries/return-navigation.png)
