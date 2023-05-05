---
title: Gestire le scadenze del set di dati
description: Scopri come pianificare la scadenza di un set di dati nell’interfaccia utente di Adobe Experience Platform.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: a1628df7d0eefc795d1eaeefce842a65c7133322
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 22%

---

# Gestire le scadenze dei set di dati {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="Elimina record e set di dati cliente indesiderati o scaduti"
>abstract="<h2>Descrizione</h2><p>Per gestire il ciclo di vita dei dati di Experience Platform non correlati alla conformità alle normative, puoi eliminare i record dei consumatori e pianificare le date di scadenza dei set di dati. Per creare o gestire le richieste dell’interessato, consulta il blocco del caso d’uso “Rispetta le richieste di privacy dell’interessato”.</p>"

>[!IMPORTANT]
>
>Le funzionalità di igiene dei dati in Adobe Experience Platform sono attualmente disponibili solo per le organizzazioni che hanno acquistato **Scudo sanitario Adobe** o **Adobe Privacy e sicurezza scudo**. Queste funzionalità saranno disponibili prossimamente. Per ulteriori informazioni sulla loro prossima disponibilità, contatta il tuo rappresentante di Adobe Service. Tuttavia, puoi immediatamente [eliminare i set di dati tramite [!UICONTROL Set di dati] Interfaccia](../../catalog/datasets/user-guide.md#delete).

La [[!UICONTROL Igiene dei dati] workspace](./overview.md) nell’interfaccia utente di Adobe Experience Platform consente di pianificare le scadenze per i set di dati. Quando un set di dati raggiunge la data di scadenza, il data lake, il servizio Identity e il profilo cliente in tempo reale iniziano processi separati per rimuovere il contenuto del set di dati dai rispettivi servizi. Una volta eliminati i dati da tutti e tre i servizi, la scadenza viene contrassegnata come completa.

>[!WARNING]
>
>Se un set di dati è impostato per la scadenza, devi modificare manualmente tutti i flussi di dati che potrebbero acquisire dati in tale set di dati in modo che i flussi di lavoro downstream non ne risentano.

Questo documento illustra come pianificare e gestire le scadenze dei set di dati nell’interfaccia utente di Platform.

## Pianificazione della scadenza di un set di dati {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="Istruzioni"
>abstract="<ul><li>Seleziona <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html?lang=it">Igiene dei dati</a> nel menu di navigazione a sinistra e quindi seleziona <b>Crea richiesta</b>.</li><li>Per eliminare i record:</li>   <li>Seleziona <b>Record</b>.</li>   <li>Seleziona un set di dati specifico da cui eliminare i record oppure scegli l’opzione per eliminarli da tutti i set di dati.</li>   <li>Fornire le identità dei consumatori i cui record devono essere cancellati. Seleziona <b>Aggiungi identità</b> per fornire le identità una alla volta oppure seleziona <b>Scegli i file</b> per caricare un file JSON di identità.</li>   <li>Se necessario, seleziona <b>Modello</b> per visualizzare il formato previsto del file JSON.</li><li>Per istruzioni, consulta la documentazione per la <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html?lang=it#schedule-dataset-expiration">pianificazione delle date di scadenza dei set di dati</a>.</li></ul>"

Per creare una nuova richiesta, seleziona **[!UICONTROL Crea richiesta]** dalla pagina principale nell’area di lavoro.

![Immagine che mostra [!UICONTROL Crea richiesta] pulsante selezionato](../images/ui/ttl/create-request-button.png)

Viene visualizzata la finestra di dialogo per la creazione della richiesta. Sotto la **[!UICONTROL Azione richiesta]** sezione , seleziona **[!UICONTROL Elimina set di dati]** per aggiornare i controlli disponibili per la pianificazione della scadenza del set di dati.

![Immagine che mostra [!UICONTROL Crea richiesta] pulsante selezionato](../images/ui/ttl/dataset-selected.png)

### Selezionare una data e un set di dati

Viene visualizzata la finestra di dialogo per la creazione della richiesta. Sotto la **[!UICONTROL Azione richiesta]** seleziona la data in cui desideri eliminare il set di dati. Puoi immettere la data manualmente (nel formato `mm/dd/yyyy`) o seleziona l’icona Calendario (![Immagine dell&#39;icona del calendario](../images/ui/ttl/calendar-icon.png)) per selezionare la data da una finestra di dialogo.

![Immagine che mostra una data di scadenza impostata per il set di dati](../images/ui/ttl/select-date.png)

Successivamente, sotto **[!UICONTROL Dettagli set di dati]**, seleziona l’icona del database (![Immagine dell’icona del database](../images/ui/ttl/database-icon.png)) per aprire una finestra di dialogo per la selezione di un set di dati. Scegli un set di dati dall’elenco a cui applicare la scadenza, quindi seleziona **[!UICONTROL Fine]**.

![Immagine che mostra un set di dati selezionato](../images/ui/ttl/select-dataset.png)

>[!NOTE]
Vengono visualizzati solo i set di dati appartenenti alla sandbox corrente.

### Invia la richiesta

La [!UICONTROL Dettagli set di dati] viene compilata per includere l&#39;identità e lo schema principali per il set di dati selezionato. Sotto **[!UICONTROL Impostazioni richieste]**, immetti un nome e una descrizione facoltativa per la richiesta, seguiti da **[!UICONTROL Invia]**.

![Immagine che mostra [!UICONTROL Invia] pulsante selezionato](../images/ui/ttl/submit.png)

Viene richiesto di confermare la data in cui il set di dati verrà eliminato. Seleziona **[!UICONTROL Invia]** per continuare.

Dopo l&#39;invio della richiesta, viene creato un ordine di lavoro e viene visualizzato nella scheda principale [!UICONTROL Igiene dei dati] workspace. Da qui è possibile monitorare lo stato dell&#39;ordine di lavoro durante l&#39;elaborazione della richiesta.

>[!NOTE]
Consulta la sezione panoramica su [Tempistiche e trasparenza](../home.md#dataset-expiration-transparency) per informazioni dettagliate sull’elaborazione delle scadenze dei set di dati una volta eseguite.

## Modificare o annullare la scadenza di un set di dati

Per modificare o annullare la scadenza di un set di dati, seleziona **[!UICONTROL Set di dati]** nella pagina principale dell’area di lavoro e seleziona la scadenza del set di dati dall’elenco.

Nella pagina dei dettagli della scadenza del set di dati, la barra a destra mostra i controlli per modificare o annullare l’eliminazione pianificata.

## Passaggi successivi

Questo documento illustra come pianificare le scadenze dei set di dati nell’interfaccia utente di Experience Platform. Per informazioni su come eseguire altre attività di igiene dei dati nell’interfaccia utente, consulta [panoramica dell&#39;interfaccia utente per l&#39;igiene dei dati](./overview.md).

Per informazioni su come pianificare le scadenze dei set di dati utilizzando l’API di igiene dati, consulta [guida all’endpoint di scadenza dei set di dati](../api/dataset-expiration.md).
