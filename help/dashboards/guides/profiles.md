---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;interfaccia utente;personalizzazione;dashboard profilo;profilo;profile;real-time customer profile;user interface;UI;customization;profile dashboard;dashboard
title: Dashboard dei profili
description: Adobe Experience Platform fornisce una dashboard attraverso la quale puoi visualizzare informazioni importanti sui dati Real-Time Customer Profile della tua organizzazione.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '4997'
ht-degree: 9%

---

# [!UICONTROL Profili] dashboard

L&#39;interfaccia utente di Adobe Experience Platform fornisce un dashboard attraverso il quale è possibile visualizzare informazioni importanti sui dati di [!DNL Real-Time Customer Profile] acquisiti durante uno snapshot giornaliero. Questa guida illustra come accedere e utilizzare il dashboard Profili nell’interfaccia utente di e fornisce informazioni sulle metriche visualizzate nel dashboard.

Consulta la [Guida all&#39;interfaccia utente del profilo cliente in tempo reale](../../profile/ui/user-guide.md) per una panoramica delle funzioni di profilo nell&#39;interfaccia utente di Experience Platform.

## Dati dashboard profilo

Nel dashboard Profili viene visualizzata un’istantanea dei dati attributo (record) di cui dispone la tua organizzazione nell’archivio Profili di Experience Platform. Lo snapshot non include dati di eventi (serie temporali).

I dati attributo nello snapshot mostrano i dati esattamente come vengono visualizzati nel momento specifico in cui lo snapshot è stato creato. In altre parole, l’istantanea non è un’approssimazione o un esempio dei dati e il dashboard Profilo non viene aggiornato in tempo reale.

>[!NOTE]
>
>Eventuali modifiche o aggiornamenti apportati ai dati dal momento in cui è stata acquisita l’istantanea non verranno riflessi nel dashboard fino all’acquisizione dell’istantanea successiva.

## Esplorare il dashboard Profili {#explore-dashboard}

Per passare al dashboard Profili nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Profili]** nella barra a sinistra, quindi seleziona la scheda **[!UICONTROL Panoramica]** per visualizzare il dashboard.

>[!NOTE]
>
>Se la tua organizzazione ha poca esperienza con Platform e non dispone ancora di set di dati di profilo attivi o criteri di unione creati, il dashboard Profili non è visibile. Nella scheda [!UICONTROL Panoramica] sono invece visualizzati collegamenti e documentazione per aiutarti a iniziare a utilizzare Profilo cliente in tempo reale.

![Dashboard dei profili di Experience Platform con profili e panoramica evidenziati.](../images/profiles/dashboard-overview.png)

### Modificare il dashboard Profili {#modify-dashboard}

È possibile modificare l&#39;aspetto del dashboard Profili selezionando **[!UICONTROL Modifica dashboard]**. Puoi spostare, aggiungere, ridimensionare e rimuovere widget dal dashboard, nonché accedere alla **[!UICONTROL Libreria widget]** per esplorare i widget disponibili e creare widget personalizzati per la tua organizzazione.

Per ulteriori informazioni, consulta la documentazione [modifica dashboard](../customize/modify.md) e [Panoramica della libreria Widget](../customize/widget-library.md).

### Aggiungi widget {#add-widget}

Seleziona **[!UICONTROL Aggiungi widget]** per passare alla libreria di widget e visualizzare un elenco dei widget disponibili da aggiungere al dashboard.

![Panoramica del dashboard Profili con l&#39;opzione Aggiungi widget evidenziata.](../images/profiles/profiles-overview-add-widget.png)

Dalla libreria dei widget è possibile sfogliare la selezione di widget di pubblico standard e personalizzati. Per informazioni su come aggiungere widget, consulta la documentazione della libreria di widget su come [aggiungere un widget](../customize/widget-library.md#add-widgets).

### Visualizza SQL {#view-sql}

Puoi visualizzare il codice SQL che genera le informazioni visualizzate nel tuo dashboard con un interruttore nell&#39;area di lavoro [!UICONTROL Panoramica]. Puoi trarre ispirazione dall’SQL delle informazioni esistenti per creare nuove query che derivano informazioni univoche dai dati di Platform in base alle esigenze aziendali. Per ulteriori informazioni su questa funzionalità, vedere la [Guida dell&#39;interfaccia utente SQL](../view-sql.md).

<!-- ## (Beta) Profile efficacy insights {#profile-efficacy-insights}

>[!IMPORTANT]
>
>The profile efficacy insight functionality is currently in beta and are not available to all users. The documentation and the functionality are subject to change.

The [!UICONTROL Efficacy] tab provides metrics on the quality and completeness of your profile data through the use of profile efficacy widgets. These widgets illustrate at a glance the composition of your profiles, trends in completeness over time, and assessments on the quality of your profile data.

![The profile efficacy dashboard.](../images/profiles/attributes-quality-assessment.png)

See the [profile efficacy widgets section](#profile-efficacy-widgets) for more information on the widgets currently available.

The layout of this dashboard is also customizable by selecting [**[!UICONTROL Modify dashboard]**](../customize/modify.md) from the [!UICONTROL Overview] tab. -->

## Sfoglia profili {#browse-profiles}

La scheda [!UICONTROL Sfoglia] consente di cercare e visualizzare i profili di sola lettura acquisiti nell&#39;organizzazione. Da qui puoi vedere informazioni importanti appartenenti al profilo sulle loro preferenze, eventi passati, interazioni e tipi di pubblico.

## Dettagli profilo {#profile-details}

Per aprire l&#39;area di lavoro [!UICONTROL Profili] [!UICONTROL Dettagli], selezionare un [!UICONTROL ID profilo] dall&#39;elenco.

![Scheda Sfoglia profili con ID profilo evidenziato.](../images/profiles/profile-id.png)

Nell&#39;area di lavoro [!UICONTROL Profili] [!UICONTROL Dettagli] sono visualizzati diversi widget preconfigurati che trasmettono informazioni specifiche del profilo. Queste informazioni consentono di comprendere rapidamente gli attributi chiave del profilo. Puoi anche personalizzare l&#39;area di lavoro [!UICONTROL Profili] [!UICONTROL Dettagli] creando widget personalizzati. Per ulteriori dettagli, consulta la sezione su [come aggiungere widget](#add-widgets).

![L&#39;area di lavoro [!UICONTROL Profili] [!UICONTROL Dettagli] con la scheda [!UICONTROL Dettagli] evidenziata.](../images/profiles/profile-details-workspace.png)

### Widget dettagli profilo {#widgets}

I widget dei dettagli del profilo preconfigurati sono i seguenti:

#### Profilo cliente {#customer-profile}

Il widget [!UICONTROL Profilo cliente] visualizza il nome e il cognome dell&#39;utente associato al profilo, nonché il relativo [!UICONTROL ID profilo]. Un ID profilo è un identificatore generato automaticamente associato a un tipo di identità e rappresenta un profilo. Per ulteriori informazioni sulle identità e sugli spazi dei nomi delle identità, consulta la [panoramica sulle identità](../../rtcdp/profile/identities-overview.md).

![Widget del profilo cliente.](../images/profiles/customer-profile.png)

#### Attributi di base {#basic-attributes}

Il widget [!UICONTROL Attributi di base] visualizza gli attributi più comunemente utilizzati per definire un singolo profilo.

![Widget attributi di base.](../images/profiles/basic-attributes.png)

#### Identità collegate {#linked-identities}

Il widget [!UICONTROL Identità collegate] visualizza tutte le altre identità associate al profilo.

Per visualizzare i dettagli delle identità del profilo in modo più approfondito e passare all&#39;area di lavoro [!UICONTROL Identità], selezionare **[!UICONTROL Visualizza grafico identità]**.

![Widget identità collegate.](../images/profiles/linked-identities.png)

#### Preferenze canale {#channel-preferences}

Il widget [!UICONTROL Preferenze canale] visualizza i canali di comunicazione da cui l&#39;utente ha acconsentito a ricevere comunicazioni. Un segno di spunta indica ogni canale da cui l’utente ha acconsentito a ricevere comunicazioni.

<!-- image needs a blue tick added below -->

![Widget preferenze canale.](../images/profiles/channel-preferences.png)

Il consenso del cliente e le preferenze di contatto sono argomenti complessi. Per scoprire come raccogliere, elaborare e filtrare le preferenze di consenso e contesto in questo Experience Platform, ti consigliamo di leggere i seguenti documenti:

* Per informazioni sui gruppi di campi dello schema necessari per [raccogliere i dati sul consenso in base allo standard Adobe](../../landing/governance-privacy-security/consent/adobe/overview.md), consulta la documentazione su questi gruppi di campi dello schema abilitati per il profilo.
   * [[!UICONTROL Dettagli su consenso e preferenze]](../../xdm/field-groups/profile/consents.md)
   * [[!UICONTROL IdentityMap]](../../xdm/field-groups/profile/identitymap.md) (richiesto se si utilizza Platform Web SDK o Mobile SDK per inviare segnali di consenso)
* Per informazioni su come elaborare i dati relativi al consenso e alle preferenze del cliente utilizzando lo standard Adobe, consulta la panoramica sull&#39;elaborazione del consenso [nell&#39;Experience Platform](../../landing/governance-privacy-security/consent/adobe/overview.md).
* È possibile utilizzare una governance dei dati e un criterio di consenso combinati per filtrare i profili per la segmentazione in base alle loro preferenze di consenso e alle regole organizzative stabilite. Per informazioni su come creare e utilizzare questi criteri combinati, consulta la guida utente su [gestione dei criteri di utilizzo dei dati](../../data-governance/policies/user-guide.md#combine-policies).

### Aggiungi widget {#add-widgets}

Per aggiungere widget personalizzati all&#39;area di lavoro [!UICONTROL Profili] [!UICONTROL Dettagli], selezionare **[!UICONTROL Personalizza dettagli profilo]**.

![Area di lavoro Dettagli profili con [!UICONTROL Dettagli profilo personalizzati] evidenziati.](../images/profiles/customize-profile-details.png)

Ora potete modificare l&#39;area di lavoro ridimensionando o riposizionando i widget. Seleziona **[!UICONTROL Aggiungi widget]** per creare un widget con attributi personalizzati.

![L&#39;area di lavoro [!UICONTROL Dettagli] dei profili con [!UICONTROL Aggiungi widget] evidenziato.](../images/profiles/add-widget.png)

Viene visualizzato il creatore del widget. Immetti un nome descrittivo per il widget nel campo di testo [!UICONTROL Titolo scheda] e seleziona **[!UICONTROL Aggiungi attributi]**.

![Area di lavoro di creazione widget con il campo [!UICONTROL Titolo scheda] e [!UICONTROL Aggiungi attributi] evidenziati.](../images/profiles/widget-creator.png)

Viene visualizzata una finestra di dialogo che contiene una visualizzazione dello schema di unione del profilo. Utilizza il campo di ricerca o scorri per trovare gli attributi sui quali desideri creare rapporti con il tuo widget. Selezionare la casella di controllo per gli attributi che si desidera includere. Seleziona **[!UICONTROL Seleziona]** per continuare il flusso di lavoro di creazione.

>[!TIP]
>
>Una selezione della casella di controllo di primo livello include tutti gli elementi figlio.

![Il diagramma schema di unione con la casella di controllo dell&#39;attributo fedeltà e [!UICONTROL Seleziona] evidenziati.](../images/profiles/union-schema-attributes.png)

Nell’area di lavoro viene visualizzata un’anteprima del widget completato. Quando sei soddisfatto degli attributi scelti, seleziona **[!UICONTROL Salva]** per confermare le scelte e tornare all&#39;area di lavoro [!UICONTROL Profili] [!UICONTROL Dettagli]. Il widget appena creato è ora visibile nell’area di lavoro.

![L&#39;area di lavoro di creazione del widget con Salva evidenziato e visualizzazione dell&#39;anteprima del widget.](../images/profiles/widget-preview.png)

## Criteri di unione {#merge-policies}

Le metriche visualizzate nel dashboard Profili sono basate su criteri di unione applicati ai dati Profilo cliente in tempo reale. Quando i dati vengono riuniti da più origini per creare il profilo cliente, i dati possono contenere valori in conflitto. Ad esempio, un set di dati può elencare un cliente come &quot;singolo&quot;, mentre un altro set di dati può elencare il cliente come &quot;sposato&quot;. È compito del criterio di unione determinare quali dati assegnare la priorità e visualizzare come parte del profilo.

Per ulteriori informazioni sui criteri di unione, tra cui come creare, modificare e dichiarare un criterio di unione predefinito per l&#39;organizzazione, fare riferimento alla [panoramica dei criteri di unione](../../profile/merge-policies/overview.md).

Il dashboard seleziona automaticamente un criterio di unione da utilizzare. Il criterio di unione applicato può essere modificato utilizzando il menu a discesa accanto al nome del criterio di unione.

>[!NOTE]
>
>Il menu a discesa mostra solo i criteri di unione che utilizzano lo schema `_xdm.context.profile`. Tuttavia, se l’organizzazione ha creato più criteri di unione, potrebbe essere necessario scorrere per visualizzare l’elenco completo dei criteri di unione disponibili.

![Scheda Panoramica profili con elenco a discesa dei criteri di unione evidenziato.](../images/profiles/select-merge-policy.png)

## Schemi di unione

Il dashboard [!UICONTROL Schema unione] visualizza lo schema di unione per una classe XDM specifica. Selezionando il menu a discesa **[!UICONTROL Classe]**, puoi visualizzare gli schemi di unione per diverse classi XDM.

Gli schemi di unione sono composti da più schemi che condividono la stessa classe e sono stati abilitati per Profilo. Consentono di visualizzare in un&#39;unica vista, una combinazione di ogni campo contenuto all&#39;interno di ogni schema che condivide la stessa classe.

Per ulteriori informazioni sulla [visualizzazione degli schemi di unione nell&#39;interfaccia utente di Platform](../../profile/ui/union-schema.md#view-union-schemas), consulta la guida dell&#39;interfaccia utente dello schema di unione.

## Widget e metriche

La dashboard è composta da widget, metriche di sola lettura che forniscono informazioni importanti sui dati del profilo.

La data e l&#39;ora dello snapshot più recente vengono visualizzate nella parte superiore della scheda [!UICONTROL Panoramica] accanto al menu a discesa dei criteri di unione. Tutti i dati del widget sono accurati a partire da quella data e ora. Il timestamp dell’istantanea viene fornito in UTC; non si trova nel fuso orario del singolo utente o organizzazione.

![Scheda Panoramica del dashboard Profili con il timestamp dell&#39;istantanea più recente evidenziato.](../images/profiles/snapshot-timestamp.png)

## Widget predefiniti {#default-widgets}

Per tutte le nuove istanze di Adobe Experience Platform viene fornito un widget predefinito che evidenzia le informazioni più recenti disponibili dai dati. I seguenti widget sono preconfigurati nella vista dei segmenti fin dall’inizio. Per informazioni complete sullo scopo e la funzione dei widget, vedi sotto.

* [[!UICONTROL Conteggio dei profili]](#profile-count)
* [[!UICONTROL Modifica del conteggio dei profili]](#profile-count-change)
* [[!UICONTROL Tendenza di modifica del conteggio dei profili]](#profiles-count-change-trend)
* [[!UICONTROL Profili per identità]](#profiles-by-identity)
* [[!UICONTROL Sovrapposizione di identità]](#identity-overlap)

>[!NOTE]
>
>A partire dal 26 luglio 2023, le dashboard di panoramica [!UICONTROL Profili], [!UICONTROL Tipi di pubblico] e [!UICONTROL Destinazioni] sono state reimpostate su un nuovo widget predefinito per tutti gli utenti che non hanno modificato le proprie visualizzazioni nei sei mesi precedenti. Consulta la documentazione nelle sezioni widget predefiniti [Destinazioni](./destinations.md#default-widgets) e [Tipi di pubblico](./audiences.md#default-widgets) per informazioni dettagliate sui widget inclusi come parte dei caricamenti di widget predefiniti. Puoi continuare a personalizzare i widget del dashboard come prima.

## Widget di IA per l’analisi dei clienti {#customer-ai-profiles-widgets}

Customer AI viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su grande scala. IA per l&#39;analisi dei clienti esegue l&#39;operazione analizzando i dati esistenti di Consumer Experience Event per prevedere **punteggi di propensione all&#39;abbandono o alla conversione**. Questi modelli di propensione dei clienti ad alta precisione consentono segmentazione e targeting più precisi. Le informazioni di [distribuzione dei punteggi](#customer-ai-distribution-of-scores) e di [riepilogo del punteggio](#customer-ai-scoring-summary) dimostrano la divisione del pubblico. Evidenzia quali profili hanno una propensione elevata/bassa/media e come sono distribuiti nei conteggi dei profili.

* [[!UICONTROL Riepilogo punteggio di AI per l’analisi dei clienti]](#customer-ai-scoring-summary)
* [[!UICONTROL Distribuzione dei punteggi in IA per l’analisi dei clienti]](#customer-ai-distribution-of-scores)

### [!UICONTROL Distribuzione dei punteggi in IA per l’analisi dei clienti] {#customer-ai-distribution-of-scores}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_distributionOfScores"
>title="Distribuzione dei punteggi"
>abstract="Questo widget mostra la distribuzione del numero totale di profili in base ai punteggi di propensione, con incrementi del 5%. La distribuzione del conteggio dei profili è determinata dal modello di IA e dal criterio di unione selezionati. Puoi modificare il modello di IA dal menu a discesa sotto il titolo del widget."

Il widget [!UICONTROL Distribuzione dei punteggi di IA per l&#39;analisi dei clienti] categorizza il numero totale di profili in base ai punteggi di tendenza. La distribuzione del conteggio dei profili è determinata dal modello di IA e dal criterio di unione selezionato, quindi viene visualizzata con incrementi del 5% che ne indicano la propensione. Il conteggio dei profili viene fornito lungo l’asse Y e i punteggi di propensione vengono forniti lungo l’asse X.

>[!NOTE]
>
>Se la visualizzazione è un punteggio di propensione alla conversione, i punteggi alti sono in verde e quelli bassi in rosso. Se prevedi una propensione all’abbandono, questo viene capovolto, i punteggi alti sono in rosso e i punteggi bassi in verde. Il bucket medio rimane giallo indipendentemente dal tipo di propensione scelto.

Il modello di intelligenza artificiale che determina i punteggi di tendenza viene scelto dal selettore a discesa sotto il titolo del widget. Il menu a discesa contiene un elenco di tutti i modelli di IA per l’analisi dei clienti configurati. Seleziona il modello di intelligenza artificiale appropriato per l’analisi dall’elenco dei modelli disponibili. Se non è disponibile alcun modello di IA per l’analisi dei clienti, un messaggio all’interno del widget indica di configurare almeno un modello di IA per l’analisi dei clienti e fornisce un collegamento ipertestuale alla pagina di configurazione del modello di IA per l’analisi dei clienti. Consulta la documentazione per le istruzioni su [come configurare un&#39;istanza di Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md).

>[!NOTE]
>
>Seleziona il menu a discesa immediatamente sotto la scheda della panoramica per modificare il criterio di unione che determina quali profili includere nell’analisi. Consulta la sezione sui [criteri di unione](#merge-policies) per una breve descrizione o la [panoramica dei criteri di unione](../../profile/merge-policies/overview.md) per ulteriori dettagli.

Per passare alla pagina delle informazioni dettagliate per il modello di IA per l&#39;analisi dei clienti selezionato, selezionare **[!UICONTROL Visualizza dettagli modello]**.

![Dashboard dei tipi di pubblico di Experience Platform con [!UICONTROL widget Distribuzione di punteggi di IA per l&#39;analisi dei clienti] e [!UICONTROL Dettagli modello di visualizzazione] evidenziati.](../images/segments/customer-ai-distribution-of-scores.png)

Viene visualizzata la pagina dettagliata Approfondimenti modello.

![Pagina approfondimenti per IA per l&#39;analisi dei clienti.](../images/profiles/customer-ai-insights-page.png)

Ulteriori informazioni su IA per l&#39;analisi dei clienti sono disponibili nella [guida dell&#39;interfaccia utente di individuazione approfondimenti](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

### [!UICONTROL Riepilogo punteggio di AI per l’analisi dei clienti] {#customer-ai-scoring-summary}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_scoringSummary"
>title="Riepilogo punteggio"
>abstract="Questo widget mostra il numero totale di profili con punteggio e li categorizza in contenitori a seconda della propensione alta, media e bassa. Il grafico ad anello illustra la composizione proporzionale dei profili totali con propensione alta, media e bassa."

Questo widget visualizza il numero totale di profili valutati e li categorizza in contenitori contenenti propensione alta, media e bassa rispettivamente come verde, giallo e rosso. Un grafico ad anello illustra la composizione proporzionale dei profili tra propensione alta, media e bassa. Un profilo può avere una propensione elevata superiore a 75, una propensione media compresa tra 25 e 74 e una bassa propensione inferiore a 24. Una legenda indica il codice del colore e le soglie di propensione. I conteggi dei profili per le propensione alta, media e bassa vengono visualizzati in una finestra di dialogo quando il cursore passa sopra la rispettiva sezione del grafico ad anello.

>[!NOTE]
>
>Se la visualizzazione è un punteggio di propensione alla conversione, i punteggi alti sono in verde e quelli bassi in rosso. Se prevedi una propensione all’abbandono, questo viene capovolto, i punteggi alti sono in rosso e i punteggi bassi in verde. Il bucket medio rimane giallo indipendentemente dal tipo di propensione scelto.

Il menu a discesa sotto il titolo del widget fornisce un elenco di tutti i modelli di IA per l’analisi dei clienti configurati. Seleziona il modello di intelligenza artificiale appropriato per l’analisi dall’elenco dei modelli disponibili. Se non è disponibile alcun modello di IA per l’analisi dei clienti, un messaggio all’interno del widget indica di configurare almeno un modello di IA per l’analisi dei clienti e fornisce un collegamento ipertestuale alla pagina di configurazione del modello di IA per l’analisi dei clienti. Per istruzioni dettagliate, consulta la documentazione su [come configurare un&#39;istanza di IA per l&#39;analisi dei clienti](../../intelligent-services/customer-ai/user-guide/configure.md).

>[!NOTE]
>
>Il numero totale di profili calcolati dipende dal criterio di unione scelto. Per modificare il criterio di unione utilizzato, seleziona il menu a discesa immediatamente sotto la scheda della panoramica. Consulta la sezione sui [criteri di unione](#merge-policies) per una breve descrizione o la [panoramica dei criteri di unione](../../profile/merge-policies/overview.md) per ulteriori dettagli.

![Dashboard dei tipi di pubblico di Experience Platform con widget di riepilogo del punteggio di IA per l&#39;analisi dei clienti evidenziato.](../images/segments/customer-ai-scoring-summary.png)

Per passare alla pagina delle informazioni dettagliate per il modello di IA per l&#39;analisi dei clienti selezionato, selezionare **[!UICONTROL Visualizza dettagli modello]**. Ulteriori informazioni su IA per l&#39;analisi dei clienti sono disponibili nella [guida dell&#39;interfaccia utente di individuazione approfondimenti](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

## Widget standard {#standard-widgets}

Adobe fornisce più widget standard da utilizzare per visualizzare diverse metriche relative ai dati profilo. Puoi anche creare widget personalizzati da condividere con la tua organizzazione utilizzando la [!UICONTROL Libreria widget]. Per ulteriori informazioni sulla creazione di widget personalizzati, leggere la [Panoramica della libreria di widget](../customize/widget-library.md).

Per ulteriori informazioni su ciascuno dei widget standard disponibili, selezionare il nome di un widget dall&#39;elenco seguente:

* [[!UICONTROL Conteggio dei profili]](#profile-count)
* [[!UICONTROL Tendenza conteggio profili]](#profile-count-trend)
* [[!UICONTROL Modifica del conteggio dei profili]](#profile-count-change)
* [[!UICONTROL Tendenza di modifica del conteggio dei profili]](#profiles-count-change-trend)
* [[!UICONTROL Tendenza di modifica conteggio profili per identità]](#profiles-count-change-trend-by-identity)
* [[!UICONTROL Profili per identità]](#profiles-by-identity)
* [[!UICONTROL Sovrapposizione di identità]](#identity-overlap)
* [[!UICONTROL Profili a identità singola]](#single-identity-profiles)
* [[!UICONTROL Profili di identità singola per identità]](#single-identity-profiles-by-identity)
* [[!UICONTROL Profili non segmentati]](#unsegmented-profiles)
* [[!UICONTROL Tendenza di modifica dei profili non segmentati]](#unsegmented-profiles-change-trend)
* [[!UICONTROL Profili non segmentati per identità]](#unsegmented-profiles-by-identity)
* [[!UICONTROL Tipi di pubblico]](#audiences)
* [[!UICONTROL Tipi di pubblico mappati allo stato di destinazione]](#audiences-mapped-to-destination-status)
* [[!UICONTROL Dimensione pubblico]](#audiences-size)
* [[!UICONTROL Sovrapposizione del pubblico per criterio di unione]](#audience-overlap-by-merge-policy)
* [[!UICONTROL Rapporto di sovrapposizione pubblico]](#audience-overlap-report)

### [!UICONTROL Conteggio dei profili] {#profile-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilecount"
>title="Conteggio dei profili"
>abstract="Questo widget visualizza il numero totale di profili uniti all’interno dell’archivio dei profili al momento dell’acquisizione dell’istantanea. Il numero dipende dal criterio di unione selezionato applicato ai dati dei profili."

Il widget **[!UICONTROL Conteggio profili]** visualizza il numero totale di profili uniti nell&#39;archivio profili al momento dello snapshot. Questo numero è il risultato dell’applicazione del criterio di unione selezionato ai dati del profilo per unire i frammenti di profilo in modo da formare un singolo profilo per ogni singolo utente.

Per ulteriori informazioni, consulta la sezione [ sui criteri di unione più indietro in questo documento](#merge-policies).

>[!NOTE]
>
>Il widget [!UICONTROL Conteggio profili] potrebbe mostrare un numero diverso rispetto al conteggio dei profili visualizzato nella scheda [!UICONTROL Sfoglia] nella sezione [!UICONTROL Profili] dell&#39;interfaccia utente per più motivi. Il motivo più comune di questa differenza è che la scheda [!UICONTROL Sfoglia] fa riferimento al numero totale di profili uniti in base al criterio di unione predefinito della tua organizzazione, mentre il widget [!UICONTROL Conteggio profili] fa riferimento al numero totale di profili uniti in base al criterio di unione selezionato per la visualizzazione nel dashboard.
>
>Un altro motivo comune è dovuto alle differenze tra il momento in cui viene acquisita l&#39;istantanea del dashboard e il momento in cui il processo di esempio viene eseguito per la scheda [!UICONTROL Sfoglia]. Puoi vedere quando il widget [!UICONTROL Conteggio profili] è stato aggiornato l&#39;ultima volta osservando la marca temporale sul widget. Per ulteriori informazioni sull&#39;attivazione del processo di esempio nella scheda [!UICONTROL Sfoglia], consulta la sezione [conteggio profili nella guida dell&#39;interfaccia utente Profilo cliente in tempo reale](../../profile/ui/user-guide.md#profile-count).

![Dashboard dei profili di Experience Platform con widget Conteggio profili evidenziato.](../images/profiles/profile-count.png)

### [!UICONTROL Tendenza conteggio profili] {#profile-count-trend}

Il widget [!UICONTROL Tendenza conteggio profili] utilizza un grafico a linee per illustrare la tendenza nel numero totale di profili contenuti nel sistema nel tempo. Questo numero totale include tutti i profili importati nel sistema dall’ultima istantanea giornaliera. I dati possono essere visualizzati in periodi di 30 giorni, 90 giorni e 12 mesi. Il periodo di tempo viene scelto da un menu a discesa nel widget.

![Widget tendenza conteggio profili.](../images/profiles/profile-count-trend.png)

### [!UICONTROL Modifica del conteggio dei profili] {#profile-count-change}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilescountchange"
>title="Modifica del conteggio dei profili"
>abstract="Questo widget visualizza il numero totale di profili uniti **aggiunti** all’archivio dei profili al momento dell’ultima istantanea. Il numero dipende dal criterio di unione selezionato applicato ai dati dei profili."

Il widget **[!UICONTROL Modifica conteggio profili]** visualizza il numero di profili uniti aggiunti all&#39;archivio profili dall&#39;istantanea precedente. Questo numero è il risultato dell’applicazione del criterio di unione selezionato ai dati del profilo per unire i frammenti di profilo in modo da formare un singolo profilo per ogni singolo utente. Puoi utilizzare il selettore a discesa per visualizzare il numero di profili aggiunti negli ultimi 30 giorni, 90 giorni o 12 mesi.

>[!NOTE]
>
>Il widget [!UICONTROL Modifica conteggio profili] riflette il numero di profili aggiunti **dopo** l&#39;acquisizione iniziale del profilo e la configurazione dell&#39;archivio profili. In altre parole, se la tua organizzazione ha configurato l&#39;archivio profili e ne ha acquisiti 4.000.000 il Giorno 1, entro 24 ore la dashboard sarà disponibile; tuttavia, il widget [!UICONTROL Modifica conteggio profili] sarà impostato su 0. Questo metodo di conteggio consente di evitare un picco associato all’acquisizione iniziale dei profili nel sistema. Nei prossimi 30 giorni, la tua organizzazione acquisirà altri 1.000.000 di profili nell’archivio Profili. Una volta acquisita l&#39;istantanea successiva, il widget [!UICONTROL Modifica conteggio profili] mostrerebbe un totale di 1.000.000 profili aggiunti, mentre il widget [!UICONTROL Conteggio profili] mostrerebbe un totale di 5.000.000 profili.

![Il dashboard dei profili dell&#39;interfaccia utente di Platform con il widget di modifica del conteggio dei profili evidenziato.](../images/profiles/profile-count-change.png)

### [!UICONTROL Tendenza di modifica del conteggio dei profili] {#profiles-count-change-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesaddedtrend"
>title="Tendenza di modifica del conteggio dei profili"
>abstract="Questo widget visualizza il numero di profili uniti che sono stati aggiunti quotidianamente all’archivio dei profili negli ultimi 30 giorni, 90 giorni o 12 mesi. Il numero dipende anche dal criterio di unione selezionato applicato ai dati dei profili."

Il widget **[!UICONTROL Tendenza di modifica del conteggio dei profili]** visualizza il numero totale di profili uniti che sono stati aggiunti all&#39;archivio profili ogni giorno negli ultimi 30 giorni, 90 giorni o 12 mesi. Questo numero viene aggiornato ogni giorno in cui viene acquisita l’istantanea, pertanto se si acquisiscono profili in Platform, il numero di profili non viene riportato fino all’acquisizione dell’istantanea successiva. Il numero di profili aggiunti è il risultato dell’applicazione del criterio di unione selezionato ai dati del profilo per unire i frammenti di profilo in modo da formare un singolo profilo per ogni singolo utente.

Per ulteriori informazioni, consulta la sezione [sui criteri di unione più indietro in questo documento](#merge-policies).

Il widget **[!UICONTROL Tendenza di modifica del conteggio dei profili]** visualizza un pulsante &#39;sottotitoli&#39; in alto a destra del widget. Per aprire la finestra di dialogo dei sottotitoli automatici, seleziona **[!UICONTROL Sottotitoli]**.

![Nella scheda Panoramica profilo è visualizzato il widget tendenza modifica conteggio profili con il pulsante Sottotitoli evidenziato.](../images/profiles/profiles-count-change-trend-captions.png)

Un modello di apprendimento automatico genera automaticamente sottotitoli per descrivere le tendenze chiave e gli eventi importanti analizzando il grafico e i dati. Le annotazioni vengono aggiunte al grafico in base alle didascalie. Seleziona una didascalia per evidenziare l’annotazione corrispondente.

![La finestra di dialogo delle didascalie automatiche per il widget della tendenza di modifica del conteggio dei profili.](../images/profiles/profiles-added-trends-automatic-captions-dialog-with-annotation.png)

### [!UICONTROL Tendenza di modifica conteggio profili per identità] {#profiles-count-change-trend-by-identity}

<!-- This widget uses a line graph to illustrate the change in number of profiles filtered by a chosen source identity and merge policy. -->

Questo widget filtra il conteggio dei profili in base a un’identità di origine selezionata e unisce i criteri, quindi illustra la modifica del numero per vari periodi utilizzando un grafico a linee. Il criterio di unione è selezionato dal menu a discesa Panoramica nella parte superiore della pagina, l’identità di origine e il periodo di tempo sono selezionati dai menu a discesa dei widget. La tendenza può essere visualizzata in periodi di 30 giorni, 90 giorni e 12 mesi.

Questo widget consente di gestire le esigenze di attivazione della destinazione dimostrando il pattern di crescita dei profili filtrati da un’identità richiesta.

![Tendenza di modifica del conteggio dei profili per widget identità.](../images/profiles/profiles-count-change-trend-by-identity.png)

### [!UICONTROL Profili per identità] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbyidentity"
>title="Profili per identità"
>abstract="Questo widget visualizza il raggruppamento per identità di tutti i profili uniti nell’archivio dei profili."

Il widget **[!UICONTROL Profili per identità]** visualizza il raggruppamento di identità in tutti i profili uniti nell&#39;archivio profili. Il numero totale di profili per identità (in altre parole, la somma dei valori mostrati per ogni spazio dei nomi) può essere maggiore del numero totale di profili uniti, perché a un profilo potrebbero essere associati più spazi dei nomi. Ad esempio, se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente verranno associati più spazi dei nomi.

Per ulteriori informazioni, consulta la sezione [sui criteri di unione più indietro in questo documento](#merge-policies).

![Dashboard panoramica dei profili con widget Profili per identità evidenziato.](../images/profiles/profiles-by-identity.png)

Per aprire la finestra di dialogo dei sottotitoli automatici, seleziona **[!UICONTROL Sottotitoli]**.

![Finestra di dialogo Profili per didascalia identità.](../images/profiles/profiles-by-identity-captions.png)

Un modello di apprendimento automatico genera automaticamente informazioni sui dati analizzando la distribuzione complessiva e le dimensioni chiave dei dati.

Per ulteriori informazioni sulle identità, consulta la [documentazione del servizio Adobe Experience Platform Identity](../../identity-service/home.md).

### [!UICONTROL Sovrapposizione di identità] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_identityoverlap"
>title="Sovrapposizione di identità"
>abstract="Questo widget visualizza mediante un diagramma di Venn la sovrapposizione dei profili nell’archivio dei profili che contengono le due identità selezionate."

Il widget **[!UICONTROL Sovrapposizione identità]** utilizza un diagramma di Venn, o diagramma di set, per visualizzare la sovrapposizione dei profili nell&#39;archivio profili che contengono le due identità selezionate.

Utilizza i menu a discesa dei widget per selezionare le identità che desideri confrontare. Nei cerchi viene visualizzato il conteggio totale relativo dei profili che contengono ogni identità. Il numero di profili contenenti entrambe le identità è rappresentato dalla dimensione della sovrapposizione tra i cerchi. Se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente verranno associate più identità. In questa situazione, è probabile che la tua organizzazione disponga di più profili contenenti frammenti di più identità.

Per ulteriori informazioni sui frammenti di profilo, consulta la sezione su [frammenti di profilo rispetto ai profili uniti](../../profile/home.md#profile-fragments-vs-merged-profiles) nella panoramica del profilo cliente in tempo reale.

Per ulteriori informazioni sulle identità, consulta la [documentazione del servizio Adobe Experience Platform Identity](../../identity-service/home.md).

![Panoramica del dashboard Profili con widget di sovrapposizione identità evidenziato.](../images/profiles/identity-overlap.png)

### [!UICONTROL Profili a identità singola] {#single-identity-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_singleidentityprofiles"
>title="Profili a identità singola"
>abstract="Questo widget fornisce un conteggio dei profili della tua organizzazione con un solo tipo di ID che ne crea l’identità. Questo tipo di ID può essere un indirizzo e-mail o un ECID."

Il widget [!UICONTROL Profili di identità singola] fornisce un conteggio dei profili della tua organizzazione che hanno un solo tipo di ID che crea la loro identità. Questo tipo di ID può essere un’e-mail o un ECID. Il conteggio dei profili viene generato dai dati contenuti nello snapshot più recente.

![Widget profili identità singola.](../images/profiles/single-identity-profiles.png)

### [!UICONTROL Profili di identità singola per identità] {#single-identity-profiles-by-identity}

Questo widget utilizza un grafico a barre per illustrare il numero totale di profili identificati con un solo identificatore univoco. Il widget supporta fino a cinque delle identità più comuni.

Per visualizzare una finestra di dialogo che descrive il conteggio totale dei profili per un’identità, utilizza il cursore per passare il puntatore sulle singole barre.

![Profili di identità singola per widget identità.](../images/profiles/single-identity-profiles-by-identity.png)

### [!UICONTROL Profili non segmentati] {#unsegmented-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofiles"
>title="Profili non segmentati"
>abstract="Questo widget fornisce il numero totale di tutti i profili non associati ad alcun pubblico e rappresenta l’opportunità di attivazione profilo nell’organizzazione."

Il widget [!UICONTROL Profili non segmentati] fornisce il numero totale di tutti i profili non associati ad alcun pubblico. Il numero generato è preciso all’ultima istantanea e rappresenta l’opportunità di attivazione del profilo nell’organizzazione. Indica anche l’opportunità di eliminare i profili che non forniscono un ROI adeguato.

![Widget dei profili non segmentati.](../images/profiles/unsegmented-profiles.png)

### [!UICONTROL Tendenza di modifica dei profili non segmentati] {#unsegmented-profiles-change-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilestrend"
>title="Tendenza dei profili non segmentati"
>abstract="Questo widget fornisce un’illustrazione del grafico a linee per il numero di profili che non sono collegati ad alcun pubblico in un dato periodo di tempo. La tendenza dei profili non collegati ad alcun pubblico può essere visualizzata su periodi di 30 giorni, 90 giorni e 12 mesi."

Il widget [!UICONTROL Tendenza di modifica profili non segmentati] utilizza un grafico a linee per illustrare il numero di profili aggiunti dall&#39;ultima istantanea giornaliera che non sono associati ad alcun pubblico. La tendenza alla modifica dei profili non allegati ad alcun pubblico può essere visualizzata in periodi di 30 giorni, 90 giorni e 12 mesi. Il periodo di tempo viene scelto da un menu a discesa nel widget. Il conteggio dei profili si riflette sull’asse y e il tempo sull’asse x.

![Il widget della tendenza dei profili non segmentati cambia.](../images/profiles/unsegmented-profiles-change-trend.png)

### [!UICONTROL Profili non segmentati per identità] {#unsegmented-profiles-by-identity}

>[!NOTE]
>
>I profili non segmentati per widget di identità sono stati dichiarati obsoleti a ottobre 2022 e non sono più disponibili.

<!-- 

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilesbyidentity"
>title="Unsegmented profiles by identity"
>abstract="This widget categorizes the total number of unsegmented profiles by their unique identifier."

The [!UICONTROL Unsegmented Profiles by Identity] widget categorizes the total number of unsegmented profiles by their unique identifier. The data is visualized in a bar chart for ease of comparison. 

![The Unsegmented Profiles by Identity widget.](../images/profiles/unsegmented-profiles-by-identity.png) -->

### [!UICONTROL Tipi di pubblico] {#audiences}

Questo widget fornisce il numero totale di tipi di pubblico pronti per essere attivati, in base al criterio di unione scelto applicato ai dati del profilo.

Seleziona **[!UICONTROL Tipi di pubblico]** per passare alla scheda [!UICONTROL Sfoglia] della dashboard [!UICONTROL Tipi di pubblico]. Da qui puoi visualizzare un elenco di tutte le definizioni dei segmenti per la tua organizzazione.

![Il widget Tipi di pubblico.](../images/profiles/audiences.png)

<!-- https://jira.corp.adobe.com/browse/PLAT-115291 -->

<!-- * [[!UICONTROL Audiences change trend]](#audiences-change-trend) -->
<!-- ### [!UICONTROL Audiences change trend] {#audiences-change-trend}

This line graph widget visualizes the change in the total number of audiences each day, trending over time. The change in the number of audiences is dependent on the selected merge policy being applied to your profile data. The period of analysis is selected from the widget dropdown menu. The bar chart can be visualized over 30 days, 90 days, and 12-month periods.

The visualization allows you to monitor the overall health of audiences within Adobe Experience Platform by understanding trends in the growth or decline of the total number of audiences. -->

<!-- ![The Audiences change trend widget.]() -->

### [!UICONTROL Rapporto di sovrapposizione pubblico] {#audience-overlap-report}

Questo widget tabula la sovrapposizione dei dati da tutti i tipi di pubblico disponibili filtrati dai criteri di unione. Per il criterio di unione scelto dal menu a discesa nella parte superiore dello schermo viene fornito un elenco di cinque tipi di pubblico, classificati dalla percentuale di sovrapposizione più alta a quella più bassa. I due tipi di pubblico analizzati sono elencati nelle colonne [!UICONTROL PUBBLICO A NOME] e [!UICONTROL PUBBLICO B NOME]. La sovrapposizione percentuale è indicata nella terza colonna con precisione di dodici cifre decimali.

Il rapporto di sovrapposizione del pubblico consente di creare nuovi tipi di pubblico ad alte prestazioni. Osservare percentuali di sovrapposizione elevate consente di eliminare i tipi di pubblico e impedire l’invio dello stesso pubblico a destinazioni diverse. Inoltre, ti aiutano a identificare informazioni nascoste che potrebbero essere utili per una migliore segmentazione. Una sovrapposizione in percentuale bassa consente di individuare profili univoci da perseguire.

Seleziona **[!UICONTROL Visualizza altro]** per aprire una finestra di dialogo a schermo intero che contiene più dati di sovrapposizione del pubblico.

![Il widget del report di sovrapposizione del pubblico con Visualizza più evidenziato .](../images/profiles/profiles-audience-overlap-report.png)

Viene visualizzata la finestra di dialogo [!UICONTROL Rapporto di sovrapposizione pubblico]. Questa finestra di dialogo può contenere fino a 50 righe di analisi di sovrapposizione del pubblico suddivise in sei colonne. Per rimuovere o aggiungere colonne dalla tabella, selezionare l&#39;icona delle impostazioni (![Icona delle impostazioni.](/help/images/icons/settings.png)).

![Finestra di dialogo Rapporto di sovrapposizione pubblico.](../images/profiles/profiles-audience-overlap-report-dialog.png)

>[!NOTE]
>
>Per modificare la classificazione dei risultati dal più alto al più basso o dal più basso al più alto, selezionare l&#39;intestazione di colonna **[!UICONTROL Sovrapposizione]**.

Per scaricare l&#39;intero report in formato PDF, selezionare il menu delle opzioni (**`...`**) seguito da **[!UICONTROL Scarica]**.

![La finestra di dialogo del report di sovrapposizione del pubblico con i puntini di sospensione e l&#39;opzione Download evidenziata.](../images/profiles/profiles-audience-overlap-report-dialog-download.png)

Per aprire un diagramma di Venn dell&#39;analisi di sovrapposizione, selezionate una riga dal rapporto. Per visualizzare il conteggio dei profili in una finestra di dialogo, passa il cursore del mouse su una sezione del diagramma di Venn.

![Finestra di dialogo Rapporto di sovrapposizione pubblico con diagramma di Venn e riga evidenziata.](../images/profiles/profiles-audience-overlap-report-dialog-venn.png)

Seleziona **[!UICONTROL Chiudi]** per tornare alla dashboard [!UICONTROL Profili].

### [!UICONTROL Tipi di pubblico mappati allo stato di destinazione] {#audiences-mapped-to-destination-status}

Il widget [!UICONTROL Tipi di pubblico mappati allo stato di destinazione] visualizza il numero totale di tipi di pubblico mappati e non mappati in una singola metrica e utilizza un grafico ad anello per illustrare la differenza proporzionale tra i totali. I numeri calcolati dipendono dal criterio di unione scelto.

I conteggi individuali per i tipi di pubblico mappati o non mappati vengono visualizzati in una finestra di dialogo quando il cursore passa sopra la rispettiva sezione del grafico ad anello.

![Tipi di pubblico mappati al widget di stato di destinazione.](../images/profiles/audiences-mapped-to-destination-status.png)

### [!UICONTROL Dimensione pubblico] {#audiences-size}

Il widget [!UICONTROL Dimensione pubblico] fornisce una tabella a due colonne che elenca i nomi di un massimo di 20 tipi di pubblico e il numero totale di profili contenuti in ciascun pubblico. L’elenco viene ordinato da alto a basso in base al numero totale di profili all’interno del pubblico. Il conteggio delle dimensioni totali del pubblico dipende dal criterio di unione applicato.

![Widget dimensione tipi di pubblico.](../images/profiles/audiences-size.png)

Per visualizzare informazioni complete su un pubblico, seleziona un nome di pubblico dall&#39;elenco fornito per passare alla pagina [!UICONTROL Tipi di pubblico] [!UICONTROL Dettagli]. Inoltre, selezionando **[!UICONTROL Visualizza tutti i tipi di pubblico]** dalla fine del widget, puoi passare alla scheda [!UICONTROL Tipi di pubblico] [!UICONTROL Sfoglia] per trovare eventuali tipi di pubblico esistenti.

![Il widget dimensione pubblico con un nome di pubblico e il testo Visualizza tutti i tipi di pubblico evidenziato.](../images/profiles/audiences-size-view-all-audiences.png)

Ulteriori informazioni sui dettagli del pubblico sono disponibili nella [documentazione di Audience Portal](../../segmentation/ui/audience-portal.md).

### [!UICONTROL Sovrapposizione del pubblico per criterio di unione] {#audience-overlap-by-merge-policy}

Questo widget utilizza un diagramma di Venn per visualizzare la sovrapposizione di due tipi di pubblico selezionati. Il criterio di unione viene scelto dal menu a discesa Panoramica nella parte superiore della pagina e i tipi di pubblico per l’analisi vengono selezionati da due menu a discesa all’interno del widget. Il numero totale di profili all’interno della definizione del segmento pertinente può essere visualizzato passando il cursore sopra un cerchio o l’intersezione.

Quando il widget mostra il crossover visivo delle definizioni dei segmenti, puoi ottimizzare la strategia di segmentazione studiando le somiglianze tra le definizioni dei segmenti.

![Dashboard dei profili dell&#39;interfaccia utente di Platform con elenco a discesa dei criteri di unione e elenco a discesa dei tipi di pubblico dei widget evidenziati.](../images/profiles/audience-overlap-by-merge-policy.png)


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

Seguendo questo documento, ora dovresti essere in grado di individuare la dashboard dei profili e comprendere le metriche visualizzate nei widget disponibili. Per ulteriori informazioni sull&#39;utilizzo dei dati di [!DNL Profile] nell&#39;interfaccia utente di Experience Platform, fare riferimento alla [guida dell&#39;interfaccia utente del profilo cliente in tempo reale](../../profile/ui/user-guide.md).
