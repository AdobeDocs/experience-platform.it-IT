---
keywords: panoramica metriche; panoramica metriche rtcdp
title: Home page e dashboard di Real-time Customer Data Platform
description: Informazioni sulle le diverse dashboard, la pagina Home e la prima esperienza utente di Adobe Real-Time CDP.
feature: Dashboards, Get Started
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: 2704184446f7945c744e7e2d2a8c3cda3fc12527
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 7%

---

# Home page di [!DNL Real-Time Customer Data Platform]

La home page di Adobe Real-time Customer Data Platform (Real-Time CDP) è la prima pagina visualizzata dopo l’accesso a Real-Time CDP.

La pagina Home di Real-Time CDP include un widget introduttivo che consente di accedere rapidamente a diverse funzioni diverse e una sezione metriche che visualizza informazioni aggiornate sui dati all’interno dell’organizzazione.

Questo documento fornisce una panoramica della home page di Real-Time CDP e del dashboard delle metriche.

![Home page dell&#39;interfaccia utente di Platform.](assets/platform-home/home.png)

## Widget guida introduttiva

Il widget [!UICONTROL Guida introduttiva a Real-Time Customer Profile] è suddiviso in quattro sezioni:

* **Inserire dati in Platform**: questo widget reindirizza l&#39;utente al catalogo delle origini. Utilizza il catalogo origini per selezionare un’origine e acquisire i dati da Experience Platform. Selezionare **[Configura origini]** per passare al catalogo delle origini. Per ulteriori informazioni, leggere la [panoramica delle origini](../sources/home.md).
* **Strutture dati modello**: questo widget reindirizza l&#39;utente alla panoramica degli schemi. Utilizza la panoramica degli schemi per cercare gli schemi esistenti o creare una blueprint che descriva la struttura dei tuoi dati. Seleziona **[!UICONTROL Crea schema]** per passare all&#39;interfaccia di creazione dello schema. Per ulteriori informazioni, leggere la [panoramica degli schemi](../xdm/home.md).
* **Genera tipi di pubblico**: questo widget indirizza l&#39;utente al Generatore di segmenti nell&#39;interfaccia utente. Utilizza Segment Builder (Generatore di segmenti) per interagire con gli elementi dati del profilo e definire i criteri per la definizione del segmento. Seleziona **[!UICONTROL Crea pubblico]** per passare al Generatore di segmenti. Per ulteriori informazioni, leggere la [Panoramica del servizio di segmentazione](../segmentation/home.md).
* **Invia dati alle destinazioni**: questo widget indirizza l&#39;utente al catalogo delle destinazioni. Utilizza il catalogo delle destinazioni per selezionare una destinazione a cui poi puoi connettersi e inviare tipi di pubblico. Seleziona **[!UICONTROL Configura destinazioni]** per passare al catalogo delle destinazioni. Per ulteriori informazioni, leggere la [panoramica delle destinazioni](../destinations/home.md).

![La home page dell&#39;interfaccia utente di Platform che visualizza il widget di introduzione](assets/platform-home/getting-started-widget.png)

## Dashboard delle metriche {#metrics-dashboard}

>[!CONTEXTUALHELP]
>id="platform_home_metrics_totalProfiles"
>title="Numero totale di profili"
>abstract="Il numero totale di profili di cui dispone la tua organizzazione in Experience Platform. Questo conteggio si basa sul criterio di unione della tua organizzazione e non include frammenti di profilo. Il numero di profili viene aggiornato ogni 24 ore."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=it#profile-count" text="Ulteriori informazioni sono disponibili nella documentazione"

Il dashboard delle metriche mostra informazioni aggiornate sui dati dell’Experience Platform. Il dashboard è diviso in due sezioni:

### La classifica

La classifica mostra il numero totale corrente di schemi, set di dati, profili e tipi di pubblico nell’organizzazione, nonché la data del loro aggiornamento più recente.

![Sezione classifica nella home page dell&#39;interfaccia utente di Platform.](assets/platform-home/leaderboard.png)

* **Schemi totali**: il contatore **Schemi totali** visualizza il numero di schemi nel sistema. Questo contatore viene aggiornato quando si crea uno schema. Per ulteriori informazioni, leggere la [panoramica degli schemi](../xdm/home.md).
* **Set di dati totali**: il contatore **Set di dati totali** mostra il numero di set di dati nel sistema e la quantità di dati in Experience Platform. Questo contatore viene aggiornato quando viene creato un set di dati. Per ulteriori informazioni sui set di dati, leggere la [panoramica dei set di dati](../catalog/datasets/overview.md).
* **Profili totali**: il conteggio di **Profili** mostra il numero totale di profili dell&#39;organizzazione all&#39;interno di Experience Platform. Non include frammenti di profilo. Questo è il tuo pubblico indirizzabile totale. Questo conteggio utilizza il [criterio di unione](profile/merge-policies.md) predefinito impostato nella configurazione del criterio di unione in Real-Time Customer Profile. Il numero di profili viene aggiornato una volta ogni 24 ore. Seleziona **[!UICONTROL Profili]** per passare alla pagina Panoramica profili e visualizzare tutte le metriche del profilo. Per ulteriori informazioni sui profili, leggere la [Panoramica del profilo cliente in tempo reale](../profile/home.md).
* **Pubblico totale**: il contatore **Pubblico totale** mostra il numero totale di tipi di pubblico creati per l&#39;organizzazione. Questo numero viene aggiornato quando vengono creati nuovi tipi di pubblico. Per ulteriori informazioni sui tipi di pubblico, leggere la [Panoramica del servizio di segmentazione](../segmentation/home.md).

### Elementi recenti

Articoli recenti elenca le modifiche più recenti apportate all&#39;organizzazione. Nell’esempio seguente, le modifiche più recenti riguardano set di dati, origini, pubblico e destinazioni.

![Sezione degli elementi recenti nella home page dell&#39;interfaccia utente di Platform.](assets/platform-home/recent-items.png)

* **Set di dati recenti**: la scheda **[!UICONTROL Set di dati recenti]** mostra i cinque set di dati più recenti creati nell&#39;organizzazione. Questo elenco viene aggiornato quando viene creato un nuovo set di dati. Selezionare un set di dati per visualizzare i dettagli dell&#39;elemento oppure selezionare **[!UICONTROL Visualizza tutti]** per un elenco di set di dati. Da qui, puoi selezionare un’origine specifica per i dettagli. Per ulteriori informazioni sui set di dati, vedere [panoramica dei set di dati](../catalog/datasets/overview.md).
* **Origini recenti**: la scheda metrica **[!UICONTROL Origini recenti]** mostra le cinque origini più recenti create all&#39;interno dell&#39;organizzazione. Questo elenco viene aggiornato al momento della creazione di una nuova origine. Selezionare un&#39;origine per visualizzare i dettagli dell&#39;elemento oppure selezionare **[!UICONTROL Visualizza tutti]** per un elenco di origini. Da qui, puoi selezionare un’origine specifica per i dettagli. Per ulteriori informazioni sulle origini, vedere [Panoramica delle origini](../sources/home.md).
* **Tipi di pubblico recenti**: la scheda metrica **[!UICONTROL Tipi di pubblico recenti]** mostra i cinque tipi di pubblico più recenti creati all&#39;interno dell&#39;organizzazione. Questo elenco viene aggiornato al momento della creazione di un nuovo pubblico. Selezionare un pubblico per visualizzare i dettagli dell&#39;elemento oppure selezionare **[!UICONTROL Visualizza tutti]** per un elenco di tipi di pubblico. Per ulteriori informazioni sui tipi di pubblico, vedere [Panoramica del servizio di segmentazione](../segmentation/home.md).
* **Destinazioni recenti**: la scheda delle metriche **[!UICONTROL Destinazioni recenti]** mostra le cinque destinazioni più recenti create all&#39;interno dell&#39;organizzazione. Questo elenco viene aggiornato quando viene creata una nuova destinazione. Selezionare una destinazione per visualizzare i dettagli dell&#39;elemento oppure selezionare **[!UICONTROL Visualizza tutti]** per un elenco di destinazioni. Per ulteriori informazioni, leggere la [panoramica delle destinazioni](../destinations/home.md).

## Risorse

Infine, il widget delle risorse fornisce ulteriori risorse di documentazione a cui puoi fare riferimento. Comprendono:

![Sezione delle risorse nella home page dell&#39;interfaccia utente di Platform.](assets/platform-home/resources.png)

* [Informazioni sugli schemi](../xdm/schema/composition.md)
* [Collegamento delle fonti](../sources/home.md)
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
