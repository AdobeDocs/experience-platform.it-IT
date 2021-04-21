---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;interfaccia utente;interfaccia utente;personalizzazione;dashboard profilo;dashboard dashboard
title: Dashboard dei profili
description: Adobe Experience Platform fornisce un dashboard tramite il quale è possibile visualizzare informazioni importanti sui dati Profilo cliente in tempo reale della tua organizzazione.
topic-legacy: guide
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 1%

---

# (Beta) [!UICONTROL Profiles] dashboard

>[!IMPORTANT]
>
>La funzionalità del dashboard descritta in questo documento è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

L’interfaccia utente di Adobe Experience Platform fornisce una dashboard attraverso la quale è possibile visualizzare informazioni importanti sui dati [!DNL Real-time Customer Profile] acquisiti durante un’istantanea giornaliera. Questa guida illustra come accedere e lavorare con il dashboard [!UICONTROL Profiles] nell’interfaccia utente e fornisce informazioni sulle metriche visualizzate nel dashboard.

Per una panoramica di tutte le funzioni Profilo nell’interfaccia utente di Experience Platform, visita la [Guida all’interfaccia utente del profilo cliente in tempo reale](../../profile/ui/user-guide.md).

## Dati del dashboard del profilo

Il dashboard [!UICONTROL Profiles] visualizza un&#39;istantanea dei dati dell&#39;attributo (record) della tua organizzazione all&#39;interno dell&#39;archivio profili in Experience Platform. Lo snapshot non include dati di eventi (serie temporali).

I dati attributo nello snapshot mostrano esattamente come vengono visualizzati nel momento specifico in cui è stata acquisita l&#39;istantanea. In altre parole, lo snapshot non è un&#39;approssimazione o un esempio dei dati e il dashboard Profilo non viene aggiornato in tempo reale.

>[!NOTE]
>
>Eventuali modifiche o aggiornamenti apportati ai dati dall&#39;acquisizione dello snapshot non verranno visualizzati nel dashboard fino all&#39;acquisizione dello snapshot successivo.

## Esplorazione del dashboard [!UICONTROL Profiles]

Per passare al dashboard [!UICONTROL Profiles] nell’interfaccia utente di Platform, seleziona **[!UICONTROL Profiles]** nella barra a sinistra, quindi seleziona la scheda **[!UICONTROL Overview]** per visualizzare il dashboard.

![](../images/profiles/dashboard-overview.png)

### Selezione dei criteri di unione

Le metriche visualizzate nel dashboard [!UICONTROL Profiles] si basano sui criteri di unione applicati ai dati del profilo cliente in tempo reale. Quando i dati vengono riuniti da più origini, è possibile che contengano valori in conflitto (ad esempio, un set di dati può elencare un cliente come &quot;singolo&quot;, mentre un altro set di dati può elencare il cliente come &quot;sposato&quot;) ed è compito del criterio di unione determinare quali dati dare priorità e visualizzare come parte del profilo.

Il dashboard selezionerà automaticamente un criterio di unione da visualizzare, ma sarà possibile modificare il criterio di unione selezionato utilizzando il menu a discesa. Per scegliere un criterio di unione diverso, selezionare il menu a discesa accanto al nome del criterio di unione, quindi selezionare il criterio di unione che si desidera visualizzare.

>[!NOTE]
>
>Il menu a discesa mostra solo i criteri di unione relativi alla classe di profilo individuale XDM. Tuttavia, se l&#39;organizzazione ha creato più criteri di unione, potrebbe essere necessario scorrere per visualizzare l&#39;elenco completo dei criteri di unione disponibili.

Per ulteriori informazioni sui criteri di unione, tra cui come creare, modificare e dichiarare un criterio di unione predefinito per l&#39;organizzazione, visitare la [guida all&#39;interfaccia utente dei criteri di unione](../../profile/ui/merge-policies.md).

![](../images/profiles/select-merge-policy.png)

### Widget e metriche

Il dashboard è composto da widget, che sono metriche di sola lettura che forniscono informazioni importanti sui dati del profilo. La data e l’ora &quot;ultimo aggiornamento&quot; di un widget mostrano quando è stata acquisita l’ultima istantanea dei dati.

![](../images/profiles/dashboard-timestamp.png)

## Widget disponibili

Experience Platform fornisce più widget che puoi utilizzare per visualizzare diverse metriche correlate ai dati del profilo. Seleziona il nome di un widget qui sotto per ulteriori informazioni:

* [[!UICONTROL Audience size]](#audience-size)
* [[!UICONTROL Profiles added]](#profiles-added)
* [[!UICONTROL Profiles added over time]](#profiles-added-over-time)
* [[!UICONTROL Profiles by namespace]](#profiles-by-namespace)
* [[!UICONTROL Namespace overlap]](#namespace-overlap)

### [!UICONTROL Audience size] {#audience-size}

Il widget **[!UICONTROL Audience size]** visualizza il numero totale di profili uniti all’interno dell’archivio dati del profilo al momento dell’acquisizione dello snapshot. Questo numero è il risultato dell’applicazione del criterio di unione selezionato ai dati del profilo per unire i frammenti di profilo in modo da formare un unico profilo per ogni singolo utente.

Per ulteriori informazioni sui frammenti e i profili uniti, inizia leggendo la sezione *Profili di profilo e profili uniti* della [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

>[!NOTE]
>
>Il criterio di unione utilizzato per calcolare questa metrica non è lo stesso del criterio di unione generato dal sistema utilizzato per calcolare [!UICONTROL Addressable audiences] nel dashboard [!UICONTROL License usage], pertanto è improbabile che il conteggio del pubblico nei dashboard [!UICONTROL Profiles] e [!UICONTROL License usage] sia esattamente lo stesso.

![](../images/profiles/audience-size.png)

### [!UICONTROL Profiles added] {#profiles-added}

Il widget **[!UICONTROL Profiles added]** visualizza il numero totale di profili uniti che sono stati aggiunti all’archivio dati del profilo dopo l’ultima istantanea. Questo numero è il risultato dell’applicazione del criterio di unione selezionato ai dati del profilo per unire i frammenti di profilo in modo da formare un unico profilo per ogni singolo utente.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Profiles added over time] {#profiles-added-over-time}

Il widget **[!UICONTROL Profiles added over time]** visualizza il numero totale di profili uniti che sono stati aggiunti giornalmente all’archivio dati del profilo negli ultimi 30 giorni. Questo numero viene aggiornato ogni giorno in cui viene acquisita l’istantanea, pertanto se desideri acquisire profili in Platform, il numero di profili non verrà riportato fino a quando non viene acquisita l’istantanea successiva.

Il conteggio dei profili aggiunti è il risultato dell’applicazione dei criteri di unione selezionati ai dati del profilo per unire i frammenti di profilo in modo da formare un unico profilo per ogni singolo utente.

![](../images/profiles/profiles-added-over-time.png)

### [!UICONTROL Profiles by namespace] {#profiles-by-namespace}

Il widget **[!UICONTROL Profiles by namespace]** visualizza la suddivisione dei namespace di identità in tutti i profili uniti nel tuo archivio profili. Il numero totale di profili per [!UICONTROL ID namespace] (in altre parole, aggiungendo insieme i valori mostrati per ogni spazio dei nomi) può essere maggiore del numero totale di profili di unione, perché a un profilo potrebbero essere associati più spazi dei nomi. Ad esempio, se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente saranno associati più namespace.

Per ulteriori informazioni sugli spazi dei nomi delle identità, visita la [documentazione del servizio Adobe Experience Platform Identity](../../identity-service/home.md).

![](../images/profiles/profiles-by-namespace.png)

### [!UICONTROL Namespace overlap] {#namespace-overlap}

Il widget **[!UICONTROL Namespace overlap]** visualizza un diagramma di Venn, o diagramma di set, che mostra la sovrapposizione di profili nell’archivio profili contenenti più spazi dei nomi di identità.

Dopo aver utilizzato i menu a discesa del widget per selezionare i namespace di identità da confrontare, i cerchi visualizzano la dimensione relativa di ogni namespace, con il numero di profili contenenti entrambi i namespace rappresentato dalla dimensione della sovrapposizione tra i cerchi.

Se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente saranno associati più namespace, pertanto è probabile che la tua organizzazione disponga di più profili contenenti frammenti da più di un namespace di identità.

Per ulteriori informazioni sugli spazi dei nomi delle identità, visita la [documentazione del servizio Adobe Experience Platform Identity](../../identity-service/home.md).

![](../images/profiles/namespace-overlap.png)

## Passaggi successivi

Seguendo questo documento, ora dovresti essere in grado di individuare il dashboard Profiles e comprendere le metriche visualizzate nei widget disponibili. Per ulteriori informazioni sull’utilizzo dei dati [!DNL Profile] nell’interfaccia utente di Experience Platform, consulta la [Guida all’interfaccia utente del profilo cliente in tempo reale](../../profile/ui/user-guide.md) .
