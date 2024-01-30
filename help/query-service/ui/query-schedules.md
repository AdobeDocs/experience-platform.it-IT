---
title: Pianificazioni query
description: Scopri come automatizzare l’esecuzione di query pianificate, eliminare o disabilitare una pianificazione di query e utilizzare le opzioni di pianificazione disponibili tramite l’interfaccia utente di Adobe Experience Platform.
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 7d2027bf315ae6e354c906e4aabf6371a92e4148
workflow-type: tm+mt
source-wordcount: '1084'
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

Verrà visualizzata l&#39;area di lavoro pianificazioni. Seleziona **[!UICONTROL Aggiungi pianificazione]** per creare una pianificazione.

![Nell&#39;area di lavoro Pianificazione editor query è evidenziata Aggiungi pianificazione.](../images/ui/query-schedules/add-schedule.png)

### Modifica i dettagli della pianificazione {#schedule-details}

Viene visualizzata la pagina dei dettagli della pianificazione. In questa pagina puoi scegliere la frequenza della query pianificata, la data di inizio e di fine, il giorno della settimana in cui verrà eseguita la query pianificata e il set di dati in cui esportare la query.

![Viene evidenziato il pannello Dettagli pianificazione.](../images/ui/query-schedules/schedule-details.png)

Puoi scegliere le seguenti opzioni per **[!UICONTROL Frequenza]**:

- **[!UICONTROL Ogni ora]**: la query pianificata viene eseguita ogni ora per il periodo di data selezionato.
- **[!UICONTROL Giornaliero]**: la query pianificata verrà eseguita ogni X giorni all’ora e nel periodo di data selezionati. L&#39;ora selezionata è in **UTC** e non il tuo fuso orario locale.
- **[!UICONTROL Ogni settimana]**: la query selezionata verrà eseguita nei giorni della settimana, dell’ora e del periodo di data selezionati. L&#39;ora selezionata è in **UTC** e non il tuo fuso orario locale.
- **[!UICONTROL Mensile]**: la query selezionata verrà eseguita ogni mese al giorno, all’ora e al periodo di data selezionati. L&#39;ora selezionata è in **UTC** e non il tuo fuso orario locale.
- **[!UICONTROL Annuale]**: la query selezionata verrà eseguita ogni anno al giorno, al mese, all’ora e al periodo di data selezionati. L&#39;ora selezionata è in **UTC** e non il tuo fuso orario locale.

Per il set di dati di output, puoi utilizzare l’opzione per aggiungere in un set di dati esistente o per creare e aggiungere in un nuovo set di dati. La seconda opzione indica che se si esegue una query per la prima volta e si crea un set di dati, tutte le esecuzioni successive continueranno a inserire dati in tale set di dati.

>[!IMPORTANT]
>
> Poiché si utilizza un set di dati esistente o si crea un nuovo set di dati, **non** devono includere `INSERT INTO` o `CREATE TABLE AS SELECT` come parte della query, poiché i set di dati sono già impostati. Inclusione di `INSERT INTO` o `CREATE TABLE AS SELECT` come parte delle query pianificate genererà un errore.

Se non hai accesso alle query con parametri, continua con [eliminare o disattivare una pianificazione](#delete-schedule) sezione.

### Impostare i parametri per una query con parametri pianificata {#set-parameters}

>[!IMPORTANT]
>
>La funzione per l’interfaccia con parametri per query è attualmente disponibile in una **solo versione limitata** e non è disponibile per tutti i clienti.

Se si crea una query pianificata per una query con parametri, è necessario impostare i valori dei parametri per queste esecuzioni della query.

![La sezione Dettagli pianificazione del flusso di lavoro di creazione della pianificazione con la sezione Parametri query evidenziata.](../images/ui/query-schedules/scheduled-query-parameter.png)

Dopo aver confermato tutti questi dettagli, seleziona **[!UICONTROL Salva]** per creare una pianificazione. L&#39;utente viene reindirizzato all&#39;area di lavoro pianificazioni che visualizza i dettagli della pianificazione appena creata, inclusi l&#39;ID pianificazione, la pianificazione stessa e il set di dati di output della pianificazione. Puoi utilizzare l’ID pianificazione per cercare ulteriori informazioni sulle esecuzioni della query pianificata stessa. Per ulteriori informazioni, leggere [guida degli endpoint di esecuzione delle query pianificate](../api/runs-scheduled-queries.md).

![Area di lavoro pianificazioni con la pianificazione appena creata evidenziata.](../images/ui/query-schedules/schedules-workspace.png)

## Visualizza esecuzioni query pianificate {#scheduled-query-runs}

Per visualizzare un elenco delle esecuzioni pianificate di un modello di query, passare alla [!UICONTROL Query pianificate] e selezionare un nome di modello dall&#39;elenco disponibile.

![La scheda Query pianificate con un modello denominato evidenziato.](../images/ui/query-schedules/view-scheduled-runs.png)

Viene visualizzato l&#39;elenco delle query eseguite per la query pianificata.

![La sezione dei dettagli dell’area di lavoro Query pianificate con un elenco delle esecuzioni delle query è evidenziata per una query pianificata.](../images/ui/query-schedules/list-of-scheduled-runs.png)

Consulta la [monitoraggio della guida con query pianificata](./monitor-queries.md#inline-actions) per informazioni complete su come monitorare lo stato di tutti i processi di query tramite l’interfaccia utente.

## Eliminare o disattivare una pianificazione {#delete-schedule}

È possibile eliminare o disabilitare una pianificazione dall&#39;area di lavoro pianificazioni di una particolare query o dall&#39; [!UICONTROL Query pianificate] area di lavoro che elenca tutte le query pianificate.

Per accedere al [!UICONTROL Schedules] della query scelta, è necessario selezionare il nome di un modello di query dalla scheda [!UICONTROL Modelli] scheda o [!UICONTROL Query pianificate] scheda. Consente di passare all&#39;editor delle query per la query. Dall’editor delle query, seleziona **[!UICONTROL Schedules]** per accedere all&#39;area di lavoro pianificazioni.

Selezionare una pianificazione dalle righe delle pianificazioni disponibili. Puoi utilizzare l’interruttore per disabilitare o abilitare la query pianificata.

>[!IMPORTANT]
>
>È necessario disattivare la pianificazione prima di eliminare una pianificazione per una query.

Seleziona **[!UICONTROL Eliminare una pianificazione]** per eliminare la pianificazione disabilitata.

![Area di lavoro pianificazioni con le opzioni Disattiva pianificazione ed Elimina pianificazione evidenziate.](../images/ui/query-schedules/delete-schedule.png)

In alternativa, [!UICONTROL Query pianificate] La scheda offre una raccolta di azioni in linea per ogni query pianificata. Le azioni in linea disponibili includono [!UICONTROL Disattiva pianificazione] o [!UICONTROL Abilita pianificazione], [!UICONTROL Elimina pianificazione], e [!UICONTROL Abbonati] agli avvisi per la query pianificata. Per istruzioni complete su come eliminare o disabilitare una query pianificata tramite la scheda Query pianificate, vedi [monitoraggio della guida con query pianificata](./monitor-queries.md#inline-actions).
