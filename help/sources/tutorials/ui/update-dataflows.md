---
keywords: Experience Platform;home;argomenti popolari;aggiorna flussi di dati;modifica pianificazione
description: Questa esercitazione illustra i passaggi necessari per aggiornare una pianificazione del flusso di dati, incluse la frequenza di acquisizione e la frequenza di intervallo, utilizzando l’area di lavoro Origini.
solution: Experience Platform
title: Aggiornare un flusso di dati di connessione sorgente nell’interfaccia utente
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: cef5c203acf3318445399669336166e6627ebe66
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 8%

---

# Aggiornare i flussi di dati nell’interfaccia utente

Questa esercitazione illustra i passaggi necessari per aggiornare un flusso di dati esistente, incluse la pianificazione e la mappatura, mediante l’area di lavoro origini.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../sandboxes/home.md): Experienci Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Aggiornare i flussi di dati {#update-dataflows}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflows_daysRemaining"
>title="Scadenza set di dati"
>abstract="Questa colonna indica il numero di giorni rimanenti al set di dati di destinazione prima della scadenza automatica.<br>Un flusso di dati avrà esito negativo se il set di dati di destinazione è scaduto. Per evitare che un flusso di dati sia di esito negativo, assicurati che la scadenza del set di dati di destinazione sia impostata sulla data corretta. Consulta la documentazione per scoprire come aggiornare le date di scadenza."

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Seleziona **[!UICONTROL Flussi dati]** dall’intestazione in alto per visualizzare un elenco dei flussi di dati esistenti.

![catalogo](../../images/tutorials/update-dataflows/catalog.png)

Il [!UICONTROL Flussi dati] La pagina contiene un elenco di tutti i flussi di dati esistenti, incluse informazioni sul set di dati di destinazione, sull’origine e sul nome dell’account corrispondenti.

Per ordinare l’elenco, seleziona l’icona del filtro ![filter](../../images/tutorials/update/filter.png) in alto a sinistra per utilizzare il pannello ordina.

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

Il pannello di ordinamento fornisce un elenco di tutte le origini disponibili. È possibile selezionare più origini dall’elenco per accedere a una selezione filtrata di flussi di dati appartenenti a origini diverse.

Seleziona l’origine con cui desideri lavorare per visualizzare un elenco dei flussi di dati esistenti. Dopo aver identificato il flusso di dati da aggiornare, seleziona i puntini di sospensione (`...`) accanto al nome del flusso di dati.

![edit-source](../../images/tutorials/update-dataflows/edit-source.png)

Viene visualizzato un menu a discesa che fornisce le opzioni per aggiornare il flusso di dati selezionato. Da qui puoi scegliere di aggiornare i set di mappatura e la pianificazione dell’acquisizione di un flusso di dati. Puoi anche selezionare le opzioni per ispezionare il flusso di dati nel dashboard di monitoraggio, abbonarti agli avvisi, nonché disabilitare o eliminare il flusso di dati.

Per aggiornare le informazioni del flusso di dati, seleziona **[!UICONTROL Aggiorna flusso di dati]**.

![update-dataflow](../../images/tutorials/update-dataflows/update-dataflow.png)

### Aggiungi dati

Il [!UICONTROL Aggiungi dati] viene visualizzato il passaggio. Selezionare il formato dati appropriato per esaminare il contenuto dei dati selezionati, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![add-data](../../images/tutorials/update-dataflows/add-data.png)

### Dettaglio del flusso di dati

In [!UICONTROL Dettagli del flusso di dati] pagina, puoi fornire un nome e una descrizione aggiornati per il flusso di dati e riconfigurare la soglia di errore del flusso di dati. Durante questo passaggio, puoi anche configurare o modificare le impostazioni per l’abbonamento agli avvisi.

Dopo aver fornito i valori aggiornati, seleziona **[!UICONTROL Successivo]**.

![dataflow-detail](../../images/tutorials/update-dataflows/dataflow-detail.png)

### Mappatura

>[!NOTE]
>
>La funzione di modifica della mappatura non è attualmente supportata per le seguenti origini: Adobe Analytics, Adobe Audience Manager, API HTTP e [!DNL Marketo Engage].

Il [!UICONTROL Mappatura] fornisce un’interfaccia in cui puoi aggiungere e rimuovere i set di mappatura associati al flusso di dati.

L’interfaccia di mappatura visualizza il set di mappatura esistente del flusso di dati e non un nuovo set di mappatura consigliato. Gli aggiornamenti delle mappature vengono applicati solo alle esecuzioni dei flussi di dati pianificate in futuro. I set di mappatura di un flusso di dati pianificato per l’acquisizione una tantum non possono essere aggiornati.

Da qui puoi utilizzare l’interfaccia di mappatura per modificare i set di mappatura applicati al flusso di dati. Per i passaggi completi su come utilizzare l&#39;interfaccia di mappatura, vedi [guida all’interfaccia utente per la preparazione dei dati](../../../data-prep/ui/mapping.md) per ulteriori informazioni.

![mappatura](../../images/tutorials/update-dataflows/mapping.png)

### Pianificazione

Il [!UICONTROL Pianificazione] viene visualizzato un passaggio che consente di aggiornare la pianificazione dell’acquisizione del flusso di dati e di acquisire automaticamente i dati di origine selezionati con le mappature aggiornate.

>[!NOTE]
>
>Non puoi ripianificare un flusso di dati pianificato per l’acquisizione una tantum.

![new-schedule](../../images/tutorials/update-dataflows/new-schedule.png)

Puoi anche aggiornare la pianificazione dell’acquisizione del flusso di dati utilizzando l’opzione di aggiornamento in linea fornita nella pagina dei flussi di dati.

Dalla pagina dei flussi di dati, seleziona i puntini di sospensione (`...`) accanto al nome del flusso di dati, quindi seleziona **[!UICONTROL Modifica pianificazione]** dal menu a discesa visualizzato.

![edit-schedule](../../images/tutorials/update-dataflows/edit-schedule.png)

Il **[!UICONTROL Modifica pianificazione]** fornisce opzioni per aggiornare la frequenza di acquisizione e la frequenza di intervallo del flusso di dati. Una volta impostati i valori di frequenza e intervallo aggiornati, selezionare **[!UICONTROL Salva]**.

![pop-up di programmazione](../../images/tutorials/update-dataflows/schedule-pop-up.png)

### Revisione

Il **[!UICONTROL Revisione]** viene visualizzato un passaggio che consente di rivedere il flusso di dati prima che venga aggiornato.

Dopo aver rivisto il flusso di dati, seleziona **[!UICONTROL Fine]** e lascia un po’ di tempo per creare il flusso di dati con i nuovi set di mappatura.

![recensione](../../images/tutorials/update-dataflows/review.png)

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente il [!UICONTROL Sorgenti] workspace per aggiornare la pianificazione dell’acquisizione e i set di mappatura del flusso di dati.

Per i passaggi su come eseguire queste operazioni a livello di programmazione utilizzando [!DNL Flow Service] API, fai riferimento al tutorial su [aggiornamento dei flussi di dati tramite l’API del servizio Flusso](../../tutorials/api/update-dataflows.md).
