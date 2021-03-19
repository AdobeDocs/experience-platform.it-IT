---
keywords: Experience Platform;home;argomenti popolari;aggiornare i flussi di dati;modificare la pianificazione
description: Questa esercitazione descrive i passaggi per aggiornare una pianificazione del flusso di dati, inclusa la frequenza di acquisizione e la frequenza di intervallo, utilizzando l’area di lavoro Origini.
solution: Experience Platform
title: Aggiorna la pianificazione del flusso di dati della connessione sorgente nell'interfaccia utente
topic: ' - Panoramica'
type: Tutorial
translation-type: tm+mt
source-git-commit: 31e4b15ad71a0d17278fbdb4d88ff42029cbe655
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 3%

---


# Aggiornare i flussi di dati nell’interfaccia utente

Questa esercitazione descrive i passaggi per aggiornare una pianificazione del flusso di dati, inclusa la frequenza di acquisizione e la frequenza di intervallo, utilizzando l’area di lavoro [!UICONTROL Sources].

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [Origini](../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
- [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Modifica pianificazione

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sources]** dal menu di navigazione a sinistra per accedere all’area di lavoro [!UICONTROL Sources]. Seleziona **[!UICONTROL Dataflows]** dall’intestazione superiore per visualizzare un elenco dei flussi di dati esistenti.

![catalogo](../../images/tutorials/update-dataflows/catalog.png)

La pagina [!UICONTROL Dataflows] contiene un elenco di tutti i flussi di dati esistenti, incluse informazioni sullo stato di esecuzione, la data dell’ultima esecuzione e il nome dell’account.

Seleziona l&#39;icona del filtro ![filter](../../images/tutorials/update/filter.png) in alto a sinistra per avviare il pannello di ordinamento.

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

Il pannello di ordinamento fornisce un elenco di tutte le origini disponibili. È possibile selezionare più di un’origine dall’elenco per accedere a una selezione filtrata di flussi di dati appartenenti a origini diverse.

Seleziona l’origine con cui desideri lavorare per visualizzare un elenco dei relativi flussi di dati esistenti. Una volta identificato il flusso di dati da riprogrammare, seleziona i puntini di sospensione (`...`) accanto al nome dell&#39;account.

![riprogrammare](../../images/tutorials/update-dataflows/reschedule.png)

Viene visualizzato un menu a discesa che fornisce le opzioni per **[!UICONTROL Edit schedule]**, **[!UICONTROL Disable dataflow]**, **[!UICONTROL View in monitoring]** e **[!UICONTROL Delete]**. Seleziona **[!UICONTROL Edit schedule]** dal menu.

![programma di modifica](../../images/tutorials/update-dataflows/edit-schedule.png)

La finestra di dialogo **[!UICONTROL Edit schedule]** offre le opzioni per aggiornare la frequenza di acquisizione e la frequenza di intervallo del flusso di dati. Una volta impostati i valori di frequenza e intervallo aggiornati, selezionare **[!UICONTROL Save]**.

>[!NOTE]
>
>Non è possibile ripianificare un flusso di dati pianificato per l’inserimento una tantum.

![finestra di dialogo di programmazione](../../images/tutorials/update-dataflows/schedule-dialog-box.png)

| Pianificazione | Descrizione |
| ---------- | ----------- |
| Frequenza | Frequenza con cui il flusso di dati raccoglie i dati. I valori accettabili per la modifica della pianificazione della frequenza per un flusso di dati già esistente includono: `minute`, `hour`, `day` o `week`. |
| Intervallo | L&#39;intervallo indica il periodo tra due esecuzioni di flusso consecutive. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero e deve essere maggiore o uguale a `15`. |

Dopo alcuni istanti, nella parte inferiore dello schermo viene visualizzata una casella di conferma per confermare l’avvenuto aggiornamento.

![conferma del programma](../../images/tutorials/update-dataflows/schedule-confirm.png)

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente l’area di lavoro [!UICONTROL Sources] per aggiornare la pianificazione dell’acquisizione di un flusso di dati.

Per i passaggi su come eseguire queste operazioni a livello di programmazione utilizzando l’ API [!DNL Flow Service], fai riferimento all’esercitazione sull’ [aggiornamento dei flussi di dati tramite l’API del servizio di flusso](../../tutorials/api/update-dataflows.md).