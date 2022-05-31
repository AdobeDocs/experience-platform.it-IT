---
title: Gestione TTL set di dati
description: Scopri come pianificare un TTL (time to live) per un set di dati nell’interfaccia utente di Adobe Experience Platform.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 22da9e39e168d9a995c7c134733aa7a1b3587749
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# Gestire le TTL dei set di dati

>[!IMPORTANT]
>
>Le funzionalità di igiene dei dati in Adobe Experience Platform sono attualmente disponibili solo per le organizzazioni che hanno acquistato Adobe Shield per il settore sanitario.

La [[!UICONTROL Igiene dei dati] workspace](./overview.md) nell’interfaccia utente di Adobe Experience Platform è possibile pianificare un’ora di pubblicazione (TTL) per un set di dati.

Questo documento illustra come pianificare e gestire i TTL dei set di dati nell’interfaccia utente di Platform.

## Pianificare un TTL

Per creare una nuova richiesta, seleziona **[!UICONTROL Crea richiesta]** dalla pagina principale nell’area di lavoro.

![Immagine che mostra [!UICONTROL Crea richiesta] pulsante selezionato](../images/ui/ttl/create-request-button.png)

<!-- The request creation dialog appears. Under the **[!UICONTROL Action]** section, select **[!UICONTROL Dataset]** to update the available controls for TTL scheduling-->

### Selezionare una data e un set di dati

Viene visualizzata la finestra di dialogo per la creazione della richiesta. Sotto la **[!UICONTROL Azione]** seleziona la data in cui desideri eliminare il set di dati. Puoi immettere la data manualmente (nel formato `mm/dd/yyyy`) o seleziona l’icona Calendario (![Immagine dell&#39;icona del calendario](../images/ui/ttl/calendar-icon.png)) per selezionare la data da una finestra di dialogo.

![Immagine che mostra una data di scadenza impostata per il TTL](../images/ui/ttl/select-date.png)

Successivamente, sotto **[!UICONTROL Dettagli set di dati]**, seleziona l’icona del database (![Immagine dell’icona del database](../images/ui/ttl/database-icon.png)) per aprire una finestra di dialogo per la selezione di un set di dati. Scegli un set di dati dall’elenco a cui applicare il TTL, quindi seleziona **[!UICONTROL Fine]**.

![Immagine che mostra un set di dati selezionato](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>Vengono visualizzati solo i set di dati appartenenti alla sandbox corrente.

### Invia la richiesta

Dopo aver selezionato un set di dati e una data TTL, seleziona **[!UICONTROL Invia]**.

![Immagine che mostra [!UICONTROL Invia] pulsante selezionato](../images/ui/ttl/submit.png)

Viene richiesto di confermare la data in cui il set di dati verrà eliminato. Seleziona **[!UICONTROL Invia]** per continuare.

Dopo l&#39;invio della richiesta, viene creato un ordine di lavoro e viene visualizzato nella scheda principale [!UICONTROL Igiene dei dati] workspace. Da qui è possibile monitorare lo stato dell&#39;ordine di lavoro durante l&#39;elaborazione della richiesta.

## Modificare o annullare un TTL

Per modificare o annullare un TTL, selezionare **[!UICONTROL Set di dati]** nella pagina principale dell’area di lavoro, quindi selezionare il TTL dall’elenco.

Nella pagina dei dettagli del TTL, la barra a destra mostra i controlli per modificare o annullare l’eliminazione pianificata.

## Passaggi successivi

Questo documento illustra come pianificare i TTL dei set di dati nell’interfaccia utente di Experience Platform. Per informazioni su come pianificare i TTL dei set di dati utilizzando l’API di igiene dati, consulta [guida all’endpoint TTL del set di dati](../api/ttl.md).
