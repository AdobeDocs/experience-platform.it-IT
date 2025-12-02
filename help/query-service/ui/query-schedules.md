---
title: Pianificazioni query
description: Scopri come automatizzare l’esecuzione di query pianificate, eliminare o disabilitare una pianificazione di query e utilizzare le opzioni di pianificazione disponibili tramite l’interfaccia utente di Adobe Experience Platform.
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 8d3da7f33aefa822e24bd60168760d856a85865f
workflow-type: tm+mt
source-wordcount: '2088'
ht-degree: 0%

---

# Pianificazioni query

Puoi automatizzare l’esecuzione delle query creando pianificazioni di query. Le query pianificate vengono eseguite su una frequenza personalizzata per gestire i dati in base a frequenza, data e ora. Se necessario, puoi anche scegliere un set di dati di output per i risultati. Le query salvate come modello possono essere pianificate dall&#39;Editor query.

>[!IMPORTANT]
>
>È possibile aggiungere una pianificazione solo a una query già creata e salvata.

## Requisiti dell’account per le query pianificate {#technical-account-user-requirements}

Per un’esecuzione affidabile delle query pianificate, Adobe consiglia agli amministratori di effettuare il provisioning di un account tecnico (utilizzando le credenziali server-to-server OAuth) per la creazione di query pianificate. È possibile creare query pianificate anche con un account utente personale, ma le query create in questo modo cesseranno di essere in esecuzione se l&#39;accesso dell&#39;utente viene rimosso o disabilitato.

Per informazioni dettagliate sulla configurazione degli account tecnici e sull&#39;assegnazione delle autorizzazioni necessarie, vedere i prerequisiti della [Guida alle credenziali](./credentials.md#prerequisites) e l&#39;autenticazione API [.](../../landing/api-authentication.md)

Per ulteriori informazioni sulla creazione e la configurazione di un account tecnico, consulta:

- [Configurazione di Developer Console](https://experienceleague.adobe.com/en/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/set-up-developer-console-and-postman): istruzioni dettagliate per la configurazione di Adobe Developer Console e l&#39;ottenimento delle credenziali OAuth.
- [Configurazione end-to-end dell&#39;account tecnico](https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-comprehensive-technical/setup): procedura dettagliata completa per la creazione e la configurazione di un account tecnico in Adobe Experience Platform.

Se utilizzi solo l’interfaccia utente di Query Service, assicurati di disporre delle autorizzazioni necessarie o coordinati con un amministratore che gestisce gli account tecnici. Tutte le query pianificate vengono aggiunte all&#39;elenco nella scheda [!UICONTROL Scheduled queries], in cui è possibile monitorare lo stato, i dettagli della pianificazione e i messaggi di errore per tutti i processi di query pianificati, nonché sottoscrivere avvisi. Per ulteriori informazioni sul monitoraggio e la gestione delle query, vedere il documento [monitoraggio delle query pianificate](./monitor-queries.md).

Questo flusso di lavoro descrive il processo di pianificazione nell’interfaccia utente di Query Service. Per informazioni su come aggiungere pianificazioni utilizzando l&#39;API, consulta la [guida dell&#39;endpoint per le query pianificate](../api/scheduled-queries.md).

>[!NOTE]
>
>Utilizza un account tecnico per garantire che le query pianificate continuino a essere eseguite anche se gli utenti lasciano l’organizzazione o se i loro ruoli cambiano. Se possibile, scegli un account tecnico per l’automazione ininterrotta delle query.

## Creare una pianificazione di query {#create-schedule}

Per pianificare una query, selezionare un modello di query dalla scheda [!UICONTROL Templates] o dalla colonna [!UICONTROL Template] della scheda [!UICONTROL Scheduled Queries]. Selezionando il nome del modello si passa all&#39;editor di query.

Se si accede a una query salvata dall&#39;Editor query, è possibile creare una pianificazione per la query o visualizzarne la pianificazione dal pannello dei dettagli.

>[!TIP]
>
>Selezionare **[!UICONTROL View schedule]** per passare all&#39;area di lavoro pianificazioni e visualizzare immediatamente qualsiasi query pianificata eseguita.

![Editor query con [!UICONTROL View schedule] e [!UICONTROL Add schedule] evidenziati.](../images/ui/query-schedules/view-add-schedule.png)

Selezionare **[!UICONTROL Add schedule]** per passare alla [pagina dettagli pianificazione](#schedule-details).

In alternativa, selezionare la scheda **[!UICONTROL Schedules]** sotto il nome della query.

![L&#39;editor delle query con la scheda Schedules evidenziata.](../images/ui/query-schedules/schedules-tab.png)

Verrà visualizzata l&#39;area di lavoro pianificazioni. Nell’interfaccia utente viene visualizzato un elenco delle esecuzioni pianificate a cui è associato il modello. Selezionare **[!UICONTROL Add Schedule]** per creare una pianificazione.

![Area di lavoro di pianificazione dell&#39;editor delle query con Aggiungi pianificazione evidenziata.](../images/ui/query-schedules/add-schedule.png)

### Aggiungi dettagli pianificazione {#schedule-details}

Viene visualizzata la pagina dei dettagli della pianificazione. In questa pagina è possibile modificare una serie di dettagli per la query pianificata. I dettagli includono [frequenza e giorno feriale dell&#39;esecuzione pianificata della query](#scheduled-query-frequency), la data di inizio e di fine, il set di dati in cui esportare i risultati e [avvisi sullo stato della query](#alerts-for-query-status).

>[!IMPORTANT]
>
>L’interfaccia utente dell’utilità di pianificazione delle query non supporta la pianificazione indefinita o permanente. È necessario specificare una data di fine. Non esiste alcun limite massimo per la data di fine.

![Il pannello Dettagli pianificazione è evidenziato.](../images/ui/query-schedules/schedule-details.png)

#### Frequenza query pianificata {#scheduled-query-frequency}

È possibile scegliere le opzioni seguenti per **[!UICONTROL Frequency]**:

- **[!UICONTROL Hourly]**: la query pianificata verrà eseguita ogni ora per il periodo di date selezionato.
- **[!UICONTROL Daily]**: la query pianificata verrà eseguita ogni X giorni alla data e all&#39;ora selezionate. L&#39;ora selezionata è tra **UTC** e non il tuo fuso orario locale.
- **[!UICONTROL Weekly]**: la query selezionata verrà eseguita nei giorni della settimana, dell&#39;ora e del periodo selezionato. L&#39;ora selezionata è tra **UTC** e non il tuo fuso orario locale.
- **[!UICONTROL Monthly]**: la query selezionata verrà eseguita ogni mese al giorno, all&#39;ora e al periodo di data selezionati. L&#39;ora selezionata è tra **UTC** e non il tuo fuso orario locale.
- **[!UICONTROL Yearly]**: la query selezionata verrà eseguita ogni anno al giorno, al mese, all&#39;ora e al periodo di data selezionati. L&#39;ora selezionata è tra **UTC** e non il tuo fuso orario locale.

### Fornisci dettagli set di dati {#dataset-details}

Gestisci i risultati della query aggiungendo i dati a un set di dati esistente o creando un nuovo set di dati e aggiungendo i dati a esso.

Selezionare **[!UICONTROL Create and append into new dataset]** per creare un set di dati quando si esegue una query per la prima volta. Le esecuzioni successive continuano a inserire dati in tale set di dati. Infine, fornisci un nome e una descrizione per il set di dati.

>[!IMPORTANT]
>
> Poiché si sta utilizzando un set di dati esistente o creando un nuovo set di dati, **non** deve includere `INSERT INTO` o `CREATE TABLE AS SELECT` come parte della query, poiché i set di dati sono già impostati. L&#39;inclusione di `INSERT INTO` o `CREATE TABLE AS SELECT` come parte delle query pianificate genererà un errore.

![Pannello Dettagli pianificazione con dettagli set di dati e opzioni [!UICONTROL Create and append into new dataset] evidenziate.](../images/ui/query-schedules/dataset-details-create-and-append.png)

In alternativa, selezionare **[!UICONTROL Append into existing dataset]** seguito dall&#39;icona del set di dati (![Icona del set di dati.](/help/images/icons/database.png)).

![Il pannello Dettagli pianificazione con i dettagli del set di dati ed Aggiungi al set di dati esistente è evidenziato.](../images/ui/query-schedules/dataset-details-existing.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Select output dataset]**.

Quindi, sfoglia i set di dati esistenti o utilizza il campo di ricerca per filtrare le opzioni. Seleziona la riga del set di dati da utilizzare. I dettagli del set di dati vengono visualizzati nel pannello a destra. Seleziona **[!UICONTROL Done]** per confermare la scelta.

![Finestra di dialogo Seleziona set di dati di output con il campo di ricerca, una riga di set di dati e Fine evidenziati.](../images/ui/query-schedules/select-output-dataset-dialog.png)

### Quarantena le query in caso di errore continuo {#quarantine}

Durante la creazione di una pianificazione, puoi registrare la query nella funzione di quarantena per proteggere le risorse di sistema e prevenire potenziali interruzioni. La funzionalità di quarantena identifica e isola automaticamente le query che hanno ripetutamente esito negativo inserendole in uno stato [!UICONTROL Quarantined]. Mettendo in quarantena le query dopo dieci errori consecutivi, puoi intervenire, rivedere e rettificare i problemi prima di consentire ulteriori esecuzioni. In questo modo è possibile mantenere l&#39;efficienza operativa e l&#39;integrità dei dati.

![L&#39;area di lavoro Pianificazioni query con [!UICONTROL Query Quarantine] evidenziato e Sì selezionato.](../images/ui/query-schedules/quarantine-enroll.png)

Dopo aver registrato una query per la funzione di quarantena, puoi attivare gli avvisi per questa modifica dello stato della query. Se una query pianificata non è registrata in quarantena, non viene visualizzata come opzione nella [finestra di dialogo Avvisi](./monitor-queries.md#alert-subscription).

È inoltre possibile registrare una query pianificata nella funzionalità di quarantena dalle azioni in linea della scheda [!UICONTROL Scheduled Queries]. Per ulteriori dettagli, consulta la [documentazione delle query di monitoraggio](./monitor-queries.md#alert-subscription).

### Impostare gli avvisi per uno stato di query pianificata {#alerts-for-query-status}

È inoltre possibile abbonarsi agli avvisi di query come parte delle impostazioni di query pianificate. Puoi configurare le impostazioni per ricevere notifiche per una serie di situazioni. Gli avvisi possono essere impostati per uno stato di quarantena, ritardi nell’elaborazione delle query o una modifica dello stato della query. Le opzioni di avviso dello stato della query disponibili includono avvio, operazione riuscita ed errore. Gli avvisi possono essere ricevuti come notifiche pop-up o e-mail. Seleziona la casella di controllo per abbonarti agli avvisi relativi allo stato della query pianificata.

![Pannello Dettagli pianificazione con le opzioni di avviso evidenziate.](../images/ui/query-editor/alerts.png)

La tabella seguente spiega i tipi di avviso per le query supportati:

| Tipo di avviso | Descrizione |
|---|---|
| `start` | Questo avviso avvisa quando viene avviata o avviata l&#39;elaborazione di una query pianificata. |
| `success` | Questo avviso informa l&#39;utente quando una query pianificata viene eseguita correttamente, indicando che la query è stata eseguita senza errori. |
| `failed` | Questo avviso viene attivato quando una query pianificata viene eseguita con un errore o non viene eseguita correttamente. Consente di identificare e risolvere tempestivamente i problemi. |
| `quarantine` | Questo avviso viene attivato quando un’esecuzione di query pianificata viene messa in quarantena. Una volta che una query è [registrata nella funzionalità di quarantena](#quarantine), qualsiasi query pianificata che non riesce a eseguire dieci esecuzioni consecutive viene automaticamente impostata su [!UICONTROL Quarantined]. Una query in quarantena richiede quindi l’intervento dell’utente prima di poter eseguire ulteriori esecuzioni. Nota: per poter sottoscrivere avvisi di quarantena, è necessario registrare le query per la funzione di quarantena. |
| `delay` | Questo avviso notifica se si verifica un [ritardo nell&#39;esito di un&#39;esecuzione di una query pianificata](./monitor-queries.md#query-run-delay) oltre la soglia specificata. È possibile impostare un&#39;ora personalizzata che attivi l&#39;avviso quando la query viene eseguita per tale durata senza completare o non riuscire. Il comportamento predefinito imposta un avviso per 150 minuti dopo l’inizio dell’elaborazione della query. |

>[!NOTE]
>
>Se scegli di impostare un avviso [!UICONTROL Query Run Delay], devi impostare il ritardo desiderato in minuti nell&#39;interfaccia utente di Experience Platform. Immetti la durata in minuti. Il ritardo massimo è di 24 ore (1440 minuti).

Per una panoramica degli avvisi in Adobe Experience Platform, inclusa la struttura della definizione delle regole di avviso, vedere la [panoramica degli avvisi](../../observability/alerts/overview.md). Per informazioni sulla gestione degli avvisi e delle regole di avviso nell&#39;interfaccia utente di Adobe Experience Platform, vedere la [guida dell&#39;interfaccia utente degli avvisi](../../observability/alerts/ui.md).

### Impostare i parametri per una query con parametri pianificata {#set-parameters}

Se si crea una query pianificata per una query con parametri, è necessario impostare i valori dei parametri per queste esecuzioni della query.

![Sezione Dettagli pianificazione del flusso di lavoro di creazione della pianificazione con la sezione Parametri query evidenziata.](../images/ui/query-schedules/scheduled-query-parameter.png)

Dopo aver confermato i dettagli della pianificazione, selezionare **[!UICONTROL Save]** per creare una pianificazione. Viene visualizzata di nuovo la scheda Pianificazioni del modello. In questa area di lavoro vengono visualizzati i dettagli della pianificazione appena creata, inclusi l’ID pianificazione, la pianificazione stessa e il set di dati di output della pianificazione.

## Visualizza esecuzioni query pianificate {#scheduled-query-runs}

Dalla scheda [!UICONTROL Schedules] del modello, seleziona l&#39;ID pianificazione per passare all&#39;elenco delle query eseguite per la query appena pianificata.

![Area di lavoro pianificazioni con la pianificazione appena creata evidenziata.](../images/ui/query-schedules/schedules-workspace.png)

In alternativa, per visualizzare un elenco delle esecuzioni pianificate di un modello di query, passare alla scheda **[!UICONTROL Scheduled queries]** e selezionare un nome di modello dall&#39;elenco disponibile.

![Scheda Query pianificate con un modello denominato evidenziato.](../images/ui/query-schedules/view-scheduled-runs.png)

Viene visualizzato l&#39;elenco delle query eseguite per la query pianificata.

### Calcola ore a livello di processo {#compute-hours}

Tieni traccia delle ore di calcolo utilizzate a livello di esecuzione delle query per le query batch CTAS/ITAS. Questa funzione offre informazioni approfondite sull’utilizzo dei calcoli, consentendoti di ottimizzare l’allocazione delle risorse e migliorare le prestazioni delle query.

>[!AVAILABILITY]
>
>La funzionalità Compute Hours è esclusiva per gli utenti che hanno acquistato lo SKU [Data Distiller](../data-distiller/overview.md). Per ulteriori informazioni, contatta il rappresentante Adobe.

![La sezione dei dettagli dell&#39;area di lavoro Query pianificate con un elenco di query viene eseguita evidenziata per una query pianificata.](../images/ui/query-schedules/list-of-scheduled-runs.png)

Nella tabella seguente vengono fornite le descrizioni di ogni colonna disponibile nella sezione dei dettagli in cui sono elencate le esecuzioni delle query pianificate.

| Titolo colonna | Descrizione |
|---------------------|----------------------------------|
| [!UICONTROL Query Run ID] | Visualizza un identificatore univoco per ogni esecuzione di query, che consente di tenere traccia e fare riferimento a singole esecuzioni delle query pianificate. |
| [!UICONTROL Query Run Start] | Indica la data e l’ora di inizio dell’esecuzione della query, per aiutarti a monitorare l’inizio di ogni esecuzione. |
| [!UICONTROL Query Run Complete] | Mostra la data e l’ora di completamento dell’esecuzione della query, per fornire ad insight la durata e lo stato dell’esecuzione. |
| [!UICONTROL Status] | Visualizza lo stato corrente dell&#39;esecuzione della query, ad esempio `Completed,` `Running,` o `Failed,` per valutare rapidamente il risultato. |
| [!UICONTROL Datasets] | Elenca i set di dati utilizzati nell’esecuzione della query, per mostrare quali origini dati sono state coinvolte nell’esecuzione. |
| [!UICONTROL Compute Hours] | Mostra il tempo di calcolo utilizzato per ogni esecuzione della query, misurato in ore. Questo consente di tenere traccia dell’utilizzo delle risorse e di ottimizzare le prestazioni delle query. |

{style="table-layout:auto"}

>[!NOTE]
>
>I dati delle ore di calcolo sono disponibili a partire dal 08/15/2024. I dati precedenti a questa data vengono visualizzati come &#39;Non disponibile&#39;.

Per informazioni complete su come monitorare lo stato di tutti i processi di query tramite l&#39;interfaccia utente, vedere la [guida monitoraggi pianificati per query](./monitor-queries.md#inline-actions).

Selezionare un **[!UICONTROL Query run ID]** dall&#39;elenco per passare alla panoramica dell&#39;esecuzione della query. Per un&#39;analisi completa delle informazioni disponibili nella [panoramica sull&#39;esecuzione delle query](./monitor-queries.md#query-run-overview), vedere la documentazione relativa al monitoraggio delle query pianificate.

Per monitorare le query pianificate tramite l&#39;API Query Service, vedere la [guida degli endpoint per l&#39;esecuzione pianificata delle query](../api/runs-scheduled-queries.md).

## Abilitare, disabilitare o eliminare una pianificazione {#delete-schedule}

È possibile abilitare, disabilitare o eliminare una pianificazione dall&#39;area di lavoro pianificazioni di una determinata query o dall&#39;area di lavoro [!UICONTROL Scheduled Queries] in cui sono elencate tutte le query pianificate.

Per accedere alla scheda [!UICONTROL Schedules] della query scelta, è necessario selezionare il nome di un modello di query dalla scheda [!UICONTROL Templates] o dalla scheda [!UICONTROL Scheduled Queries]. Consente di passare all&#39;editor delle query per la query. Dall&#39;editor delle query, selezionare **[!UICONTROL Schedules]** per accedere all&#39;area di lavoro pianificazioni.

Seleziona una pianificazione dalle righe delle pianificazioni disponibili per popolare il pannello dei dettagli. Utilizza l’interruttore per disabilitare (o abilitare) la query pianificata.

### Eliminare le query disabilitate

>[!IMPORTANT]
>
>È necessario disattivare la pianificazione prima di eliminare una pianificazione per una query.

![Elenco delle pianificazioni di un modello con il pannello dei dettagli evidenziato.](../images/ui/query-schedules/schedule-details-panel.png)

Viene visualizzata una finestra di dialogo di conferma. Selezionare **[!UICONTROL Disable]** per confermare l&#39;azione.

![Finestra di dialogo per disabilitare la conferma della pianificazione.](../images/ui/query-schedules/disable-schedule-confirmation-dialog.png)

Selezionare **[!UICONTROL Delete a schedule]** per eliminare la pianificazione disabilitata.

![Area di lavoro pianificazioni con Elimina pianificazione evidenziata.](../images/ui/query-schedules/delete-schedule.png)

In alternativa, la scheda [!UICONTROL Scheduled Queries] offre una raccolta di azioni in linea per ogni query pianificata. Le azioni in linea disponibili includono [!UICONTROL Disable schedule] o [!UICONTROL Enable schedule], [!UICONTROL Delete schedule] e [!UICONTROL Subscribe] per gli avvisi per la query pianificata. Per istruzioni complete su come eliminare o disabilitare una query pianificata tramite la scheda Query pianificate, vedere la [guida Monitoraggio query pianificate](./monitor-queries.md#inline-actions).
