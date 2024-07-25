---
title: Scadenze automatizzate del set di dati
description: Scopri come pianificare la scadenza di un set di dati nell’interfaccia utente di Adobe Experience Platform.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 18%

---

# Scadenze di set di dati automatizzate {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="Elimina record e set di dati cliente indesiderati o scaduti"
>abstract="<h2>Descrizione</h2><p>Per gestire il ciclo di vita dei dati di Experience Platform non correlati alla conformità alle normative, puoi eliminare i record dei consumatori e pianificare le date di scadenza dei set di dati. Per creare o gestire le richieste dell’interessato, consulta il blocco del caso d’uso “Rispetta le richieste di privacy dell’interessato”.</p>"

L&#39;area di lavoro [[!UICONTROL Ciclo di vita dati]](./overview.md) nell&#39;interfaccia utente di Adobe Experience Platform consente di pianificare le scadenze per i set di dati. Quando un set di dati raggiunge la data di scadenza, il data lake, Identity Service e Real-Time Customer Profile iniziano processi separati per rimuovere i contenuti del set di dati dai rispettivi servizi. Una volta eliminati i dati da tutti e tre i servizi, la scadenza viene contrassegnata come completata.

>[!WARNING]
>
>Se un set di dati è impostato per la scadenza, è necessario modificare manualmente i flussi di dati che potrebbero acquisire dati in tale set di dati in modo che i flussi di lavoro a valle non vengano influenzati negativamente.

Questo documento illustra come pianificare e automatizzare le scadenze dei set di dati nell’interfaccia utente di Platform.

>[!NOTE]
>
>La scadenza del set di dati non elimina attualmente i dati dall’Edge Network di Adobe Experience Platform. Tuttavia, non è possibile che i dati rimangano all’interno dell’Edge Network dopo la scadenza del set di dati. Questo perché il contratto di licenza del servizio di 15 giorni per la scadenza del set di dati si sovrappone al periodo di 14 giorni in cui i dati esistono all’interno dell’Edge Network prima di essere eliminati.

Advanced Data Lifecycle Management supporta le eliminazioni dei dataset tramite l&#39;[endpoint di scadenza del dataset](../api/dataset-expiration.md) e le eliminazioni degli ID (dati a livello di riga) utilizzando le identità primarie tramite l&#39;[endpoint workorder](../api/workorder.md). Puoi anche gestire le scadenze dei set di dati e le [eliminazioni di record](./record-delete.md) tramite l&#39;interfaccia utente di Platform. Per ulteriori informazioni, consulta la documentazione collegata.

>[!NOTE]
>
>Il ciclo di vita dei dati non supporta l’eliminazione in batch.

## Pianificare la scadenza di un set di dati {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="Istruzioni"
>abstract="<ul><li>Seleziona <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html?lang=it">Ciclo di vita dei dati</a> nel menu di navigazione a sinistra, quindi seleziona <b>Crea richiesta</b>.</li><li>Per eliminare i record:</li>   <li>Seleziona <b>Record</b>.</li>   <li>Seleziona un set di dati specifico da cui eliminare i record oppure scegli l’opzione per eliminarli da tutti i set di dati.</li>   <li>Fornire le identità dei consumatori i cui record devono essere cancellati. Seleziona <b>Aggiungi identità</b> per fornire le identità una alla volta oppure seleziona <b>Scegli i file</b> per caricare un file JSON di identità.</li>   <li>Se necessario, seleziona <b>Modello</b> per visualizzare il formato previsto del file JSON.</li><li>Per istruzioni, consulta la documentazione per la <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html?lang=it#schedule-dataset-expiration">pianificazione delle date di scadenza dei set di dati</a>.</li></ul>"

Per creare una richiesta, selezionare **[!UICONTROL Crea richiesta]** dalla pagina principale nell&#39;area di lavoro.

>[!IMPORTANT]
>
>Gli utenti di Real-Time CDP, Adobe Journey Optimizer e Customer Journey Analytics hanno 20 ordini di lavoro con scadenza set di dati pianificati in sospeso. Gli utenti di Healthcare Shield e Privacy and Security Shield hanno 50 ordini di lavoro in attesa di scadenza del set di dati pianificati. Ciò significa che puoi pianificare l’eliminazione di 20 o 50 set di dati in qualsiasi momento.<br>Ad esempio, se hai 20 scadenze pianificate per un set di dati e un set di dati deve essere eliminato domani, non puoi impostarne altre fino a dopo l&#39;eliminazione.

![L&#39;area di lavoro [!UICONTROL Ciclo di vita dati] con [!UICONTROL Crea richiesta] evidenziata.](../images/ui/ttl/create-request-button.png)

Viene visualizzato il flusso di lavoro per la creazione delle richieste. Nella sezione [!UICONTROL Azione richiesta], seleziona **[!UICONTROL Elimina set di dati]** per aggiornare i controlli per la pianificazione della scadenza dei set di dati.

![Il flusso di lavoro per la creazione delle richieste con l&#39;opzione [!UICONTROL Elimina set di dati] evidenziata.](../images/ui/ttl/dataset-selected.png)

### Seleziona una data e un set di dati {#select-date-and-dataset}

Nella sezione **[!UICONTROL Azione richiesta]**, seleziona una data entro la quale desideri eliminare il set di dati. È possibile immettere la data manualmente (nel formato `mm/dd/yyyy`) o selezionare l&#39;icona del calendario (![Icona del calendario.](/help/images/icons/calendar.png)) per selezionare la data da una finestra di dialogo.

![Finestra di dialogo del calendario con data di scadenza selezionata ed evidenziata per il set di dati.](../images/ui/ttl/select-date.png)

In **[!UICONTROL Dettagli set di dati]**, selezionare l&#39;icona del database (![Icona del database.](/help/images/icons/database.png)) per aprire una finestra di dialogo di selezione del set di dati. Scegli un set di dati dall&#39;elenco a cui applicare la scadenza, quindi seleziona **[!UICONTROL Fine]**.

![Finestra di dialogo [!UICONTROL Seleziona set di dati] con un set di dati selezionato ed evidenziato [!UICONTROL Fine].](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>Vengono visualizzati solo i set di dati appartenenti alla sandbox corrente.

### Inviare la richiesta {#submit-request}

La sezione [!UICONTROL Dettagli set di dati] viene compilata in modo da includere l&#39;identità e lo schema primari per il set di dati selezionato. In **[!UICONTROL Impostazioni richiesta]**, immettere un nome e una descrizione facoltativa per la richiesta, seguiti da **[!UICONTROL Invia]**.

![Richiesta di scadenza del set di dati completata con [!UICONTROL Impostazioni richiesta] e pulsante [!UICONTROL Invia] evidenziati.](../images/ui/ttl/submit.png)

Viene visualizzata una finestra di dialogo [!UICONTROL Conferma richiesta]. Ti viene chiesto di confermare il nome del set di dati e la data in cui verrà eliminato. Seleziona **[!UICONTROL Invia]** per continuare.

Dopo l&#39;invio della richiesta, viene creato un ordine di lavoro che viene visualizzato nella scheda principale dell&#39;area di lavoro [!UICONTROL Ciclo di vita dati]. Da qui è possibile monitorare lo stato dell&#39;ordine di lavoro durante l&#39;elaborazione della richiesta.

>[!NOTE]
>
>Consulta la sezione panoramica su [timeline e trasparenza](../home.md#dataset-expiration-transparency) per informazioni dettagliate sull&#39;elaborazione delle scadenze dei set di dati dopo l&#39;esecuzione.

## Modificare o annullare la scadenza di un set di dati {#edit-or-cancel}

Per modificare o annullare la scadenza di un set di dati, selezionare **[!UICONTROL Set di dati]** nella pagina principale dell&#39;area di lavoro e selezionare la scadenza del set di dati dall&#39;elenco.

Nella pagina dei dettagli della scadenza del set di dati, la barra a destra mostra i controlli per modificare o annullare l’eliminazione pianificata.

## Passaggi successivi

Questo documento illustra come pianificare le scadenze dei set di dati nell’interfaccia utente di Experience Platform. Per informazioni su come eseguire altre attività di minimizzazione dei dati nell&#39;interfaccia utente, consulta la [panoramica dell&#39;interfaccia utente del ciclo di vita dei dati](./overview.md).

Per informazioni su come pianificare le scadenze dei set di dati utilizzando l&#39;API di igiene dei dati, consulta la [guida dell&#39;endpoint di scadenza del set di dati](../api/dataset-expiration.md).
