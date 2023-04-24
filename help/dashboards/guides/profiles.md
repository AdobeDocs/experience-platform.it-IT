---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;interfaccia utente;interfaccia utente;personalizzazione;dashboard profilo;dashboard dashboard
title: Guida al dashboard dei profili
description: Adobe Experience Platform fornisce un dashboard tramite il quale è possibile visualizzare informazioni importanti sui dati del profilo cliente in tempo reale della tua organizzazione.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: a28c1c00fd0b33af3b797ecf2b4d45154dedc823
workflow-type: tm+mt
source-wordcount: '3385'
ht-degree: 10%

---

# [!UICONTROL Profili] dashboard

L’interfaccia utente di Adobe Experience Platform fornisce una dashboard attraverso la quale puoi visualizzare informazioni importanti sul tuo [!DNL Real-Time Customer Profile] come acquisiti durante un&#39;istantanea giornaliera. Questa guida illustra come accedere e lavorare con il dashboard Profili nell’interfaccia utente e fornisce informazioni sulle metriche visualizzate nel dashboard.

Per una panoramica di tutte le funzioni Profilo nell’interfaccia utente di Experience Platform, consulta la sezione [Guida all’interfaccia utente del profilo cliente in tempo reale](../../profile/ui/user-guide.md).

## Dati del dashboard del profilo

Nel dashboard Profili viene visualizzata un’istantanea dei dati dell’attributo (record) dell’organizzazione all’interno dell’archivio profili in Experience Platform. Lo snapshot non include dati di eventi (serie temporali).

I dati attributo nello snapshot mostrano esattamente come vengono visualizzati nel momento specifico in cui è stata acquisita l&#39;istantanea. In altre parole, lo snapshot non è un&#39;approssimazione o un esempio dei dati e il dashboard Profilo non viene aggiornato in tempo reale.

>[!NOTE]
>
>Eventuali modifiche o aggiornamenti apportati ai dati dall&#39;acquisizione dello snapshot non verranno visualizzati nel dashboard fino all&#39;acquisizione dello snapshot successivo.

## Esplorazione del dashboard Profili

Per passare al dashboard Profili nell’interfaccia utente di Platform, seleziona **[!UICONTROL Profili]** nella barra a sinistra, seleziona la **[!UICONTROL Panoramica]** per visualizzare il dashboard.

>[!NOTE]
>
>Se l’organizzazione è nuova di Platform e non dispone ancora di set di dati di profilo attivi o di criteri di unione creati, il dashboard Profili non è visibile. Invece, [!UICONTROL Panoramica] visualizza collegamenti e documentazione per iniziare a usare Profilo cliente in tempo reale.

![La dashboard Profili di Experience Platform con Profili e Panoramica evidenziata.](../images/profiles/dashboard-overview.png)

### Modifica del dashboard Profili

Puoi modificare l’aspetto del dashboard Profili selezionando **[!UICONTROL Modifica dashboard]**. Questo consente di spostare, aggiungere e rimuovere i widget dal dashboard e di accedere al **[!UICONTROL Libreria widget]** per esplorare i widget disponibili e creare widget personalizzati per la tua organizzazione.

Fai riferimento alla [modifica delle dashboard](../customize/modify.md) e [Panoramica della libreria Widget](../customize/widget-library.md) documentazione per ulteriori informazioni.

### Aggiungi widget {#add-widget}

Seleziona **[!UICONTROL Aggiungi widget]** per passare alla libreria dei widget e visualizzare un elenco dei widget disponibili da aggiungere al dashboard.

![Panoramica del dashboard Profili con il widget di aggiunta evidenziato.](../images/profiles/profiles-overview-add-widget.png)

Dalla libreria dei widget è possibile sfogliare la selezione di widget per segmenti standard e personalizzati.Per informazioni su come aggiungere i widget, consulta la documentazione della libreria dei widget su come [aggiungere un widget](../customize/widget-library.md#add-widgets).

<!-- ## (Beta) Profile efficacy insights {#profile-efficacy-insights}

>[!IMPORTANT]
>
>The profile efficacy insight functionality is currently in beta and are not available to all users. The documentation and the functionality are subject to change.

The [!UICONTROL Efficacy] tab provides metrics on the quality and completeness of your profile data through the use of profile efficacy widgets. These widgets illustrate at a glance the composition of your profiles, trends in completeness over time, and assessments on the quality of your profile data.

![The profile efficacy dashboard.](../images/profiles/attributes-quality-assessment.png)

See the [profile efficacy widgets section](#profile-efficacy-widgets) for more information on the widgets currently available.

The layout of this dashboard is also customizable by selecting [**[!UICONTROL Modify dashboard]**](../customize/modify.md) from the [!UICONTROL Overview] tab. -->

## Sfoglia profili {#browse-profiles}

La [!UICONTROL Sfoglia] consente di cercare e visualizzare i profili di sola lettura acquisiti nell’organizzazione. Da qui puoi vedere informazioni importanti appartenenti al profilo relative alle loro preferenze, eventi passati, interazioni e segmenti

Per ulteriori informazioni sulle funzionalità di visualizzazione del profilo fornite nell’interfaccia utente di Platform, consulta la documentazione su [navigazione dei profili in Adobe Real-time Customer Data Platform](../../rtcdp/profile/profile-browse.md).

## Unisci criteri {#merge-policies}

Le metriche visualizzate nel dashboard Profili si basano sui criteri di unione applicati ai dati del profilo cliente in tempo reale. Quando i dati vengono riuniti da più sorgenti per creare il profilo del cliente, i dati possono contenere valori in conflitto. Ad esempio, un set di dati può elencare un cliente come &quot;singolo&quot;, mentre un altro può elencare il cliente come &quot;sposato&quot;. È compito del criterio di unione determinare quali dati assegnare priorità e visualizzare come parte del profilo.

Per ulteriori informazioni sui criteri di unione, tra cui come creare, modificare e dichiarare un criterio di unione predefinito per l&#39;organizzazione, fare riferimento alla sezione [panoramica dei criteri di unione](../../profile/merge-policies/overview.md).

Il dashboard selezionerà automaticamente un criterio di unione da utilizzare. I criteri di unione applicati possono essere modificati utilizzando il menu a discesa accanto al nome del criterio di unione.

>[!NOTE]
>
>Il menu a discesa mostra solo i criteri di unione che utilizzano `_xdm.context.profile` schema. Tuttavia, se l&#39;organizzazione ha creato più criteri di unione, può essere necessario scorrere per visualizzare l&#39;elenco completo dei criteri di unione disponibili.

![La scheda Panoramica dei profili con il menu a discesa dei criteri di unione evidenziato.](../images/profiles/select-merge-policy.png)

## Schemi dell’Unione

La [!UICONTROL Schema dell&#39;unione] dashboard visualizza lo schema di unione per una specifica classe XDM. Selezionando la **[!UICONTROL Classe]** a discesa, puoi visualizzare gli schemi di unione per diverse classi XDM.

Gli schemi di unione sono composti da più schemi che condividono la stessa classe e sono stati abilitati per Profilo. Consentono di visualizzare in un’unica visualizzazione una fusione di ogni campo contenuto in ogni schema che condivide la stessa classe.

Per ulteriori informazioni, consulta la guida all’interfaccia utente per lo schema dell’unione . [visualizzazione degli schemi di unione nell’interfaccia utente di Platform](../../profile/ui/union-schema.md#view-union-schemas).

## Widget e metriche

Il dashboard è composto da widget, che sono metriche di sola lettura che forniscono informazioni importanti sui dati del profilo.

La data e l’ora dell’istantanea più recente vengono visualizzate nella parte superiore della [!UICONTROL Panoramica] accanto al menu a discesa dei criteri di unione . Tutti i dati dei widget sono accurati a partire da quella data e ora. La marca temporale dello snapshot è fornita in UTC; non si trova nel fuso orario del singolo utente o organizzazione.

![La scheda Panoramica del dashboard Profili con la marca temporale più recente evidenziata.](../images/profiles/snapshot-timestamp.png)

## Widget standard {#standard-widgets}

Adobe fornisce diversi widget standard che puoi utilizzare per visualizzare diverse metriche correlate ai dati del profilo. Puoi anche creare widget personalizzati da condividere con la tua organizzazione utilizzando [!UICONTROL Libreria widget]. Per ulteriori informazioni sulla creazione di widget personalizzati, si prega di iniziare leggendo [Panoramica della libreria Widget](../customize/widget-library.md).

Per ulteriori informazioni su ciascuno dei widget standard disponibili, seleziona il nome di un widget dal seguente elenco:

* [[!UICONTROL Conteggio dei profili]](#profile-count)
* [[!UICONTROL Tendenza al conteggio dei profili]](#profile-count-trend)
* [[!UICONTROL Modifica del conteggio dei profili]](#profile-count-change)
* [[!UICONTROL Tendenza di modifica del conteggio dei profili]](#profiles-count-change-trend)
* [[!UICONTROL Tendenza di modifica del conteggio dei profili in base all&#39;identità]](#profiles-count-change-trend-by-identity)
* [[!UICONTROL Profili per identità]](#profiles-by-identity)
* [[!UICONTROL Sovrapposizione di identità]](#identity-overlap)
* [[!UICONTROL Profili a identità singola]](#single-identity-profiles)
* [[!UICONTROL Singoli profili di identità per identità]](#single-identity-profiles-by-identity)
* [[!UICONTROL Profili non segmentati]](#unsegmented-profiles)
* [[!UICONTROL I profili non segmentati cambiano tendenza]](#unsegmented-profiles-change-trend)
* [[!UICONTROL Profili non segmentati per identità]](#unsegmented-profiles-by-identity)
* [[!UICONTROL Tipi di pubblico]](#audiences)
* [[!UICONTROL Tipi di pubblico mappati sullo stato di destinazione]](#audiences-mapped-to-destination-status)
* [[!UICONTROL Dimensione del pubblico]](#audiences-size)
* [[!UICONTROL Sovrapposizione del pubblico per criterio di unione]](#audience-overlap-by-merge-policy)
* [[!UICONTROL Rapporto di sovrapposizione del pubblico]](#audience-overlap-report)

### [!UICONTROL Conteggio dei profili] {#profile-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilecount"
>title="Conteggio dei profili"
>abstract="Questo widget visualizza il numero totale di profili uniti all’interno dello store di profili al momento dell’acquisizione dello snapshot. Il numero dipende dal criterio di unione selezionato applicato ai dati dei profili."

La **[!UICONTROL Numero di profili]** nel widget viene visualizzato il numero totale di profili uniti all’interno dell’archivio profili al momento dell’acquisizione dello snapshot. Questo numero è il risultato dell’applicazione del criterio di unione selezionato ai dati del profilo per unire i frammenti di profilo in modo da formare un unico profilo per ogni singolo utente.

Consulta la sezione [sezione sui criteri di unione in precedenza in questo documento](#merge-policies) per saperne di più.

>[!NOTE]
>
>La [!UICONTROL Numero di profili] widget può mostrare un numero diverso dal conteggio del profilo mostrato sul [!UICONTROL Sfoglia] nella scheda [!UICONTROL Profili] per diversi motivi. Il motivo più comune è che [!UICONTROL Sfoglia] fa riferimento al numero totale di profili uniti in base ai criteri di unione predefiniti della tua organizzazione, mentre la [!UICONTROL Numero di profili] Il widget fa riferimento al numero totale di profili uniti in base al criterio di unione selezionato per la visualizzazione nel dashboard.
>
>Un altro motivo comune è dovuto alle differenze tra il momento in cui viene acquisita l’istantanea del dashboard e il momento in cui il processo di esempio viene eseguito per la [!UICONTROL Sfoglia] scheda . Puoi vedere quando [!UICONTROL Numero di profili] l&#39;ultimo aggiornamento del widget è stato effettuato osservando la marca temporale nel widget. Per ulteriori informazioni sull’attivazione del processo di esempio nel [!UICONTROL Sfoglia] scheda , vedi [sezione conteggio profilo nella guida all’interfaccia utente del profilo cliente in tempo reale](https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=en#profile-count).

![Il dashboard Profili Experience Platform con il widget Conteggio profili evidenziato.](../images/profiles/profile-count.png)

### [!UICONTROL Tendenza al conteggio dei profili] {#profile-count-trend}

La [!UICONTROL Tendenza al conteggio dei profili] widget utilizza un grafico a linee per illustrare la tendenza del numero totale di profili contenuti nel sistema nel tempo. Questo numero totale include tutti i profili importati nel sistema dall’ultima istantanea giornaliera. I dati possono essere visualizzati in 30 giorni, 90 giorni e 12 mesi. Il periodo di tempo viene scelto da un menu a discesa nel widget.

![Il widget di tendenza del conteggio del profilo.](../images/profiles/profile-count-trend.png)

### [!UICONTROL Modifica del conteggio dei profili] {#profile-count-change}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilescountchange"
>title="Modifica del conteggio dei profili"
>abstract="Questo widget visualizza il numero totale di profili uniti **aggiunti** allo store di profili al momento dell’ultimo snapshot. Il numero dipende dal criterio di unione selezionato applicato ai dati dei profili."

La **[!UICONTROL Modifica del conteggio dei profili]** widget visualizza il numero di profili uniti aggiunti all’archivio profili a partire dallo snapshot precedente. Questo numero è il risultato dell’applicazione del criterio di unione selezionato ai dati del profilo per unire i frammenti di profilo in modo da formare un unico profilo per ogni singolo utente. Puoi utilizzare il selettore a discesa per visualizzare il numero di profili aggiunti negli ultimi 30 giorni, 90 giorni o 12 mesi.

>[!NOTE]
>
>La [!UICONTROL Modifica del conteggio dei profili] Il widget riflette il numero di profili aggiunti **dopo** l’acquisizione del profilo iniziale e la configurazione dell’archivio profili. In altre parole, se la tua organizzazione configurasse l’archivio profili e acquisisse 4.000.000 il giorno 1, entro 24 ore il dashboard sarebbe disponibile, tuttavia il [!UICONTROL Modifica del conteggio dei profili] widget è impostato su 0. Questo viene fatto per evitare un picco associato all’acquisizione iniziale di profili nel sistema. Nei successivi 30 giorni, l’organizzazione acquisisce ulteriori 1.000.000 profili nell’archivio profili. Dopo l&#39;istantanea successiva, la [!UICONTROL Modifica del conteggio dei profili] Il widget mostrerebbe un totale di 1.000.000 profili aggiunti, mentre il [!UICONTROL Numero di profili] Il widget visualizzava 5.000.000 profili totali.

![Dashboard dei profili dell&#39;interfaccia utente della piattaforma con il widget di modifica del conteggio dei profili evidenziato.](../images/profiles/profile-count-change.png)

### [!UICONTROL Tendenza di modifica del conteggio dei profili] {#profiles-count-change-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesaddedtrend"
>title="Tendenza di modifica del conteggio dei profili"
>abstract="Questo widget visualizza il numero di profili uniti che sono stati aggiunti quotidianamente allo store di profili negli ultimi 30 giorni, 90 giorni o 12 mesi. Il numero dipende anche dal criterio di unione selezionato applicato ai dati di profilo."

La **[!UICONTROL Tendenza di modifica del conteggio dei profili]** Il widget visualizza il numero totale di profili uniti che sono stati aggiunti ogni giorno all’archivio profili negli ultimi 30 giorni, 90 giorni o 12 mesi. Questo numero viene aggiornato ogni giorno in cui viene acquisita l’istantanea, pertanto se desideri acquisire profili in Platform, il numero di profili non verrà riportato fino a quando non viene acquisita l’istantanea successiva. Il conteggio dei profili aggiunti è il risultato dell’applicazione dei criteri di unione selezionati ai dati del profilo per unire i frammenti di profilo in modo da formare un unico profilo per ogni singolo utente.

Consulta la sezione [sezione sui criteri di unione in precedenza in questo documento](#merge-policies) per saperne di più.

La **[!UICONTROL Tendenza di modifica del conteggio dei profili]** in alto a destra del widget viene visualizzato il pulsante &quot;didascalie&quot;. Seleziona **[!UICONTROL Sottotitoli]** per aprire la finestra di dialogo didascalie automatiche.

![Nella scheda Panoramica profilo è visualizzato il widget di tendenza della modifica del conteggio dei profili con il pulsante didascalie evidenziato.](../images/profiles/profiles-count-change-trend-captions.png)

Un modello di apprendimento automatico genera automaticamente didascalie per descrivere le tendenze chiave e gli eventi importanti analizzando il grafico e i dati. Le annotazioni vengono aggiunte al grafico in base alle didascalie. Selezionate una didascalia per attivare l’annotazione corrispondente.

![Finestra di dialogo delle didascalie automatiche per il widget di tendenza della modifica del conteggio dei profili.](../images/profiles/profiles-added-trends-automatic-captions-dialog-with-annotation.png)

### [!UICONTROL Tendenza di modifica del conteggio dei profili in base all&#39;identità] {#profiles-count-change-trend-by-identity}

<!-- This widget uses a line graph to illustrate the change in number of profiles filtered by a chosen source identity and merge policy. -->

Questo widget filtra il conteggio dei profili in base a un&#39;identità di origine selezionata e ai criteri di unione, quindi illustra la modifica del numero per diversi periodi utilizzando un grafico a linee. Il criterio di unione viene selezionato dal menu a discesa della panoramica nella parte superiore della pagina, l’identità sorgente e il periodo di tempo sono selezionati dai menu a discesa dei widget. La tendenza può essere visualizzata per periodi di 30 giorni, 90 giorni e 12 mesi.

Questo widget ti aiuta a gestire le tue esigenze di attivazione di destinazione dimostrando il pattern di crescita dei profili filtrati da un’identità richiesta.

![La tendenza del conteggio dei profili cambia in base al widget di identità.](../images/profiles/profiles-count-change-trend-by-identity.png)

### [!UICONTROL Profili per identità] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbyidentity"
>title="Profili per identità"
>abstract="Questo widget visualizza il raggruppamento per identità di tutti i profili uniti nell’archivio dei profili."

La **[!UICONTROL Profili per identità]** Il widget visualizza la suddivisione delle identità in tutti i profili uniti nel tuo archivio profili. Il numero totale di profili per identità (in altre parole, l’aggiunta insieme dei valori mostrati per ogni spazio dei nomi) potrebbe essere superiore al numero totale di profili uniti, in quanto a un profilo potrebbero essere associati più namespace. Ad esempio, se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente saranno associati più namespace.

Consulta la sezione [sezione sui criteri di unione in precedenza in questo documento](#merge-policies) per saperne di più.

![Il dashboard Panoramica profili con il widget Profili per identità evidenziato.](../images/profiles/profiles-by-identity.png)

Seleziona **[!UICONTROL Sottotitoli]** per aprire la finestra di dialogo didascalie automatiche.

![Finestra di dialogo dei profili per didascalie di identità.](../images/profiles/profiles-by-identity-captions.png)

Un modello di apprendimento automatico genera automaticamente informazioni sui dati analizzando la distribuzione complessiva e le dimensioni chiave dei dati.

Per saperne di più sulle identità, visita il [Documentazione del servizio Adobe Experience Platform Identity](../../identity-service/home.md).

### [!UICONTROL Sovrapposizione di identità] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_identityoverlap"
>title="Sovrapposizione di identità"
>abstract="Questo widget visualizza mediante un diagramma di Venn la sovrapposizione dei profili nell’archivio dei profili che contengono le due identità selezionate."

La **[!UICONTROL Sovrapposizione identità]** Il widget utilizza un diagramma di Venn, o diagramma set, per visualizzare la sovrapposizione dei profili nell’archivio profili che contengono le due identità selezionate.

Utilizza i menu a discesa dei widget per selezionare le identità da confrontare. I cerchi mostrano il conteggio totale relativo dei profili che contengono ogni identità. Il numero di profili contenenti entrambe le identità è rappresentato dalla dimensione della sovrapposizione tra i cerchi. Se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente saranno associate più identità, pertanto è probabile che la tua organizzazione abbia più profili contenenti frammenti da più di una identità.

Per ulteriori informazioni sui frammenti di profilo, consulta la sezione su [frammenti di profilo e profili uniti](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en#profile-fragments-vs-merged-profiles) nella panoramica Profilo cliente in tempo reale.

Per saperne di più sulle identità, visita il [Documentazione del servizio Adobe Experience Platform Identity](../../identity-service/home.md).

![Panoramica del dashboard Profili con il widget di sovrapposizione identità evidenziato.](../images/profiles/identity-overlap.png)

### [!UICONTROL Profili a identità singola] {#single-identity-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_singleidentityprofiles"
>title="Profili a identità singola"
>abstract="Questo widget fornisce un conteggio dei profili della tua organizzazione con un solo tipo di ID che ne crea l’identità. Questo tipo di ID può essere un indirizzo e-mail o un ECID."

La [!UICONTROL Profili identità singoli] widget fornisce un conteggio dei profili della tua organizzazione con un solo tipo di ID che ne crea l&#39;identità. Questo tipo di ID può essere un indirizzo e-mail o un ECID. Il conteggio del profilo viene generato dai dati contenuti nell&#39;istantanea più recente.

![Widget Singolo profilo identità.](../images/profiles/single-identity-profiles.png)

### [!UICONTROL Singoli profili di identità per identità] {#single-identity-profiles-by-identity}

Questo widget utilizza un grafico a barre per illustrare il numero totale di profili identificati con un solo identificatore univoco. Il widget supporta fino a cinque delle identità più comuni.

Passa il puntatore del mouse sopra le singole barre per visualizzare una finestra di dialogo che descrive il conteggio totale dei profili per un’identità.

![I profili di identità singola per widget di identità.](../images/profiles/single-identity-profiles-by-identity.png)

### [!UICONTROL Profili non segmentati] {#unsegmented-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofiles"
>title="Profili non segmentati"
>abstract="Questo widget fornisce il numero totale di tutti i profili non collegati ad alcun segmento e rappresenta l’opportunità per l’attivazione dei profili in tutta l’organizzazione."

La [!UICONTROL Profili non segmentati] widget fornisce il numero totale di tutti i profili non collegati ad alcun segmento. Il numero generato è accurato rispetto all’ultima istantanea e rappresenta l’opportunità di attivazione del profilo in tutta l’organizzazione. Indica inoltre l’opportunità di eliminare i profili che non forniscono un ROI adeguato.

![Il widget Profili non segmentati.](../images/profiles/unsegmented-profiles.png)

### [!UICONTROL I profili non segmentati cambiano tendenza] {#unsegmented-profiles-change-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilestrend"
>title="Tendenza dei profili non segmentati"
>abstract="Questo widget fornisce un grafico a linee illustrativo del numero di profili non collegati ad alcun segmento in un dato periodo di tempo. La tendenza dei profili non associati ad alcun segmento può essere visualizzata su periodi di 30 giorni, 90 giorni e 12 mesi."

La [!UICONTROL I profili non segmentati cambiano tendenza] il widget utilizza un grafico a linee per illustrare il numero di profili aggiunti dall’ultima istantanea giornaliera e non collegati ad alcun segmento. La tendenza al cambiamento dei profili non associati ad alcun segmento può essere visualizzata su periodi di 30 giorni, 90 giorni e 12 mesi. Il periodo di tempo viene scelto da un menu a discesa nel widget. Il conteggio dei profili si riflette sull’asse y e sul tempo sull’asse x.

![I profili non segmentati cambiano widget di tendenza.](../images/profiles/unsegmented-profiles-change-trend.png)

### [!UICONTROL Profili non segmentati per identità] {#unsegmented-profiles-by-identity}

>[!NOTE]
>
>I profili non segmentati dai widget di identità sono stati dichiarati obsoleti a partire da ottobre 2022 e non sono più disponibili.

<!-- 

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilesbyidentity"
>title="Unsegmented profiles by identity"
>abstract="This widget categorizes the total number of unsegmented profiles by their unique identifier."

The [!UICONTROL Unsegmented Profiles by Identity] widget categorizes the total number of unsegmented profiles by their unique identifier. The data is visualized in a bar chart for ease of comparison. 

![The Unsegmented Profiles by Identity widget.](../images/profiles/unsegmented-profiles-by-identity.png) -->

### [!UICONTROL Tipi di pubblico] {#audiences}

Questo widget fornisce il numero totale di segmenti pronti per essere attivati, in base al criterio di unione scelto applicato ai dati del profilo.

Seleziona **[!UICONTROL Tipi di pubblico]** per passare al [!UICONTROL Segmenti] dashboard [!UICONTROL Sfoglia] scheda . Da qui puoi vedere un elenco di tutte le definizioni di segmenti per la tua organizzazione.

![Il widget Pubblico.](../images/profiles/audiences.png)

<!-- https://jira.corp.adobe.com/browse/PLAT-115291 -->

<!-- * [[!UICONTROL Audiences change trend]](#audiences-change-trend) -->
<!-- ### [!UICONTROL Audiences change trend] {#audiences-change-trend}

This line graph widget visualizes the change in the total number of audiences each day, trending over time. The change in the number of audiences is dependent on the selected merge policy being applied to your profile data. The period of analysis is selected from the widget dropdown menu. The bar chart can be visualized over 30 days, 90 days, and 12-month periods.  

The visualization allows you to monitor the overall health of audiences within Adobe Experience Platform by understanding trends in the growth or decline of the total number of audiences. -->

<!-- ![The Audiences change trend widget.]() -->

### [!UICONTROL Rapporto di sovrapposizione del pubblico] {#audience-overlap-report}

Questo widget tabularizza i dati di sovrapposizione del pubblico da tutti i segmenti disponibili filtrati in base ai criteri di unione. Per il criterio di unione scelto dal menu a discesa nella parte superiore dello schermo, viene fornito un elenco di cinque tipi di pubblico con una classificazione tra le percentuali di sovrapposizione più alte e più basse. I due segmenti analizzati sono elencati nella variabile [!UICONTROL SEGMENTO DI UN NOME] e [!UICONTROL NOME SEGMENTO B] colonne. La sovrapposizione percentuale viene fornita nella terza colonna con un’approssimazione di dodici posizioni decimali.

Il rapporto di sovrapposizione del pubblico ti aiuta a creare nuovi segmenti ad alte prestazioni. Osservando le sovrapposizioni ad alta percentuale puoi sopprimere i tipi di pubblico e impedire l’invio dello stesso pubblico a destinazioni diverse. Inoltre, ti aiutano a identificare informazioni nascoste che potrebbero essere utili per una migliore segmentazione. Una sovrapposizione a bassa percentuale consente di individuare profili univoci da perseguire.

Seleziona **[!UICONTROL Visualizza altro]** per aprire una finestra di dialogo a schermo intero contenente più dati di sovrapposizione del pubblico.

![Il widget di rapporto di sovrapposizione pubblico con Visualizza più evidenziato .](../images/profiles/profiles-audience-overlap-report.png)

La [!UICONTROL Rapporto di sovrapposizione del pubblico] viene visualizzata la finestra di dialogo . Questa finestra di dialogo può contenere fino a 50 righe di analisi di sovrapposizione del pubblico suddivise in sei colonne. Seleziona l’icona delle impostazioni (![Icona delle impostazioni.](../images/profiles/settings-icon.png)) per rimuovere o aggiungere colonne dalla tabella.

![Finestra di dialogo del rapporto di sovrapposizione del pubblico.](../images/profiles/profiles-audience-overlap-report-dialog.png)

>[!NOTE]
>
>Seleziona la **[!UICONTROL Sovrapposizione]** intestazione di colonna per modificare la classificazione dei risultati tra il più alto e il più basso o il più alto.

Per scaricare l’intero rapporto in formato PDF, seleziona il menu delle opzioni (**`...`**) seguita da **[!UICONTROL Scarica]**.

![La finestra di dialogo del rapporto di sovrapposizione pubblico con l’opzione ellissi e Scarica evidenziata.](../images/profiles/profiles-audience-overlap-report-dialog-download.png)

Seleziona una riga dal rapporto per aprire un diagramma di Venn dell’analisi della sovrapposizione. Passa il puntatore del mouse su una sezione del diagramma di Venn per visualizzare il conteggio dei profili in una finestra di dialogo.

![La finestra di dialogo del rapporto di sovrapposizione del pubblico viene visualizzata con un diagramma di Venn e una riga evidenziata.](../images/profiles/profiles-audience-overlap-report-dialog-venn.png)

Seleziona **[!UICONTROL Chiudi]** per tornare al [!UICONTROL Profili] dashboard.

### [!UICONTROL Tipi di pubblico mappati sullo stato di destinazione] {#audiences-mapped-to-destination-status}

La [!UICONTROL Tipi di pubblico mappati sullo stato di destinazione] widget visualizza il numero totale di tipi di pubblico mappati e non mappati in un’unica metrica e utilizza un grafico ad anello per illustrare la differenza proporzionale tra i loro totali. I numeri calcolati dipendono dal criterio di unione scelto.

I singoli conteggi per tipi di pubblico mappati o non mappati vengono visualizzati in una finestra di dialogo quando il cursore passa sopra la rispettiva sezione del grafico ad anello.

![Il pubblico mappato al widget di stato della destinazione.](../images/profiles/audiences-mapped-to-destination-status.png)

### [!UICONTROL Dimensione del pubblico] {#audiences-size}

La [!UICONTROL Dimensione del pubblico] widget fornisce una tabella a due colonne in cui sono elencati fino a 20 segmenti e il numero totale di tipi di pubblico contenuti in ciascun segmento. L’elenco è ordinato da alto a basso in base al numero totale di tipi di pubblico. Il numero totale di dimensioni del pubblico dipende dal criterio di unione applicato.

![Il widget Dimensione pubblico.](../images/profiles/audiences-size.png)

Per visualizzare informazioni complete su un segmento, seleziona un nome di segmento dall’elenco fornito per passare al [!UICONTROL Segmenti] [!UICONTROL Dettaglio] pagina. Inoltre, selezionando **[!UICONTROL Visualizza tutti i segmenti]** dalla fine del widget, puoi passare al [!UICONTROL Segmenti] [!UICONTROL Sfoglia] per trovare eventuali segmenti esistenti.

![Il widget Dimensione pubblico con un nome di segmento e visualizza il testo di tutti i segmenti evidenziato.](../images/profiles/audiences-size-view-all-segments.png)

Consulta la documentazione per ulteriori informazioni sul [[!UICONTROL Segmenti] [!UICONTROL  Sfoglia] scheda](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#browse).

### [!UICONTROL Sovrapposizione del pubblico per criterio di unione] {#audience-overlap-by-merge-policy}

Questo widget utilizza un diagramma di Venn per visualizzare la sovrapposizione di due segmenti selezionati. Il criterio di unione viene selezionato dal menu a discesa della panoramica nella parte superiore della pagina e i segmenti da analizzare sono selezionati da due menu a discesa all’interno del widget. Il numero totale di profili contenuti nella definizione del segmento pertinente può essere visto passando il cursore su un cerchio o sull’intersezione.

Quando il widget visualizza il crossover visivo delle definizioni dei segmenti, puoi ottimizzare la strategia di segmentazione studiando le somiglianze tra le definizioni dei segmenti.

![Dashboard dei profili dell&#39;interfaccia utente della piattaforma con il menu a discesa dei criteri di unione e gli elenchi a discesa dei segmenti dei widget evidenziati.](../images/profiles/audience-overlap-by-merge-policy.png)


<!-- ## (Beta) Profile efficacy widgets {#profile-efficacy-widgets}

>[!IMPORTANT]
>
>The profile efficacy widgets are currently in Beta and are not available to all users. The documentation and the functionality are subject to change.

Adobe provides multiple widgets to assess the completeness of the ingested profiles available for your data analysis. Each of the profile efficacy widgets can be filtered by the merge policy. To change the merge policy filter, select the[!UICONTROL Profiles using merge policy] dropdown and choose the appropriate policy from the available list.

To learn more about each of the profile efficacy widgets, select the name of a widget from the following list:

* [[!UICONTROL Attribute quality assessment]](#attributes-quality-assessment)
* [[!UICONTROL Profiles by completeness]](#profiles-by-completeness)
* [[!UICONTROL Profiles completeness trend]](#profiles-completeness-trend)

### (Beta) [!UICONTROL Attributes quality assessment] {#attributes-quality-assessment}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_attributesqualityassessment"
>title="Attributes quality assessment"
>abstract="This widget shows the completeness and cardinality of all profiles according to their attributes. Each row describes one attribute. The **Profiles** column provides the number of profiles that have this attribute and are filled with non-null values. The **Completeness** percentage is determined by the total number of profiles that have this attribute and are filled with non-null values divided by the total number of non-empty values in the profiles for that attribute. **Cardinality** provides the total number of unique non-null values of this attribute across all attributes."

The [!UICONTROL Attribute quality assessment] widget shows the completeness and cardinality of all profiles according to their attributes. The data is accurate to the last processing date. This information is presented as a table with four columns where each row in the table represents a single attribute.

| Column  | Description  |
|---|---|
| Attribute  | The name of the attribute.  |
| Profiles  | The number of profiles that have this attribute and are filled with non-null values.  |
| Completeness  | This percentage is determined by the total number of profiles that have this attribute and are filled with non-null values. The number is calculated by dividing the total number of profiles by the total number of non-empty values in the profiles for that attribute.  |
| Cardinality  | The total number of **unique** non-null values of this attribute. It is measured across all profiles. |

![The attributes quality assessment widget](../images/profiles/attributes-quality-assessment.png)

### (Beta) [!UICONTROL Profiles by completeness] {#profiles-by-completeness}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbycompleteness"
>title="Profiles by completeness"
>abstract="The donut chart displays the percentage of profile attributes that are filled with non-null values among all observed attributes. It illustrates the proportion of profiles that are of high, medium, or low completeness. High completeness profiles have more than 70% of their attributes filled. Medium completeness profiles have between 30% and 70% of their attributes filled. Low completeness profiles have less than 30% of their attributes filled."

The [!UICONTROL Profiles by completeness] widget creates a donut chart of profile completeness since the last processing date. The completeness of a profile is measured by the percentage of attributes that are filled with non-null values among all observed attributes.

This widget shows the proportion of profiles that are of high, medium, or low completeness. By default, there are three levels of completeness configured: 

* High completeness: Profiles have more than 70% of their attributes filled. 
* Medium completeness: Profiles have between 30% and 70% of their attributes filled. 
* Low completeness: Profiles have less than 30% of their attributes filled. 

![The profiles by completeness widget](../images/profiles/profiles-by-completeness.png)

### (Beta) [!UICONTROL Profiles completeness trend] {#profiles-completeness-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilescompletenesstrend"
>title="Profiles completeness trend"
>abstract="This widget creates a stacked area chart to depict the trend of profile completeness over time. Completeness is measured by the percentage of attributes that are filled with non-null values among all observed attributes."

This widget creates a stacked area chart to depict the trend of profile completeness over time. Completeness is measured by the percentage of attributes filled with non-null values among all observed attributes. It categorizes the profile completeness as high, medium, or low completeness since the last processing date.

The x-axis represents time, the y-axis represents the number of profiles, and the colors represent the three levels of profile completeness. 

The three levels of completeness are:

* High completeness: Profiles have more than 70% of attributes filled. 
* Medium completeness: Profiles have less than 70% and more than 30% of attributes filled. 
* Low completeness: Profiles have less than 30% of attributes filled.

![The profiles completeness trend widget](../images/profiles/profiles-completeness-trend.png) -->

## Passaggi successivi

Seguendo questo documento, ora dovresti essere in grado di individuare il dashboard dei profili e comprendere le metriche visualizzate nei widget disponibili. Per ulteriori informazioni sull’utilizzo di [!DNL Profile] nell’interfaccia utente di Experience Platform, fai riferimento alla [Guida all’interfaccia utente del profilo cliente in tempo reale](../../profile/ui/user-guide.md).
