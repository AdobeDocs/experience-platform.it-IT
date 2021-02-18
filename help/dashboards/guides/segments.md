---
keywords: ' Experience Platform;profilo;segmento;segmenti;segmentazione;interfaccia utente;interfaccia utente;personalizzazione;dashboard del segmento;dashboard'
title: Pannello Segmenti
description: 'Adobe Experience Platform fornisce una dashboard attraverso la quale puoi visualizzare informazioni importanti sui segmenti creati dalla tua organizzazione. '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 2f2459c1c88c97a3ab322b08ee178463fbb4a592
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 1%

---


# (Beta) Pannello segmenti {#segment-dashboard}

>[!IMPORTANT]
>
>La funzionalità del dashboard descritta in questo documento è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

L’interfaccia utente di Adobe Experience Platform (interfaccia utente) fornisce un dashboard attraverso il quale è possibile visualizzare informazioni importanti sui segmenti, come acquisito durante un’istantanea giornaliera. Questa guida descrive come accedere e utilizzare il dashboard dei segmenti nell’interfaccia utente e fornisce ulteriori informazioni sulle visualizzazioni visualizzate nel dashboard.

Per una panoramica di tutte le funzioni del servizio di segmentazione Adobe Experience Platform nell&#39;interfaccia utente della piattaforma, visitare la [Guida dell&#39;interfaccia utente del servizio di segmentazione](../../segmentation/ui/overview.md).

## Segmentazione dei dati del dashboard

Il dashboard del segmento visualizza un&#39;istantanea dei dati attributo (record) di cui dispone l&#39;organizzazione all&#39;interno dell&#39;archivio dei profili in  Experience Platform. Lo snapshot non include dati di eventi (serie temporali).

I dati attributo nello snapshot mostrano esattamente come appaiono nel momento specifico in cui è stata scattata l&#39;istantanea. In altre parole, l&#39;istantanea non è un&#39;approssimazione o un esempio dei dati e il dashboard del segmento non viene aggiornato in tempo reale.

>[!NOTE]
>
>Eventuali modifiche o aggiornamenti apportati ai dati dopo l&#39;acquisizione dell&#39;istantanea non verranno visualizzati nel dashboard fino all&#39;acquisizione dell&#39;istantanea successiva.

## Esplorazione del dashboard dei segmenti

Per passare al dashboard dei segmenti nell&#39;interfaccia utente della piattaforma, seleziona **[!UICONTROL Segments]** nella barra a sinistra, quindi seleziona la scheda **[!UICONTROL Overview]** per visualizzare il dashboard.

![](../images/segments/dashboard-overview.png)

### Selezionare un segmento

Il dashboard seleziona automaticamente un segmento da visualizzare, ma puoi modificare il segmento visualizzato utilizzando il menu a discesa. Per scegliere un segmento diverso, selezionate il menu a discesa accanto al nome del segmento, quindi selezionate il segmento da visualizzare.

>[!NOTE]
>
>Il menu a discesa mostra tutti i segmenti creati finora dalla tua organizzazione. Questo può significare che dovrete scorrere per visualizzare l&#39;elenco completo dei segmenti disponibili.

![](../images/segments/change-segment.png)

### Widget e metriche

Il dashboard dei segmenti è composto da widget, che sono metriche di sola lettura e forniscono informazioni importanti sul segmento selezionato. La data e l’ora dell’&quot;ultimo aggiornamento&quot; del widget mostrano quando è stata scattata l’ultima istantanea dei dati.

![](../images/segments/widget-timestamp.png)

## widget disponibili

 Experience Platform fornisce più widget che potete utilizzare per visualizzare diverse metriche correlate al segmento. Seleziona il nome di un widget qui sotto per saperne di più:

* [[!UICONTROL Segment size]](#segment-size)
* [[!UICONTROL Profiles added over time]](#profiles-added-over-time)
* [[!UICONTROL Profiles by namespace]](#profiles-by-namespace)

### [!UICONTROL Segment size] {#segment-size}

Il widget **[!UICONTROL Segment size]** visualizza il numero totale di profili uniti all&#39;interno del segmento selezionato al momento dell&#39;acquisizione dello snapshot. Questo numero è il risultato dell&#39;applicazione del criterio di unione dei segmenti ai dati del profilo per unire insieme i frammenti del profilo e creare un unico profilo per ogni individuo del segmento.

Per ulteriori informazioni sui frammenti e i profili uniti, consultare la [Panoramica sul profilo cliente in tempo reale](../../profile/home.md).

![](../images/segments/segment-size.png)

### [!UICONTROL Profiles added over time] {#profiles-added-over-time}

Il widget **[!UICONTROL Profiles added over time]** fornisce informazioni sul numero totale di profili nel segmento come acquisiti durante lo snapshot giornaliero, per gli ultimi 30 giorni. Questo widget mostra come la dimensione del segmento potrebbe essere cambiata in un periodo di 30 giorni, in quanto i nuovi profili sono idonei per il segmento o sono usciti dal segmento.

Per ulteriori informazioni sulla valutazione dei segmenti e sulle modalità di qualifica e uscita dei profili dai segmenti, consultare la [documentazione del servizio di segmentazione](../../segmentation/home.md).

![](../images/segments/profiles-added-over-time.png)

### [!UICONTROL Profiles by namespace] {#profiles-by-namespace}

Il widget **[!UICONTROL Profiles by namespace]** visualizza la suddivisione degli spazi dei nomi in tutti i profili uniti nel segmento selezionato. Il numero totale di profili per namespace di identità ([!UICONTROL ID namespace] nel widget) può essere superiore al numero totale di profili nel segmento, perché a un profilo potrebbero essere associati più spazi dei nomi. In altre parole, l&#39;aggiunta insieme dei valori mostrati per ogni spazio nomi può superare il totale dei profili nel segmento, perché se un cliente interagisce con il tuo marchio su più di un canale, più spazi dei nomi possono essere associati a quel singolo cliente.

Per ulteriori informazioni sugli spazi dei nomi di identità, consultare la [documentazione del servizio Adobe Experience Platform Identity](../../identity-service/home.md).

![](../images/segments/profiles-by-namespace.png)

## Passaggi successivi

Seguendo questo documento, ora dovresti essere in grado di individuare il dashboard dei segmenti e selezionare un segmento da visualizzare. È inoltre necessario comprendere le metriche visualizzate nei widget disponibili. Per ulteriori informazioni sull&#39;utilizzo dei segmenti nell&#39;interfaccia utente del Experience Platform , fare riferimento alla [Guida all&#39;interfaccia utente del servizio di segmentazione](../../segmentation/ui/overview.md).