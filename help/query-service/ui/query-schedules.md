---
title: Pianificazioni query
description: Scopri come automatizzare l’esecuzione di query pianificate, eliminare o disabilitare una pianificazione di query e utilizzare le opzioni di pianificazione disponibili tramite l’interfaccia utente di Adobe Experience Platform.
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 8d307b9c1c80c7b1672f2bf6b7acb4b85c4dae1b
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 0%

---

# Pianificazioni query

Puoi automatizzare l’esecuzione delle query creando pianificazioni di query. Le query pianificate vengono eseguite su una frequenza personalizzata per gestire i dati in base a frequenza, data e ora. Se necessario, puoi anche scegliere un set di dati di output per i risultati. Le query salvate come modello possono essere pianificate dall&#39;Editor query.

>[!IMPORTANT]
>
>È possibile aggiungere una pianificazione solo a una query già creata, salvata ed eseguita.

Tutte le query pianificate vengono aggiunte all’elenco in [!UICONTROL Query pianificate] scheda. Da tale area di lavoro è possibile monitorare lo stato di tutti i processi di query pianificati tramite l’interfaccia utente. Il giorno [!UICONTROL Query pianificate] scheda puoi trovare informazioni importanti sull’esecuzione della query e abbonarti agli avvisi. Le informazioni disponibili includono lo stato, i dettagli della pianificazione e i messaggi/codici di errore in caso di errore di esecuzione. Consulta la [Monitorare il documento delle query pianificate](./monitor-queries.md) per ulteriori informazioni.

Questo flusso di lavoro descrive il processo di pianificazione nell’interfaccia utente di Query Service. Per informazioni su come aggiungere pianificazioni utilizzando l’API, leggi la [guida dell’endpoint &quot;scheduled queries&quot;](../api/scheduled-queries.md).

## Creare una pianificazione di query {#create-schedule}

Per pianificare una query, selezionare un modello di query dalla [!UICONTROL Modelli] scheda o [!UICONTROL Modello] colonna del [!UICONTROL Query pianificate] scheda. Selezionando il nome del modello si passa all&#39;editor di query.

Se si accede a una query salvata dall&#39;Editor query, è possibile creare una pianificazione per la query o visualizzarne la pianificazione dal pannello dei dettagli.

>[!TIP]
>
>Seleziona **[!UICONTROL Visualizza pianificazione]** per passare all&#39;area di lavoro pianificazioni e visualizzare immediatamente qualsiasi query pianificata eseguita.

![Editor query con [!UICONTROL Visualizza pianificazione] e [!UICONTROL Aggiungi pianificazione] evidenziato.](../images/ui/query-schedules/view-add-schedule.png)

Seleziona **[!UICONTROL Aggiungi pianificazione]** per passare al [pagina dettagli pianificazione](#schedule-details).

In alternativa, seleziona la **[!UICONTROL Schedules]** sotto il nome della query.

![Editor query con la scheda Schedules evidenziata.](../images/ui/query-schedules/schedules-tab.png)

Verrà visualizzata l&#39;area di lavoro pianificazioni. Nell’interfaccia utente viene visualizzato un elenco delle esecuzioni pianificate a cui è associato il modello. Seleziona **[!UICONTROL Aggiungi pianificazione]** per creare una pianificazione.

![Nell&#39;area di lavoro Pianificazione editor query è evidenziata Aggiungi pianificazione.](../images/ui/query-schedules/add-schedule.png)

### Aggiungi dettagli pianificazione {#schedule-details}

Viene visualizzata la pagina dei dettagli della pianificazione. In questa pagina è possibile modificare una serie di dettagli per la query pianificata. I dettagli includono [frequenza e giorno feriale della query pianificata](#scheduled-query-frequency) run, la data di inizio e di fine, il set di dati in cui esportare i risultati e [avvisi sullo stato delle query](#alerts-for-query-status).

![Viene evidenziato il pannello Dettagli pianificazione.](../images/ui/query-schedules/schedule-details.png)

#### Frequenza query pianificata {#scheduled-query-frequency}

Puoi scegliere le seguenti opzioni per **[!UICONTROL Frequenza]**:

- **[!UICONTROL Ogni ora]**: la query pianificata viene eseguita ogni ora per il periodo di data selezionato.
- **[!UICONTROL Giornaliero]**: la query pianificata verrà eseguita ogni X giorni all’ora e nel periodo di data selezionati. L&#39;ora selezionata è in **UTC** e non il tuo fuso orario locale.
- **[!UICONTROL Ogni settimana]**: la query selezionata verrà eseguita nei giorni della settimana, dell’ora e del periodo di data selezionati. L&#39;ora selezionata è in **UTC** e non il tuo fuso orario locale.
- **[!UICONTROL Mensile]**: la query selezionata verrà eseguita ogni mese al giorno, all’ora e al periodo di data selezionati. L&#39;ora selezionata è in **UTC** e non il tuo fuso orario locale.
- **[!UICONTROL Annuale]**: la query selezionata verrà eseguita ogni anno al giorno, al mese, all’ora e al periodo di data selezionati. L&#39;ora selezionata è in **UTC** e non il tuo fuso orario locale.

### Fornisci dettagli set di dati {#dataset-details}

Gestisci i risultati della query aggiungendo i dati a un set di dati esistente o creando un nuovo set di dati e aggiungendo i dati a esso.

Seleziona **[!UICONTROL Crea e aggiungi al nuovo set di dati]** per creare un set di dati quando si esegue una query per la prima volta. Le esecuzioni successive continuano a inserire dati in tale set di dati. Infine, fornisci un nome e una descrizione per il set di dati.

>[!IMPORTANT]
>
> Poiché si utilizza un set di dati esistente o si crea un nuovo set di dati, **non** devono includere `INSERT INTO` o `CREATE TABLE AS SELECT` come parte della query, poiché i set di dati sono già impostati. Inclusione di `INSERT INTO` o `CREATE TABLE AS SELECT` come parte delle query pianificate genererà un errore.

![Il pannello Dettagli pianificazione con i dettagli del set di dati e il [!UICONTROL Crea e aggiungi al nuovo set di dati] opzioni evidenziate.](../images/ui/query-schedules/dataset-details-create-and-append.png)

In alternativa, seleziona **[!UICONTROL Aggiungi a set di dati esistente]** seguito dall’icona del set di dati (![Icona del set di dati.](../images/ui/query-schedules/dataset-icon.png)).

![Il pannello Dettagli pianificazione con i dettagli del set di dati ed Aggiungi al set di dati esistente è evidenziato.](../images/ui/query-schedules/dataset-details-existing.png)

Il **[!UICONTROL Seleziona set di dati di output]** viene visualizzata.

Quindi, sfoglia i set di dati esistenti o utilizza il campo di ricerca per filtrare le opzioni. Seleziona la riga del set di dati da utilizzare. I dettagli del set di dati vengono visualizzati nel pannello a destra. Seleziona **[!UICONTROL Fine]** per confermare la scelta.

![Viene evidenziata la finestra di dialogo Seleziona set di dati di output con il campo di ricerca, una riga di set di dati e l’opzione Fine.](../images/ui/query-schedules/select-output-dataset-dialog.png)

### Quarantena le query in caso di errore continuo {#quarantine}

Durante la creazione di una pianificazione, puoi registrare la query nella funzione di quarantena per proteggere le risorse di sistema e prevenire potenziali interruzioni. La funzione di quarantena identifica e isola automaticamente le query che hanno ripetutamente esito negativo inserendole in una [!UICONTROL In quarantena] stato. Mettendo in quarantena le query dopo dieci errori consecutivi, puoi intervenire, rivedere e rettificare i problemi prima di consentire ulteriori esecuzioni. In questo modo è possibile mantenere l&#39;efficienza operativa e l&#39;integrità dei dati.

![L’area di lavoro Query pianificate con [!UICONTROL Quarantena query] evidenziate e Sì selezionate.](../images/ui/query-schedules/quarantine-enroll.png)

Dopo aver registrato una query per la funzione di quarantena, puoi attivare gli avvisi per questa modifica dello stato della query. Se una query pianificata non è iscritta alla quarantena, non viene visualizzata come opzione su [la finestra di dialogo Avvisi](./monitor-queries.md#alert-subscription).

È inoltre possibile registrare una query pianificata nella funzione di quarantena dalle azioni in linea di [!UICONTROL Query pianificate] scheda. Consulta la [monitorare la documentazione delle query](./monitor-queries.md#alert-subscription) per ulteriori dettagli.

### Impostare gli avvisi per uno stato di query pianificata {#alerts-for-query-status}

È inoltre possibile abbonarsi agli avvisi di query come parte delle impostazioni di query pianificate. Ciò significa che si ricevono notifiche quando si cambia lo stato della query. Gli avvisi possono essere ricevuti come notifiche pop-up o e-mail. Le opzioni di avviso dello stato della query disponibili includono avvio, operazione riuscita ed errore. Selezionare la casella di controllo per sottoscrivere gli avvisi relativi allo stato della query pianificata.

![Il pannello Dettagli pianificazione con le opzioni Avviso evidenziate.](../images/ui/query-editor/alerts.png)

Per una panoramica degli avvisi in Adobe Experience Platform, inclusa la struttura della definizione delle regole di avviso, vedi [panoramica degli avvisi](../../observability/alerts/overview.md). Per informazioni sulla gestione degli avvisi e delle regole di avviso nell’interfaccia utente di Adobe Experience Platform, consulta [Guida all’interfaccia utente Avvisi](../../observability/alerts/ui.md).

### Impostare i parametri per una query con parametri pianificata {#set-parameters}

>[!IMPORTANT]
>
>La funzione per l’interfaccia con parametri per query è attualmente disponibile in una **solo versione limitata** e non è disponibile per tutti i clienti. Se non hai accesso alle query con parametri, continua con [eliminare o disattivare una pianificazione](#delete-schedule) sezione.

Se si crea una query pianificata per una query con parametri, è necessario impostare i valori dei parametri per queste esecuzioni della query.

![La sezione Dettagli pianificazione del flusso di lavoro di creazione della pianificazione con la sezione Parametri query evidenziata.](../images/ui/query-schedules/scheduled-query-parameter.png)

Dopo aver confermato i dettagli della pianificazione, seleziona **[!UICONTROL Salva]** per creare una pianificazione. Viene visualizzata di nuovo la scheda Pianificazioni del modello. In questa area di lavoro vengono visualizzati i dettagli della pianificazione appena creata, inclusi l’ID pianificazione, la pianificazione stessa e il set di dati di output della pianificazione.

## Visualizza esecuzioni query pianificate {#scheduled-query-runs}

Dal modello di [!UICONTROL Schedules] , seleziona l’ID pianificazione per passare all’elenco delle query eseguite per la query appena pianificata.

![Area di lavoro pianificazioni con la pianificazione appena creata evidenziata.](../images/ui/query-schedules/schedules-workspace.png)

In alternativa, per visualizzare un elenco delle esecuzioni pianificate di un modello di query, passare alla **[!UICONTROL Query pianificate]** e selezionare un nome di modello dall&#39;elenco disponibile.

![La scheda Query pianificate con un modello denominato evidenziato.](../images/ui/query-schedules/view-scheduled-runs.png)

Viene visualizzato l&#39;elenco delle query eseguite per la query pianificata.

![La sezione dei dettagli dell’area di lavoro Query pianificate con un elenco delle esecuzioni delle query è evidenziata per una query pianificata.](../images/ui/query-schedules/list-of-scheduled-runs.png)

Consulta la [monitoraggio della guida con query pianificata](./monitor-queries.md#inline-actions) per informazioni complete su come monitorare lo stato di tutti i processi di query tramite l’interfaccia utente.

Seleziona un **[!UICONTROL ID esecuzione query]** dall’elenco, per passare alla panoramica dell’esecuzione della query. Per una disaggregazione completa delle informazioni disponibili [panoramica dell’esecuzione delle query](./monitor-queries.md#query-run-overview), consulta la documentazione sul monitoraggio delle query pianificate.

Per monitorare le query pianificate tramite l’API Query Service, consulta la sezione [guida degli endpoint di esecuzione delle query pianificate](../api/runs-scheduled-queries.md).

## Abilitare, disabilitare o eliminare una pianificazione {#delete-schedule}

È possibile abilitare, disabilitare o eliminare una pianificazione dall&#39;area di lavoro pianificazioni di una particolare query o dall&#39; [!UICONTROL Query pianificate] area di lavoro che elenca tutte le query pianificate.

Per accedere al [!UICONTROL Schedules] della query scelta, è necessario selezionare il nome di un modello di query dalla scheda [!UICONTROL Modelli] scheda o [!UICONTROL Query pianificate] scheda. Consente di passare all&#39;editor delle query per la query. Dall’editor delle query, seleziona **[!UICONTROL Schedules]** per accedere all&#39;area di lavoro pianificazioni.

Seleziona una pianificazione dalle righe delle pianificazioni disponibili per popolare il pannello dei dettagli. Utilizza l’interruttore per disabilitare (o abilitare) la query pianificata.

### Eliminare le query disabilitate

>[!IMPORTANT]
>
>È necessario disattivare la pianificazione prima di eliminare una pianificazione per una query.

![L’elenco delle pianificazioni di un modello con il pannello dei dettagli evidenziato.](../images/ui/query-schedules/schedule-details-panel.png)

Viene visualizzata una finestra di dialogo di conferma. Seleziona **[!UICONTROL Disattiva]** per confermare l’azione.

![La finestra di dialogo di conferma Disattiva pianificazione.](../images/ui/query-schedules/disable-schedule-confirmation-dialog.png)

Seleziona **[!UICONTROL Eliminare una pianificazione]** per eliminare la pianificazione disabilitata.

![Area di lavoro pianificazioni con Elimina pianificazione evidenziata.](../images/ui/query-schedules/delete-schedule.png)

In alternativa, [!UICONTROL Query pianificate] La scheda offre una raccolta di azioni in linea per ogni query pianificata. Le azioni in linea disponibili includono [!UICONTROL Disattiva pianificazione] o [!UICONTROL Abilita pianificazione], [!UICONTROL Elimina pianificazione], e [!UICONTROL Abbonati] agli avvisi per la query pianificata. Per istruzioni complete su come eliminare o disabilitare una query pianificata tramite la scheda Query pianificate, vedi [monitoraggio della guida con query pianificata](./monitor-queries.md#inline-actions).
