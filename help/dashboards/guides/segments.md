---
keywords: Experience Platform;profilo;segmento;segmenti;segmentazione;interfaccia utente;interfaccia utente;personalizzazione;dashboard segmenti;dashboard dashboard
title: Dashboard dei segmenti
description: 'Adobe Experience Platform fornisce una dashboard tramite la quale è possibile visualizzare informazioni importanti sui segmenti creati dalla tua organizzazione. '
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: 2842344f4b17d76bf1c3313500e691357df31ebc
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 0%

---

# Dashboard dei segmenti {#segment-dashboard}

L’interfaccia utente di Adobe Experience Platform offre una dashboard attraverso la quale è possibile visualizzare informazioni importanti sui segmenti, acquisite durante un’istantanea giornaliera. Questa guida illustra come accedere e lavorare con il dashboard dei segmenti nell’interfaccia utente e fornisce ulteriori informazioni sulle visualizzazioni visualizzate nel dashboard.

Per una panoramica di tutte le funzioni del servizio di segmentazione di Adobe Experience Platform all’interno dell’interfaccia utente di Platform, visita il [Guida all’interfaccia utente del servizio di segmentazione](../../segmentation/ui/overview.md).

## Dati del dashboard dei segmenti

Il dashboard dei segmenti visualizza un’istantanea dei dati dell’attributo (record) dell’organizzazione nell’archivio profili di Experience Platform. Lo snapshot non include dati di eventi (serie temporali).

I dati attributo nello snapshot mostrano esattamente come vengono visualizzati nel momento specifico in cui è stata acquisita l&#39;istantanea. In altre parole, lo snapshot non è un&#39;approssimazione o un esempio dei dati e il dashboard dei segmenti non viene aggiornato in tempo reale.

>[!NOTE]
>
>Eventuali modifiche o aggiornamenti apportati ai dati dall&#39;acquisizione dello snapshot non verranno visualizzati nel dashboard fino all&#39;acquisizione dello snapshot successivo.

## Esplorazione del dashboard dei segmenti

Per passare al [!UICONTROL Segmenti] nell’interfaccia utente di Platform, seleziona **[!UICONTROL Segmenti]** nella barra a sinistra, seleziona la **[!UICONTROL Panoramica]** per visualizzare il dashboard.

>[!NOTE]
>
>Se la tua organizzazione è nuova di Platform e non dispone ancora di set di dati di profilo attivi o di criteri di unione creati, la [!UICONTROL Segmenti] dashboard non è visibile. Invece, [!UICONTROL Panoramica] visualizza collegamenti e documentazione per iniziare a usare la segmentazione.

![](../images/segments/dashboard-overview.png)

### Modifica della [!UICONTROL Segmenti] dashboard

Puoi modificare l’aspetto della [!UICONTROL Segmenti] dashboard selezionando **[!UICONTROL Modifica dashboard]**. Questo consente di spostare, aggiungere e rimuovere i widget dal dashboard e di accedere al **[!UICONTROL Libreria widget]** per esplorare i widget disponibili e creare widget personalizzati per la tua organizzazione.

Fai riferimento alla [modifica delle dashboard](../customize/modify.md) e [panoramica della libreria widget](../customize/widget-library.md) documentazione per ulteriori informazioni.

## Selezionare un segmento

Il dashboard seleziona automaticamente un segmento da visualizzare, tuttavia puoi modificare il segmento utilizzando il menu a discesa o il selettore di segmenti.

Per scegliere un segmento diverso, seleziona il menu a discesa accanto al nome del segmento o utilizza il selettore del segmento per aprire la finestra di dialogo di selezione del segmento.

![](../images/segments/change-segment.png)

![](../images/segments/select-segment-dialog.png)

## Widget e metriche

Il dashboard dei segmenti è composto da widget, che sono metriche di sola lettura che forniscono informazioni importanti sul segmento selezionato.

La data e l’ora &quot;ultimo aggiornamento&quot; di un widget mostrano quando è stata acquisita l’ultima istantanea dei dati. La data e l’ora dell’istantanea sono indicate in UTC; non si trova nel fuso orario del singolo utente o dell’organizzazione IMS.

![](../images/segments/widget-timestamp.png)

## Widget standard

Adobe fornisce più widget standard che puoi utilizzare per visualizzare diverse metriche correlate ai tuoi segmenti. Puoi anche creare widget personalizzati da condividere con la tua organizzazione utilizzando [!UICONTROL Libreria widget]. Per ulteriori informazioni sulla creazione di widget personalizzati, si prega di iniziare leggendo [panoramica della libreria widget](../customize/widget-library.md).

Per ulteriori informazioni su ciascuno dei widget standard disponibili, seleziona il nome di un widget dal seguente elenco:

* [[!UICONTROL Dimensione del pubblico]](#audience-size)
* [[!UICONTROL Tendenza delle dimensioni del pubblico]](#audience-size-trend)
* [[!UICONTROL Sovrapposizione identità]](#identity-overlap)
* [[!UICONTROL Profili per identità]](#profiles-by-identity)

### [!UICONTROL Dimensione del pubblico] {#audience-size}

La **[!UICONTROL Dimensione del pubblico]** widget visualizza il numero totale di profili uniti all’interno del segmento selezionato al momento dell’acquisizione dello snapshot. Questo numero è il risultato dell’applicazione dei criteri di unione dei segmenti ai dati del profilo per unire i frammenti di profilo in modo da formare un unico profilo per ogni individuo nel segmento.

Per ulteriori informazioni sui frammenti e i profili uniti, inizia leggendo il [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

![](../images/segments/audience-size.png)

### [!UICONTROL Tendenza delle dimensioni del pubblico] {#audience-size-trend}

La **[!UICONTROL Tendenza delle dimensioni del pubblico]** widget fornisce informazioni sul numero totale di profili nel segmento acquisiti durante l’istantanea giornaliera, negli ultimi 30 giorni, 90 giorni o 12 mesi. Questo widget mostra come la dimensione del segmento potrebbe essere cambiata nel tempo, in quanto i nuovi profili si qualificano o escono dal segmento.

Per ulteriori informazioni sulla valutazione dei segmenti e su come i profili si qualificano e si ritirano dai segmenti, consulta [Documentazione del servizio di segmentazione](../../segmentation/home.md).

![La panoramica dei segmenti mostra il widget di tendenza della dimensione del pubblico.](../images/segments/audience-size-trend-captions.png)

La **[!UICONTROL Tendenza delle dimensioni del pubblico]** widget fornisce un [!UICONTROL Sottotitoli] in alto a destra del widget. Seleziona **[!UICONTROL Sottotitoli]** per aprire la finestra di dialogo didascalie automatiche. Un modello di apprendimento automatico genera automaticamente didascalie per descrivere le tendenze chiave e gli eventi importanti analizzando il grafico e i dati dei segmenti.

![Finestra di dialogo delle didascalie automatiche per il widget di tendenza Dimensione pubblico.](../images/segments/audience-size-trend-automatic-captions-dialog.png)

### [!UICONTROL Sovrapposizione identità] {#identity-overlap}

La **[!UICONTROL Sovrapposizione identità]** Il widget visualizza un diagramma di Venn, o diagramma di set, che mostra la sovrapposizione di profili nel segmento contenente più identità.

Dopo aver utilizzato i menu a discesa del widget per selezionare le identità da confrontare, i cerchi visualizzano la dimensione relativa di ogni identità, con il numero di profili contenenti entrambi i namespace rappresentati dalla dimensione della sovrapposizione tra i cerchi.

Se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente saranno associate più identità, pertanto è probabile che la tua organizzazione abbia più profili contenenti frammenti da più di una identità.

Per saperne di più sulle identità, visita il [Documentazione del servizio Adobe Experience Platform Identity](../../identity-service/home.md).

![](../images/segments/identity-overlap.png)

### [!UICONTROL Profili per identità] {#profiles-by-identity}

La **[!UICONTROL Profili per identità]** widget visualizza la suddivisione delle identità in tutti i profili uniti nel segmento selezionato. Il numero totale di profili per identità può essere superiore al numero totale di profili nel segmento, perché a un profilo potrebbero essere associate più identità. In altre parole, l’aggiunta dei valori mostrati per ogni identità può avere un totale superiore alla dimensione totale del pubblico nel segmento, perché se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente possono essere associate più identità.

Per saperne di più sulle identità, visita il [Documentazione del servizio Adobe Experience Platform Identity](../../identity-service/home.md).

![](../images/segments/profiles-by-identity.png)

## Passaggi successivi

Seguendo questo documento, ora dovresti essere in grado di individuare il dashboard dei segmenti e selezionare un segmento da visualizzare. È inoltre necessario comprendere le metriche visualizzate nei widget disponibili. Per ulteriori informazioni sull’utilizzo dei segmenti nell’interfaccia utente di Experience Platform, consulta [Guida all’interfaccia utente del servizio di segmentazione](../../segmentation/ui/overview.md).
