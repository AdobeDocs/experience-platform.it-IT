---
title: Flussi di dati bozza nell’interfaccia utente
description: Scopri come salvare i flussi di dati come bozza e pubblicarli in un secondo momento, quando utilizzi l’area di lavoro origini.
exl-id: ee00798e-152a-4618-acb3-db40f2f55fae
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# Flussi di dati bozza nell’interfaccia utente

Per salvare l’avanzamento del flusso di lavoro di acquisizione dei dati non completati, imposta il flusso di dati su uno stato di bozza. Puoi riprendere e completare i flussi di dati bozza in un secondo momento.

Questo documento descrive come salvare i flussi di dati quando si utilizza l’area di lavoro origini nell’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo documento richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.

## Salvare un flusso di dati come bozza

Puoi mettere in pausa l’avanzamento della creazione del flusso di dati in qualsiasi momento dopo aver selezionato i dati da portare in Platform.

Ad esempio, se desideri salvare l&#39;avanzamento durante il passaggio dei dettagli del flusso di dati, seleziona **[!UICONTROL Salva come bozza]**.

![Passaggio dei dettagli del flusso di dati del flusso di lavoro di origine con l&#39;opzione Salva come bozza selezionata.](../../images/tutorials/draft/save-as-draft.png)

Una volta salvata la bozza, verrai indirizzato alla pagina dell’account, dove puoi visualizzare un elenco dei flussi di dati esistenti, incluse le bozze.

![Elenco di flussi di dati per un account specificato.](../../images/tutorials/draft/draft-dataflow.png)

>[!TIP]
>
>I flussi di dati bozza non saranno abilitati e il loro stato sarà impostato su `draft`.

Per continuare con la bozza, seleziona i puntini di sospensione (`...`) accanto al nome del flusso di dati, quindi seleziona **[!UICONTROL Aggiorna flusso di dati]**.

>[!NOTE]
>
>Se la bozza include informazioni sulla pianificazione, la finestra a discesa consente di scegliere di **[!UICONTROL modificare la pianificazione]**.

![Finestra a discesa con flusso di dati di aggiornamento selezionato.](../../images/tutorials/draft/update-dataflow.png)

### Accedere alle bozze dal catalogo di origine

Puoi accedere ai flussi di dati bozza anche tramite il catalogo dei flussi di dati. Seleziona **[!UICONTROL Flussi dati]** dall&#39;intestazione superiore per accedere al catalogo dei flussi dati. Da qui, individua la bozza dall&#39;elenco dei flussi di dati esistenti nell&#39;organizzazione, seleziona i puntini di sospensione (`...`) accanto al nome, quindi seleziona **[!UICONTROL Aggiorna flusso di dati]**.

![Elenco di flussi di dati per una determinata organizzazione.](../../images/tutorials/draft/catalog-access.png)

## Publish flusso di dati bozza

Sei tornato al passaggio [!UICONTROL Aggiungi dati] del flusso di lavoro origini, in cui puoi riconfermare il formato dei dati e continuare a progredire nel flusso di dati.

Dopo aver confermato la formattazione, il delimitatore e il tipo di compressione dei dati, seleziona **[!UICONTROL Avanti]** per continuare.

![Il passaggio di aggiunta dati del flusso di lavoro origini.](../../images/tutorials/draft/select-data.png)

Quindi, conferma i dettagli del flusso di dati. Utilizza l’interfaccia dei dettagli del flusso di dati per aggiornare le configurazioni relative a nome, descrizione, acquisizione parziale, impostazioni di diagnostica degli errori e preferenze degli avvisi del flusso di dati.

Al termine delle configurazioni, seleziona **[!UICONTROL Avanti]** per continuare.

![Passaggio dei dettagli del flusso di dati del flusso di lavoro delle origini.](../../images/tutorials/draft/dataflow-detail.png)

Viene visualizzato il passaggio [!UICONTROL Mapping]. Durante questo passaggio, puoi riconfigurare le configurazioni di mappatura del flusso di dati. Per una guida completa sulle funzioni di preparazione dei dati utilizzate per la mappatura, visita la [guida dell&#39;interfaccia utente di preparazione dei dati](../../../data-prep/ui/mapping.md).

Dopo aver completato la riconfigurazione della mappatura, seleziona **[!UICONTROL Avanti]** per continuare.

![Passaggio di mappatura del flusso di lavoro di origine.](../../images/tutorials/draft/mapping.png)

Utilizza il passaggio [!UICONTROL Pianificazione] per stabilire una pianificazione dell&#39;acquisizione per il flusso di dati. È possibile impostare la frequenza di acquisizione su `once`, `minute`, `hour`, `day` o `week`. Al termine, selezionare **[!UICONTROL Avanti]** per continuare.

![Passaggio di pianificazione del flusso di lavoro di origine.](../../images/tutorials/draft/scheduling.png)

Infine, controlla i dettagli del flusso di dati e seleziona **[!UICONTROL Fine]** per pubblicare la bozza.

![Passaggio di revisione del flusso di lavoro origini.](../../images/tutorials/draft/review.png)

Dopo il salvataggio e la pubblicazione di una bozza, il flusso di dati verrà attivato e non sarà più possibile ripristinarlo come bozza.

## Passaggi successivi

Seguendo questa esercitazione, hai imparato a salvare l’avanzamento e impostare un flusso di dati come bozza. Per ulteriori informazioni sulle origini, visitare la [panoramica delle origini](../../home.md).
