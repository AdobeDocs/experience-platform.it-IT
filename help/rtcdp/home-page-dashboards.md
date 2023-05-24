---
keywords: panoramica metriche; panoramica metriche rtcdp
title: Home page e dashboard di Real-time Customer Data Platform
description: Dashboard, home page e la prima esperienza utente di Adobe Experience Platform
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: 8ea657e379248616d3140bc0a7b0c25a918bc857
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 1%

---

# [!DNL Real-Time Customer Data Platform] home page

La home page di Adobe Real-time Customer Data Platform (Real-Time CDP) è la prima pagina visualizzata dopo l’accesso a Real-Time CDP.

La pagina Home di Real-Time CDP include un widget introduttivo che consente di accedere rapidamente a diverse funzioni diverse e una sezione metriche che visualizza informazioni aggiornate sui dati all’interno dell’organizzazione.

Questo documento fornisce una panoramica della home page di Real-Time CDP e del dashboard delle metriche.

![La home page dell’interfaccia utente di Platform.](assets/platform-home/home.png)

## Widget guida introduttiva

Il [!UICONTROL Guida introduttiva a Real-Time Customer Profile] il widget è diviso in quattro sezioni:

* **Inserire dati in Platform**: questo widget indirizza l’utente al catalogo delle origini. Utilizza il catalogo origini per selezionare un’origine e acquisire i dati da Experience Platform. Per ulteriori informazioni, leggere [panoramica sulle origini](../sources/home.md)
* **Modellare le strutture di dati**: questo widget reindirizza alla panoramica degli schemi. Utilizza la panoramica degli schemi per cercare gli schemi esistenti o creare blocchi predefiniti che descrivono la struttura dei dati. Per ulteriori informazioni, leggere [panoramica degli schemi](../xdm/home.md).
* **Segmentazione dei tipi di pubblico**: questo widget indirizza l’utente al [!DNL Segment Builder] nell’interfaccia utente. Utilizza il [!DNL Segment Builder] per interagire con gli elementi dati del profilo e definire regole per i segmenti. Per ulteriori informazioni, leggere [Panoramica del servizio di segmentazione](../segmentation/home.md).
* **Inviare dati alle destinazioni**: questo widget indirizza l’utente al catalogo delle destinazioni. Utilizza il catalogo delle destinazioni per selezionare una destinazione a cui poi puoi connettersi e inviare segmenti. Per ulteriori informazioni, leggere [panoramica sulle destinazioni](../destinations/home.md)

![La home page dell’interfaccia utente di Platform che mostra il widget per iniziare](assets/platform-home/getting-started-widget.png)

## Dashboard delle metriche

Il dashboard delle metriche mostra informazioni aggiornate sui dati dell’Experience Platform. Il dashboard è diviso in due sezioni:

### La classifica

La classifica mostra il numero totale corrente di schemi, set di dati, profili e segmenti nell’organizzazione, nonché la data del loro aggiornamento più recente.

![La sezione classifica nella home page dell’interfaccia utente di Platform.](assets/platform-home/leaderboard.png)

* **Schemi totali**: Il **Schemi totali** contatore indica il numero di schemi nel sistema. Questo contatore viene aggiornato quando si crea uno schema. Per ulteriori informazioni, leggere [panoramica degli schemi](../xdm/home.md).
* **Set di dati totali**: Il **Set di dati totali** mostra il numero di set di dati nel sistema e la quantità di dati in [!DNL Platform]. Questo contatore viene aggiornato quando viene creato un set di dati. Per ulteriori informazioni sui set di dati, consulta [panoramica dei set di dati](../catalog/datasets/overview.md).
* **Profili totali**: Il **Profili** conteggio mostra il numero totale di persone con profili nel [!DNL Real-Time Customer Profile]. Non include frammenti di profilo. Questo è il tuo pubblico indirizzabile totale. Questo conteggio utilizza il valore predefinito [criterio di unione](profile/merge-policies.md) come impostato nella configurazione del criterio di unione in Profilo unificato. Il numero di profili viene aggiornato una volta ogni 24 ore. Per ulteriori informazioni sui profili, consulta [Panoramica del profilo cliente in tempo reale](../profile/home.md).
* **Segmenti totali**: **Segmenti** mostra il numero totale di segmenti creati per l’organizzazione. Questo numero viene aggiornato quando vengono creati nuovi segmenti. Per ulteriori informazioni sui segmenti, consulta [Panoramica del servizio di segmentazione](../segmentation/home.md).

### Elementi recenti

Articoli recenti elenca le modifiche più recenti apportate all&#39;organizzazione. Nell’esempio seguente, le modifiche più recenti riguardano set di dati, origini, segmenti e destinazioni.

![La sezione degli elementi recenti nella home page dell’interfaccia utente di Platform.](assets/platform-home/recent-items.png)

* **Set di dati recenti**: Il **[!UICONTROL Set di dati recenti]** mostra i cinque set di dati più recenti creati all’interno dell’organizzazione. Questo elenco viene aggiornato quando viene creato un nuovo set di dati. Seleziona un set di dati per visualizzare i dettagli di tale elemento oppure seleziona **[!UICONTROL Visualizza tutto]** per un elenco di set di dati. Da qui, puoi selezionare un’origine specifica per i dettagli. Per ulteriori informazioni sui set di dati, consulta [panoramica dei set di dati](../catalog/datasets/overview.md).
* **Origini recenti**: Il **[!UICONTROL Origini recenti]** La scheda metrica mostra le cinque origini più recenti create all’interno dell’organizzazione. Questo elenco viene aggiornato al momento della creazione di una nuova origine. Selezionare un&#39;origine per visualizzare i dettagli dell&#39;elemento oppure selezionare **[!UICONTROL Visualizza tutto]** per un elenco di origini. Da qui, puoi selezionare un’origine specifica per i dettagli. Per ulteriori informazioni sulle origini, consulta [Panoramica sulle origini](../sources/home.md).
* **Segmenti recenti**: Il **[!UICONTROL Segmenti recenti]** La scheda metrica mostra i cinque segmenti più recenti creati all’interno dell’organizzazione. Questo elenco viene aggiornato quando viene creato un nuovo segmento. Seleziona un segmento per visualizzare i dettagli di quell’elemento, oppure seleziona **[!UICONTROL Visualizza tutto]** per un elenco di segmenti. Per ulteriori informazioni sui segmenti, consulta [Panoramica del servizio di segmentazione](../segmentation/home.md).
* **Destinazioni recenti**: Il **[!UICONTROL Destinazioni recenti]** La scheda metrica mostra le cinque destinazioni più recenti create all’interno dell’organizzazione. Questo elenco viene aggiornato quando viene creata una nuova destinazione. Selezionare una destinazione per visualizzare i dettagli dell&#39;elemento oppure selezionare **[!UICONTROL Visualizza tutto]** per un elenco di destinazioni. Per ulteriori informazioni, leggere [panoramica sulle destinazioni](../destinations/home.md).

## Risorse

Infine, il widget delle risorse fornisce ulteriori risorse di documentazione a cui puoi fare riferimento. Comprendono:

![La sezione delle risorse nella home page dell’interfaccia utente di Platform.](assets/platform-home/resources.png)

* [Informazioni sugli schemi](../xdm/schema/composition.md)
* [Collegamento delle sorgenti](../sources/home.md)
* [Come popolare Real-Time Customer Profile](../profile/home.md)
* [Connessione delle destinazioni](../destinations/home.md)
* [Gestisci accesso](../access-control/abac/overview.md)

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
