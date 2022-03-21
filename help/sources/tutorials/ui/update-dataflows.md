---
keywords: Experience Platform;home;argomenti popolari;aggiornare i flussi di dati;modificare la pianificazione
description: Questa esercitazione descrive i passaggi per aggiornare una pianificazione del flusso di dati, inclusa la frequenza di acquisizione e la frequenza di intervallo, utilizzando l’area di lavoro Origini.
solution: Experience Platform
title: Aggiornare un flusso di dati di connessione sorgente nell’interfaccia utente
topic-legacy: overview
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: 6a9ad0ce5d664e3b32cab4183b54fabd5d9d19e3
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 0%

---

# Aggiornare i flussi di dati nell’interfaccia utente

Questa esercitazione descrive come aggiornare un flusso di dati esistente, inclusa la relativa pianificazione e mappatura, utilizzando l’area di lavoro origini.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Aggiornare i flussi di dati

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. Seleziona **[!UICONTROL Flussi di dati]** dall’intestazione superiore per visualizzare un elenco dei flussi di dati esistenti.

![catalogo](../../images/tutorials/update-dataflows/catalog.png)

La [!UICONTROL Flussi di dati] contiene un elenco di tutti i flussi di dati esistenti, incluse informazioni sul set di dati di destinazione, l’origine e il nome dell’account corrispondenti.

Per eseguire l’ordinamento dell’elenco, seleziona l’icona del filtro ![filter](../../images/tutorials/update/filter.png) in alto a sinistra per utilizzare il pannello di ordinamento.

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

Il pannello di ordinamento fornisce un elenco di tutte le origini disponibili. È possibile selezionare più di un’origine dall’elenco per accedere a una selezione filtrata di flussi di dati appartenenti a origini diverse.

Seleziona l’origine con cui desideri lavorare per visualizzare un elenco dei relativi flussi di dati esistenti. Una volta identificato il flusso di dati da aggiornare, seleziona i puntini di sospensione (`...`) accanto al nome del flusso di dati.

![edit-source](../../images/tutorials/update-dataflows/edit-source.png)

Viene visualizzato un menu a discesa che fornisce le opzioni per aggiornare il flusso di dati selezionato. Da qui puoi scegliere di aggiornare i set di mappatura e la pianificazione dell’acquisizione di un flusso di dati. Puoi anche selezionare le opzioni per controllare il flusso di dati nel dashboard di monitoraggio, abbonarti agli avvisi, nonché disabilitare o eliminare il flusso di dati.

Per aggiornare le informazioni del flusso di dati, seleziona **[!UICONTROL Aggiornamento del flusso di dati]**.

![update-dataflow](../../images/tutorials/update-dataflows/update-dataflow.png)

### Aggiungi dati

La [!UICONTROL Aggiungi dati] viene visualizzato il passaggio . Selezionare il formato di dati appropriato per esaminare il contenuto dei dati selezionati, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![add-data](../../images/tutorials/update-dataflows/add-data.png)

### Dettaglio flusso di dati

In [!UICONTROL Dettaglio flusso di dati] , puoi fornire un nome e una descrizione aggiornati per il flusso di dati e riconfigurare la soglia di errore del flusso di dati. Durante questo passaggio, puoi anche configurare o modificare le impostazioni per la sottoscrizione degli avvisi.

Dopo aver fornito i valori aggiornati, seleziona **[!UICONTROL Successivo]**.

![dettaglio del flusso di dati](../../images/tutorials/update-dataflows/dataflow-detail.png)

### Mappatura

>[!NOTE]
>
>La funzione di mappatura della modifica non è attualmente supportata per le seguenti origini: Adobe Analytics, Adobe Audience Manager, API HTTP e [!DNL Marketo Engage].

La [!UICONTROL Mappatura] page offre un’interfaccia che consente di aggiungere e rimuovere set di mappature associati al flusso di dati.

L&#39;interfaccia di mappatura visualizza il set di mappatura esistente del flusso di dati e non un nuovo set di mappatura consigliato. Gli aggiornamenti di mappatura vengono applicati solo alle esecuzioni del flusso di dati pianificate in futuro. Per un flusso di dati pianificato per l’inserimento una tantum non è possibile aggiornare i relativi set di mappatura.

Da qui, puoi utilizzare l&#39;interfaccia di mappatura per modificare i set di mappatura applicati al flusso di dati. Per i passaggi completi sull’utilizzo dell’interfaccia di mappatura, consulta la sezione [guida all’interfaccia utente di preparazione dei dati](../../../data-prep/ui/mapping.md) per ulteriori informazioni.

![mappatura](../../images/tutorials/update-dataflows/mapping.png)

### Pianificazione

La [!UICONTROL Pianificazione] viene visualizzato un passaggio che consente di aggiornare la pianificazione dell’acquisizione del flusso di dati e di acquisire automaticamente i dati di origine selezionati con le mappature aggiornate.

>[!NOTE]
>
>Non è possibile ripianificare un flusso di dati pianificato per l’inserimento una tantum.

![nuovo programma](../../images/tutorials/update-dataflows/new-schedule.png)

Puoi anche aggiornare la pianificazione dell’acquisizione del flusso di dati utilizzando l’opzione di aggiornamento in linea fornita nella pagina dei flussi di dati.

Dalla pagina dei dataflows, selezionate i puntini di sospensione (`...`) accanto al nome del flusso di dati, quindi seleziona **[!UICONTROL Modifica pianificazione]** dal menu a discesa visualizzato.

![programma di modifica](../../images/tutorials/update-dataflows/edit-schedule.png)

La **[!UICONTROL Modifica pianificazione]** La finestra di dialogo fornisce le opzioni per aggiornare la frequenza di acquisizione e la frequenza di intervallo del flusso di dati. Una volta impostati i valori di frequenza e intervallo aggiornati, seleziona **[!UICONTROL Salva]**.

![pianificazione a comparsa](../../images/tutorials/update-dataflows/schedule-pop-up.png)

### Revisione

La **[!UICONTROL Revisione]** viene visualizzato un passaggio che ti consente di rivedere il flusso di dati prima di aggiornarlo.

Dopo aver esaminato il flusso di dati, seleziona **[!UICONTROL Fine]** e lascia un certo tempo per il flusso di dati con i nuovi set di mappatura da creare.

![revisione](../../images/tutorials/update-dataflows/review.png)

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente il [!UICONTROL Origini] per aggiornare la pianificazione dell’acquisizione e i set di mappatura del flusso di dati.

Per i passaggi su come eseguire queste operazioni a livello di programmazione utilizzando il [!DNL Flow Service] API, consulta l’esercitazione su [aggiornamento dei flussi di dati tramite l’API del servizio di flusso](../../tutorials/api/update-dataflows.md).
