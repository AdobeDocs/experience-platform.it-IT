---
keywords: Experience Platform;home;argomenti popolari; eliminare flussi di dati
description: L’area di lavoro origini consente di eliminare i flussi di dati batch e in streaming esistenti che contengono errori o sono diventati obsoleti.
solution: Experience Platform
title: Eliminare i flussi di dati nell’interfaccia utente
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 1%

---

# Eliminare i flussi di dati nell’interfaccia utente

L&#39;area di lavoro [!UICONTROL Origini] consente di eliminare i flussi di dati batch e di streaming esistenti che contengono errori o sono diventati obsoleti.

Questa esercitazione fornisce i passaggi per eliminare i flussi di dati utilizzando l&#39;area di lavoro [!UICONTROL Sources].

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Origini](../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
- [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Elimina flussi di dati

Nell&#39;interfaccia utente di [Experience Platform](https://platform.adobe.com), seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini], quindi seleziona **[!UICONTROL Flussi dati]** dall&#39;intestazione superiore.

![catalogo](../../images/tutorials/delete/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Flussi dati]**. In questa pagina è riportato un elenco di flussi di dati visualizzabili, con informazioni sul set di dati di destinazione, l’origine, il nome dell’account e la data di creazione.

Seleziona l&#39;icona del filtro (![icona-filtro](/help/images/icons/filter.png)) in alto a sinistra per avviare il pannello di ordinamento.

![flussi di dati](../../images/tutorials/delete/dataflows.png)

Il pannello di ordinamento fornisce un elenco di tutte le origini. È possibile selezionare più origini dall&#39;elenco per accedere a una selezione filtrata di flussi di dati associati alle origini selezionate.

Seleziona l’origine con cui desideri lavorare per visualizzare un elenco dei flussi di dati esistenti. Dopo aver identificato il flusso di dati da eliminare, seleziona i puntini di sospensione (`...`) accanto al nome del flusso di dati.

![filtro-flussi di dati](../../images/tutorials/delete/dataflows-filter.png)

Viene visualizzato un menu a discesa che fornisce le opzioni per modificare la pianificazione del flusso di dati, disabilitarlo o eliminarlo completamente.

Seleziona **[!UICONTROL Elimina]** per eliminare il flusso di dati.

![elimina](../../images/tutorials/delete/delete.png)

Viene visualizzata una finestra di dialogo di conferma finale. Seleziona **[!UICONTROL Elimina]** per completare il processo.

![conferma](../../images/tutorials/delete/confirm.png)

Dopo alcuni istanti, nella parte inferiore della schermata viene visualizzata una casella di conferma per confermare l’eliminazione.

![confermato](../../images/tutorials/delete/confirmed.png)

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente l&#39;area di lavoro [!UICONTROL Sources] per eliminare un flusso di dati esistente.

Vedere il tutorial sull&#39;eliminazione di [flussi di dati tramite l&#39;API del servizio Flusso](../../tutorials/api/delete-dataflows.md) per i passaggi su come eseguire queste operazioni a livello di programmazione utilizzando le chiamate API.
