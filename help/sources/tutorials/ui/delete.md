---
keywords: Experience Platform;home;argomenti popolari; eliminare i flussi di dati
description: L'area di lavoro origini consente di eliminare i flussi di dati in batch e streaming esistenti che contengono errori o che sono diventati obsoleti.
solution: Experience Platform
title: Eliminare i flussi di dati nell’interfaccia utente
topic-legacy: overview
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 1%

---

# Eliminare i flussi di dati nell’interfaccia utente

L’area di lavoro [!UICONTROL Sources] ti consente di eliminare i flussi di dati in batch e streaming esistenti che contengono errori o che sono diventati obsoleti.

Questa esercitazione descrive i passaggi necessari per eliminare i flussi di dati utilizzando l&#39;area di lavoro [!UICONTROL Sources].

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [Origini](../../home.md):  [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
- [Sandbox](../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Eliminare i flussi di dati

Nell&#39; [Interfaccia Experience Platform](https://platform.adobe.com), seleziona **[!UICONTROL Sources]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Sources], quindi seleziona **[!UICONTROL Dataflows]** dall&#39;intestazione superiore.

![catalogo](../../images/tutorials/delete/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Dataflows]** . In questa pagina è riportato un elenco di flussi di dati visualizzabili, che include informazioni sul set di dati di destinazione, l’origine, il nome dell’account e la data di creazione.

Seleziona l&#39;icona del filtro (![filter-icon](../../images/tutorials/delete/filter.png)) in alto a sinistra per avviare il pannello di ordinamento.

![flussi di dati](../../images/tutorials/delete/dataflows.png)

Il pannello di ordinamento fornisce un elenco di tutte le origini. È possibile selezionare più di un’origine dall’elenco per accedere a una selezione filtrata di flussi di dati associati alle sorgenti selezionate.

Seleziona l’origine con cui desideri lavorare per visualizzare un elenco dei relativi flussi di dati esistenti. Dopo aver identificato il flusso di dati da eliminare, seleziona i puntini di sospensione (`...`) accanto al nome del flusso di dati.

![dataflows-filter](../../images/tutorials/delete/dataflows-filter.png)

Viene visualizzato un menu a discesa che fornisce le opzioni per modificare la pianificazione del flusso di dati, disattivarlo o eliminarlo completamente.

Selezionare **[!UICONTROL Delete]** per eliminare il flusso di dati.

![delete](../../images/tutorials/delete/delete.png)

Viene visualizzata una finestra di dialogo di conferma finale. Selezionare **[!UICONTROL Delete]** per completare il processo.

![confermare](../../images/tutorials/delete/confirm.png)

Dopo alcuni istanti, nella parte inferiore dello schermo viene visualizzata una casella di conferma per confermare l’eliminazione.

![confermato](../../images/tutorials/delete/confirmed.png)

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente l’area di lavoro [!UICONTROL Sources] per eliminare un flusso di dati esistente.

Per informazioni su come eseguire queste operazioni a livello di programmazione utilizzando le chiamate API, consulta l’esercitazione sull’ [eliminazione dei flussi di dati tramite l’API del servizio di flusso](../../tutorials/api/delete-dataflows.md) .
