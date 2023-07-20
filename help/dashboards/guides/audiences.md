---
keywords: Experience Platform;profilo;pubblico;pubblico;segmentazione;interfaccia utente;personalizzazione;dashboard pubblico;dashboard
title: Guida al dashboard di Audiences
description: Adobe Experience Platform fornisce una dashboard attraverso la quale puoi visualizzare informazioni importanti sui tipi di pubblico creati dalla tua organizzazione.
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: f4f4deda02c96e567cbd0815783f192d1c54096c
workflow-type: tm+mt
source-wordcount: '2098'
ht-degree: 7%

---

# [!UICONTROL Tipi di pubblico] dashboard {#audiences-dashboard}

L’interfaccia utente di Adobe Experience Platform fornisce una dashboard attraverso la quale puoi visualizzare informazioni importanti sui tipi di pubblico, acquisite durante un’istantanea giornaliera. Questa guida illustra come accedere e utilizzare [!UICONTROL Tipi di pubblico] nell’interfaccia utente e fornisce ulteriori informazioni sulle visualizzazioni visualizzate nel dashboard.

Per una panoramica di tutte le funzioni del servizio di segmentazione di Adobe Experience Platform nell’interfaccia utente di Platform, visita [Guida dell’interfaccia utente di Segmentation Service](../../segmentation/ui/overview.md).

## [!UICONTROL Tipi di pubblico] dati dashboard

Il [!UICONTROL Tipi di pubblico] Nel dashboard viene visualizzata un’istantanea dei dati attributo (record) di cui dispone la tua organizzazione nell’archivio profili di Experience Platform. Lo snapshot non include dati di eventi (serie temporali).

I dati attributo nello snapshot mostrano i dati esattamente come vengono visualizzati nel momento specifico in cui lo snapshot è stato creato. In altre parole, l&#39;istantanea non è un&#39;approssimazione o un campione dei dati e [!UICONTROL Tipi di pubblico] il dashboard non viene aggiornato in tempo reale.

>[!NOTE]
>
>Eventuali modifiche o aggiornamenti apportati ai dati dal momento in cui è stata acquisita l’istantanea non verranno riflessi nel dashboard fino all’acquisizione dell’istantanea successiva.

## Esplora [!UICONTROL Tipi di pubblico] dashboard {#explore}

Per passare al [!UICONTROL Tipi di pubblico] nell’interfaccia utente di Platform, seleziona **[!UICONTROL Tipi di pubblico]** nella barra a sinistra, seleziona quindi **[!UICONTROL Panoramica]** per visualizzare il dashboard.

>[!NOTE]
>
>Se la tua organizzazione non utilizza ancora Platform e non dispone ancora di set di dati di profilo attivi o criteri di unione creati, il [!UICONTROL Tipi di pubblico] dashboard non visibile. Al contrario, [!UICONTROL Panoramica] Nella scheda vengono visualizzati collegamenti e documentazione per aiutarti a iniziare a utilizzare la segmentazione.

![Il [!UICONTROL Tipi di pubblico] dashboard [!UICONTROL Panoramica] scheda con [!UICONTROL Tipi di pubblico] e [!UICONTROL Panoramica] evidenziato.](../images/audiences/dashboard-overview.png)

### Modifica il [!UICONTROL Tipi di pubblico] dashboard {#modify}

È possibile modificare l&#39;aspetto del [!UICONTROL Tipi di pubblico] dashboard selezionando **[!UICONTROL Modifica dashboard]**. Questo consente di spostare, aggiungere e rimuovere widget dal dashboard, nonché di accedere al **[!UICONTROL Libreria widget]** per esplorare i widget disponibili e creare widget personalizzati per la tua organizzazione.

Consulta la sezione [modifica delle dashboard](../customize/modify.md) e [Panoramica della libreria dei widget](../customize/widget-library.md) per ulteriori informazioni.

### Aggiungi widget {#add-widget}

Seleziona **[!UICONTROL Aggiungi widget]** per passare alla libreria widget e visualizzare un elenco dei widget disponibili da aggiungere al dashboard.

![Il [!UICONTROL Tipi di pubblico] panoramica della dashboard con [!UICONTROL Aggiungi widget] evidenziato.](../images/audiences/audiences-overview-add-widget.png)

Dalla libreria dei widget, puoi sfogliare la selezione di widget di pubblico standard e personalizzati. Per informazioni su come aggiungere widget, consulta la documentazione della libreria di widget su come [aggiungi un widget](../customize/widget-library.md#add-widgets).

## Selezionare un pubblico {#select-audience}

Il dashboard seleziona automaticamente un pubblico da visualizzare. Tuttavia, puoi modificare il pubblico utilizzando il menu a discesa o il selettore del pubblico.

Per scegliere un pubblico diverso, seleziona il menu a discesa accanto al nome del pubblico oppure utilizza il selettore del pubblico per aprire la finestra di dialogo di selezione del pubblico.

>[!IMPORTANT]
>
>Nell’elenco dei tipi di pubblico selezionabili vengono visualizzati solo i tipi di pubblico con un conteggio di profili superiore a zero.

![Panoramica della dashboard Tipi di pubblico con il menu a discesa Pubblico globale evidenziato.](../images/audiences/change-audience.png)

![Il [!UICONTROL Seleziona pubblico] finestra di dialogo che visualizza tutti i tipi di pubblico disponibili.](../images/audiences/select-audience-dialog.png)

## Widget e metriche {#widgets-and-metrics}

Il [!UICONTROL Tipi di pubblico] la dashboard è composta da widget, metriche di sola lettura che forniscono informazioni importanti sul pubblico selezionato.

La data e l&#39;ora dell&#39;istantanea più recente vengono visualizzate nella parte superiore della [!UICONTROL Panoramica] accanto al menu a discesa del pubblico. Tutti i dati del widget sono accurati a partire da quella data e ora. Il timestamp dell’istantanea viene fornito in UTC; non si trova nel fuso orario del singolo utente o organizzazione.

![La scheda Panoramica tipi di pubblico con una marca temporale widget evidenziata.](../images/audiences/widget-timestamp.png)

## Widget standard {#standard-widgets}

Adobe fornisce più widget standard che puoi utilizzare per visualizzare diverse metriche relative ai tipi di pubblico. Puoi anche creare widget personalizzati da condividere con la tua organizzazione utilizzando [!UICONTROL Libreria widget]. Per ulteriori informazioni sulla creazione di widget personalizzati, leggere [Panoramica della libreria dei widget](../customize/widget-library.md).

Per ulteriori informazioni su ciascuno dei widget standard disponibili, selezionare il nome di un widget dall&#39;elenco seguente:

* [[!UICONTROL Dimensione del pubblico]](#audience-size)
* [[!UICONTROL Ordine di attivazione pubblico]](#audience-activation-order)
* [[!UICONTROL Tendenza delle dimensioni del pubblico]](#audience-size-trend)
* [[!UICONTROL Tendenza di modifica della dimensione del pubblico]](#audience-size-change-trend)
* [[!UICONTROL Tendenza dimensione pubblico per identità]](#audience-size-trend-by-identity)
* [[!UICONTROL Sovrapposizione del pubblico]](#audience-overlap)
* [[!UICONTROL Rapporto di sovrapposizione pubblico]](#audience-overlap-report)
* [[!UICONTROL Sovrapposizione di identità]](#identity-overlap)
* [[!UICONTROL Profili per identità]](#profiles-by-identity)
* [[!UICONTROL Attivazioni pianificate]](#scheduled-activations)

### [!UICONTROL Dimensione del pubblico] {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesize"
>title="Dimensione del pubblico"
>abstract="Questo widget visualizza il numero totale di profili uniti all’interno del pubblico selezionato. Questo numero dipende dal criterio di unione applicato ai dati ed è esatto al momento dello snapshot più recente."

Il **[!UICONTROL Dimensione pubblico]** widget mostra il numero totale di profili uniti nel pubblico selezionato al momento dello scatto dell’istantanea. Questo numero è il risultato dell’applicazione del criterio di unione del pubblico ai dati del profilo per unire i frammenti di profilo e formare un singolo profilo per ogni individuo nel pubblico.

Per ulteriori informazioni su frammenti e profili uniti, consulta [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

![Il [!UICONTROL Tipi di pubblico] panoramica della dashboard con [!UICONTROL Dimensione pubblico] widget evidenziato.](../images/audiences/audience-size.png)

### [!UICONTROL Tendenza delle dimensioni del pubblico] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="Tendenza delle dimensioni del pubblico"
>abstract="Questo widget fornisce informazioni sul numero totale di profili che soddisfano i criteri di **qualsiasi** definizione del segmento, acquisito durante lo snapshot giornaliero, per gli ultimi 30 giorni, 90 giorni o 12 mesi."

Il **[!UICONTROL Tendenza dimensione pubblico]** Il widget fornisce un’illustrazione del grafico a linee per il numero totale di profili idonei per **qualsiasi** pubblico in un determinato periodo di tempo. La tendenza della dimensione del pubblico può essere visualizzata in periodi di 30 giorni, 90 giorni e 12 mesi. Il periodo di tempo viene scelto da un menu a discesa nel widget. La dimensione del pubblico si riflette sull’asse y e il tempo sull’asse x.

Questo widget include anche il [!UICONTROL Sottotitoli] funzionalità in cui un modello di apprendimento automatico analizza il grafico e i dati del pubblico e genera automaticamente sottotitoli per descrivere le tendenze chiave e gli eventi importanti. Seleziona **[!UICONTROL Sottotitoli]** per aprire la finestra di dialogo sottotitoli automatici.

![Il [!UICONTROL Tipi di pubblico] In panoramica viene visualizzato il widget tendenza dimensione pubblico.](../images/audiences/audience-size-trend-captions.png)

Viene visualizzata la finestra di dialogo Didascalie automatiche che fornisce informazioni approfondite sui dati.

![La finestra di dialogo dei sottotitoli automatici per il widget tendenza dimensione pubblico.](../images/audiences/audience-size-trend-automatic-captions-dialog.png)

Per ulteriori informazioni sulla valutazione dei tipi di pubblico e su come i profili si qualificano per i tipi di pubblico e su come uscirne, consulta [Documentazione del servizio di segmentazione](../../segmentation/home.md).

### [!UICONTROL Tendenza di modifica della dimensione del pubblico] {#audience-size-change-trend}

Questo widget fornisce un grafico a linee che illustra la differenza nel numero totale di profili idonei per un determinato pubblico tra le istantanee giornaliere più recenti. Il pubblico scelto per l’analisi viene selezionato dal menu a discesa Panoramica. Il periodo di analisi delle tendenze può essere visualizzato in periodi di 30 giorni, 90 giorni e 12 mesi. Il periodo di tempo viene scelto da un menu a discesa nel widget. La dimensione del pubblico si riflette sull’asse y e il tempo sull’asse x.

![Il widget tendenza modifica dimensione pubblico.](../images/audiences/audience-size-change-trend.png)

### [!UICONTROL Tendenza dimensione pubblico per identità] {#audience-size-trend-by-identity}

Questo widget illustra la tendenza delle dimensioni del pubblico per un particolare pubblico in base al tipo di identità scelto dal menu a discesa del widget. Il pubblico utilizzato per l’analisi viene selezionato dal menu a discesa Panoramica. Il periodo di analisi delle tendenze può essere visualizzato in periodi di 30 giorni, 90 giorni e 12 mesi. Il periodo di tempo viene scelto da un menu a discesa nel widget.

![La tendenza della dimensione del pubblico per widget di identità.](../images/audiences/audience-size-trend-by-identity.png)

### [!UICONTROL Ordine di attivazione pubblico] {#audience-activation-order}

Il [!UICONTROL Ordine di attivazione pubblico] il widget fornisce una tabella a tre colonne che elenca il nome della destinazione, la piattaforma e la data di attivazione del pubblico. L’elenco è ordinato da alto a basso in base all’attualità e può contenere fino a 10 righe.

![Il widget dell&#39;ordine di attivazione del pubblico.](../images/audiences/audience-activation-order.png)

### [!UICONTROL Sovrapposizione del pubblico] {#audience-overlap}

Questo widget utilizza un diagramma di Venn per visualizzare il numero di persone che corrispondono ai criteri per entrambi i tipi di pubblico. I tipi di pubblico utilizzati per il confronto vengono selezionati dai menu a discesa dei widget. Il numero totale di profili all’interno della definizione del segmento pertinente può essere visualizzato passando il cursore sopra un cerchio o nell’intersezione del diagramma di Venn.

Questo widget consente di ottimizzare la strategia di segmentazione visualizzando le somiglianze nei risultati delle definizioni dei segmenti.

![Il widget di sovrapposizione pubblico.](../images/audiences/audience-overlap.png)

### [!UICONTROL Rapporto di sovrapposizione pubblico] {#audience-overlap-report}

Questo widget tabula i dati di sovrapposizione profilo per un pubblico specifico. Per il pubblico scelto dal menu a discesa nella parte superiore dello schermo viene fornito un elenco di cinque tipi di pubblico, classificati dalla percentuale di sovrapposizione più alta a quella più bassa. Per maggiore chiarezza, il pubblico scelto è elencato in [!UICONTROL NOME DEL PUBBLICO] colonna. L’analisi della sovrapposizione dei tipi di pubblico viene fornita per il secondo pubblico elencato in [!UICONTROL NOME PUBBLICO B] colonna. La sovrapposizione percentuale è indicata nella terza colonna con precisione di dodici cifre decimali.

Il rapporto di sovrapposizione del pubblico consente di creare nuovi tipi di pubblico ad alte prestazioni. Osservare percentuali di sovrapposizione elevate consente di eliminare i tipi di pubblico e impedire l’invio dello stesso pubblico a destinazioni diverse. Inoltre, ti aiutano a identificare informazioni nascoste che potrebbero essere utili per una migliore segmentazione. Una sovrapposizione in percentuale bassa consente di individuare profili univoci da perseguire.

Seleziona **[!UICONTROL Visualizza altro]** per aprire una finestra di dialogo a schermo intero che contiene più dati di sovrapposizione del pubblico.

![Il widget del rapporto di sovrapposizione pubblico con Visualizza più evidenziato.](../images/audiences/audience-overlap-report.png)

Il [!UICONTROL Rapporto di sovrapposizione pubblico] viene visualizzata. Questa finestra di dialogo può contenere fino a 50 righe di analisi di sovrapposizione del pubblico suddivise in sei colonne. Seleziona l’icona delle impostazioni (![Icona delle impostazioni.](../images/audiences/settings-icon.png)) per rimuovere o aggiungere colonne dalla tabella.

![Finestra di dialogo Rapporto di sovrapposizione pubblico.](../images/audiences/audience-overlap-report-dialog.png)

>[!NOTE]
>
>Seleziona la **[!UICONTROL Sovrapposizione]** intestazione di colonna per modificare la classificazione dei risultati dal livello più alto a quello più basso o dal livello più basso a quello più alto.

Per scaricare l&#39;intero report in formato PDF, selezionare il menu delle opzioni (**`...`**) seguito da **[!UICONTROL Scarica]**.

![Viene evidenziata la finestra di dialogo Rapporto di sovrapposizione pubblico con i puntini di sospensione e l’opzione Scarica.](../images/audiences/audience-overlap-report-dialog-download.png)

Selezionare una riga dal report per aprire un diagramma di Venn dell&#39;analisi di sovrapposizione. Passa il puntatore del mouse su una sezione del diagramma di Venn per visualizzare il conteggio dei profili in una finestra di dialogo.

![La finestra di dialogo Rapporto di sovrapposizione pubblico presenta un diagramma di Venn ed è evidenziata una riga.](../images/audiences/audience-overlap-report-dialog-venn.png)

Seleziona **[!UICONTROL Chiudi]** per tornare al [!UICONTROL Tipi di pubblico] dashboard.

### [!UICONTROL Sovrapposizione di identità] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="Sovrapposizione di identità"
>abstract="Questo widget mostra la sovrapposizione di profili nel pubblico contenente entrambe le identità selezionate. I cerchi mostrano la dimensione relativa di ogni identità. Il numero di profili contenenti entrambi gli spazi dei nomi è rappresentato dalla sovrapposizione tra i cerchi."

Il **[!UICONTROL Sovrapposizione identità]** Un widget mostra un diagramma di Venn, o diagramma di set, che mostra la sovrapposizione di profili nel pubblico contenenti più identità.

Utilizza i menu a discesa sul widget per selezionare le identità che desideri confrontare. I cerchi visualizzano la dimensione relativa di ciascuna identità scelta, con il numero di profili contenenti entrambi gli spazi dei nomi rappresentato dalla dimensione della sovrapposizione tra i cerchi.

Se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente verranno associate più identità. Questa situazione rende probabile che la tua organizzazione disponga di più profili contenenti frammenti di più identità.

Per ulteriori informazioni sulle identità, visita il [Documentazione del servizio Identity](../../identity-service/home.md).

![Il [!UICONTROL Tipi di pubblico] panoramica del dashboard con widget di sovrapposizione identità evidenziato.](../images/audiences/identity-overlap.png)

### [!UICONTROL Profili per identità] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="Profili per identità"
>abstract="Questo widget visualizza il raggruppamento delle identità per ogni profilo unito nel pubblico selezionato."

Il **[!UICONTROL Profili per identità]** il widget mostra il raggruppamento delle identità per ogni profilo unito nel pubblico selezionato. Il numero totale di profili per identità potrebbe essere maggiore del numero totale di profili nel pubblico, perché a un profilo potrebbero essere associate più identità. In altre parole, la somma dei valori mostrati per ogni identità può superare la dimensione totale del pubblico. Questo perché se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente possono essere associate più identità.

Seleziona **[!UICONTROL Sottotitoli]** per aprire la finestra di dialogo sottotitoli automatici.

![Il [!UICONTROL Tipi di pubblico] panoramica della dashboard con l’opzione Profili per widget identità e Didascalie evidenziata.](../images/audiences/profiles-by-identity.png)

Un modello di apprendimento automatico genera automaticamente informazioni sui dati analizzando la distribuzione complessiva e le dimensioni chiave dei dati.

Per ulteriori informazioni sulle identità, visita il [Documentazione del servizio Identity](../../identity-service/home.md).

### Attivazioni pianificate {#scheduled-activations}

Il [!UICONTROL Attivazioni pianificate] Il widget fornisce una vista in forma di tabella delle destinazioni attivate più di recente. La tabella include la piattaforma di destinazione, il nome del flusso di attivazione verso questa destinazione e la data di inizio e di fine dell’attivazione per il pubblico selezionato. Se non è stata specificata una data di fine per l’attivazione, viene visualizzato come [!UICONTROL In corso]. Il pubblico per l’analisi viene selezionato dal menu a discesa nella parte superiore della pagina.

Il widget consente di scoprire subito dove e quando il pubblico viene attivato e rende più trasparenti le attivazioni duplicate o non necessarie. Queste informazioni accumulate evidenziano anche dove sono state escluse eventuali attivazioni.

![Il widget Attivazioni pianificate.](../images/audiences/scheduled-activations.png)

## Passaggi successivi

Seguendo questo documento dovresti essere in grado di individuare [!UICONTROL Tipi di pubblico] e selezionare un pubblico da visualizzare. Dovresti anche comprendere le metriche visualizzate nei widget disponibili. Per ulteriori informazioni sull’utilizzo dei tipi di pubblico nell’interfaccia utente di Experience Platform, consulta [Guida dell’interfaccia utente di Segmentation Service](../../segmentation/ui/overview.md).
