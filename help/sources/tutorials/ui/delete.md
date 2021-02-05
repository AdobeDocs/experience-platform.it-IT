---
keywords: ' Experience Platform;casa;argomenti popolari; eliminare i dataflows'
description: L’area di lavoro origini consente di eliminare i flussi di dati in batch e in streaming esistenti contenenti errori o che sono diventati obsoleti.
solution: Experience Platform
title: Eliminare i flussi di dati nell’interfaccia
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 1%

---


# Eliminare i flussi di dati nell’interfaccia utente

L&#39;area di lavoro [!UICONTROL Sources] consente di eliminare i flussi di dati in batch e in streaming esistenti che contengono errori o che sono diventati obsoleti.

Questa esercitazione fornisce i passaggi per eliminare i flussi di dati utilizzando l&#39;area di lavoro [!UICONTROL Sources].

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Origini](../../home.md):  [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
- [Sandbox](../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

## Eliminare i flussi di dati

Nell&#39;interfaccia [ Experience Platform](https://platform.adobe.com), selezionare **[!UICONTROL Sources]** dalla navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Sources], quindi selezionare **[!UICONTROL Dataflows]** dall&#39;intestazione superiore.

![catalogo](../../images/tutorials/delete/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Dataflows]**. In questa pagina è presente un elenco di flussi di dati visualizzabili, con informazioni sul set di dati di destinazione, l’origine, il nome account e la data di creazione.

Selezionate l&#39;icona del filtro (![filter-icon](../../images/tutorials/delete/filter.png)) in alto a sinistra per avviare il pannello di ordinamento.

![flussi di dati](../../images/tutorials/delete/dataflows.png)

Il pannello di ordinamento fornisce un elenco di tutte le origini. È possibile selezionare più origini dall&#39;elenco per accedere a una selezione filtrata di flussi di dati associati alle origini specifiche selezionate.

Selezionate l&#39;origine con cui desiderate lavorare per visualizzare un elenco dei relativi flussi di dati esistenti. Dopo aver identificato il flusso di dati da eliminare, selezionate le ellissi (`...`) accanto al nome del flusso di dati.

![dataflows-filter](../../images/tutorials/delete/dataflows-filter.png)

Viene visualizzato un menu a discesa che fornisce opzioni per modificare la pianificazione del flusso di dati, disattivare il flusso di dati o eliminarlo completamente.

Selezionare **[!UICONTROL Delete]** per eliminare il flusso di dati.

![delete](../../images/tutorials/delete/delete.png)

Viene visualizzata una finestra di dialogo di conferma finale. Selezionare **[!UICONTROL Delete]** per completare il processo.

![verify](../../images/tutorials/delete/confirm.png)

Dopo alcuni istanti, nella parte inferiore dello schermo viene visualizzata una casella di conferma per confermare l’avvenuta eliminazione.

![confermata](../../images/tutorials/delete/confirmed.png)

## Passaggi successivi

Seguendo questa esercitazione, è stato utilizzato l&#39;area di lavoro [!UICONTROL Sources] per eliminare un flusso di dati esistente.

Per informazioni su come eseguire queste operazioni a livello di programmazione mediante le chiamate API, vedere l&#39;esercitazione sull&#39;eliminazione dei flussi di dati mediante l&#39;API del servizio di flusso](../../tutorials/api/delete-dataflows.md).[