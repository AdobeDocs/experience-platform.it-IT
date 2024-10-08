---
description: Scopri come creare un connettore di origine Adobe Analytics nell’interfaccia utente per inserire i dati delle classificazioni in Adobe Experience Platform.
title: Creare una connessione Source Adobe Analytics per i dati delle classificazioni nell’interfaccia utente
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: 02b5c5f963c21247adbb1d13114f92b22f8758de
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# Creare una connessione di origine di Adobe Analytics per i dati di classificazione nell’interfaccia utente

>[!TIP]
>
>Per impostazione predefinita, i dati delle classificazioni di Adobe Analytics vengono aggiornati settimanalmente. L’acquisizione dei dati per le classificazioni verrà elaborata sette giorni dopo la configurazione iniziale del flusso di dati. Il primo caricamento acquisisce tutti i dati e l’acquisizione settimanale successiva esegue i dati incrementali.

Leggi questo tutorial per i passaggi su come acquisire i dati delle classificazioni Adobe Analytics in Adobe Experience Platform tramite l’interfaccia utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato in base al quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Il connettore di origine delle classificazioni di Analytics richiede che i dati siano stati migrati nella nuova infrastruttura di classificazioni di Adobe Analytics prima dell’utilizzo. Per confermare lo stato di migrazione dei tuoi dati, contatta il team del tuo account di Adobe.

## Seleziona le classificazioni

Nell&#39;interfaccia utente di Experience Platform, selezionare **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria *Adobe applications*, selezionare **[!UICONTROL Adobe Analytics]**, quindi **[!UICONTROL Configura]**.

>[!TIP]
>
>Le origini nel catalogo delle origini visualizzano l&#39;opzione **[!UICONTROL Configura]** se non è presente alcun account autenticato. Una volta autenticato un account, l&#39;opzione diventa **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini nell&#39;interfaccia utente di Experience Platform con l&#39;origine di Adobe Analytics selezionata.](../../../../images/tutorials/create/classifications/catalog.png)

Quindi seleziona [!UICONTROL Classificazioni] e seleziona i set di dati di classificazione da acquisire per l&#39;Experience Platform.

Puoi selezionare fino a 30 set di dati di classificazioni diversi da includere nell’Experience Platform. Tutti i set di dati selezionati verranno visualizzati nella barra a destra. Al termine, selezionare [!UICONTROL Avanti] per continuare.

![Pagina delle classificazioni con diversi set di dati di classificazione selezionati.](../../../../images/tutorials/create/classifications/select.png)

## Rivedere le classificazioni

Viene visualizzato il passaggio **[!UICONTROL Rivedi]**, che consente di rivedere i set di dati di classificazioni selezionati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: mostra la piattaforma di origine e lo stato della connessione.
* **[!UICONTROL Tipo di dati]**: mostra il numero di classificazioni selezionate.
* **[!UICONTROL Pianificazione]**: mostra la frequenza di sincronizzazione per i dati delle classificazioni. **Nota**: i dati delle classificazioni vengono aggiornati settimanalmente.

Dopo aver rivisto il flusso di dati, fai clic su **[!UICONTROL Fine]** e attendi un po&#39; di tempo per la creazione del flusso di dati.

![Pagina di revisione per i dati delle classificazioni di Adobe Analytics.](../../../../images/tutorials/create/classifications/review.png)

## Passaggi successivi

Seguendo questa esercitazione, hai creato un connettore sata per le classificazioni di Analytics che porta in Experience Platform i dati delle classificazioni. Per ulteriori informazioni su [!DNL Analytics] e sui dati delle classificazioni, vedere i seguenti documenti:

* [Panoramica del connettore di origine di Adobe Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Creare una connessione di origine di Analytics per i dati della suite di rapporti nell’interfaccia utente](./analytics.md)
* [Informazioni sulle classificazioni](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
