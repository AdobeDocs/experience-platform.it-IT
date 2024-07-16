---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;interfaccia utente;personalizzazione;dashboard profilo;profilo;profile;real-time customer profile;user interface;UI;customization;profile dashboard;dashboard
title: Dashboard delle destinazioni
description: Adobe Experience Platform fornisce una dashboard attraverso la quale puoi visualizzare informazioni importanti sulle destinazioni attive della tua organizzazione.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: a8b5ed09e8e28075a3a4f37ad30f01c1cc389b9c
workflow-type: tm+mt
source-wordcount: '3243'
ht-degree: 19%

---

# [!UICONTROL Destinazioni] dashboard

L’interfaccia utente di Adobe Experience Platform fornisce una dashboard attraverso la quale è possibile visualizzare informazioni importanti sulle destinazioni attive dell’organizzazione, acquisite durante uno snapshot giornaliero. Questa guida illustra come accedere e lavorare con il dashboard delle destinazioni nell’interfaccia utente di e fornisce ulteriori informazioni sulle metriche visualizzate nel dashboard.

Per una panoramica delle destinazioni e un catalogo di tutte le destinazioni disponibili in Experience Platform, visita la [documentazione sulle destinazioni](../../destinations/home.md).

## [!UICONTROL Destinazioni] dati dashboard {#destinations-dashboard-data}

Nel dashboard Destinazioni viene visualizzata un’istantanea delle destinazioni abilitate dalla tua organizzazione in Experience Platform. I dati nello snapshot mostrano esattamente come vengono visualizzati nel momento specifico in cui lo snapshot è stato creato. In altre parole, l’istantanea non è un’approssimazione o un esempio dei dati e il dashboard delle destinazioni non viene aggiornato in tempo reale.

>[!NOTE]
>
>Eventuali modifiche o aggiornamenti apportati ai dati dal momento in cui è stata acquisita l’istantanea non verranno riflessi nel dashboard fino all’acquisizione dell’istantanea successiva.

## Esplora il dashboard [!UICONTROL Destinazioni] {#explore}

Per passare al dashboard delle destinazioni all&#39;interno dell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Destinazioni]** nella barra a sinistra, quindi seleziona la scheda **[!UICONTROL Panoramica]** per visualizzare il dashboard.

La data e l&#39;ora dello snapshot più recente vengono visualizzate nella parte superiore della [!UICONTROL Panoramica] accanto al menu a discesa di destinazione. Tutti i dati del widget sono accurati a partire da quella data e ora. Il timestamp dell’istantanea viene fornito in UTC; non si trova nel fuso orario del singolo utente o organizzazione.

>[!NOTE]
>
>Se la tua organizzazione non ha ancora Experienci Platform e non dispone ancora di destinazioni attive, la dashboard Destinazioni e la scheda [!UICONTROL Panoramica] non sono visibili. Se invece selezioni [!UICONTROL Destinazioni] dalla navigazione a sinistra, viene visualizzata la scheda [!UICONTROL Catalogo]. Per ulteriori informazioni sulla scheda [!UICONTROL Catalogo], consulta la guida dell&#39;area di lavoro [[!UICONTROL Destinazioni]](../../destinations/ui/destinations-workspace.md).

![Panoramica delle destinazioni dell&#39;interfaccia utente di Platform con lo snapshot più recente evidenziato.](../images/destinations/snapshot-timestamp.png)

### Modifica il dashboard [!UICONTROL Destinazioni] {#modify}

Selezionare **[!UICONTROL Modifica dashboard]** per modificare l&#39;aspetto del dashboard delle destinazioni. Le modifiche al dashboard sono per utente e non a livello di organizzazione. Potete spostare, aggiungere, ridimensionare e rimuovere widget dal dashboard e accedere alla libreria di widget per personalizzare il dashboard. Dalla libreria dei widget, puoi esplorare i widget disponibili e creare widget personalizzati per la tua organizzazione.

Per ulteriori informazioni, consulta la documentazione [modifica dashboard](../customize/modify.md) e [panoramica della libreria widget](../customize/widget-library.md).

### Aggiungi widget {#add-widget}

Seleziona **[!UICONTROL Aggiungi widget]** per passare alla libreria di widget e visualizzare un elenco dei widget disponibili da aggiungere al dashboard.

![Panoramica del dashboard Destinazioni con Aggiungi widget evidenziato.](../images/destinations/destinations-overview-add-widget.png)

Dalla libreria dei widget, puoi sfogliare la selezione di widget di pubblico standard e personalizzati. Per informazioni su come aggiungere widget, consulta la documentazione della libreria di widget su come [aggiungere un widget](../customize/widget-library.md#add-widgets).

### Visualizza SQL {#view-sql}

Puoi visualizzare il codice SQL che genera le informazioni visualizzate nel tuo dashboard con un interruttore nell&#39;area di lavoro [!UICONTROL Panoramica]. Puoi trarre ispirazione dall’SQL delle informazioni esistenti per creare nuove query che derivano informazioni univoche dai dati di Platform in base alle esigenze aziendali. Per ulteriori informazioni su questa funzionalità, vedere la [Guida dell&#39;interfaccia utente SQL](../view-sql.md).

## Widget predefiniti {#default-widgets}

Per tutte le nuove istanze di Adobe Experience Platform viene fornito un widget predefinito che evidenzia le informazioni più recenti disponibili dai dati. I seguenti widget sono preconfigurati nella vista dei segmenti fin dall’inizio. Per informazioni complete sullo scopo e la funzione dei widget, vedi sotto.

* [[!UICONTROL Destinazioni più utilizzate]](#most-used-destinations)
* [[!UICONTROL Destinazioni create di recente]](#recently-created-destinations)
* [[!UICONTROL Segmenti attivati di recente]](#recently-activated-segments)

>[!NOTE]
>
>A partire dal 26 luglio 2023, le dashboard Panoramica di [!UICONTROL Profili], [!UICONTROL Tipi di pubblico] e [!UICONTROL Destinazioni] sono state reimpostate su un nuovo widget predefinito per tutti gli utenti che non hanno modificato le proprie visualizzazioni nei sei mesi precedenti.
>Consulta la documentazione nelle sezioni dei widget predefiniti di [Profili](./profiles.md#default-widgets) e [Tipi di pubblico](./audiences.md#default-widgets) per informazioni dettagliate sui widget inclusi come parte dei rollout dei widget predefiniti. Puoi continuare a personalizzare i widget del dashboard come prima.

## Widget standard {#standard-widgets}

Adobe fornisce più widget standard da utilizzare per visualizzare diverse metriche correlate alle destinazioni e valutare la completezza dei tipi di pubblico disponibili per l’analisi dei dati. Puoi anche creare widget personalizzati da condividere con la tua organizzazione utilizzando la [!UICONTROL Libreria widget]. Per ulteriori informazioni sulla creazione di widget personalizzati, leggere la [Panoramica della libreria di widget](../customize/widget-library.md).

### Prerequisiti {#prerequisites}

Prima di continuare con le descrizioni dei widget standard, accertati di conoscere le definizioni dei seguenti termini chiave utilizzati in tutta la documentazione:

* **Definizione segmento:** Una definizione segmento è un **insieme di regole** utilizzate per descrivere le caratteristiche o il comportamento chiave di un pubblico di destinazione. Queste regole includono dati di attributi ed eventi che qualificano i profili come parte di un pubblico.
* **Pubblico**: un set di persone, account, famiglie o altre entità che hanno in comune caratteristiche e/o comportamenti specifici.
* **Mappato/Mappatura**: la mappatura dei dati è il processo di mappatura dei campi dei dati di origine ai campi di destinazione correlati in una destinazione.
* **Identità**: un&#39;identità è un identificatore che rappresenta in modo univoco un singolo cliente, ad esempio un ID cookie, un ID dispositivo o un ID e-mail.
* **Attiva**: attiva è l&#39;azione intrapresa da un utente per mappare uno o più profili di pubblico a una destinazione come Oracle Eloqua, Google o il Marketing Cloud Salesforce.

Per ulteriori informazioni su ciascuno dei widget standard disponibili, selezionare il nome di un widget dall&#39;elenco seguente:

* [[!UICONTROL Destinazioni più utilizzate]](#most-used-destinations)
* [[!UICONTROL Destinazioni create di recente]](#recently-created-destinations)
* [[!UICONTROL Tipi di pubblico attivati di recente]](#recently-activated-audiences)
* [[!UICONTROL Tipi di pubblico attivati di recente per destinazione]](#recently-activated-audiences-by-destination)
* [[!UICONTROL Tendenza delle dimensioni del pubblico]](#audience-size-trend)
* [[!UICONTROL Tipi di pubblico non mappati per identità]](#unmapped-audiences-by-identity)
* [[!UICONTROL Tipi di pubblico mappati per identità]](#mapped-audiences-by-identity)
* [[!UICONTROL Pubblico comune]](#common-audiences)
* [[!UICONTROL Pubblico mappato]](#mapped-audiences)
* [[!UICONTROL Stato del pubblico mappato]](#mapped-audience-health)
* [[!UICONTROL Conteggio delle destinazioni]](#destinations-count)
* [[!UICONTROL Stato destinazione]](#destination-status)
* [[!UICONTROL Destinazioni attive per piattaforma di destinazione]](#active-destinations-by-destination-platform)
* [[!UICONTROL Tipi di pubblico attivati su tutte le destinazioni]](#activated-audiences-across-all-destinations)
* [[!UICONTROL Tipi di pubblico attivati]](#activated-audiences)

### [!UICONTROL Destinazioni più utilizzate] {#most-used-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mostuseddestinations"
>title="Destinazioni più utilizzate"
>abstract="Questo widget visualizza le destinazioni più attive dell&#39;organizzazione in base al numero di tipi di pubblico mappati. Questi numeri sono precisi al momento dell’ultimo snapshot. Questa classificazione fornisce informazioni sulle destinazioni attualmente più utilizzate, evidenziando quelle che potrebbero essere sottoutilizzate."

Il widget **[!UICONTROL Destinazioni più utilizzate]** visualizza le destinazioni principali della tua organizzazione in base al numero di tipi di pubblico mappati, all&#39;ultima istantanea. Questa classificazione fornisce informazioni approfondite sulle destinazioni utilizzate, mostrando potenzialmente anche quelle che potrebbero essere sottoutilizzate.

Ad esempio, se ieri hai configurato una destinazione ma non hai mappato alcun pubblico su di essa, potresti vedere che la destinazione è attualmente sottoutilizzata.

Il numero di tipi di pubblico mappati mostrato nella colonna [!UICONTROL Conteggio dei tipi di pubblico] è accurato all&#39;ultima istantanea giornaliera. La mappatura di un nuovo pubblico sulla destinazione non aggiorna il conteggio fino allo scatto dell’istantanea successiva.

Selezionate il nome di una destinazione dall&#39;elenco visualizzato sul widget per passare ai dettagli della destinazione per quella particolare destinazione. Puoi anche selezionare **[!UICONTROL Visualizza tutto]** per passare alla scheda **[!UICONTROL Sfoglia]** e quindi selezionare il nome di una destinazione per visualizzarne i dettagli.

![Scheda Panoramica del dashboard Destinazioni con il widget Destinazioni più utilizzate evidenziato.](../images/destinations/most-used-destinations.png)

### [!UICONTROL Destinazioni create di recente] {#recently-created-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlycreateddestinations"
>title="Destinazioni create di recente"
>abstract="Questo widget visualizza un elenco delle destinazioni configurate più recentemente all’interno della tua organizzazione."

Il widget **[!UICONTROL Destinazioni create di recente]** ti consente di visualizzare un elenco delle destinazioni configurate più di recente dalla tua organizzazione.

La data di creazione mostrata è accurata rispetto all&#39;ultima istantanea giornaliera. In altre parole, se si crea una nuova destinazione, questa non verrà visualizzata nell&#39;elenco fino a quando non viene acquisita l&#39;istantanea successiva.

Selezionando il nome di una destinazione dall&#39;elenco visualizzato sul widget, potrai accedere ai dettagli della destinazione collegati dalla scheda **[!UICONTROL Sfoglia]**. Puoi anche selezionare **[!UICONTROL Visualizza tutto]** per passare alla scheda **[!UICONTROL Sfoglia]** e quindi selezionare il nome di una destinazione per visualizzarne i dettagli.

Per ulteriori informazioni su come configurare tipi specifici di destinazioni, consulta la [documentazione sulle destinazioni](../../destinations/home.md).

![Scheda Panoramica del dashboard Destinazioni con il widget Destinazioni create di recente evidenziato.](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Tipi di pubblico attivati di recente] {#recently-activated-audiences}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegments"
>title="Tipi di pubblico attivati di recente"
>abstract="Questo widget fornisce un elenco dei tipi pubblico mappati più recentemente a una destinazione. Questo elenco fornisce uno snapshot dei tipi di pubblico e delle destinazioni attivamente utilizzati nel sistema e può essere utile per risolvere eventuali mappature errate."

Il widget **[!UICONTROL Tipi di pubblico attivati di recente]** fornisce un elenco degli ultimi tipi di pubblico mappati su una destinazione. Questo elenco fornisce uno snapshot dei tipi di pubblico e delle destinazioni attivamente utilizzati nel sistema e può essere utile per risolvere eventuali mappature errate.

La data [!UICONTROL Aggiornato] visualizzata mostra l&#39;ultima volta che il pubblico è stato attivato nella destinazione ed è accurata rispetto all&#39;ultima istantanea giornaliera. In altre parole, se attivi un pubblico nella destinazione, la data aggiornata non cambierà fino a quando non viene acquisita l’istantanea successiva.

Selezionando il nome di un pubblico dall’elenco visualizzato sul widget, puoi passare ai dettagli del pubblico. Puoi anche selezionare **[!UICONTROL Visualizza tutto]** per passare alla scheda [!UICONTROL Tipi di pubblico] [!UICONTROL Sfoglia] e quindi selezionare il nome di un pubblico per visualizzarne i dettagli.

Per ulteriori informazioni sull&#39;utilizzo dei tipi di pubblico in Experience Platform, consulta la [Panoramica del servizio di segmentazione](../../segmentation/home.md).

![Scheda Panoramica del dashboard Destinazioni con il widget Tipi di pubblico attivati di recente evidenziato.](../images/destinations/recently-activated-audiences.png)

### [!UICONTROL Tipi di pubblico attivati di recente per destinazione] {#recently-activated-audiences-by-destination}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegmentsbydestination"
>title="Tipi di pubblico attivati di recente per destinazione"
>abstract="Questo widget visualizza i primi cinque tipi di pubblico attivati più recentemente in ordine decrescente in base alla destinazione scelta nel menu a discesa della panoramica."

Il widget **[!UICONTROL Tipi di pubblico attivati di recente per destinazione]** visualizza i primi cinque tipi di pubblico attivati di recente in ordine decrescente in base alla destinazione scelta nel menu a discesa Panoramica. È simile al widget [!UICONTROL Tipi di pubblico attivati di recente], ma i dati visualizzati **solo** si applicano alla destinazione selezionata.

Questo widget contiene due metriche: il nome del pubblico e la data dell’ultima attivazione del pubblico nella destinazione. I dati visualizzati sono corretti all&#39;ultima istantanea giornaliera.

Puoi visualizzare i dettagli di un pubblico selezionando il nome del pubblico dall’elenco visualizzato.

![I tipi di pubblico attivati di recente dal widget di destinazione.](../images/destinations/recently-activated-audiences-by-destination.png)

Consulta la sezione sui prerequisiti per le [definizioni dei termini utilizzati](#prerequisites) in questa descrizione.

### [!UICONTROL Tendenza delle dimensioni del pubblico] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_audiencesizetrend"
>title="Tendenza delle dimensioni del pubblico"
>abstract="Questo widget mostra il numero di profili contenuti nel pubblico, che viene inviato quotidianamente all’account di destinazione. Con il primo menu a discesa si regola il periodo di tempo per la tendenza del pubblico. Con il secondo menu a discesa del widget si seleziona il pubblico per l’analisi. La destinazione viene scelta dal menu a discesa della panoramica."

Il widget **[!UICONTROL Tendenza dimensione pubblico]** rappresenta la relazione del conteggio dei profili in un periodo di tempo per un pubblico mappato a tale account di destinazione. Il widget utilizza un grafico a linee per illustrare il numero di profili contenuti nel pubblico che vengono inviati quotidianamente all’account di destinazione.

È possibile regolare un periodo di tempo per la tendenza del pubblico negli ultimi 30 giorni, 90 giorni o 12 mesi utilizzando il primo menu a discesa.

Nel secondo menu a discesa sono elencati tutti i tipi di pubblico disponibili che possono essere inviati all’account di destinazione scelto nella parte superiore della dashboard.

![Widget tendenza dimensioni pubblico.](../images/destinations/audience-size-trend.png)

Il widget **[!UICONTROL Tendenza dimensione pubblico]** fornisce un pulsante [!UICONTROL Sottotitoli] in alto a destra del widget. Seleziona **[!UICONTROL Sottotitoli]** per aprire la finestra di dialogo Sottotitoli automatici. Un modello di apprendimento automatico genera automaticamente sottotitoli per descrivere le tendenze chiave e gli eventi importanti analizzando i dati del grafico e del pubblico.

![Finestra di dialogo dei sottotitoli automatici per il widget della tendenza delle dimensioni del pubblico.](../images/destinations/audience-size-trend-captions.png)

### [!UICONTROL Tipi di pubblico non mappati per identità] {#unmapped-audiences-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_unmappedsegmentsbyidentity"
>title="Tipi di pubblico non mappati per identità"
>abstract="Questo widget elenca i primi cinque tipi di pubblico **non mappati** classificati in base al conteggio delle identità decrescente per una determinata destinazione e identità. Gli ID dei filtri elencati nel menu a discesa del widget cambiano a seconda dell’account di destinazione selezionato nella parte superiore della pagina della panoramica."

Il widget **[!UICONTROL Tipi di pubblico non mappati per identità]** elenca i primi cinque tipi di pubblico **Non mappati** classificati in base al conteggio di identità decrescente per una determinata destinazione e identità. Evidenzia i tipi di pubblico più utili da mappare sull’account di destinazione scelto in base all’ID scelto.

Il menu a discesa ID destinazione filtra i tipi di pubblico disponibili. Gli ID filtro elencati nel menu a discesa cambiano a seconda dell’account di destinazione selezionato nella parte superiore della pagina della panoramica.

La colonna delle identità conta il numero di ID sorgente all’interno del pubblico che possono essere mappati all’ID scelto nel menu a discesa ID widget.

![Tipi di pubblico non mappati per widget di identità.](../images/destinations/unmapped-audiences-by-identity.png)

Consulta la sezione sui prerequisiti per le [definizioni dei termini utilizzati](#prerequisites) in questa descrizione.

### [!UICONTROL Tipi di pubblico mappati per identità] {#mapped-audiences-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedsegmentsbyidentity"
>title="Tipi di pubblico mappati per identità"
>abstract="Questo widget fornisce un elenco dei primi cinque tipi di pubblico **mappati**. L’elenco è in ordine decrescente in base al numero di ID di origine presenti nei tipi di pubblico. L’ID di destinazione da conteggiare viene selezionato dal menu a discesa sotto il titolo del widget. Gli ID di destinazione disponibili nel menu a discesa del widget dipendono dalla destinazione scelta nella parte superiore della dashboard della panoramica."

Questo widget fornisce un elenco dei primi cinque tipi di pubblico **mappati**. L’elenco è in ordine decrescente in base al numero di ID di origine presenti nei tipi di pubblico. L’ID di destinazione da conteggiare viene selezionato dal menu a discesa sotto il titolo del widget. Gli ID di destinazione disponibili dal menu a discesa nel widget cambieranno in base al filtro dell’account di destinazione scelto nella parte superiore della dashboard di panoramica.

![I tipi di pubblico mappati per widget di identità.](../images/destinations/mapped-audiences-by-identity.png)

Il widget **[!UICONTROL Tipi di pubblico mappati per identità]** evidenzia a colpo d&#39;occhio la probabilità di eseguire correttamente il targeting delle opportunità di profilo per una campagna nella destinazione scelta. Una campagna mirata efficiente non dipende dal numero di profili inviati alla destinazione, ma piuttosto dal numero di ID di origine che probabilmente verranno associati agli ID di destinazione, in modo da fornire dati utili e actionable.

### Segmenti di pubblico comuni {#common-audiences}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_commonaudiences"
>title="Segmenti di pubblico comuni"
>abstract="Questo widget fornisce un elenco dei primi cinque tipi di pubblico attivati nell’account di destinazione scelto nella parte superiore della pagina e la destinazione selezionata nel menu a discesa del widget. L’elenco dei tipi di pubblico viene ordinato in base a quanto recentemente sono stati attivati. Il pubblico attivato più recentemente viene visualizzato in alto."

Il widget **[!UICONTROL Tipi di pubblico comuni]** fornisce un elenco dei primi cinque tipi di pubblico attivati nell&#39;account di destinazione scelto nella parte superiore della pagina e la destinazione selezionata nel menu a discesa del widget. L’elenco dei tipi di pubblico viene ordinato in base a quanto recentemente sono stati attivati. Il pubblico attivato più recentemente viene visualizzato in alto.

La colonna [!UICONTROL AUDIENCE SIZE] fornisce il conteggio totale dei profili di ciascun pubblico elencato.

![Il widget Tipi di pubblico comuni.](../images/destinations/common-audiences.png)

### Tipi di pubblico mappato {#mapped-audiences}

Il widget [!UICONTROL Tipi di pubblico mappati] visualizza il numero totale di tipi di pubblico mappati che possono essere attivati nella destinazione selezionata nella parte superiore della pagina.

Seleziona **[!UICONTROL Tipi di pubblico]** per passare alla scheda [!UICONTROL Sfoglia] della dashboard Tipi di pubblico. In questa area di lavoro viene visualizzato un elenco di tutte le definizioni di segmenti per l’organizzazione.

![Widget dei tipi di pubblico mappati.](../images/destinations/mapped-audiences.png)

### Integrità del pubblico mappato {#mapped-audience-health}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedaudiencehealth"
>title="Integrità del pubblico mappato"
>abstract="Questo widget fornisce un elenco di massimo 20 tipi di pubblico mappati, il cui conteggio totale di profili si discosta di almeno un fattore di deviazione standard dalla dimensione media del pubblico mappata a tale destinazione nei 30 giorni. Fornisce una metrica calcolata per la dispersione delle dimensioni del pubblico dalla media degli ultimi 30 giorni. Le dimensioni del pubblico sono in ordine decrescente."

Il widget fornisce un elenco di un massimo di 20 tipi di pubblico mappati i cui conteggi totali dei profili, all’ultima istantanea giornaliera, si discostano di un fattore di almeno una deviazione standard dalla dimensione media del pubblico di 30 giorni mappata a quella destinazione.

In breve, fornisce una metrica calcolata per la dispersione delle dimensioni del pubblico dalla media negli ultimi 30 giorni. Confronta se la dimensione del pubblico di oggi è al di fuori della deviazione standard storica osservata nei dati degli ultimi 30 giorni.

Tutte le dimensioni del pubblico nel sistema sono ordinate da un pubblico di dimensioni elevate a uno di dimensioni inferiori, come indicato nella colonna [!UICONTROL DIMENSIONI PIÙ RECENTI].

Se il conteggio dei profili di pubblico mappati non rientra in una deviazione standard dalla dimensione media dei profili mappati negli ultimi 30 giorni, ciò indica un’anomalia nel sistema che deve essere esaminata.

Se un pubblico all&#39;interno del widget [!UICONTROL Integrità del pubblico mappato] si sta deviando di un ampio margine, è necessario fare riferimento al grafico di tendenza delle dimensioni del pubblico e individuare il pubblico anomalo. Questa tendenza può fornire ulteriori informazioni sullo stato di salute del pubblico.

>[!NOTE]
>
>La dimensione predefinita del widget Stato pubblico mappato può ostacolare le informazioni della tabella. Modifica le dimensioni del widget per migliorare la leggibilità dei nomi di pubblico e dei titoli di colonna mappati. Per istruzioni su [come ridimensionare un widget](../customize/modify.md), consulta la documentazione sulle dashboard di modifica.

![Widget di integrità del pubblico mappato.](../images/destinations/mapped-audience-health.png)

### [!UICONTROL Conteggio delle destinazioni] {#destinations-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_destinationscount"
>title="Conteggio delle destinazioni"
>abstract="Questo widget fornisce il numero totale di endpoint disponibili in cui un pubblico può essere attivato e consegnato all’interno del sistema. Questo numero include sia le destinazioni attive che quelle inattive."

Il widget [!UICONTROL Numero destinazioni] fornisce il numero totale di endpoint disponibili in cui un pubblico può essere attivato e distribuito all&#39;interno del sistema. Questo numero include sia le destinazioni attive che quelle inattive.

Sotto il conteggio totale, seleziona **[!UICONTROL Destinazioni]** per passare alla scheda Sfoglia destinazioni. In questa pagina sono elencate tutte le destinazioni con cui è stata stabilita una connessione fino a oggi.

![Widget conteggio destinazioni.](../images/destinations/destinations-count.png)

### [!UICONTROL Stato destinazione] {#destination-status}

Il widget [!UICONTROL Stato destinazione] visualizza il numero totale di destinazioni abilitate come una singola metrica e utilizza un grafico ad anello per illustrare la differenza proporzionale tra le destinazioni abilitate e disabilitate.

I conteggi individuali per le destinazioni abilitate o disabilitate vengono visualizzati in una finestra di dialogo quando il cursore passa sopra la rispettiva sezione del grafico ad anello.

![Widget dello stato di destinazione.](../images/destinations/destination-status.png)

### [!UICONTROL Destinazioni attive per piattaforma di destinazione] {#active-destinations-by-destination-platform}

Il widget fornisce una tabella a due colonne per mostrare un elenco di piattaforme di destinazione attive e il numero totale di destinazioni attive per ogni piattaforma di destinazione. L’elenco delle piattaforme di destinazione è ordinato da alto a basso.

![Destinazioni attive per widget piattaforma di destinazione.](../images/destinations/active-destinations-by-destination-platform.png)

### [!UICONTROL Tipi di pubblico attivati su tutte le destinazioni] {#activated-audiences-across-all-destinations}

Il widget [!UICONTROL Tipi di pubblico attivati su tutte le destinazioni] fornisce in un&#39;unica metrica il numero totale di tipi di pubblico attivati su tutte le destinazioni. Questo numero corrisponde all&#39;istantanea più recente.

![I tipi di pubblico attivati in tutti i widget delle destinazioni.](../images/destinations/activated-audiences-across-all-destinations.png)

Seleziona **[!UICONTROL Tipi di pubblico]** per passare alla scheda Destinazioni [!UICONTROL Sfoglia]. Questa pagina fornisce un elenco di tutte le destinazioni abilitate e una serie di metriche rilevanti. Per ulteriori informazioni, consulta la documentazione nella scheda [[!UICONTROL Sfoglia]](../../destinations/ui/destinations-workspace.md#browse).

Consulta la sezione sui prerequisiti per le [definizioni dei termini utilizzati](#prerequisites) in questa descrizione.

### [!UICONTROL Tipi di pubblico attivati] {#activated-audiences}

Questo widget fornisce una singola metrica per il numero totale di tipi di pubblico attivati in una destinazione.

![Widget tipi di pubblico attivati.](../images/destinations/activated-audiences.png)

Seleziona **[!UICONTROL Tipi di pubblico]** per passare alla pagina dei dettagli del dashboard delle destinazioni. Nella scheda [!UICONTROL Dati attivazione] viene visualizzato un elenco dei tipi di pubblico mappati sulla destinazione, inclusa la data di inizio e di fine (se applicabile) e altre informazioni rilevanti per l&#39;esportazione dei dati, come tipo di esportazione, pianificazione e frequenza. Per visualizzare i dettagli su un determinato pubblico, selezionarne il nome dalla colonna [!UICONTROL Nome pubblico].

![La pagina dei dettagli del dashboard delle destinazioni presenta la scheda Dati di attivazione evidenziata.](../images/destinations/activation-data-tab.png)

Questo widget consente di comprendere il valore delle destinazioni in base al numero di tipi di pubblico attivati immediatamente. Consente inoltre di accedere facilmente a informazioni più dettagliate per ulteriori analisi.

Consulta la sezione sui prerequisiti per le [definizioni dei termini utilizzati](#prerequisites) in questa descrizione.

## Passaggi successivi

Seguendo questo documento, ora dovresti essere in grado di individuare la dashboard delle destinazioni e comprendere le metriche visualizzate nei widget disponibili. Per ulteriori informazioni sull&#39;utilizzo delle destinazioni in Experience Platform, consulta la [documentazione sulle destinazioni](../../destinations/home.md).
