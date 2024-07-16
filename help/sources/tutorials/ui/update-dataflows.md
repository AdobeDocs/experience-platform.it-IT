---
keywords: Experience Platform;home;argomenti popolari;aggiorna flussi di dati;modifica pianificazione
description: Questa esercitazione illustra i passaggi necessari per aggiornare una pianificazione del flusso di dati, incluse la frequenza di acquisizione e la frequenza di intervallo, utilizzando l’area di lavoro Origini.
solution: Experience Platform
title: Aggiornare un flusso di dati di connessione Source nell’interfaccia utente
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: cef5c203acf3318445399669336166e6627ebe66
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 9%

---

# Aggiornare i flussi di dati nell’interfaccia utente

Questa esercitazione illustra i passaggi necessari per aggiornare un flusso di dati esistente, incluse la pianificazione e la mappatura, mediante l’area di lavoro origini.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Aggiornare i flussi di dati {#update-dataflows}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflows_daysRemaining"
>title="Scadenza set di dati"
>abstract="Questa colonna indica il numero di giorni rimanenti al set di dati di destinazione prima della scadenza automatica.<br>Un flusso di dati avrà esito negativo se il set di dati di destinazione è scaduto. Per evitare che un flusso di dati sia di esito negativo, assicurati che la scadenza del set di dati di destinazione sia impostata sulla data corretta. Consulta la documentazione per scoprire come aggiornare le date di scadenza."

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Seleziona **[!UICONTROL Flussi dati]** dall&#39;intestazione superiore per visualizzare un elenco dei flussi dati esistenti.

![catalogo](../../images/tutorials/update-dataflows/catalog.png)

La pagina [!UICONTROL Flussi dati] contiene un elenco di tutti i flussi di dati esistenti, incluse informazioni sul set di dati di destinazione, sull&#39;origine e sul nome account corrispondenti.

Per ordinare l&#39;elenco, seleziona l&#39;icona del filtro ![filter](../../images/tutorials/update/filter.png) in alto a sinistra per utilizzare il pannello di ordinamento.

![flussi di dati filtro](../../images/tutorials/update-dataflows/filter-dataflows.png)

Il pannello di ordinamento fornisce un elenco di tutte le origini disponibili. È possibile selezionare più origini dall’elenco per accedere a una selezione filtrata di flussi di dati appartenenti a origini diverse.

Seleziona l’origine con cui desideri lavorare per visualizzare un elenco dei flussi di dati esistenti. Dopo aver identificato il flusso di dati da aggiornare, seleziona i puntini di sospensione (`...`) accanto al nome del flusso di dati.

![edit-source](../../images/tutorials/update-dataflows/edit-source.png)

Viene visualizzato un menu a discesa che fornisce le opzioni per aggiornare il flusso di dati selezionato. Da qui puoi scegliere di aggiornare i set di mappatura e la pianificazione dell’acquisizione di un flusso di dati. Puoi anche selezionare le opzioni per ispezionare il flusso di dati nel dashboard di monitoraggio, abbonarti agli avvisi, nonché disabilitare o eliminare il flusso di dati.

Per aggiornare le informazioni del flusso di dati, seleziona **[!UICONTROL Aggiorna flusso di dati]**.

![aggiornamento-flusso di dati](../../images/tutorials/update-dataflows/update-dataflow.png)

### Aggiungi dati

Viene visualizzato il passaggio [!UICONTROL Aggiungi dati]. Selezionare il formato dati appropriato per esaminare il contenuto dei dati selezionati, quindi selezionare **[!UICONTROL Avanti]** per continuare.

![add-data](../../images/tutorials/update-dataflows/add-data.png)

### Dettaglio del flusso di dati

Nella pagina [!UICONTROL Dettagli flusso di dati] puoi fornire un nome e una descrizione aggiornati per il flusso di dati, nonché riconfigurare la soglia di errore del flusso di dati. Durante questo passaggio, puoi anche configurare o modificare le impostazioni per l’abbonamento agli avvisi.

Dopo aver fornito i valori aggiornati, seleziona **[!UICONTROL Avanti]**.

![dettagli flusso di dati](../../images/tutorials/update-dataflows/dataflow-detail.png)

### Mappatura

>[!NOTE]
>
>La funzione di modifica della mappatura non è attualmente supportata per le seguenti origini: Adobe Analytics, Adobe Audience Manager, API HTTP e [!DNL Marketo Engage].

La pagina [!UICONTROL Mapping] offre un&#39;interfaccia in cui è possibile aggiungere e rimuovere i set di mappatura associati al flusso di dati.

L’interfaccia di mappatura visualizza il set di mappatura esistente del flusso di dati e non un nuovo set di mappatura consigliato. Gli aggiornamenti delle mappature vengono applicati solo alle esecuzioni dei flussi di dati pianificate in futuro. I set di mappatura di un flusso di dati pianificato per l’acquisizione una tantum non possono essere aggiornati.

Da qui puoi utilizzare l’interfaccia di mappatura per modificare i set di mappatura applicati al flusso di dati. Per i passaggi completi su come utilizzare l&#39;interfaccia di mappatura, consulta la [guida dell&#39;interfaccia utente per la preparazione dei dati](../../../data-prep/ui/mapping.md) per ulteriori informazioni.

![mappatura](../../images/tutorials/update-dataflows/mapping.png)

### Pianificazione

Viene visualizzato il passaggio [!UICONTROL Pianificazione], che consente di aggiornare la pianificazione dell&#39;acquisizione del flusso di dati e di acquisire automaticamente i dati di origine selezionati con le mappature aggiornate.

>[!NOTE]
>
>Non puoi ripianificare un flusso di dati pianificato per l’acquisizione una tantum.

![new-schedule](../../images/tutorials/update-dataflows/new-schedule.png)

Puoi anche aggiornare la pianificazione dell’acquisizione del flusso di dati utilizzando l’opzione di aggiornamento in linea fornita nella pagina dei flussi di dati.

Dalla pagina dei flussi di dati, seleziona i puntini di sospensione (`...`) accanto al nome del flusso di dati, quindi seleziona **[!UICONTROL Modifica pianificazione]** dal menu a discesa visualizzato.

![modifica-pianificazione](../../images/tutorials/update-dataflows/edit-schedule.png)

La finestra di dialogo **[!UICONTROL Modifica pianificazione]** offre opzioni per aggiornare la frequenza di acquisizione e la frequenza di intervallo del flusso di dati. Dopo aver impostato i valori di frequenza e intervallo aggiornati, selezionare **[!UICONTROL Salva]**.

![popup di pianificazione](../../images/tutorials/update-dataflows/schedule-pop-up.png)

### Controlla

Viene visualizzato il passaggio **[!UICONTROL Rivedi]**, che consente di rivedere il flusso di dati prima che venga aggiornato.

Dopo aver esaminato il flusso di dati, seleziona **[!UICONTROL Fine]** e attendi che venga creato il flusso di dati con i nuovi set di mappatura.

![revisione](../../images/tutorials/update-dataflows/review.png)

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente l&#39;area di lavoro [!UICONTROL Sources] per aggiornare la pianificazione dell&#39;acquisizione e i set di mappatura del flusso di dati.

Per i passaggi su come eseguire queste operazioni a livello di programmazione utilizzando l&#39;API [!DNL Flow Service], fare riferimento al tutorial su [aggiornamento dei flussi di dati tramite l&#39;API del servizio Flusso](../../tutorials/api/update-dataflows.md).
