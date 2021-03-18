---
keywords: Experience Platform;home;argomenti popolari;aggiornare account
description: In alcuni casi, potrebbe essere necessario aggiornare i dettagli di un account di origini esistente. L'area di lavoro Origini consente di aggiungere, modificare ed eliminare i dettagli di una connessione batch o in streaming esistente, inclusi nome, descrizione e credenziali.
solution: Experience Platform
title: Aggiorna i dettagli dell'account di connessione sorgente nell'interfaccia utente
topic: ' - Panoramica'
type: Tutorial
translation-type: tm+mt
source-git-commit: 4a7405e2c8c97442d2781295dd827c6940aa33eb
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 1%

---


# Aggiornare i dettagli dell’account nell’interfaccia utente

In alcuni casi, potrebbe essere necessario aggiornare i dettagli di un account di origini esistente. L’area di lavoro [!UICONTROL Sources] consente di aggiungere, modificare ed eliminare i dettagli di una connessione batch o in streaming esistente, inclusi nome, descrizione e credenziali.

Questa esercitazione fornisce passaggi per aggiornare i dettagli e le credenziali di un account esistente dall&#39;area di lavoro [!UICONTROL Sources].

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [Origini](../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
- [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Aggiorna account

Accedi all&#39; [Interfaccia Experience Platform](https://platform.adobe.com) e seleziona **[!UICONTROL Sources]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Sources]. Seleziona **[!UICONTROL Accounts]** dall&#39;intestazione superiore per visualizzare gli account esistenti.

![catalogo](../../images/tutorials/update/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Accounts]** . In questa pagina è presente un elenco di account visualizzabili, che include informazioni sulla loro origine, nome utente, numero di flussi di dati e data di creazione.

Seleziona l&#39;icona del filtro ![filter](../../images/tutorials/update/filter.png) in alto a sinistra per avviare il pannello di ordinamento.

![elenco degli account](../../images/tutorials/update/accounts-list.png)

Il pannello di ordinamento fornisce un elenco di tutte le origini. È possibile selezionare più di un&#39;origine dall&#39;elenco per accedere a una selezione filtrata di account associati a origini diverse.

Selezionare l&#39;origine con cui si desidera lavorare per visualizzare un elenco dei relativi account esistenti. Una volta identificato l&#39;account che si desidera aggiornare, selezionare i puntini di sospensione (`...`) accanto al nome dell&#39;account.

![ordinamento dei conti](../../images/tutorials/update/accounts-sort.png)

Viene visualizzato un menu a discesa che fornisce le opzioni per **[!UICONTROL Add data]**, **[!UICONTROL Edit details]** e **[!UICONTROL Delete]**. Seleziona **[!UICONTROL Edit details]** dal menu per aggiornare il tuo account.

![update](../../images/tutorials/update/update.png)

La finestra di dialogo **[!UICONTROL Edit account details]** consente di aggiornare il nome, la descrizione e le credenziali di autenticazione di un account. Dopo aver aggiornato le informazioni desiderate, seleziona **[!UICONTROL Save]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Dopo alcuni istanti, nella parte inferiore dello schermo viene visualizzata una casella di conferma per confermare l’avvenuto aggiornamento.

![confermato](../../images/tutorials/update/update-confirmed.png)

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente l&#39;area di lavoro [!UICONTROL Sources] per aggiornare le informazioni di un account di origine esistente.

Per informazioni su come eseguire queste operazioni a livello di programmazione utilizzando l’ API [!DNL Flow Service], fai riferimento all’esercitazione sull’ [aggiornamento delle informazioni di connessione tramite l’API del servizio di flusso](../../tutorials/api/update.md).