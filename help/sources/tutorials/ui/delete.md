---
keywords: Experience Platform;home;argomenti popolari; eliminare i flussi di dati
description: L'area di lavoro origini consente di eliminare i flussi di dati in batch e streaming esistenti che contengono errori o che sono diventati obsoleti.
solution: Experience Platform
title: Eliminare i flussi di dati nell’interfaccia utente
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%

---

# Eliminare i flussi di dati nell’interfaccia utente

La [!UICONTROL Origini] workspace consente di eliminare i flussi di dati in batch e in streaming esistenti che contengono errori o che sono diventati obsoleti.

Questa esercitazione fornisce i passaggi per eliminare i flussi di dati utilizzando [!UICONTROL Origini] workspace.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [Origini](../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
- [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Eliminare i flussi di dati

In [Interfaccia utente Experience Platform](https://platform.adobe.com), seleziona **[!UICONTROL Origini]** dalla navigazione a sinistra per accedere al [!UICONTROL Origini] area di lavoro, quindi selezionare **[!UICONTROL Flussi di dati]** dall’intestazione superiore.

![catalogo](../../images/tutorials/delete/catalog.png)

La **[!UICONTROL Flussi di dati]** viene visualizzata la pagina . In questa pagina è riportato un elenco di flussi di dati visualizzabili, che include informazioni sul set di dati di destinazione, l’origine, il nome dell’account e la data di creazione.

Seleziona l’icona del filtro (![icona del filtro](../../images/tutorials/delete/filter.png)) in alto a sinistra per avviare il pannello di ordinamento.

![flussi di dati](../../images/tutorials/delete/dataflows.png)

Il pannello di ordinamento fornisce un elenco di tutte le origini. È possibile selezionare più di un’origine dall’elenco per accedere a una selezione filtrata di flussi di dati associati alle sorgenti selezionate.

Seleziona l’origine con cui desideri lavorare per visualizzare un elenco dei relativi flussi di dati esistenti. Una volta identificato il flusso di dati da eliminare, seleziona i puntini di sospensione (`...`) accanto al nome del flusso di dati.

![dataflows-filter](../../images/tutorials/delete/dataflows-filter.png)

Viene visualizzato un menu a discesa che fornisce le opzioni per modificare la pianificazione del flusso di dati, disattivarlo o eliminarlo completamente.

Seleziona **[!UICONTROL Elimina]** per eliminare il flusso di dati.

![delete](../../images/tutorials/delete/delete.png)

Viene visualizzata una finestra di dialogo di conferma finale. Seleziona **[!UICONTROL Elimina]** per completare il processo.

![confermare](../../images/tutorials/delete/confirm.png)

Dopo alcuni istanti, nella parte inferiore dello schermo viene visualizzata una casella di conferma per confermare l’eliminazione.

![confermato](../../images/tutorials/delete/confirmed.png)

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente il [!UICONTROL Origini] per eliminare un flusso di dati esistente.

Guarda l’esercitazione su [eliminazione dei flussi di dati tramite l’API del servizio di flusso](../../tutorials/api/delete-dataflows.md) per informazioni su come eseguire queste operazioni a livello di programmazione utilizzando le chiamate API.
