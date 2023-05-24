---
keywords: Experience Platform;home;argomenti popolari;aggiornare gli account
description: In alcuni casi, potrebbe essere necessario aggiornare i dettagli di un conto origini esistente. L'area di lavoro Origini consente di aggiungere, modificare ed eliminare i dettagli di una connessione batch o streaming esistente, inclusi nome, descrizione e credenziali.
solution: Experience Platform
title: Aggiornamento dei dettagli dell’account della connessione di origine nell’interfaccia utente
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# Aggiornamento dei dettagli dell’account nell’interfaccia utente

In alcuni casi, potrebbe essere necessario aggiornare i dettagli di un conto origini esistente. Il [!UICONTROL Sorgenti] workspace consente di aggiungere, modificare ed eliminare i dettagli di una connessione batch o streaming esistente, inclusi nome, descrizione e credenziali.

Questa esercitazione descrive i passaggi necessari per aggiornare i dettagli e le credenziali di un account esistente da [!UICONTROL Sorgenti] Workspace.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Sorgenti](../../home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
- [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Aggiorna account

Accedi a [Interfaccia utente Experience Platform](https://platform.adobe.com) e quindi seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Seleziona **[!UICONTROL Account]** dall’intestazione superiore per visualizzare i conti esistenti.

![catalogo](../../images/tutorials/update/catalog.png)

Il **[!UICONTROL Account]** viene visualizzata. In questa pagina è riportato un elenco di account visualizzabili, con informazioni sulla loro origine, nome utente, numero di flussi di dati e data di creazione.

Seleziona l’icona del filtro ![filter](../../images/tutorials/update/filter.png) in alto a sinistra per avviare il pannello ordina.

![elenco account](../../images/tutorials/update/accounts-list.png)

Il pannello di ordinamento fornisce un elenco di tutte le origini. È possibile selezionare più origini dall&#39;elenco per accedere a una selezione filtrata di account associati a origini diverse.

Seleziona l’origine con cui vuoi lavorare per visualizzare un elenco dei suoi account esistenti. Dopo aver identificato l’account da aggiornare, seleziona i puntini di sospensione (`...`) accanto al nome account.

![accounts-sort](../../images/tutorials/update/accounts-sort.png)

Viene visualizzato un menu a discesa che fornisce le opzioni per **[!UICONTROL Aggiungi dati]**, **[!UICONTROL Modifica dettagli]**, e **[!UICONTROL Elimina]**. Seleziona **[!UICONTROL Modifica dettagli]** dal menu per aggiornare l’account.

![update](../../images/tutorials/update/update.png)

Il **[!UICONTROL Modifica dettagli account]** consente di aggiornare il nome, la descrizione e le credenziali di autenticazione di un account. Dopo aver aggiornato le informazioni desiderate, seleziona **[!UICONTROL Salva]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Dopo alcuni istanti, nella parte inferiore della schermata viene visualizzata una casella di conferma per confermare la riuscita dell’aggiornamento.

![aggiornamento-confermato](../../images/tutorials/update/update-confirmed.png)

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente il [!UICONTROL Sorgenti] per aggiornare le informazioni di un account di origine esistente.

Per i passaggi su come eseguire queste operazioni a livello di programmazione utilizzando [!DNL Flow Service] API, fai riferimento al tutorial su [aggiornamento delle informazioni di connessione tramite l’API del servizio Flow](../../tutorials/api/update.md).
