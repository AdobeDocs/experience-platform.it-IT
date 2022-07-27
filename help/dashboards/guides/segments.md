---
keywords: Experience Platform;profilo;segmento;segmenti;segmentazione;interfaccia utente;interfaccia utente;personalizzazione;dashboard segmenti;dashboard dashboard
title: Dashboard dei segmenti
description: 'Adobe Experience Platform fornisce una dashboard tramite la quale è possibile visualizzare informazioni importanti sui segmenti creati dalla tua organizzazione. '
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: 2d84a9a7caf080abd51e846f39e4090cb4aa05c7
workflow-type: tm+mt
source-wordcount: '1576'
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

Fai riferimento alla [modifica delle dashboard](../customize/modify.md) e [Panoramica della libreria Widget](../customize/widget-library.md) documentazione per ulteriori informazioni.

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

Adobe fornisce più widget standard che puoi utilizzare per visualizzare diverse metriche correlate ai tuoi segmenti. Puoi anche creare widget personalizzati da condividere con la tua organizzazione utilizzando [!UICONTROL Libreria widget]. Per ulteriori informazioni sulla creazione di widget personalizzati, si prega di iniziare leggendo [Panoramica della libreria Widget](../customize/widget-library.md).

Per ulteriori informazioni su ciascuno dei widget standard disponibili, seleziona il nome di un widget dal seguente elenco:

* [[!UICONTROL Dimensione del pubblico]](#audience-size)
* [[!UICONTROL Sovrapposizione identità]](#identity-overlap)
* [[!UICONTROL Profili per identità]](#profiles-by-identity)
* [[!UICONTROL Ordine di attivazione del pubblico]](#audience-activation-order)
* [[!UICONTROL Tendenza delle dimensioni del pubblico]](#audience-size-trend)
* [[!UICONTROL Tendenza al cambiamento della dimensione del pubblico]](#audience-size-change-trend)
* [[!UICONTROL Tendenza delle dimensioni del pubblico in base all’identità]](#audience-size-trend-by-identity)
* [[!UICONTROL Sovrapposizione del pubblico]](#audience-overlap)

### [!UICONTROL Dimensione del pubblico] {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesize"
>title="Dimensione del pubblico"
>abstract="Questo widget visualizza il numero totale di profili uniti all’interno del segmento selezionato. Questo numero dipende dal criterio di unione applicato ai dati ed è corretto al momento dell&#39;istantanea più recente."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/segments.html#audience-size" text="Ulteriori informazioni dalla documentazione"

La **[!UICONTROL Dimensione del pubblico]** widget visualizza il numero totale di profili uniti all’interno del segmento selezionato al momento dell’acquisizione dello snapshot. Questo numero è il risultato dell’applicazione dei criteri di unione dei segmenti ai dati del profilo per unire i frammenti di profilo in modo da formare un unico profilo per ogni individuo nel segmento.

Per ulteriori informazioni sui frammenti e i profili uniti, inizia leggendo il [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

![](../images/segments/audience-size.png)

### [!UICONTROL Sovrapposizione identità] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="Sovrapposizione identità"
>abstract="Questo widget mostra la sovrapposizione di profili nel segmento contenente entrambe le identità selezionate. I cerchi mostrano la dimensione relativa di ogni identità. Il numero di profili contenenti entrambi i namespace è rappresentato dalla sovrapposizione tra i cerchi."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/segments.html#identity-overlap" text="Ulteriori informazioni dalla documentazione"

La **[!UICONTROL Sovrapposizione identità]** Il widget visualizza un diagramma di Venn, o diagramma di set, che mostra la sovrapposizione di profili nel segmento contenente più identità.

Utilizza i menu a discesa del widget per selezionare le identità da confrontare. I cerchi visualizzano la dimensione relativa di ciascuna identità selezionata, con il numero di profili contenenti entrambi i namespace rappresentati dalla dimensione della sovrapposizione tra i cerchi.

Se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente saranno associate più identità, pertanto è probabile che la tua organizzazione abbia più profili contenenti frammenti da più di una identità.

Per saperne di più sulle identità, visita il [Documentazione del servizio Adobe Experience Platform Identity](../../identity-service/home.md).

![](../images/segments/identity-overlap.png)

### [!UICONTROL Profili per identità] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="Profili per identità"
>abstract="Questo widget visualizza la suddivisione delle identità per ogni profilo unito nel segmento selezionato."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/segments.html#profiles-by-identity" text="Ulteriori informazioni dalla documentazione"

La **[!UICONTROL Profili per identità]** widget visualizza la suddivisione delle identità in ogni profilo unito del segmento selezionato. Il numero totale di profili per identità può essere superiore al numero totale di profili nel segmento, perché a un profilo potrebbero essere associate più identità. In altre parole, l’aggiunta dei valori mostrati per ogni identità può avere un totale superiore alla dimensione totale del pubblico nel segmento, perché se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente possono essere associate più identità.

Seleziona **[!UICONTROL Sottotitoli]** per aprire la finestra di dialogo didascalie automatiche.

![Finestra di dialogo dei profili per didascalie di identità.](../images/segments/profiles-by-identity.png)

Un modello di apprendimento automatico genera automaticamente informazioni sui dati analizzando la distribuzione complessiva e le dimensioni chiave dei dati.

Per saperne di più sulle identità, visita il [Documentazione del servizio Adobe Experience Platform Identity](../../identity-service/home.md).

### [!UICONTROL Ordine di attivazione del pubblico] {#audience-activation-order}

La [!UICONTROL Ordine di attivazione del pubblico] widget fornisce una tabella a tre colonne in cui sono elencati i [!UICONTROL nome della destinazione], [!UICONTROL piattaforma]e l&#39;attivazione [!UICONTROL date] del pubblico. L&#39;elenco è ordinato da alto a basso in base al recente e può contenere fino a 10 righe.

![Il widget dell&#39;ordine di attivazione del pubblico.](../images/segments/audience-activation-order.png)

### [!UICONTROL Tendenza delle dimensioni del pubblico] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="Tendenza delle dimensioni del pubblico"
>abstract="Questo widget fornisce informazioni sul numero totale di profili che soddisfano i criteri di **qualsiasi** definizione del segmento, acquisita durante l’istantanea giornaliera, per gli ultimi 30 giorni, 90 giorni o 12 mesi."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/segments.html#audience-size-trend" text="Ulteriori informazioni dalla documentazione"

La **[!UICONTROL Tendenza delle dimensioni del pubblico]** widget fornisce un grafico a linee illustrativo del numero totale di profili che soddisfano i criteri di **qualsiasi** definizione del segmento in un determinato periodo di tempo. La tendenza della dimensione del pubblico può essere visualizzata per periodi di 30 giorni, 90 giorni e 12 mesi. Il periodo di tempo viene scelto da un menu a discesa nel widget. La dimensione del pubblico si riflette sull’asse y e il tempo sull’asse x.

Questo widget include anche [!UICONTROL Sottotitoli] funzione in cui un modello di apprendimento automatico analizza il grafico e i dati dei segmenti e genera automaticamente didascalie per descrivere le tendenze chiave e gli eventi importanti. Seleziona **[!UICONTROL Sottotitoli]** per aprire la finestra di dialogo didascalie automatiche.

![La panoramica dei segmenti mostra il widget di tendenza della dimensione del pubblico.](../images/segments/audience-size-trend-captions.png)

Viene visualizzata la finestra di dialogo didascalie automatiche che fornisce informazioni sui dati.

![Finestra di dialogo delle didascalie automatiche per il widget di tendenza Dimensione pubblico.](../images/segments/audience-size-trend-automatic-captions-dialog.png)

Per ulteriori informazioni sulla valutazione dei segmenti e su come i profili si qualificano e si ritirano dai segmenti, consulta [Documentazione del servizio di segmentazione](../../segmentation/home.md).

### [!UICONTROL Tendenza al cambiamento della dimensione del pubblico] {#audience-size-change-trend}

Questo widget fornisce un grafico a linee che illustra la differenza nel numero totale di profili qualificati per un dato segmento tra le istantanee giornaliere più recenti. Il segmento scelto per l’analisi viene selezionato dal menu a discesa della panoramica. Il periodo di analisi delle tendenze può essere visualizzato in 30 giorni, 90 giorni e 12 mesi. Il periodo di tempo viene scelto da un menu a discesa nel widget. La dimensione del pubblico si riflette sull’asse y e il tempo sull’asse x.

![Il widget di tendenza della modifica della dimensione del pubblico.](../images/segments/audience-size-change-trend.png)

### [!UICONTROL Tendenza delle dimensioni del pubblico in base all’identità] {#audience-size-trend-by-identity}

Questo widget illustra la tendenza delle dimensioni del pubblico per un particolare segmento in base al tipo di identità scelto dal menu a discesa del widget. Il segmento utilizzato per l’analisi viene selezionato dal menu a discesa della panoramica. Il periodo di analisi delle tendenze può essere visualizzato in 30 giorni, 90 giorni e 12 mesi. Il periodo di tempo viene scelto da un menu a discesa nel widget.

![La tendenza della dimensione del pubblico in base al widget di identità.](../images/segments/audience-size-trend-by-identity.png)

### [!UICONTROL Sovrapposizione del pubblico] {#audience-overlap}

Questo widget rappresenta il numero di profili da due segmenti che soddisfano i criteri per entrambe le definizioni di segmenti. I segmenti utilizzati per il confronto vengono selezionati dai menu a discesa dei widget. Il numero totale di profili contenuti nella definizione del segmento pertinente può essere visto passando il cursore su un cerchio o sull’intersezione del diagramma di Venn.

Questo widget consente di ottimizzare la strategia di segmentazione visualizzando le somiglianze nei risultati delle definizioni dei segmenti.

![Il widget di sovrapposizione pubblico.](../images/segments/audience-overlap.png)

<!-- * [[!UICONTROL Audience overlap report]](#audience-overlap-report) -->
<!-- ### [!UICONTROL Audience overlap report] {#audience-overlap-report} -->

<!-- View an ordered list of audiences by Highest or Lowest overlap percentages. -->

<!-- ![The Audience overlap report widget.]() -->

<!-- https://jira.corp.adobe.com/browse/PLAT-125511 -->

## Passaggi successivi

Seguendo questo documento, ora dovresti essere in grado di individuare il dashboard dei segmenti e selezionare un segmento da visualizzare. È inoltre necessario comprendere le metriche visualizzate nei widget disponibili. Per ulteriori informazioni sull’utilizzo dei segmenti nell’interfaccia utente di Experience Platform, consulta [Guida all’interfaccia utente del servizio di segmentazione](../../segmentation/ui/overview.md).
