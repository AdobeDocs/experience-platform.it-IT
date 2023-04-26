---
keywords: panoramica delle metriche; Panoramica sulle metriche rtcdp
title: Home page e dashboard di Real-time Customer Data Platform
description: Dashboard, home page e la prima esperienza utente di Adobe Experience Platform
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: 8ea657e379248616d3140bc0a7b0c25a918bc857
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 1%

---

# [!DNL Real-Time Customer Data Platform] home page

La home page di Adobe Real-time Customer Data Platform (Real-Time CDP) è la prima pagina che viene visualizzata dopo l’accesso a Real-Time CDP.

La home page di Real-Time CDP include un widget introduttivo che consente di accedere rapidamente a diverse funzioni e a una sezione metriche che visualizza informazioni aggiornate sui dati all’interno dell’organizzazione.

Questo documento fornisce una panoramica della home page di Real-Time CDP e del dashboard delle metriche.

![Pagina principale dell’interfaccia utente di Platform.](assets/platform-home/home.png)

## Widget introduttivo

La [!UICONTROL Guida introduttiva al profilo cliente in tempo reale] Il widget è diviso in quattro sezioni:

* **Inserire dati in Platform**: Questo widget ti indirizza al catalogo delle sorgenti. Utilizza il catalogo delle sorgenti per selezionare un’origine e acquisire i dati da Experience Platform. Per ulteriori informazioni, consulta la sezione [panoramica di origini](../sources/home.md)
* **Strutture di dati del modello**: Questo widget ti indirizza alla panoramica degli schemi. Utilizza la panoramica degli schemi per individuare gli schemi esistenti o creare blocchi predefiniti che descrivono la struttura dei dati. Per ulteriori informazioni, consulta la sezione [panoramica degli schemi](../xdm/home.md).
* **Tipi di pubblico dei segmenti**: Questo widget ti indirizza al [!DNL Segment Builder] nell’interfaccia utente di . Utilizza la [!DNL Segment Builder] per interagire con gli elementi dati del profilo e definire regole per i segmenti. Per ulteriori informazioni, consulta la sezione [Panoramica del servizio di segmentazione](../segmentation/home.md).
* **Inviare dati alle destinazioni**: Questo widget ti indirizza al catalogo delle destinazioni. Utilizza il catalogo delle destinazioni per selezionare una destinazione a cui connetterti e invia i segmenti. Per ulteriori informazioni, consulta la sezione [panoramica sulle destinazioni](../destinations/home.md)

![Pagina principale dell’interfaccia utente della piattaforma in cui viene visualizzato il widget guida introduttiva](assets/platform-home/getting-started-widget.png)

## Dashboard delle metriche

Il dashboard delle metriche mostra informazioni aggiornate sui dati di Experience Platform. Il dashboard è diviso in due sezioni:

### La classifica

La classifica mostra il numero totale corrente di schemi, set di dati, profili e segmenti nell’organizzazione, nonché la data di aggiornamento più recente.

![La sezione della classifica nella home page dell’interfaccia utente di Platform.](assets/platform-home/leaderboard.png)

* **Totale schemi**: La **Totale schemi** visualizza il numero di schemi nel sistema. Questo contatore viene aggiornato quando viene creato uno schema. Per ulteriori informazioni, consulta la sezione [panoramica degli schemi](../xdm/home.md).
* **Set di dati totali**: La **Set di dati totali** contatore mostra il numero di set di dati nel sistema e la quantità di dati in [!DNL Platform]. Questo contatore viene aggiornato quando viene creato un set di dati. Per ulteriori informazioni sui set di dati, consulta la sezione [panoramica dei set di dati](../catalog/datasets/overview.md).
* **Profili totali**: La **Profili** count mostra il numero totale di persone con profili nel [!DNL Real-Time Customer Profile]. Non include frammenti di profilo. Questo è il tuo pubblico totalmente indirizzabile. Questo conteggio utilizza il valore predefinito [criterio di unione](profile/merge-policies.md) come impostato nella configurazione dei criteri di unione nel profilo unificato. Il numero di profili viene aggiornato una volta ogni 24 ore. Per ulteriori informazioni sui profili, consulta la sezione [Panoramica del profilo cliente in tempo reale](../profile/home.md).
* **Segmenti totali**: **Segmenti** mostra il numero totale di segmenti creati per l’organizzazione. Questo numero viene aggiornato quando vengono creati nuovi segmenti. Per ulteriori informazioni sui segmenti, consulta la sezione [Panoramica del servizio di segmentazione](../segmentation/home.md).

### Articoli recenti

Articoli recenti elenca le modifiche più recenti apportate all’organizzazione. Nell’esempio seguente, le modifiche più recenti riguardano set di dati, origini, segmenti e destinazioni.

![La sezione degli elementi recenti nella home page dell’interfaccia utente di Platform.](assets/platform-home/recent-items.png)

* **Set di dati recenti**: La **[!UICONTROL Set di dati recenti]** la scheda mostra i cinque set di dati più recenti creati all’interno dell’organizzazione. Questo elenco viene aggiornato quando viene creato un nuovo set di dati. Seleziona un set di dati per visualizzare i dettagli dell’elemento o seleziona **[!UICONTROL Visualizza tutto]** per un elenco di set di dati. Da qui puoi selezionare una sorgente specifica per i dettagli. Per ulteriori informazioni sui set di dati, consulta la sezione [panoramica dei set di dati](../catalog/datasets/overview.md).
* **Fonti recenti**: La **[!UICONTROL Fonti recenti]** la scheda metrica mostra le cinque origini più recenti create all’interno dell’organizzazione. Questo elenco viene aggiornato al momento della creazione di una nuova origine. Selezionare un&#39;origine per visualizzare i dettagli dell&#39;elemento oppure selezionare **[!UICONTROL Visualizza tutto]** per un elenco delle origini. Da qui puoi selezionare una sorgente specifica per i dettagli. Per ulteriori informazioni sulle origini, consulta [Panoramica delle origini](../sources/home.md).
* **Segmenti recenti**: La **[!UICONTROL Segmenti recenti]** la scheda metrica mostra i cinque segmenti più recenti creati all’interno dell’organizzazione. Questo elenco viene aggiornato al momento della creazione di un nuovo segmento. Seleziona un segmento per visualizzare i dettagli dell’elemento oppure seleziona **[!UICONTROL Visualizza tutto]** per un elenco di segmenti. Per ulteriori informazioni sui segmenti, vedi [Panoramica del servizio di segmentazione](../segmentation/home.md).
* **Destinazioni recenti**: La **[!UICONTROL Destinazioni recenti]** la scheda metrica mostra le cinque destinazioni più recenti create all’interno dell’organizzazione. Questo elenco viene aggiornato al momento della creazione di una nuova destinazione. Selezionare una destinazione per visualizzare i dettagli dell&#39;elemento oppure selezionare **[!UICONTROL Visualizza tutto]** per un elenco delle destinazioni. Per ulteriori informazioni, consulta la sezione [panoramica sulle destinazioni](../destinations/home.md).

## Risorse

Infine, il widget risorse ti fornisce ulteriori risorse di documentazione a cui puoi fare riferimento. Comprendono:

![La sezione risorse nella home page dell’interfaccia utente di Platform.](assets/platform-home/resources.png)

* [Informazioni sugli schemi](../xdm/schema/composition.md)
* [Connessione delle sorgenti](../sources/home.md)
* [Come compilare il profilo cliente in tempo reale](../profile/home.md)
* [Collegare le destinazioni](../destinations/home.md)
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
