---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;interfaccia utente;interfaccia utente;personalizzazione;dashboard profilo;dashboard dashboard
title: Dashboard delle destinazioni
description: Adobe Experience Platform fornisce un dashboard tramite il quale puoi visualizzare informazioni importanti sulle destinazioni attive della tua organizzazione.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: 86041e3165d4ea9cb55717f24b002afa084ff420
workflow-type: tm+mt
source-wordcount: '1709'
ht-degree: 0%

---

# [!UICONTROL Destinazioni] dashboard

L’interfaccia utente di Adobe Experience Platform fornisce una dashboard attraverso la quale è possibile visualizzare informazioni importanti sulle destinazioni attive dell’organizzazione, acquisite durante un’istantanea giornaliera. Questa guida illustra come accedere e lavorare con il dashboard delle destinazioni nell’interfaccia utente e fornisce ulteriori informazioni sulle metriche visualizzate nel dashboard.

Per una panoramica delle destinazioni e un catalogo di tutte le destinazioni disponibili all&#39;interno dell&#39;Experience Platform, visita [documentazione sulle destinazioni](../../destinations/home.md).

## [!UICONTROL Destinazioni] dati del dashboard {#destinations-dashboard-data}

La [!UICONTROL Destinazioni] nel dashboard viene visualizzata un’istantanea delle destinazioni abilitate dall’organizzazione in Experience Platform. I dati nello snapshot mostrano esattamente come vengono visualizzati nel momento specifico in cui è stata acquisita l&#39;istantanea. In altre parole, lo snapshot non è un&#39;approssimazione o un esempio dei dati e il dashboard delle destinazioni non viene aggiornato in tempo reale.

>[!NOTE]
>
>Eventuali modifiche o aggiornamenti apportati ai dati dall&#39;acquisizione dello snapshot non verranno visualizzati nel dashboard fino all&#39;acquisizione dello snapshot successivo.

## Esplorazione del dashboard delle destinazioni

Per passare al dashboard delle destinazioni nell’interfaccia utente di Platform, seleziona **[!UICONTROL Destinazioni]** nella barra a sinistra, seleziona la **[!UICONTROL Panoramica]** per visualizzare il dashboard.

>[!NOTE]
>
>Se la tua organizzazione ha poca esperienza con Experience Platform e non dispone ancora di destinazioni attive, la [!UICONTROL Destinazioni] dashboard [!UICONTROL Panoramica] non sono visibili. Invece, selezionando [!UICONTROL Destinazioni] nel menu di navigazione a sinistra viene visualizzata la [!UICONTROL Catalogo] scheda . Per ulteriori informazioni sulle [!UICONTROL Catalogo] , fai riferimento alla [[!UICONTROL Destinazioni] guida all’area di lavoro](../../destinations/ui/destinations-workspace.md).

![](../images/destinations/dashboard-overview.png)

### Modifica del dashboard delle destinazioni

Puoi modificare l’aspetto del dashboard delle destinazioni selezionando **[!UICONTROL Modifica dashboard]**. Questo consente di spostare, aggiungere e rimuovere i widget dal dashboard e di accedere al **[!UICONTROL Libreria widget]** per esplorare i widget disponibili e creare widget personalizzati per la tua organizzazione.

Fai riferimento alla [modifica delle dashboard](../customize/modify.md) e [panoramica della libreria widget](../customize/widget-library.md) documentazione per ulteriori informazioni.

## Widget standard

Adobe fornisce diversi widget standard che puoi utilizzare per visualizzare diverse metriche correlate alle destinazioni e valutare la completezza dei segmenti disponibili per l’analisi dei dati. Puoi anche creare widget personalizzati da condividere con la tua organizzazione utilizzando [!UICONTROL Libreria widget]. Per ulteriori informazioni sulla creazione di widget personalizzati, si prega di iniziare leggendo [panoramica della libreria widget](../customize/widget-library.md).

Per ulteriori informazioni su ciascuno dei widget standard disponibili, seleziona il nome di un widget dal seguente elenco:

* [[!UICONTROL Destinazioni più utilizzate]](#most-used-destinations)
* [[!UICONTROL Destinazioni create di recente]](#recently-created-destinations)
* [[!UICONTROL Segmenti attivati di recente]](#recently-activated-segments)
* [[!UICONTROL Segmenti attivati di recente per destinazione]](#recently-activated-segments-by-destination)
* [[!UICONTROL Tendenza delle dimensioni del pubblico]](#audience-size-trends)
* [[!UICONTROL Segmenti non mappati per identità]](#unmapped-segments-by-identity)
* [[!UICONTROL Segmenti mappati per identità]](#mapped-segments-by-identity)
* [[!UICONTROL Tipi di pubblico comuni]](#common-audiences)
* [[!UICONTROL Conteggio destinazioni]](#destinations-count)

### [!UICONTROL Destinazioni più utilizzate] {#most-used-destinations}

La **[!UICONTROL Destinazioni più utilizzate]** widget visualizza le principali destinazioni della tua organizzazione in base al numero di segmenti mappati, a partire dall&#39;ultima istantanea. Questa classificazione fornisce informazioni sulle destinazioni che vengono utilizzate, mostrando al contempo quelle che potrebbero essere sottoutilizzate.

Ad esempio, se hai configurato una destinazione ieri ma non hai mappato alcun segmento su di essa, puoi vedere che la destinazione è attualmente sottoutilizzata.

Il numero di segmenti mappati visualizzati nella colonna del conteggio dei segmenti è preciso a partire dall’ultima istantanea giornaliera. La mappatura di un nuovo segmento alla destinazione non aggiornerà il conteggio fino a quando non viene acquisita la successiva istantanea.

Selezionando il nome di una destinazione dall&#39;elenco mostrato sul widget, potrai accedere ai dettagli della destinazione come collegati dal **[!UICONTROL Sfoglia]** scheda . Puoi anche selezionare **[!UICONTROL Visualizza tutto]** per passare al **[!UICONTROL Sfoglia]** , quindi seleziona il nome di una destinazione per visualizzarne i dettagli.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Destinazioni create di recente] {#recently-created-destinations}

La **[!UICONTROL Destinazioni create di recente]** widget consente di visualizzare un elenco delle destinazioni configurate più di recente della tua organizzazione.

La data di creazione mostrata corrisponde all’ultima istantanea giornaliera. In altre parole, se crei una nuova destinazione, questa verrà visualizzata nell’elenco solo dopo l’acquisizione dello snapshot successivo.

Selezionando il nome di una destinazione dall&#39;elenco mostrato sul widget, potrai accedere ai dettagli della destinazione come collegati dal **[!UICONTROL Sfoglia]** scheda . Puoi anche selezionare **[!UICONTROL Visualizza tutto]** per passare al **[!UICONTROL Sfoglia]** , quindi seleziona il nome di una destinazione per visualizzarne i dettagli.

Per ulteriori informazioni su come configurare tipi specifici di destinazioni, visita il [documentazione sulle destinazioni](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Segmenti attivati di recente] {#recently-activated-segments}

La **[!UICONTROL Segmenti attivati di recente]** widget fornisce un elenco dei segmenti mappati più di recente a una destinazione. Questo elenco fornisce un’istantanea dei segmenti e delle destinazioni attivamente utilizzati nel sistema e può essere utile per risolvere eventuali mappature errate.

La data aggiornata visualizzata visualizza l’ultima volta che il segmento è stato attivato nella destinazione ed è accurata dell’ultima istantanea giornaliera. In altre parole, se attivi un segmento nella destinazione, la data aggiornata non cambierà fino a quando non viene acquisita la successiva istantanea.

Selezionando il nome di un segmento dall’elenco visualizzato sul widget, passerai ai dettagli del segmento. Puoi anche selezionare **[!UICONTROL Visualizza tutto]** per passare alla scheda di ricerca dei segmenti, quindi selezionare il nome di un segmento per visualizzarne i dettagli.

Per ulteriori informazioni sull’utilizzo dei segmenti in Experience Platform, inizia leggendo il [Panoramica del servizio di segmentazione](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

### [!UICONTROL Segmenti attivati di recente per destinazione] {#recently-activated-segments-by-destination}

La **[!UICONTROL Segmenti attivati di recente per destinazione]** widget visualizza i primi cinque segmenti attivati più di recente in ordine decrescente in base alla destinazione scelta nel menu a discesa della panoramica. È simile al [!UICONTROL Segmenti attivati di recente] widget, ma i dati visualizzati **only** si applica alla destinazione selezionata.

Questo widget contiene due metriche: il nome del segmento e la data dell’ultima attivazione del segmento nella destinazione. I dati visualizzati sono corretti a partire dall&#39;ultima istantanea giornaliera.

Per visualizzare i dettagli di un segmento, seleziona il nome di un segmento dall’elenco visualizzato.

![I segmenti sono stati attivati di recente per widget di destinazione.](../images/destinations/recently-activated-segments-by-destination.png)

### [!UICONTROL Tendenza delle dimensioni del pubblico] {#audience-size-trend}

La **[!UICONTROL Tendenza delle dimensioni del pubblico]** widget rappresenta la relazione del conteggio di profilo in un periodo di tempo per un segmento mappato a tale account di destinazione. Il widget utilizza un grafico a linee per illustrare il numero di profili contenuti nel segmento, che vengono inviati quotidianamente all’account di destinazione.

È possibile regolare un periodo di tempo per la tendenza del pubblico negli ultimi 30 giorni, 90 giorni o 12 mesi utilizzando il primo menu a discesa.

Il secondo menu a discesa elenca ogni segmento disponibile che può essere inviato all’account di destinazione scelto nella parte superiore del dashboard.

![Il widget di tendenza della dimensione del pubblico.](../images/destinations/audience-size-trend.png)

### [!UICONTROL Segmenti non mappati per identità] {#unmapped-segments-by-identity}

La **[!UICONTROL Segmenti non mappati per identità]** elenchi dei primi cinque **non mappato** i segmenti sono classificati in base al conteggio delle identità decrescente per una determinata destinazione e identità. Evidenzia i segmenti che sono i più vantaggiosi da mappare all’account di destinazione scelto in base all’ID scelto.

Il menu a discesa ID destinazione filtra i segmenti disponibili. Gli ID filtro elencati nel menu a discesa variano a seconda dell’account di destinazione selezionato nella parte superiore della pagina della panoramica.

La colonna identità conta il numero di ID sorgente all’interno del segmento che possono essere mappati sull’ID scelto nel menu a discesa ID widget.

![I segmenti non mappati per widget di identità.](../images/destinations/unmapped-segments-by-identity.png)

### [!UICONTROL Segmenti mappati per identità] {#mapped-segments-by-identity}

Questo widget fornisce un elenco dei primi cinque **mappato** segmenti. L’elenco è ordinato da alto a basso in base al numero di ID sorgente contenuti nei segmenti. L&#39;ID di destinazione da conteggiare viene selezionato dal menu a discesa sotto il titolo del widget. Gli ID di destinazione disponibili nel menu a discesa nel widget vengono modificati in base al filtro dell’account di destinazione scelto nella parte superiore del dashboard della panoramica.

![I segmenti mappati per widget di identità.](../images/destinations/mapped-segments-by-identity.png)

La **[!UICONTROL Segmenti mappati per identità]** Il widget evidenzia immediatamente la probabilità di riuscire a eseguire il targeting delle opportunità di profilo per una campagna all&#39;interno della destinazione selezionata. Una campagna con targeting efficiente non dipende dal numero di profili inviati alla destinazione, ma dal numero di ID sorgente che probabilmente verranno confrontati con gli ID di destinazione per fornire dati utili e fruibili.

### Tipi di pubblico comuni

La **[!UICONTROL Tipi di pubblico comuni]** widget fornisce un elenco dei primi cinque segmenti attivati nell’account di destinazione selezionato nella parte superiore della pagina e della destinazione selezionata nel menu a discesa del widget. L’elenco dei segmenti viene ordinato in base a come sono stati attivati di recente. Il segmento attivato più di recente viene visualizzato nella parte superiore.

La [!UICONTROL DIMENSIONE DEL PUBBLICO] fornisce il conteggio totale dei profili di ciascun segmento elencato.

![Il widget Pubblico comune.](../images/destinations/common-audiences.png)

### Stato del pubblico mappato

Il widget fornisce un elenco di fino a 20 segmenti mappati il cui profilo totale conta, a partire dall’ultima istantanea giornaliera, un fattore di almeno una deviazione standard rispetto alla dimensione media del pubblico mappata a tale destinazione nei 30 giorni successivi.

In breve, fornisce una metrica calcolata per la dispersione delle dimensioni del pubblico dalla media negli ultimi 30 giorni. Confronta se la dimensione del pubblico attuale è al di fuori della deviazione standard storica osservata nei dati degli ultimi 30 giorni.

Tutte le dimensioni del pubblico nel sistema vengono ordinate da un pubblico di dimensioni elevate a un pubblico di dimensioni ridotte, come indicato nella [!UICONTROL DIMENSIONE PIÙ RECENTE] colonna.

Se il conteggio del profilo mappato del segmento non corrisponde a una deviazione standard rispetto alla dimensione media del profilo mappato negli ultimi 30 giorni, indica un’anomalia nel sistema e deve essere analizzata.

Se un segmento all’interno di [!UICONTROL Stato del pubblico mappato] Il widget si discosta di un ampio margine, fai riferimento al grafico delle tendenze delle dimensioni del pubblico e individua il segmento anomalo. La tendenza può fornire ulteriori informazioni sullo stato di salute del segmento.

![Il widget di stato del pubblico mappato.](../images/destinations/mapped-audience-health.png)

### [!UICONTROL Conteggio destinazioni] (#destinations-count)

La [!UICONTROL Conteggio destinazioni] widget fornisce il numero totale di endpoint disponibili in cui un pubblico può essere attivato e consegnato all&#39;interno del sistema. Questo numero include sia le destinazioni attive che quelle inattive.

Sotto il conteggio totale, seleziona **[!UICONTROL Destinazioni]** per passare alla scheda di ricerca delle destinazioni . In questa pagina sono elencate tutte le destinazioni con le quali hai stabilito una connessione fino ad oggi.

![Il widget Conteggio destinazioni.](../images/destinations/destinations-count.png)

## Passaggi successivi

Seguendo questo documento, ora dovresti essere in grado di individuare il dashboard delle destinazioni e comprendere le metriche visualizzate nei widget disponibili. Per ulteriori informazioni sull’utilizzo delle destinazioni nell’Experience Platform, consulta [documentazione sulle destinazioni](../../destinations/home.md).
