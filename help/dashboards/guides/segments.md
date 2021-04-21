---
keywords: Experience Platform;profilo;segmento;segmenti;segmentazione;interfaccia utente;interfaccia utente;personalizzazione;dashboard segmenti;dashboard dashboard
title: Dashboard dei segmenti
description: 'Adobe Experience Platform fornisce una dashboard tramite la quale è possibile visualizzare informazioni importanti sui segmenti creati dalla tua organizzazione. '
topic-legacy: guide
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 1%

---

# (Beta) Dashboard dei segmenti {#segment-dashboard}

>[!IMPORTANT]
>
>La funzionalità del dashboard descritta in questo documento è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

L’interfaccia utente di Adobe Experience Platform offre una dashboard attraverso la quale è possibile visualizzare informazioni importanti sui segmenti, acquisite durante un’istantanea giornaliera. Questa guida illustra come accedere e lavorare con il dashboard dei segmenti nell’interfaccia utente e fornisce ulteriori informazioni sulle visualizzazioni visualizzate nel dashboard.

Per una panoramica di tutte le funzioni del servizio di segmentazione di Adobe Experience Platform nell’interfaccia utente di Platform, visita la [guida all’interfaccia utente del servizio di segmentazione](../../segmentation/ui/overview.md).

## Dati del dashboard dei segmenti

Il dashboard dei segmenti visualizza un’istantanea dei dati dell’attributo (record) dell’organizzazione nell’archivio profili di Experience Platform. Lo snapshot non include dati di eventi (serie temporali).

I dati attributo nello snapshot mostrano esattamente come vengono visualizzati nel momento specifico in cui è stata acquisita l&#39;istantanea. In altre parole, lo snapshot non è un&#39;approssimazione o un esempio dei dati e il dashboard dei segmenti non viene aggiornato in tempo reale.

>[!NOTE]
>
>Eventuali modifiche o aggiornamenti apportati ai dati dall&#39;acquisizione dello snapshot non verranno visualizzati nel dashboard fino all&#39;acquisizione dello snapshot successivo.

## Esplorazione del dashboard dei segmenti

Per passare al dashboard dei segmenti all’interno dell’interfaccia utente di Platform, seleziona **[!UICONTROL Segments]** nella barra a sinistra, quindi seleziona la scheda **[!UICONTROL Overview]** per visualizzare il dashboard.

![](../images/segments/dashboard-overview.png)

### Selezionare un segmento

Il dashboard seleziona automaticamente un segmento da visualizzare, ma puoi modificare il segmento visualizzato utilizzando il menu a discesa. Per scegliere un segmento diverso, seleziona il menu a discesa accanto al nome del segmento, quindi seleziona il segmento da visualizzare.

>[!NOTE]
>
>Il menu a discesa mostra tutti i segmenti creati finora dalla tua organizzazione. Questo può significare che dovrai scorrere per visualizzare l’elenco completo dei segmenti disponibili.

![](../images/segments/change-segment.png)

### Widget e metriche

Il dashboard dei segmenti è composto da widget, che sono metriche di sola lettura che forniscono informazioni importanti sul segmento selezionato. La data e l&#39;ora &quot;ultimo aggiornamento&quot; del widget mostrano quando è stata effettuata l&#39;ultima istantanea dei dati.

![](../images/segments/widget-timestamp.png)

## Widget disponibili

Experience Platform fornisce più widget che puoi utilizzare per visualizzare diverse metriche correlate al tuo segmento. Seleziona il nome di un widget qui sotto per ulteriori informazioni:

* [[!UICONTROL Segment size]](#segment-size)
* [[!UICONTROL Profiles added over time]](#profiles-added-over-time)
* [[!UICONTROL Profiles by namespace]](#profiles-by-namespace)

### [!UICONTROL Segment size] {#segment-size}

Il widget **[!UICONTROL Segment size]** visualizza il numero totale di profili uniti all’interno del segmento selezionato al momento dell’acquisizione dello snapshot. Questo numero è il risultato dell’applicazione dei criteri di unione dei segmenti ai dati del profilo per unire i frammenti di profilo in modo da formare un unico profilo per ogni individuo nel segmento.

Per ulteriori informazioni sui frammenti e i profili uniti, inizia leggendo la [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

![](../images/segments/segment-size.png)

### [!UICONTROL Profiles added over time] {#profiles-added-over-time}

Il widget **[!UICONTROL Profiles added over time]** fornisce informazioni sul numero totale di profili nel segmento acquisiti durante lo snapshot giornaliero, per gli ultimi 30 giorni. Questo widget mostra come la dimensione del segmento potrebbe essere cambiata in un periodo di 30 giorni, in quanto i nuovi profili si qualificano per o escono dal segmento.

Per ulteriori informazioni sulla valutazione dei segmenti e su come i profili si qualificano e se escono dai segmenti, consulta la [documentazione Servizio di segmentazione](../../segmentation/home.md).

![](../images/segments/profiles-added-over-time.png)

### [!UICONTROL Profiles by namespace] {#profiles-by-namespace}

Il widget **[!UICONTROL Profiles by namespace]** visualizza la suddivisione dei namespace in tutti i profili uniti nel segmento selezionato. Il numero totale di profili per namespace di identità ([!UICONTROL ID namespace] nel widget) può essere superiore al numero totale di profili nel segmento, perché a un profilo potrebbero essere associati più namespace. In altre parole, l’aggiunta dei valori mostrati per ogni namespace può avere un totale superiore ai profili totali nel segmento, perché se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente possono essere associati più namespace.

Per ulteriori informazioni sugli spazi dei nomi delle identità, visita la [documentazione del servizio Adobe Experience Platform Identity](../../identity-service/home.md).

![](../images/segments/profiles-by-namespace.png)

## Passaggi successivi

Seguendo questo documento, ora dovresti essere in grado di individuare il dashboard dei segmenti e selezionare un segmento da visualizzare. È inoltre necessario comprendere le metriche visualizzate nei widget disponibili. Per ulteriori informazioni sull’utilizzo dei segmenti nell’interfaccia utente di Experience Platform, consulta la [Guida all’interfaccia utente del servizio di segmentazione](../../segmentation/ui/overview.md) .
