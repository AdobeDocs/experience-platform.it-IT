---
keywords: Experience Platform;home;argomenti popolari; analytics;classificazioni
description: Scopri come creare un connettore di origine Adobe Analytics nell’interfaccia utente per inserire i dati delle classificazioni in Adobe Experience Platform.
solution: Experience Platform
title: Creare una connessione sorgente Adobe Analytics per i dati delle classificazioni nell’interfaccia utente
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: fcebef97ba9cc667f80afd55980c5460912a56fb
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 2%

---

# Creare una connessione di origine di Adobe Analytics per i dati di classificazione nell’interfaccia utente

Questo tutorial descrive i passaggi necessari per creare una connessione a un’origine dati per le classificazioni di Adobe Analytics nell’interfaccia utente per inserire i dati delle classificazioni in Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experienci Platform organizza i dati sull’esperienza del cliente.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experienci Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Il Connettore dati per le classificazioni di Analytics richiede che i dati siano stati migrati al nuovo [!DNL Classifications] infrastruttura Adobe Analytics prima dell’utilizzo. Per confermare lo stato di migrazione dei tuoi dati, contatta il team del tuo account di Adobe.

## Seleziona le classificazioni

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e quindi seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere all’area di lavoro origini. Il **[!UICONTROL Catalogo]** nella schermata vengono visualizzate le origini disponibili con cui creare connessioni in entrata. Ogni scheda sorgente mostra un’opzione per configurare un nuovo account o aggiungere dati a un account esistente.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto **[!UICONTROL applicazioni Adobe]** categoria, seleziona la **[!UICONTROL Adobe Analytics]** e quindi selezionare **[!UICONTROL Aggiungi dati]** per iniziare a lavorare con i dati delle classificazioni di Analytics.

![](../../../../images/tutorials/create/classifications/catalog.png)

Il **[!UICONTROL Dati aggiunta origine di Analytics]** viene visualizzato il passaggio. Seleziona **[!UICONTROL Classificazioni]** nell’intestazione in alto per visualizzare un elenco di [!DNL Classifications] set di dati, incluse informazioni sull’ID dimensione, il nome della suite di rapporti e l’ID della suite di rapporti.

Ogni pagina viene visualizzata fino a dieci pagine diverse [!DNL Classifications] set di dati tra cui puoi scegliere. Seleziona **[!UICONTROL Successivo]** nella parte inferiore della pagina per cercare altre opzioni. Il pannello a destra mostra il numero totale di [!DNL Classifications] i set di dati selezionati e i relativi nomi. Questo pannello consente inoltre di rimuovere [!DNL Classifications] set di dati selezionati per errore o deseleziona tutte le selezioni con una sola azione.

È possibile selezionare fino a 30 diversi [!DNL Classifications] set di dati da inserire in [!DNL Platform].

Dopo aver selezionato il [!DNL Classifications] set di dati, seleziona **[!UICONTROL Successivo]** in alto a destra.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Rivedere le classificazioni

Il **[!UICONTROL Revisione]** viene visualizzato un passaggio che consente di rivedere [!DNL Classifications] set di dati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: mostra la piattaforma di origine e lo stato della connessione.
* **[!UICONTROL Tipo di dati]**: mostra il numero di selezionati [!DNL Classifications].
* **[!UICONTROL Pianificazione]**: mostra la frequenza di sincronizzazione per [!DNL Classifications] dati.

Dopo aver rivisto il flusso di dati, fai clic su **[!UICONTROL Fine]** e lascia un po’ di tempo per creare il flusso di dati.

![](../../../../images/tutorials/create/classifications/review.png)

## Monitorare il flusso di dati delle classificazioni

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso. Dalla sezione **[!UICONTROL Catalogo]** schermata, seleziona **[!UICONTROL Flussi dati]** per visualizzare un elenco dei flussi stabiliti associati al [!DNL Classifications] account.

![](../../../../images/tutorials/create/classifications/dataflows.png)

Il **[!UICONTROL Flussi dati]** viene visualizzata la schermata. In questa pagina è riportato un elenco di flussi di dati, con informazioni sul nome, i dati di origine e lo stato di esecuzione del flusso di dati. A destra, è il valore **[!UICONTROL Proprietà]** che contiene i metadati relativi al tuo [!DNL Classifications] flusso di dati.

Seleziona la **[!UICONTROL Set di dati di destinazione]** desideri accedere a.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

Il **[!UICONTROL Attività set di dati]** Questa pagina visualizza informazioni sul set di dati di destinazione selezionato, inclusi dettagli sullo stato del batch, l’ID del set di dati e lo schema.

![](../../../../images/tutorials/create/classifications/dataset.png)

## Passaggi successivi

Seguendo questa esercitazione, hai creato un connettore dati per le classificazioni di Analytics che porta [!DNL Classifications] dati in [!DNL Platform]. Per ulteriori informazioni su, consulta i seguenti documenti [!DNL Analytics] e [!DNL Classifications] dati:

* [Panoramica del connettore dati di Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Creare una connessione dati di Analytics nell’interfaccia utente](./analytics.md)
* [Informazioni sulle classificazioni](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html?lang=it)
