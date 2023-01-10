---
keywords: Experience Platform;home;argomenti popolari;aggiornare account
description: In alcuni casi, potrebbe essere necessario aggiornare i dettagli di un account di origini esistente. L'area di lavoro Origini consente di aggiungere, modificare ed eliminare i dettagli di una connessione batch o in streaming esistente, inclusi nome, descrizione e credenziali.
solution: Experience Platform
title: Aggiorna i dettagli dell'account di connessione sorgente nell'interfaccia utente
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# Aggiornare i dettagli dell’account nell’interfaccia utente

In alcuni casi, potrebbe essere necessario aggiornare i dettagli di un account di origini esistente. La [!UICONTROL Origini] workspace consente di aggiungere, modificare ed eliminare i dettagli di una connessione batch o in streaming esistente, inclusi nome, descrizione e credenziali.

Questa esercitazione fornisce i passaggi per aggiornare i dettagli e le credenziali di un account esistente dal [!UICONTROL Origini] workspace.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [Origini](../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
- [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Aggiorna account

Accedi a [Interfaccia utente Experience Platform](https://platform.adobe.com) quindi seleziona **[!UICONTROL Origini]** dalla navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. Seleziona **[!UICONTROL Account]** dall&#39;intestazione superiore per visualizzare gli account esistenti.

![catalogo](../../images/tutorials/update/catalog.png)

La **[!UICONTROL Account]** viene visualizzata la pagina . In questa pagina è presente un elenco di account visualizzabili, che include informazioni sulla loro origine, nome utente, numero di flussi di dati e data di creazione.

Seleziona l’icona del filtro ![filter](../../images/tutorials/update/filter.png) in alto a sinistra per avviare il pannello di ordinamento.

![elenco degli account](../../images/tutorials/update/accounts-list.png)

Il pannello di ordinamento fornisce un elenco di tutte le origini. È possibile selezionare più di un&#39;origine dall&#39;elenco per accedere a una selezione filtrata di account associati a origini diverse.

Selezionare l&#39;origine con cui si desidera lavorare per visualizzare un elenco dei relativi account esistenti. Una volta identificato l&#39;account da aggiornare, seleziona i puntini di sospensione (`...`) accanto al nome dell’account.

![ordinamento dei conti](../../images/tutorials/update/accounts-sort.png)

Viene visualizzato un menu a discesa che fornisce le opzioni per **[!UICONTROL Aggiungi dati]**, **[!UICONTROL Modifica dettagli]** e **[!UICONTROL Elimina]**. Seleziona **[!UICONTROL Modifica dettagli]** dal menu per aggiornare l&#39;account.

![update](../../images/tutorials/update/update.png)

La **[!UICONTROL Modifica dettagli account]** consente di aggiornare il nome, la descrizione e le credenziali di autenticazione di un account. Dopo aver aggiornato le informazioni desiderate, seleziona **[!UICONTROL Salva]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Dopo alcuni istanti, nella parte inferiore dello schermo viene visualizzata una casella di conferma per confermare l’avvenuto aggiornamento.

![confermato](../../images/tutorials/update/update-confirmed.png)

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente il [!UICONTROL Origini] per aggiornare le informazioni di un account di origine esistente.

Per i passaggi su come eseguire queste operazioni a livello di programmazione utilizzando il [!DNL Flow Service] API, consulta l’esercitazione su [aggiornamento delle informazioni di connessione tramite l’API del servizio di flusso](../../tutorials/api/update.md).
