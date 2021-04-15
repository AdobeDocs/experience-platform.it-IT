---
keywords: Experience Platform;guida introduttiva;customer ai;argomenti comuni;input ai clienti;output ai clienti
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Input e output in Customer AI
topic: Introduzione
description: Ulteriori informazioni sugli eventi, gli input e gli output richiesti utilizzati da Customer AI.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
translation-type: tm+mt
source-git-commit: 2ef2a6431865e8ffdc2abd6cf527249e8b5ca4d0
workflow-type: tm+mt
source-wordcount: '2867'
ht-degree: 0%

---

# Ingresso e uscita in Customer AI

Il documento seguente illustra i diversi eventi, input e output richiesti utilizzati in Customer AI.

## Introduzione

Customer AI funziona analizzando uno dei seguenti set di dati per prevedere i punteggi di propensione di abbandono o conversione:

- Set di dati di Consumer Experience Event (CEE)
- Dati Adobe Analytics utilizzando il [connettore di origine Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Dati Adobe Audience Manager utilizzando il [connettore di origine Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)

>[!IMPORTANT]
>
>I connettori sorgente impiegano fino a quattro settimane per eseguire il backfill dei dati. Se recentemente hai impostato un connettore, devi verificare che il set di dati abbia la lunghezza minima dei dati richiesti per Customer AI. Controlla la sezione [Dati storici](#data-requirements) per verificare di disporre di dati sufficienti per l&#39;obiettivo di previsione.

Questo documento richiede una comprensione di base dello schema CEE. Prima di continuare, controlla la documentazione [Preparazione dati di Intelligent Services](../data-preparation.md) .

La tabella seguente illustra alcuni termini comuni utilizzati in questo documento:

| Termine | Definizione |
| --- | --- |
| [Experience Data Model (XDM)](../../xdm/home.md) | XDM è il framework fondamentale che consente a Adobe Experience Cloud, basato su Adobe Experience Platform, di inviare il messaggio giusto alla persona giusta, sul canale giusto, al momento giusto. La metodologia su cui viene generato l’Experience Platform, sistema XDM, rende operativi gli schemi Experience Data Model per l’utilizzo da parte dei servizi Platform. |
| Schema XDM | Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i diversi sistemi, diventa più facile mantenere il significato e quindi ottenere valore dai dati. Prima di poter acquisire i dati in Platform, è necessario comporre uno schema per descrivere la struttura dei dati e fornire vincoli al tipo di dati che possono essere contenuti all’interno di ciascun campo. Gli schemi sono costituiti da una classe XDM di base e da zero o più mixin. |
| Classe XDM | Tutti gli schemi XDM descrivono i dati che possono essere classificati come record o serie temporali. Il comportamento dei dati di uno schema è definito dalla classe dello schema, che viene assegnata a uno schema al momento della sua creazione. Le classi XDM descrivono il numero minimo di proprietà che uno schema deve contenere per rappresentare un particolare comportamento di dati. |
| [Mixins](../../xdm/schema/composition.md) | Componente che definisce uno o più campi in uno schema. I mixin applicano la modalità di visualizzazione dei campi nella gerarchia dello schema e quindi presentano la stessa struttura in ogni schema in cui sono inclusi. I mixin sono compatibili solo con classi specifiche, come identificato dal loro attributo `meta:intendedToExtend` . |
| [Tipo di dati](../../xdm/schema/composition.md) | Componente che può anche fornire uno o più campi per uno schema. Tuttavia, a differenza dei mixin, i tipi di dati non sono vincolati a una particolare classe. Questo rende i tipi di dati un’opzione più flessibile per descrivere le strutture di dati comuni riutilizzabili tra più schemi con classi potenzialmente diverse. I tipi di dati descritti in questo documento sono supportati dagli schemi CEE e Adobe Analytics. |
| Abbandono | Misurazione della percentuale di account che annullano o scelgono di non rinnovare gli abbonamenti. Un elevato tasso di abbandono può avere un impatto negativo sui ricavi mensili ricorrenti (MRR) e può anche indicare insoddisfazione per un prodotto o servizio. |
| [Profilo cliente in tempo reale](../../profile/home.md) | Profilo cliente in tempo reale fornisce un profilo consumatore centralizzato per una gestione delle esperienze mirata e personalizzata. Ogni profilo contiene dati aggregati in tutti i sistemi, nonché account con marca temporale utilizzabili per eventi che coinvolgono il singolo utente che si sono verificati in uno dei sistemi utilizzati con Experience Platform. |

## Dati di input di Customer AI

>[!TIP]
>
> Customer AI determina automaticamente quali eventi sono utili per le previsioni e genera un avviso se i dati disponibili non sono sufficienti a generare previsioni di qualità.

Customer AI supporta i set di dati CEE, Adobe Analytics e Adobe Audience Manager. Lo schema CEE richiede l’aggiunta di mixin durante il processo di creazione dello schema. Se utilizzi set di dati Adobe Analytics o Adobe Audience Manager, il connettore di origine mappa direttamente gli eventi standard (Commerce, Dettagli pagina Web, Applicazione e Ricerca) elencati di seguito durante il processo di connessione.

Per ulteriori informazioni sulla mappatura dei dati di Adobe Analytics o dei dati di Audience Manager, visita la guida [Mappature dei campi di Analytics](../../sources/connectors/adobe-applications/analytics.md) o [Mappature dei campi di Audience Manager](../../sources/connectors/adobe-applications/mapping/audience-manager.md) .

### Eventi standard utilizzati da Customer AI {#standard-events}

Gli eventi esperienza XDM vengono utilizzati per determinare vari comportamenti dei clienti. A seconda della struttura dei dati, i tipi di evento elencati di seguito potrebbero non includere tutti i comportamenti del cliente. Spetta a te determinare quali campi contengono i dati necessari per identificare in modo chiaro e inequivocabile l’attività degli utenti web. A seconda dell’obiettivo di previsione, i campi obbligatori necessari possono cambiare.

Customer AI si basa su diversi tipi di eventi per la creazione di feature modello. Questi tipi di evento vengono aggiunti automaticamente allo schema utilizzando più mixin XDM.

>[!NOTE]
>
>Se utilizzi dati Adobe Analytics o Adobe Audience Manager, lo schema viene creato automaticamente con gli eventi standard richiesti necessari per acquisire i dati. Se si sta creando uno schema CEE personalizzato per l&#39;acquisizione dei dati, è necessario considerare quali mixin sono necessari per acquisire i dati.

Non è necessario disporre di dati per ciascuno degli eventi standard elencati di seguito, ma per alcuni scenari sono necessari alcuni eventi. Se sono disponibili dati di eventi standard, è consigliabile includerli nello schema. Ad esempio, se desideri creare un’applicazione Customer AI per prevedere gli eventi di acquisto, è utile disporre di dati dei tipi di dati `Commerce` e `Web page details`.

Per visualizzare un mixin nell’interfaccia utente di Platform, seleziona la scheda **[!UICONTROL Schemas]** nella barra a sinistra, quindi seleziona la scheda **[!UICONTROL Mixins]** .


| Mixina | Tipo evento | Percorso campo XDM |
| --- | --- | --- |
| [!UICONTROL Commerce Details] | ordine | <li> commerce.order.purchaseID </li> <li> productListItems.SKU </li> |
|  | productListViews | <li> commerce.productListViews.value </li> <li> productListItems.SKU </li> |
|  | checkout | <li> commerce.checkouts.value </li> <li> productListItems.SKU </li> |
|  | acquisti | <li> commerce.purchases.value </li> <li> productListItems.SKU </li> |
|  | productListRemovals | <li> commerce.productListRemovals.value </li> <li> productListItems.SKU </li> |
|  | productListViews | <li> commerce.productListOpens.value </li> <li> productListItems.SKU </li> |
|  | productViews | <li> commerce.productViews.value </li> <li> productListItems.SKU </li> |
| [!UICONTROL Web Details] | webVisit | web.webPageDetails.name |
|  | webInteraction | web.webInteraction.linkClicks.value |
| [!UICONTROL Application Details] | applicationCloses | <li> application.applicationCloses.value </li> <li> application.name </li> |
|  | applicationCrash | <li> application.crashes.value </li> <li> application.name </li> |
|  | applicationFeatureUsages | <li> application.featureUsages.value </li> <li> application.name </li> |
|  | applicationFirstLaunches | <li> application.firstLaunches.value </li> <li> application.name </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> application.name </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> application.name </li> |
|  | applicationUpdate | <li> application.upgrades.value </li> <li> application.name </li> |
| [!UICONTROL Search Details] | ricerca | search.keywords |

Inoltre, Customer AI può utilizzare i dati di abbonamento per generare modelli di abbandono migliori. I dati di abbonamento sono necessari per ciascun profilo utilizzando il formato di dati [[!UICONTROL Subscription]](../../xdm/data-types/subscription.md) . La maggior parte dei campi sono facoltativi, tuttavia, per un modello di abbandono ottimale si consiglia vivamente di fornire dati per il maggior numero possibile di campi, ad esempio `startDate`, `endDate` e altri dettagli pertinenti.

### Dati storici {#data-requirements}

Customer AI richiede dati storici per la formazione sui modelli, ma la quantità di dati richiesti si basa su due elementi chiave: finestra dei risultati e popolazione ammissibile.

Per impostazione predefinita, Customer AI cerca un utente che abbia avuto attività negli ultimi 120 giorni, se non viene fornita alcuna definizione di popolazione idonea durante la configurazione dell’applicazione. Inoltre, Customer AI richiede un minimo di 500 eventi qualificati e 500 non qualificati (1000 totali) di dati storici basati su una definizione di obiettivo prevista.

Negli esempi seguenti viene fornita una formula semplice per determinare la quantità minima di dati necessari. Se il requisito minimo è superiore, è probabile che il modello fornisca risultati più precisi. Se la quantità minima richiesta è inferiore a quella richiesta, il modello non riuscirà in quanto non vi è una quantità sufficiente di dati per l&#39;addestramento del modello.

**Formula**:

Lunghezza minima dei dati richiesti = popolazione ammissibile + finestra dei risultati

>[!NOTE]
>
> 30 è il numero minimo di giorni richiesti per la popolazione ammissibile. Se non viene fornito, il valore predefinito è 120 giorni.

Esempi :

- Desideri prevedere se è probabile che un cliente acquisti un orologio nei prossimi 30 giorni. Desideri inoltre valutare gli utenti che hanno un po&#39; di attività web negli ultimi 60 giorni. In questo caso la lunghezza minima dei dati richiesti = 60 giorni + 30 giorni. La popolazione ammissibile è di 60 giorni e la finestra di risultato è di 30 giorni per un totale di 90 giorni.

- Desideri prevedere se è probabile che l’utente acquisti un orologio nei successivi 7 giorni. In questo caso la lunghezza minima dei dati richiesti = 120 giorni + 7 giorni. Il valore predefinito della popolazione ammissibile è 120 giorni e il periodo di risultato è 7 giorni per un totale di 127 giorni.

- Desideri prevedere se è probabile che il cliente acquisti un orologio nei prossimi 7 giorni. Vuoi anche valutare gli utenti che hanno qualche attività web negli ultimi 7 giorni. In questo caso la lunghezza minima dei dati richiesti = 30 giorni + 7 giorni. La popolazione ammissibile necessita di un minimo di 30 giorni e la finestra di risultato è di 7 giorni per un totale di 37 giorni.

Oltre ai dati minimi richiesti, Customer AI funziona al meglio anche con i dati recenti. In questo caso d’uso, Customer AI sta facendo una previsione per il futuro sulla base dei recenti dati comportamentali di un utente. In altre parole, è probabile che dati più recenti producano una previsione più accurata.

### Scenari di esempio

In questa sezione sono descritti diversi scenari per le istanze di Customer AI e i tipi di evento richiesti e consigliati. Per ulteriori informazioni sul mixin e sul relativo percorso del campo, consulta la [tabella eventi standard](#standard-events) precedente .

>[!NOTE]
>
> I tipi di evento richiesti vengono utilizzati per identificare in modo chiaro e senza ambiguità le attività degli utenti web. Il numero di tipi di evento richiesti cambierà in base all&#39;obiettivo di previsione e alla struttura dello schema. Se non sei sicuro che sia necessario un particolare tipo di evento, è consigliabile includere tale tipo di evento durante la creazione dello schema CEE. Se utilizzi i dati di Adobe Analytics o Adobe Audience Manager, gli eventi standard richiesti dovrebbero essere disponibili a seconda dei dati in streaming.

### Scenario 1: Conversione da acquistare su un sito web di e-commerce per la vendita al dettaglio

**Obiettivo di previsione:** prevedere la propensione alla conversione per i profili idonei ad acquistare un determinato articolo di abbigliamento su un sito web.

**Tipi di eventi standard richiesti:**

I tipi di evento elencati di seguito sono necessari per un output di Customer AI ottimale con questo particolare obiettivo di previsione. È possibile escludere un evento obbligatorio a seconda dell’obiettivo di previsione, tuttavia, escludere più eventi può portare a risultati scadenti.

- ordine
- checkout
- acquisti
- webVisit
- ricerca

**Tipi di eventi standard aggiuntivi consigliati:**

Uno qualsiasi dei tipi di evento [rimanenti](#standard-events) può essere richiesto in base alla complessità dell&#39;obiettivo e della popolazione idonea durante la configurazione dell&#39;istanza di Customer AI. Se i dati sono disponibili per un particolare tipo di dati, è consigliabile includerli nello schema.

### Scenario 2: Conversione dell&#39;abbonamento su un sito web del servizio di streaming multimediale

**Obiettivo di previsione:** prevedere la propensione alla conversione dell’abbonamento affinché i profili idonei si impegnino a un determinato livello di abbonamento, ad esempio un piano standard o premium.

**Tipi di eventi standard richiesti:**

I tipi di evento elencati di seguito sono necessari per un output di Customer AI ottimale con questo particolare obiettivo di previsione. È possibile escludere un evento obbligatorio a seconda dell’obiettivo di previsione, tuttavia, escludere più eventi può portare a risultati scadenti.

- ordine
- checkout
- acquisti
- webVisit
- ricerca

In questo esempio, `order`, `checkouts` e `purchases` vengono utilizzati per indicare che un abbonamento è stato acquistato e il relativo tipo.

Inoltre, per un modello accurato, si consiglia di utilizzare alcune delle proprietà disponibili nel tipo di dati di [sottoscrizione](../../xdm/data-types/subscription.md).

**Tipi di eventi standard aggiuntivi consigliati:**

Uno qualsiasi dei tipi di evento [rimanenti](#standard-events) può essere richiesto in base alla complessità dell&#39;obiettivo e della popolazione idonea durante la configurazione dell&#39;istanza di Customer AI. Se i dati sono disponibili per un particolare tipo di dati, è consigliabile includerli nello schema.

### Scenario 3: Churn (Abbandono) su un sito web di e-commerce retail

**Obiettivo di previsione:** prevedere la probabilità che non si verifichi un evento di acquisto.

**Tipi di eventi standard richiesti:**

I tipi di evento elencati di seguito sono necessari per un output di Customer AI ottimale con questo particolare obiettivo di previsione. È possibile escludere un evento obbligatorio a seconda dell’obiettivo di previsione, tuttavia, escludere più eventi può portare a risultati scadenti.

- ordine
- checkout
- acquisti
- webVisit
- ricerca

**Tipi di eventi standard aggiuntivi consigliati:**

Uno qualsiasi dei tipi di evento [rimanenti](#standard-events) può essere richiesto in base alla complessità dell&#39;obiettivo e della popolazione idonea durante la configurazione dell&#39;istanza di Customer AI. Se i dati sono disponibili per un particolare tipo di dati, è consigliabile includerli nello schema.

### Scenario 4: Upselling conversion su un sito web di e-commerce retail

**Obiettivo di previsione:** prevedere la propensione di acquisto della popolazione che ha acquistato un prodotto specifico per acquistare un nuovo prodotto correlato.

**Tipi di eventi standard richiesti:**

I tipi di evento elencati di seguito sono necessari per un output di Customer AI ottimale con questo particolare obiettivo di previsione. È possibile escludere un evento obbligatorio a seconda dell’obiettivo di previsione, tuttavia, escludere più eventi può portare a risultati scadenti.

- ordine
- checkout
- acquisti
- webVisit
- ricerca

**Tipi di eventi standard aggiuntivi consigliati:**

Uno qualsiasi dei tipi di evento [rimanenti](#standard-events) può essere richiesto in base alla complessità dell&#39;obiettivo e della popolazione idonea durante la configurazione dell&#39;istanza di Customer AI. Se i dati sono disponibili per un particolare tipo di dati, è consigliabile includerli nello schema.

### Scenario 5: Annulla sottoscrizione (churn) su un canale di notizie online

**Obiettivo di previsione:** prevedere la propensione della popolazione idonea a annullare l’abbonamento a un servizio il mese prossimo.

**Tipi di eventi standard richiesti:**

I tipi di evento elencati di seguito sono necessari per un output di Customer AI ottimale con questo particolare obiettivo di previsione. È possibile escludere un evento obbligatorio a seconda dell’obiettivo di previsione, tuttavia, escludere più eventi può portare a risultati scadenti.

- webVisit
- ricerca

Inoltre, per un modello accurato, si consiglia di utilizzare alcune delle proprietà disponibili nel tipo di dati di [sottoscrizione](../../xdm/data-types/subscription.md).

**Tipi di eventi standard aggiuntivi consigliati:**

Uno qualsiasi dei tipi di evento [rimanenti](#standard-events) può essere richiesto in base alla complessità dell&#39;obiettivo e della popolazione idonea durante la configurazione dell&#39;istanza di Customer AI. Se i dati sono disponibili per un particolare tipo di dati, è consigliabile includerli nello schema.

### Scenario 6: Avvia app mobile

**Obiettivo di previsione:** prevedere la propensione dei profili idonei a lanciare un’app mobile a pagamento nei prossimi X giorni. Simile alla previsione dell’indicatore di prestazioni chiave (KPI, Key Performance Indicator) di &quot;Utenti attivi mensili&quot;.

**Tipi di eventi standard richiesti:**

I tipi di evento elencati di seguito sono necessari per un output di Customer AI ottimale con questo particolare obiettivo di previsione. È possibile escludere un evento obbligatorio a seconda dell’obiettivo di previsione, tuttavia, escludere più eventi può portare a risultati scadenti.

- ordine
- checkout
- acquisti
- webVisit
- applicationCloses
- applicationCrash
- applicationFeatureUsages
- applicationFirstLaunches
- applicationInstalls
- applicationLaunches
- applicationUpdate

In questo esempio, `order`, `checkouts` e `purchases` vengono utilizzati quando è necessario acquistare un’app mobile.

**Tipi di eventi standard aggiuntivi consigliati:**

Uno qualsiasi dei tipi di evento [rimanenti](#standard-events) può essere richiesto in base alla complessità dell&#39;obiettivo e della popolazione idonea durante la configurazione dell&#39;istanza di Customer AI. Se i dati sono disponibili per un particolare tipo di dati, è consigliabile includerli nello schema.

### Scenario 7: Caratteristiche realizzate (Adobe Audience Manager)

**Obiettivo di previsione:** prevedere la propensione per alcune caratteristiche da realizzare.

**Tipi di eventi standard richiesti:**

Per utilizzare le caratteristiche di Adobe Audience Manager, è necessario creare una connessione sorgente utilizzando il [connettore sorgente Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). Il connettore di origine crea automaticamente lo schema con i mixin appropriati. Non è necessario aggiungere manualmente altri tipi di eventi affinché lo schema funzioni con Customer AI.

Quando configuri una nuova istanza AI del cliente, puoi utilizzare `audienceName` e `audienceID` per selezionare una caratteristica particolare per il punteggio durante la definizione dell’obiettivo.

## Dati di output di Customer AI

Customer AI genera diversi attributi per singoli profili ritenuti idonei. Esistono due modi per utilizzare il punteggio (output) in base al provisioning eseguito. Se disponi di un set di dati abilitato per il profilo cliente in tempo reale, puoi utilizzare informazioni dal profilo cliente in tempo reale nel [Generatore di segmenti](../../segmentation/ui/segment-builder.md). Se non disponi di un set di dati abilitato per il profilo, puoi [scaricare l’output di Customer AI](./user-guide/download-scores.md) set di dati disponibili sul data lake.

>[!NOTE]
>
> I valori di output vengono utilizzati da Profilo cliente in tempo reale che può essere utilizzato per creare e definire segmenti.

La tabella seguente descrive i vari attributi trovati nell’output di Customer AI:

| Attributo | Descrizione |
| ----- | ----------- |
| Punteggio | La probabilità relativa che un cliente raggiunga l’obiettivo previsto entro il periodo di tempo definito. Questo valore non deve essere trattato come una percentuale di probabilità, ma piuttosto come la probabilità di un individuo rispetto alla popolazione complessiva. Questo punteggio va da 0 a 100. |
| Probabilità | Questo attributo è la vera probabilità di un profilo di raggiungere l’obiettivo previsto entro l’intervallo di tempo definito. Quando si confrontano gli output tra obiettivi diversi, si consiglia di considerare la probabilità rispetto al percentile o al punteggio. La probabilità deve sempre essere utilizzata per determinare la probabilità media tra la popolazione ammissibile, in quanto la probabilità tende a essere sul lato inferiore per gli eventi che non si verificano frequentemente. Valori per l&#39;intervallo di probabilità compresi tra 0 e 1. |
| Percentile | Questo valore fornisce informazioni sulle prestazioni di un profilo rispetto ad altri profili con punteggio simile. Ad esempio, un profilo con un grado percentile di 99 per abbandono indica che si trova ad un rischio di esecuzione più elevato rispetto al 99% di tutti gli altri profili con punteggio. Le percentuali sono comprese tra 1 e 100. |
| Tipo di tendenza | Il tipo di propensione selezionato. |
| Data punteggio | Data in cui si è verificato il punteggio. |
| Fattori influenti | Motivi previsti sul motivo per cui un profilo è probabile che si converta o si abbandono. I fattori sono formati dai seguenti attributi:<ul><li>Codice: L’attributo di profilo o di comportamento che influenza positivamente il punteggio previsto di un profilo. </li><li>Valore: Il valore dell’attributo di profilo o di comportamento.</li><li>Importanza: Indica il peso del profilo o dell’attributo comportamentale sul punteggio previsto (basso, medio, alto)</li></ul> |

## Passaggi successivi {#next-steps}

Dopo aver preparato i dati e aver impostato tutte le credenziali e gli schemi, inizia seguendo la guida [Configura un&#39;istanza di Customer AI](./user-guide/configure.md) . Questa guida descrive come creare un’istanza per Customer AI.
