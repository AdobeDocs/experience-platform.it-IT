---
keywords: Experience Platform ;profilo;profilo cliente in tempo reale;interfaccia utente;interfaccia utente;personalizzazione;dashboard profilo;dashboard
title: Dashboard profili
description: Adobe Experience Platform fornisce una dashboard attraverso la quale puoi visualizzare informazioni importanti sui dati del profilo cliente in tempo reale della tua organizzazione.
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 2f2459c1c88c97a3ab322b08ee178463fbb4a592
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 1%

---


# (Beta) [!UICONTROL Profiles] dashboard

>[!IMPORTANT]
>
>La funzionalità del dashboard descritta in questo documento è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

L&#39;interfaccia utente di Adobe Experience Platform (interfaccia utente) fornisce un dashboard attraverso il quale è possibile visualizzare informazioni importanti sui dati [!DNL Real-time Customer Profile], così come acquisiti durante uno snapshot giornaliero. Questa guida descrive come accedere e utilizzare il dashboard [!UICONTROL Profiles] nell&#39;interfaccia utente e fornisce informazioni sulle metriche visualizzate nel dashboard.

Per una panoramica di tutte le funzioni di profilo nell&#39;interfaccia utente del Experience Platform , visita la [Guida all&#39;interfaccia utente del profilo cliente in tempo reale](../../profile/ui/user-guide.md).

## Dati dashboard profilo

Il dashboard di [!UICONTROL Profiles] visualizza un&#39;istantanea dei dati attributo (record) dell&#39;organizzazione all&#39;interno dell&#39;archivio dei profili in  Experience Platform. Lo snapshot non include dati di eventi (serie temporali).

I dati attributo nello snapshot mostrano esattamente come appaiono nel momento specifico in cui è stata scattata l&#39;istantanea. In altre parole, l&#39;istantanea non è un&#39;approssimazione o un esempio dei dati e il dashboard Profilo non viene aggiornato in tempo reale.

>[!NOTE]
>
>Eventuali modifiche o aggiornamenti apportati ai dati dopo l&#39;acquisizione dell&#39;istantanea non verranno visualizzati nel dashboard fino all&#39;acquisizione dell&#39;istantanea successiva.

## Esplorazione del dashboard [!UICONTROL Profiles]

Per passare al dashboard [!UICONTROL Profiles] nell&#39;interfaccia utente della piattaforma, seleziona **[!UICONTROL Profiles]** nella barra a sinistra, quindi seleziona la scheda **[!UICONTROL Overview]** per visualizzare il dashboard.

![](../images/profiles/dashboard-overview.png)

### Selezione dei criteri di unione

Le metriche visualizzate nel dashboard [!UICONTROL Profiles] si basano su criteri di unione applicati ai dati del profilo cliente in tempo reale. Quando i dati vengono uniti da più origini, è possibile che i dati contengano valori in conflitto (ad esempio, un set di dati può elencare un cliente come &quot;singolo&quot;, mentre un altro set di dati può elencare il cliente come &quot;sposato&quot;) ed è compito del criterio di unione determinare quali dati dare priorità e visualizzare come parte del profilo.

Il dashboard seleziona automaticamente un criterio di unione da visualizzare, ma puoi modificare il criterio di unione selezionato utilizzando il menu a discesa. Per scegliere un altro criterio di unione, selezionare il menu a discesa accanto al nome del criterio di unione, quindi selezionare il criterio di unione che si desidera visualizzare.

>[!NOTE]
>
>Nel menu a discesa sono visualizzati solo i criteri di unione relativi alla classe di profilo individuale XDM. Tuttavia, se l&#39;organizzazione ha creato più criteri di unione, potrebbe essere necessario scorrere per visualizzare l&#39;elenco completo dei criteri di unione disponibili.

Per ulteriori informazioni sui criteri di unione, tra cui come creare, modificare e dichiarare un criterio di unione predefinito per l&#39;organizzazione, consultare la [guida dell&#39;interfaccia utente dei criteri di unione](../../profile/ui/merge-policies.md).

![](../images/profiles/select-merge-policy.png)

### Widget e metriche

Il dashboard è composto da widget, che sono metriche di sola lettura che forniscono informazioni importanti sui dati del profilo. La data e l’ora dell’ultimo aggiornamento di un widget mostrano quando è stata scattata l’ultima istantanea dei dati.

![](../images/profiles/dashboard-timestamp.png)

## widget disponibili

 Experience Platform fornisce più widget che potete utilizzare per visualizzare diverse metriche correlate ai dati del profilo. Seleziona il nome di un widget qui sotto per saperne di più:

* [[!UICONTROL Audience size]](#audience-size)
* [[!UICONTROL Profiles added]](#profiles-added)
* [[!UICONTROL Profiles added over time]](#profiles-added-over-time)
* [[!UICONTROL Profiles by namespace]](#profiles-by-namespace)
* [[!UICONTROL Namespace overlap]](#namespace-overlap)

### [!UICONTROL Audience size] {#audience-size}

Il widget **[!UICONTROL Audience size]** visualizza il numero totale di profili uniti nell&#39;archivio dati Profilo al momento dell&#39;acquisizione dello snapshot. Questo numero è il risultato dell&#39;applicazione del criterio di unione selezionato ai dati del profilo per unire insieme i frammenti del profilo e creare un unico profilo per ogni singolo utente.

Per ulteriori informazioni sui frammenti e i profili uniti, consultare la sezione *Frammenti di profilo rispetto ai profili uniti* della [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

>[!NOTE]
>
>Il criterio di unione utilizzato per calcolare questa metrica non è lo stesso del criterio di unione generato dal sistema utilizzato per calcolare [!UICONTROL Addressable audiences] nel dashboard [!UICONTROL License usage], pertanto è improbabile che il numero di audience nei dashboard [!UICONTROL Profiles] e [!UICONTROL License usage] sia esattamente lo stesso.

![](../images/profiles/audience-size.png)

### [!UICONTROL Profiles added] {#profiles-added}

Il widget **[!UICONTROL Profiles added]** visualizza il numero totale di profili uniti che sono stati aggiunti all&#39;archivio dati Profilo dopo l&#39;ultima istantanea. Questo numero è il risultato dell&#39;applicazione del criterio di unione selezionato ai dati del profilo per unire insieme i frammenti del profilo e creare un unico profilo per ogni singolo utente.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Profiles added over time] {#profiles-added-over-time}

Il widget **[!UICONTROL Profiles added over time]** visualizza il numero totale di profili uniti che sono stati aggiunti giornalmente all&#39;archivio dati Profilo negli ultimi 30 giorni. Questo numero viene aggiornato ogni giorno in cui viene scattata l&#39;istantanea, quindi se si desidera acquisire i profili in Piattaforma, il numero di profili non verrà riportato fino a quando non verrà scattata l&#39;istantanea successiva.

Il numero di profili aggiunti è il risultato dell&#39;applicazione del criterio di unione selezionato ai dati del profilo per unire insieme i frammenti del profilo e creare un unico profilo per ciascun utente.

![](../images/profiles/profiles-added-over-time.png)

### [!UICONTROL Profiles by namespace] {#profiles-by-namespace}

Il widget **[!UICONTROL Profiles by namespace]** visualizza la suddivisione degli spazi dei nomi identità in tutti i profili uniti nel tuo archivio profili. Il numero totale di profili per [!UICONTROL ID namespace] (in altre parole, aggiungendo insieme i valori mostrati per ogni spazio dei nomi) potrebbe essere superiore al numero totale di profili unione, perché a un profilo potrebbero essere associati più spazi dei nomi. Ad esempio, se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente saranno associati più spazi dei nomi.

Per ulteriori informazioni sugli spazi dei nomi di identità, consultare la [documentazione del servizio Adobe Experience Platform Identity](../../identity-service/home.md).

![](../images/profiles/profiles-by-namespace.png)

### [!UICONTROL Namespace overlap] {#namespace-overlap}

Il widget **[!UICONTROL Namespace overlap]** visualizza un diagramma di Venn, o diagramma di set, che mostra la sovrapposizione di profili nell&#39;archivio profili contenente più spazi dei nomi di identità.

Dopo aver utilizzato i menu a discesa del widget per selezionare gli spazi dei nomi di identità da confrontare, i cerchi visualizzano la dimensione relativa di ciascuno spazio dei nomi, con il numero di profili contenenti entrambi gli spazi dei nomi rappresentato dalla dimensione della sovrapposizione tra i cerchi.

Se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente saranno associati più spazi dei nomi, pertanto è probabile che la tua organizzazione abbia più profili contenenti frammenti da più di uno spazio dei nomi identità.

Per ulteriori informazioni sugli spazi dei nomi di identità, consultare la [documentazione del servizio Adobe Experience Platform Identity](../../identity-service/home.md).

![](../images/profiles/namespace-overlap.png)

## Passaggi successivi

Seguendo questo documento è ora possibile individuare il dashboard Profili e comprendere le metriche visualizzate nei widget disponibili. Per ulteriori informazioni sull&#39;utilizzo di dati [!DNL Profile] nell&#39;interfaccia utente del Experience Platform , fare riferimento alla [Guida all&#39;interfaccia utente del profilo cliente in tempo reale](../../profile/ui/user-guide.md).