---
description: Scopri come aggiornare un flusso di dati di origini esistenti nell’interfaccia utente di Experience Platform.
title: Aggiornare un flusso di dati di connessione Source nell’interfaccia utente
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: c3082a8769f317407197b3fd05b36cfe00b36470
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 8%

---

# Aggiornare i flussi di dati nell’interfaccia utente

Leggi questa esercitazione per i passaggi su come aggiornare un flusso di dati esistente, incluse le configurazioni di pianificazione e mappatura, utilizzando l’area di lavoro origini nell’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Aggiornare i flussi di dati {#update-dataflows}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflows_daysRemaining"
>title="Scadenza set di dati"
>abstract="Questa colonna indica il numero di giorni rimanenti al set di dati di destinazione prima della scadenza automatica.<br>Un flusso di dati avrà esito negativo se il set di dati di destinazione è scaduto. Per evitare che un flusso di dati sia di esito negativo, assicurati che la scadenza del set di dati di destinazione sia impostata sulla data corretta. Consulta la documentazione per scoprire come aggiornare le date di scadenza."

Nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra, quindi seleziona **[!UICONTROL Flussi dati]** dall&#39;intestazione superiore.

![Catalogo delle origini con la scheda intestazione dei flussi di dati selezionata.](../../images/tutorials/update-dataflows/catalog.png)

>[!TIP]
>
>Puoi ordinare e filtrare i flussi di dati utilizzando le funzionalità di filtro. Per ulteriori informazioni, leggere la guida su [filtraggio degli oggetti di origine nell&#39;interfaccia utente](./filter.md).

Nella pagina [!UICONTROL Flussi dati] viene visualizzato un elenco di tutti i flussi di dati esistenti nell&#39;organizzazione. Individuare il flusso di dati che si desidera aggiornare, quindi selezionare i puntini di sospensione (`...`) accanto ad esso. Viene visualizzato un menu a discesa con un elenco di opzioni tra cui puoi scegliere per effettuare configurazioni aggiuntive al flusso di dati esistente.

Per aggiornare il flusso di dati, seleziona **[!UICONTROL Aggiorna flusso di dati]**.

![Menu a discesa in cui sono elencate le opzioni per l&#39;aggiornamento dei flussi di dati.](../../images/tutorials/update-dataflows/dropdown_update.png)

Si viene indirizzati al flusso di lavoro di origine in cui è possibile procedere all&#39;aggiornamento di aspetti del flusso di dati, inclusi i relativi dettagli nel passaggio [!UICONTROL Fornisci dettagli flusso di dati].

### Aggiorna mappatura {#update-mapping}

>[!NOTE]
>
>La funzione di modifica della mappatura non è attualmente supportata per le seguenti origini: Adobe Analytics, Adobe Audience Manager, API HTTP e [!DNL Marketo Engage].

Durante questo processo, puoi anche aggiornare i set di mappatura associati al flusso di dati.  L’interfaccia di mappatura visualizza la mappatura esistente del flusso di dati e non un nuovo set di mappatura consigliato. Gli aggiornamenti delle mappature vengono applicati solo alle esecuzioni dei flussi di dati pianificate in futuro. I set di mappatura di un flusso di dati pianificato per l’acquisizione una tantum non possono essere aggiornati.

Utilizza l’interfaccia di mappatura per modificare i set di mappatura applicati al flusso di dati. Per i passaggi completi su come utilizzare l&#39;interfaccia di mappatura, consulta la [guida dell&#39;interfaccia utente per la preparazione dei dati](../../../data-prep/ui/mapping.md) per ulteriori informazioni.

![Passaggio di mappatura del flusso di lavoro origini. Utilizzare questo passaggio per aggiornare i mapping associati al flusso di dati.](../../images/tutorials/update-dataflows/mapping.png)

### Aggiorna pianificazione

Dopo aver aggiornato le mappature del flusso di dati, puoi procedere con l’aggiornamento della pianificazione di acquisizione per acquisire il flusso di dati con i suoi nuovi dati di mappatura. Puoi aggiornare solo la pianificazione di acquisizione dei flussi di dati configurati per l’acquisizione in una pianificazione ricorrente. Non puoi ripianificare un flusso di dati configurato per l’acquisizione una tantum.

Puoi anche aggiornare la pianificazione dell’acquisizione del flusso di dati utilizzando l’opzione di aggiornamento in linea fornita nella pagina dei flussi di dati.

Dalla pagina dei flussi di dati, seleziona i puntini di sospensione (`...`) accanto al nome del flusso di dati, quindi seleziona **[!UICONTROL Modifica pianificazione]** dal menu a discesa visualizzato.

![Passaggio di pianificazione del flusso di lavoro origini. Utilizzare questo passaggio per aggiornare la pianificazione del flusso di dati.](../../images/tutorials/update-dataflows/dropdown_edit.png)

La finestra di dialogo **[!UICONTROL Modifica pianificazione]** offre opzioni per aggiornare la frequenza di acquisizione e la frequenza di intervallo del flusso di dati. Dopo aver impostato i valori di frequenza e intervallo aggiornati, selezionare **[!UICONTROL Salva]**.

![Finestra popup che consente di modificare la pianificazione di acquisizione del flusso di dati.](../../images/tutorials/update-dataflows/edit_schedule.png)

### Disattiva flusso di dati

Puoi disattivare il flusso di dati utilizzando lo stesso menu a discesa. Per disabilitare il flusso di dati, seleziona **[!UICONTROL Disabilita flusso di dati]**.

![Menu a discesa con opzione per disabilitare il flusso di dati.](../../images/tutorials/update-dataflows/dropdown_disable.png)

Selezionare [!UICONTROL Disattiva] dalla finestra popup visualizzata.

![Finestra popup in cui confermare di voler disabilitare il flusso di dati.](../../images/tutorials/update-dataflows/disable_dataflow.png)

Se e quando in seguito riabiliti questo flusso di dati, Experience Platform pianifica automaticamente le esecuzioni di backfill per coprire il periodo durante il quale il flusso di dati è stato disabilitato. Experienci Platform Ad esempio, se il flusso di dati è stato configurato per essere eseguito su base oraria ed è stato disabilitato per 48 ore, al momento della riabilitazione del flusso di dati verranno eseguite 48 esecuzioni di backfill per elaborare gli intervalli persi.

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente l&#39;area di lavoro [!UICONTROL Sources] per aggiornare la pianificazione dell&#39;acquisizione e i set di mappatura del flusso di dati.

Per i passaggi su come eseguire queste operazioni a livello di programmazione utilizzando l&#39;API [!DNL Flow Service], fare riferimento al tutorial su [aggiornamento dei flussi di dati tramite l&#39;API del servizio Flusso](../../tutorials/api/update-dataflows.md).
