---
title: Gestire le scadenze dei set di dati
description: Scopri come pianificare la scadenza di un set di dati nell’interfaccia utente di Adobe Experience Platform.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 7931c8fe4a1ca5d255a80e7e6b0deb976d53c3de
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 16%

---

# Gestire le scadenze dei set di dati {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="Elimina record e set di dati cliente indesiderati o scaduti"
>abstract="<h2>Descrizione</h2><p>Per gestire il ciclo di vita dei dati di Experience Platform non correlati alla conformità alle normative, puoi eliminare i record dei consumatori e pianificare le date di scadenza dei set di dati. Per creare o gestire le richieste dell’interessato, consulta il blocco del caso d’uso &quot;Rispetta le richieste di privacy dell’interessato&quot;.</p>"

Il [[!UICONTROL Ciclo di vita dei dati] workspace](./overview.md) nell’interfaccia utente di Adobe Experience Platform consente di pianificare le scadenze per i set di dati. Quando un set di dati raggiunge la data di scadenza, il data lake, Identity Service e Real-Time Customer Profile iniziano processi separati per rimuovere i contenuti del set di dati dai rispettivi servizi. Una volta eliminati i dati da tutti e tre i servizi, la scadenza viene contrassegnata come completata.

>[!WARNING]
>
>Se un set di dati è impostato per la scadenza, è necessario modificare manualmente i flussi di dati che potrebbero acquisire dati in tale set di dati in modo che i flussi di lavoro a valle non vengano influenzati negativamente.

Questo documento illustra come pianificare e gestire le scadenze dei set di dati nell’interfaccia utente di Platform.

>[!NOTE]
>
>La scadenza del set di dati non elimina attualmente i dati dalla rete Edge di Adobe Experience Platform. Tuttavia, non è possibile che i dati rimangano all’interno della rete Edge dopo la scadenza del set di dati. Questo perché il contratto di licenza del servizio di 14 giorni per la scadenza del set di dati coincide con il periodo di 14 giorni in cui i dati esistono all’interno della rete Edge prima di essere eliminati.

## Pianificare la scadenza di un set di dati {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="Istruzioni"
>abstract="<ul><li>Seleziona <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html?lang=it">Ciclo di vita dei dati</a> nel menu di navigazione a sinistra, seleziona quindi <b>Crea richiesta</b>.</li><li>Per eliminare i record:</li>   <li>Seleziona <b>Record</b>.</li>   <li>Seleziona un set di dati specifico da cui eliminare i record oppure scegli l’opzione per eliminarli da tutti i set di dati.</li>   <li>Fornire le identità dei consumatori i cui record devono essere cancellati. Seleziona <b>Aggiungi identità</b> per fornire le identità una alla volta oppure seleziona <b>Scegli i file</b> per caricare un file JSON di identità.</li>   <li>Se necessario, seleziona <b>Modello</b> per visualizzare il formato previsto del file JSON.</li><li>Per istruzioni, consulta la documentazione per la <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html?lang=it#schedule-dataset-expiration">pianificazione delle date di scadenza dei set di dati</a>.</li></ul>"

Per creare una richiesta, seleziona **[!UICONTROL Crea richiesta]** dalla pagina principale nell’area di lavoro.

>[!IMPORTANT]
>
Puoi avere fino a 20 scadenze di set di dati pianificate simultaneamente. Ciò significa che puoi pianificare l’eliminazione di 20 set di dati in qualsiasi momento. Non vi sono restrizioni sull’ora o sull’anno per cui queste scadenze sono impostate. Ad esempio, se hai 20 scadenze pianificate per un set di dati e un set di dati deve essere eliminato domani, non puoi impostarne altre fino a dopo l’eliminazione.

![Il [!UICONTROL Ciclo di vita dei dati] workspace con [!UICONTROL Crea richiesta] evidenziato.](../images/ui/ttl/create-request-button.png)

Viene visualizzato il flusso di lavoro per la creazione delle richieste. Sotto [!UICONTROL Azione richiesta] sezione, seleziona **[!UICONTROL Elimina set di dati]** per aggiornare i controlli per la pianificazione della scadenza dei set di dati.

![Il flusso di lavoro di creazione delle richieste con [!UICONTROL Elimina set di dati] opzione evidenziata.](../images/ui/ttl/dataset-selected.png)

### Seleziona una data e un set di dati {#select-date-and-dataset}

Sotto **[!UICONTROL Azione richiesta]** , seleziona una data entro la quale desideri eliminare il set di dati. È possibile immettere la data manualmente (nel formato `mm/dd/yyyy`) o seleziona l’icona del calendario (![Icona del calendario.](../images/ui/ttl/calendar-icon.png)) per selezionare la data da una finestra di dialogo.

![Una finestra di dialogo del calendario con una data di scadenza selezionata ed evidenziata per il set di dati.](../images/ui/ttl/select-date.png)

Avanti, sotto **[!UICONTROL Dettagli set di dati]**, selezionare l&#39;icona del database (![Icona del database.](../images/ui/ttl/database-icon.png)) per aprire una finestra di dialogo per la selezione del set di dati. Scegli un set di dati dall’elenco a cui applicare la scadenza, quindi seleziona **[!UICONTROL Fine]**.

![Il [!UICONTROL Seleziona set di dati] finestra di dialogo con un set di dati selezionato [!UICONTROL Fine] evidenziato.](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
Vengono visualizzati solo i set di dati appartenenti alla sandbox corrente.

### Inviare la richiesta {#submit-request}

Il [!UICONTROL Dettagli set di dati] La sezione viene compilata in modo da includere l’identità e lo schema primari per il set di dati selezionato. Sotto **[!UICONTROL Impostazioni richiesta]**, immettere un nome e una descrizione facoltativa per la richiesta, seguita da **[!UICONTROL Invia]**.

![Una richiesta di scadenza del set di dati completata con [!UICONTROL Impostazioni richiesta] e [!UICONTROL Invia] pulsante evidenziato.](../images/ui/ttl/submit.png)

A [!UICONTROL Conferma richiesta] viene visualizzata. Ti viene chiesto di confermare il nome del set di dati e la data in cui verrà eliminato. Seleziona **[!UICONTROL Invia]** per continuare.

Dopo l&#39;invio della richiesta, viene creato un ordine di lavoro che viene visualizzato nella scheda principale del [!UICONTROL Ciclo di vita dei dati] Workspace. Da qui è possibile monitorare lo stato dell&#39;ordine di lavoro durante l&#39;elaborazione della richiesta.

>[!NOTE]
>
Consulta la sezione panoramica su [tempistiche e trasparenza](../home.md#dataset-expiration-transparency) per informazioni dettagliate su come vengono elaborate le scadenze dei set di dati una volta eseguite.

## Modificare o annullare la scadenza di un set di dati {#edit-or-cancel}

Per modificare o annullare la scadenza di un set di dati, seleziona **[!UICONTROL Set di dati]** nella pagina principale dell’area di lavoro e seleziona la scadenza del set di dati dall’elenco.

Nella pagina dei dettagli della scadenza del set di dati, la barra a destra mostra i controlli per modificare o annullare l’eliminazione pianificata.

## Passaggi successivi

Questo documento illustra come pianificare le scadenze dei set di dati nell’interfaccia utente di Experienci Platform. Per informazioni su come eseguire altre attività di minimizzazione dei dati nell’interfaccia utente, consulta [panoramica dell’interfaccia utente del ciclo di vita dei dati](./overview.md).

Per informazioni su come pianificare le scadenze dei set di dati utilizzando l’API di igiene dei dati, consulta [guida dell’endpoint &quot;dataset expiration&quot;](../api/dataset-expiration.md).
