---
keywords: panoramica metriche; panoramica metriche rtcdp
title: Home page e dashboard di Real-time Customer Data Platform
description: Dashboard, home page e la prima esperienza utente di Adobe Experience Platform
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 2%

---

# [!DNL Real-Time Customer Data Platform] home page e dashboard

Quando accedi a Real-Time CDP, viene visualizzata la home page di Adobe Real-time Customer Data Platform (Real-Time CDP), che include una dashboard delle metriche.

La home page è solo una delle posizioni in cui vengono visualizzate le schede metriche. Real-Time CDP fornisce schede di metrica per tutta la tua esperienza. Queste metriche ti informano sui dati, sul profilo e sui segmenti di pubblico nel sistema.

![immagine](assets/home.png)

Se al momento dell&#39;accesso a Real-Time CDP non sono presenti dati, la dashboard nella home page non viene visualizzata. In questo caso, la pagina Home fornisce materiale di apprendimento per la prima esperienza utente. Quando i dati vengono raccolti, in altre parole, come <!--sources-->vengono creati set di dati, profili, segmenti e destinazioni e i dati fluiscono nel sistema; il dashboard viene aggiornato automaticamente per visualizzare informazioni su tali dati<!-- in metric cards-->.

## Visualizzazione dashboard della pagina iniziale

<!--The dashboard shows information in several areas. Each category of information displays for the time range shown beneath the data.-->

Il dashboard è diviso in<!-- two areas.-->:

* **La classifica** è nella parte superiore del dashboard. La classifica mostra il numero di set di dati, profili, segmenti e destinazioni nel sistema.

   ![immagine](assets/leaderboard.png)

<!-- * **Metric cards** display beneath the leaderboard. Metric cards show additional information, such as percentages or trends. Metric cards appear as data is collected.
    ![image](assets/home-metrics.jpg)
Some information is shown in different ways on both the leaderboard and metric cards. -->
* **Elementi recenti** elenca i cinque set di dati, origini, segmenti e destinazioni più recenti aggiunti al sistema.

   ![immagine](assets/recent.png)

Altre metriche, ad esempio per profili e segmenti, sono disponibili in altre parti di Real-time Customer Data Platform.

### Set di dati

Il **[!UICONTROL Set di dati]** mostra il numero di set di dati nel sistema e la quantità di dati in [!DNL Platform]. Questo contatore viene aggiornato quando viene creato un set di dati.

Per ulteriori informazioni sui set di dati, consulta [panoramica dei set di dati](../catalog/datasets/overview.md).

### Profili

Il **[!UICONTROL Profili]** conteggio mostra il numero totale di persone con profili nel [!DNL Real-Time Customer Profile]. Non include frammenti di profilo. Questo è il tuo pubblico indirizzabile totale.

Questo conteggio utilizza il valore predefinito [criterio di unione](profile/merge-policies.md) come impostato nella configurazione del criterio di unione in Profilo unificato.

Il numero di profili viene aggiornato una volta ogni 24 ore.

Per ulteriori informazioni sui profili, consulta [Una visione unificata del cliente in Real-Time CDP](profile/profile-overview.md).

### Segmenti

**[!UICONTROL Segmenti]** mostra il numero totale di segmenti creati per l’organizzazione. Questo numero viene aggiornato quando vengono creati nuovi segmenti.

Per ulteriori informazioni sui segmenti, consulta [Panoramica del servizio di segmentazione](segmentation/segmentation-overview.md).

### Destinazioni

**[!UICONTROL Destinazioni]** mostra il numero totale di destinazioni create per l’organizzazione. Questo numero viene aggiornato quando vengono create nuove destinazioni.

Per ulteriori informazioni sulle destinazioni, consulta [Panoramica sulle destinazioni](destinations/overview.md).

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Select **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-Time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Select **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-Time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Select **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->

### Set di dati recenti

Il **[!UICONTROL Set di dati recenti]** mostra i cinque set di dati più recenti creati all’interno dell’organizzazione. Questo elenco viene aggiornato quando viene creato un nuovo set di dati.

Seleziona un set di dati per visualizzare i dettagli di tale elemento oppure **[!UICONTROL Visualizza tutto]** per visualizzare l’elenco dei set di dati. Da qui, puoi selezionare un’origine specifica per i dettagli.

Per ulteriori informazioni sui set di dati, consulta [panoramica dei set di dati](../catalog/datasets/overview.md).

### Origini recenti

Il **[!UICONTROL Origini recenti]** La scheda metrica mostra le cinque origini più recenti create all’interno dell’organizzazione. Questo elenco viene aggiornato al momento della creazione di una nuova origine.

Selezionare un&#39;origine per visualizzare i dettagli dell&#39;elemento oppure **[!UICONTROL Visualizza tutto]** per visualizzare l&#39;elenco delle origini. Da qui, puoi selezionare un’origine specifica per i dettagli.

Per ulteriori informazioni sulle origini, consulta [Panoramica sulle origini](sources/sources-overview.md).

### Segmenti recenti

Il **[!UICONTROL Segmenti recenti]** La scheda metrica mostra i cinque segmenti più recenti creati all’interno dell’organizzazione. Questo elenco viene aggiornato quando viene creato un nuovo segmento.

Seleziona un segmento per visualizzare i dettagli di quell’elemento, oppure **[!UICONTROL Visualizza tutto]** per visualizzare informazioni su altri segmenti.

Per ulteriori informazioni sui segmenti, consulta [Panoramica del servizio di segmentazione](segmentation/segmentation-overview.md).

### Destinazioni recenti

Il **[!UICONTROL Destinazioni recenti]** La scheda metrica mostra le cinque destinazioni più recenti create all’interno dell’organizzazione. Questo elenco viene aggiornato quando viene creata una nuova destinazione.

Selezionare una destinazione per visualizzare i dettagli dell&#39;elemento oppure **[!UICONTROL Visualizza tutto]** per visualizzare informazioni su altre destinazioni.

Per ulteriori informazioni sulle destinazioni, consulta [Panoramica sulle destinazioni](destinations/overview.md).
