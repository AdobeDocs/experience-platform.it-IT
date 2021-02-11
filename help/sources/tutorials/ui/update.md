---
keywords: ' Experience Platform;home;argomenti popolari;aggiornare gli account'
description: In alcuni casi, potrebbe essere necessario aggiornare i dettagli di un account di origine esistente. L'area di lavoro Origini consente di aggiungere, modificare ed eliminare dettagli di una connessione batch o in streaming esistente, inclusi nome, descrizione e credenziali.
solution: Experience Platform
title: Aggiorna dettagli account connessione origine nell'interfaccia utente
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: ac477ee8053b30e88a38800ebe33fc9b5a520308
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 1%

---


# Aggiornamento dei dettagli dell&#39;account nell&#39;interfaccia utente

In alcuni casi, potrebbe essere necessario aggiornare i dettagli di un account di origine esistente. L&#39;area di lavoro [!UICONTROL Sources] consente di aggiungere, modificare ed eliminare dettagli di una connessione batch o in streaming esistente, inclusi nome, descrizione e credenziali.

L&#39;area di lavoro [!UICONTROL Sources] consente inoltre di modificare la pianificazione dei flussi di dati batch, aggiornandone la frequenza di inserimento e la frequenza degli intervalli.

Questa esercitazione fornisce i passaggi per aggiornare i dettagli e le credenziali di un account esistente dall&#39;area di lavoro [!UICONTROL Sources], nonché per aggiornare la pianificazione dell&#39;assimilazione di un flusso di dati.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Origini](../../home.md): DNL  Experience Platform consente di acquisire dati da varie fonti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Piattaforma.
- [Sandbox](../../../sandboxes/home.md): DNL  Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

## Aggiorna account

Accedete all&#39;interfaccia utente del Experience Platform [](https://platform.adobe.com), quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Sources]. Selezionate **[!UICONTROL Accounts]** dall&#39;intestazione superiore per visualizzare gli account esistenti.

![catalogo](../../images/tutorials/update/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Accounts]**. In questa pagina è presente un elenco di account visualizzabili, con informazioni sull’origine, il nome utente, il numero di flussi di dati e la data di creazione.

Selezionate l&#39;icona del filtro ![filter](../../images/tutorials/update/filter.png) in alto a sinistra per avviare il pannello di ordinamento.

![accounts-list](../../images/tutorials/update/accounts-list.png)

Il pannello di ordinamento fornisce un elenco di tutte le origini. È possibile selezionare più origini dall&#39;elenco per accedere a una selezione filtrata di account associati a origini diverse.

Selezionate l’origine con cui desiderate lavorare per visualizzare un elenco dei relativi account esistenti. Dopo aver identificato l&#39;account da aggiornare, selezionate le ellissi (`...`) accanto al nome dell&#39;account.

![ordinamento degli account](../../images/tutorials/update/accounts-sort.png)

Viene visualizzato un menu a discesa che fornisce opzioni per **[!UICONTROL Add data]**, **[!UICONTROL Edit details]** e **[!UICONTROL Delete]**. Selezionare **[!UICONTROL Edit details]** dal menu per aggiornare l&#39;account.

![update](../../images/tutorials/update/update.png)

La finestra di dialogo **[!UICONTROL Edit account details]** consente di aggiornare il nome, la descrizione e le credenziali di autenticazione di un account. Dopo aver aggiornato le informazioni desiderate, selezionate **[!UICONTROL Save]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Dopo alcuni istanti, nella parte inferiore della schermata viene visualizzata una casella di conferma per confermare l’esito positivo dell’aggiornamento.

![update-Confirm](../../images/tutorials/update/update-confirmed.png)

## Modifica pianificazione

È possibile modificare la pianificazione di assimilazione di un flusso di dati dalla pagina **[!UICONTROL Accounts]**. Dall&#39;elenco degli account, selezionate l&#39;account che contiene il flusso di dati da riprogrammare.

![select-account](../../images/tutorials/update/select-account.png)

Viene visualizzata la pagina dei flussi di dati. Questa pagina contiene un elenco dei flussi di dati esistenti associati all&#39;account selezionato. Selezionate le ellissi (`...`) accanto al flusso di dati da riprogrammare.

![riprogrammare](../../images/tutorials/update/reschedule.png)

Viene visualizzato un menu a discesa che fornisce opzioni per **[!UICONTROL Edit schedule]**, **[!UICONTROL Enable dataflow]**, **[!UICONTROL View in monitoring]** e **[!UICONTROL Delete]**. Seleziona **[!UICONTROL Edit schedule]** dal menu.

![pianificazione delle modifiche](../../images/tutorials/update/edit-schedule.png)

La finestra di dialogo **[!UICONTROL Edit schedule]** contiene opzioni per aggiornare la frequenza di inserimento e la frequenza di intervallo del flusso di dati. Una volta impostati i valori di frequenza e intervallo aggiornati, selezionare **[!UICONTROL Save]**.

![Pianificazione-finestra di dialogo](../../images/tutorials/update/schedule-dialog-box.png)

| Pianificazione | Descrizione |
| ---------- | ----------- |
| Frequenza | Frequenza con cui il flusso di dati raccoglie i dati. I valori accettabili per la modifica della pianificazione delle frequenze per un flusso di dati già esistente includono: `minute`, `hour`, `day` o `week`. |
| Intervallo | L&#39;intervallo indica il periodo tra due esecuzioni di flusso consecutive. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero e deve essere maggiore o uguale a `15`. |

Dopo alcuni istanti, nella parte inferiore della schermata viene visualizzata una casella di conferma per confermare l’esito positivo dell’aggiornamento.

![pianificazione-conferma](../../images/tutorials/update/schedule-confirm.png)

## Passaggi successivi

Seguendo questa esercitazione, avete utilizzato l&#39;area di lavoro [!UICONTROL Sources] per aggiornare le informazioni sull&#39;account e modificare la pianificazione del flusso di dati.

Per informazioni su come eseguire queste operazioni a livello di programmazione utilizzando l&#39;API [!DNL Flow Service], fare riferimento all&#39;esercitazione sull&#39; [aggiornamento delle informazioni sulla connessione mediante l&#39;API del servizio di flusso](../../tutorials/api/update.md).