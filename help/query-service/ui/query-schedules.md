---
title: Pianificazioni query
description: Scopri come automatizzare le esecuzioni delle query pianificate, eliminare o disabilitare una pianificazione delle query e utilizzare le opzioni di pianificazione disponibili tramite l’interfaccia utente di Adobe Experience Platform.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# Pianificazioni query

È possibile automatizzare le esecuzioni delle query creando pianificazioni delle query. Le query pianificate vengono eseguite su una cadenza personalizzata per gestire i dati in base a frequenza, data e ora. Puoi anche scegliere un set di dati di output per i risultati, se necessario. Le query salvate come modello possono essere pianificate dall’Editor query.

>[!IMPORTANT]
>
>Di seguito è riportato un elenco di limitazioni per le query pianificate quando si utilizza l’editor delle query. Non si applicano al [!DNL Query Service] API:<br/>È possibile aggiungere una pianificazione solo a una query già creata, salvata ed eseguita.<br/>You **impossibile** aggiungi una pianificazione a una query con parametri.<br/>Query pianificate **impossibile** contiene un blocco anonimo.

Tutte le query pianificate vengono aggiunte all’elenco nel [!UICONTROL Query pianificate] scheda . Da quell’area di lavoro puoi monitorare lo stato di tutti i processi di query pianificati tramite l’interfaccia utente. Sulla [!UICONTROL Query pianificate] è possibile trovare informazioni importanti sulle esecuzioni della query e sottoscrivere gli avvisi. Le informazioni disponibili includono lo stato, i dettagli della pianificazione e i messaggi/codici di errore in caso di errore durante l’esecuzione. Consulta la sezione [Monitoraggio del documento delle query pianificate](./monitor-queries.md) per ulteriori informazioni.

## Creare pianificazioni di query {#create-schedule}

Per aggiungere una pianificazione a una query, selezionare un modello di query dal [!UICONTROL Modelli] oppure [!UICONTROL Query pianificate] scheda per passare all’Editor query.

Per informazioni su come aggiungere le pianificazioni utilizzando l’API, leggi la [guida all’endpoint delle query pianificate](../api/scheduled-queries.md).

Quando si accede a una query salvata dall’Editor delle query, l’ [!UICONTROL Pianificazioni] sotto il nome della query viene visualizzata la scheda . Seleziona **[!UICONTROL Pianificazioni]**.

![Editor query con la scheda Pianificazioni evidenziata.](../images/ui/query-schedules/schedules-tab.png)

Viene visualizzata l&#39;area di lavoro pianificazioni. Seleziona **[!UICONTROL Aggiungi pianificazione]** per creare una pianificazione.

![Area di lavoro Pianificazione editor query con Aggiungi pianificazione evidenziata.](../images/ui/query-schedules/add-schedule.png)

Viene visualizzata la pagina dei dettagli della pianificazione. In questa pagina puoi scegliere la frequenza della query pianificata, la data di inizio e di fine, il giorno della settimana in cui verrà eseguita la query pianificata e il set di dati in cui esportare la query.

![Il pannello Dettagli pianificazione è evidenziato.](../images/ui/query-schedules/schedule-details.png)

Puoi scegliere le seguenti opzioni per **[!UICONTROL Frequenza]**:

- **[!UICONTROL Orario]**: La query pianificata viene eseguita ogni ora per il periodo di data selezionato.
- **[!UICONTROL Giornaliero]**: La query pianificata verrà eseguita ogni X giorni all’ora e al periodo di data selezionato. Tieni presente che l’ora selezionata è in **UTC** e non il fuso orario locale.
- **[!UICONTROL Settimanale]**: La query selezionata verrà eseguita nei giorni della settimana, dell’ora e del periodo di data selezionati. Tieni presente che l’ora selezionata è in **UTC** e non il fuso orario locale.
- **[!UICONTROL Mensile]**: La query selezionata viene eseguita ogni mese al giorno, all’ora e al periodo di data selezionato. Tieni presente che l’ora selezionata è in **UTC** e non il fuso orario locale.
- **[!UICONTROL Annuale]**: La query selezionata viene eseguita ogni anno al giorno, al mese, all’ora e al periodo di data selezionato. Tieni presente che l’ora selezionata è in **UTC** e non il fuso orario locale.

Per il set di dati di output, puoi utilizzare un set di dati esistente o crearne uno nuovo.

>[!IMPORTANT]
>
> Poiché utilizzi un set di dati esistente o crei un nuovo, lo fai **not** devono includere `INSERT INTO` o `CREATE TABLE AS SELECT` come parte della query, poiché i set di dati sono già impostati. Includere `INSERT INTO` o `CREATE TABLE AS SELECT` come parte delle query pianificate si verifica un errore.

Dopo aver confermato tutti questi dettagli, seleziona **[!UICONTROL Salva]** per creare una pianificazione. Viene visualizzata l’area di lavoro pianificazioni che visualizza i dettagli della nuova pianificazione creata, inclusi l’ID pianificazione, la pianificazione stessa e il set di dati di output della pianificazione. Puoi utilizzare l’ID pianificazione per cercare ulteriori informazioni sulle esecuzioni della query pianificata stessa. Per saperne di più, leggere il [guida agli endpoint di esecuzione delle query programmate](../api/runs-scheduled-queries.md).

![Area di lavoro pianificazioni con la pianificazione appena creata evidenziata.](../images/ui/query-schedules/schedules-workspace.png)

## Eliminare o disabilitare una pianificazione {#delete-schedule}

È possibile eliminare o disattivare una pianificazione dall&#39;area di lavoro pianificazioni. È necessario selezionare un modello di query dal [!UICONTROL Modelli] oppure [!UICONTROL Query pianificate] scheda per passare all’Editor query e selezionare **[!UICONTROL Pianificazione]** per accedere all&#39;area di lavoro pianificazioni.

Selezionare una pianificazione dalle righe delle pianificazioni disponibili. Puoi utilizzare l’interruttore per disattivare o abilitare la query pianificata.

>[!IMPORTANT]
>
>È necessario disattivare la pianificazione prima di eliminare una pianificazione per una query.

Seleziona **[!UICONTROL Eliminare una pianificazione]** per eliminare la pianificazione disabilitata.

![Area di lavoro pianificazioni con Disabilita pianificazione ed Elimina pianificazione evidenziata.](../images/ui/query-schedules/delete-schedule.png)


