---
title: Pianificazioni query
description: Scopri come automatizzare l’esecuzione di query pianificate, eliminare o disabilitare una pianificazione di query e utilizzare le opzioni di pianificazione disponibili tramite l’interfaccia utente di Adobe Experience Platform.
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# Pianificazioni query

Puoi automatizzare l’esecuzione delle query creando pianificazioni di query. Le query pianificate vengono eseguite su una frequenza personalizzata per gestire i dati in base a frequenza, data e ora. Se necessario, puoi anche scegliere un set di dati di output per i risultati. Le query salvate come modello possono essere pianificate dall&#39;Editor query.

>[!IMPORTANT]
>
>Di seguito è riportato un elenco di limitazioni per le query pianificate quando si utilizza l’editor di query. Non si applicano al [!DNL Query Service] API:<br/>È possibile aggiungere una pianificazione solo a una query già creata, salvata ed eseguita.<br/>Tu **non può** aggiungere una pianificazione a una query con parametri.<br/>Query pianificate **non può** contiene un blocco anonimo.

Tutte le query pianificate vengono aggiunte all’elenco in [!UICONTROL Query pianificate] scheda. Da tale area di lavoro è possibile monitorare lo stato di tutti i processi di query pianificati tramite l’interfaccia utente. Il giorno [!UICONTROL Query pianificate] scheda puoi trovare informazioni importanti sull’esecuzione della query e abbonarti agli avvisi. Le informazioni disponibili includono lo stato, i dettagli della pianificazione e i messaggi/codici di errore in caso di errore di esecuzione. Consulta la [Monitorare il documento delle query pianificate](./monitor-queries.md) per ulteriori informazioni.

## Creare pianificazioni di query {#create-schedule}

Per aggiungere una pianificazione a una query, selezionare un modello di query dalla [!UICONTROL Modelli] scheda o [!UICONTROL Query pianificate] per passare all’editor delle query.

Per informazioni su come aggiungere pianificazioni utilizzando l’API, leggi la [guida dell’endpoint &quot;scheduled queries&quot;](../api/scheduled-queries.md).

Quando si accede a una query salvata dall&#39;editor di query, [!UICONTROL Schedules] sotto il nome della query. Seleziona **[!UICONTROL Schedules]**.

![Editor query con la scheda Schedules evidenziata.](../images/ui/query-schedules/schedules-tab.png)

Verrà visualizzata l&#39;area di lavoro pianificazioni. Seleziona **[!UICONTROL Aggiungi pianificazione]** per creare una pianificazione.

![Nell&#39;area di lavoro Pianificazione editor query è evidenziata Aggiungi pianificazione.](../images/ui/query-schedules/add-schedule.png)

Viene visualizzata la pagina dei dettagli della pianificazione. In questa pagina puoi scegliere la frequenza della query pianificata, la data di inizio e di fine, il giorno della settimana in cui verrà eseguita la query pianificata e il set di dati in cui esportare la query.

![Viene evidenziato il pannello Dettagli pianificazione.](../images/ui/query-schedules/schedule-details.png)

Puoi scegliere le seguenti opzioni per **[!UICONTROL Frequenza]**:

- **[!UICONTROL Ogni ora]**: la query pianificata viene eseguita ogni ora per il periodo di data selezionato.
- **[!UICONTROL Giornaliero]**: la query pianificata verrà eseguita ogni X giorni all’ora e nel periodo di data selezionati. L&#39;ora selezionata è in **UTC** e non il tuo fuso orario locale.
- **[!UICONTROL Ogni settimana]**: la query selezionata verrà eseguita nei giorni della settimana, dell’ora e del periodo di data selezionati. L&#39;ora selezionata è in **UTC** e non il tuo fuso orario locale.
- **[!UICONTROL Mensile]**: la query selezionata verrà eseguita ogni mese al giorno, all’ora e al periodo di data selezionati. L&#39;ora selezionata è in **UTC** e non il tuo fuso orario locale.
- **[!UICONTROL Annuale]**: la query selezionata verrà eseguita ogni anno al giorno, al mese, all’ora e al periodo di data selezionati. L&#39;ora selezionata è in **UTC** e non il tuo fuso orario locale.

Per il set di dati di output, puoi utilizzare un set di dati esistente o crearne uno nuovo.

>[!IMPORTANT]
>
> Poiché si utilizza un set di dati esistente o si crea un nuovo set di dati, **non** devono includere `INSERT INTO` o `CREATE TABLE AS SELECT` come parte della query, poiché i set di dati sono già impostati. Inclusione di `INSERT INTO` o `CREATE TABLE AS SELECT` come parte delle query pianificate genererà un errore.

Dopo aver confermato tutti questi dettagli, seleziona **[!UICONTROL Salva]** per creare una pianificazione. L&#39;utente viene reindirizzato all&#39;area di lavoro pianificazioni che visualizza i dettagli della pianificazione appena creata, inclusi l&#39;ID pianificazione, la pianificazione stessa e il set di dati di output della pianificazione. Puoi utilizzare l’ID pianificazione per cercare ulteriori informazioni sulle esecuzioni della query pianificata stessa. Per ulteriori informazioni, leggere [guida degli endpoint di esecuzione delle query pianificate](../api/runs-scheduled-queries.md).

![Area di lavoro pianificazioni con la pianificazione appena creata evidenziata.](../images/ui/query-schedules/schedules-workspace.png)

## Eliminare o disattivare una pianificazione {#delete-schedule}

È possibile eliminare o disattivare una pianificazione dall&#39;area di lavoro pianificazioni. È necessario selezionare un modello di query da [!UICONTROL Modelli] scheda o [!UICONTROL Query pianificate] per passare all’editor delle query e selezionare **[!UICONTROL Pianificazione]** per accedere all&#39;area di lavoro pianificazioni.

Selezionare una pianificazione dalle righe delle pianificazioni disponibili. Puoi utilizzare l’interruttore per disabilitare o abilitare la query pianificata.

>[!IMPORTANT]
>
>È necessario disattivare la pianificazione prima di eliminare una pianificazione per una query.

Seleziona **[!UICONTROL Eliminare una pianificazione]** per eliminare la pianificazione disabilitata.

![Area di lavoro pianificazioni con le opzioni Disattiva pianificazione ed Elimina pianificazione evidenziate.](../images/ui/query-schedules/delete-schedule.png)
