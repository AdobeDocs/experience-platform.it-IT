---
keywords: Experience Platform;guida introduttiva;customer ai;argomenti più comuni;customer ai input;customer ai output
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Input e output in IA per l’analisi dei clienti
description: Scopri di più sugli eventi, gli input e gli output richiesti utilizzati da Customer AI.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '3195'
ht-degree: 1%

---

# Input e output in IA per l’analisi dei clienti

Il documento seguente illustra i diversi eventi, input e output richiesti utilizzati in Customer AI.

## Introduzione

IA per l’analisi dei clienti funziona analizzando uno dei seguenti set di dati per prevedere i punteggi di tendenza di abbandono o conversione:

- Dati di Adobe Analytics utilizzando [Connettore di origine di Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Adobe Audience Manager dati utilizzando [Connettore sorgente in Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- Set di dati di Experience Event (EE)
- Set di dati di Consumer Experience Event (CEE)

Puoi aggiungere più set di dati da origini diverse se ciascuno di essi condivide lo stesso tipo di identità (spazio dei nomi), ad esempio un ECID. Per ulteriori informazioni sull’aggiunta di più set di dati, consulta [Guida utente di Customer AI](./user-guide/configure.md#select-data)

>[!IMPORTANT]
>
>I connettori sorgente richiedono fino a quattro settimane per la retrocompilazione dei dati. Se hai impostato di recente un connettore, è necessario verificare che il set di dati abbia la lunghezza minima dei dati richiesta per IA per l’analisi dei clienti. Rivedi il [dati storici](#data-requirements) per verificare di disporre di dati sufficienti per l’obiettivo predittivo.

Questo documento richiede una conoscenza di base dello schema CEE. Rivedi il [Preparazione dei dati di Intelligent Services](../data-preparation.md) prima di continuare.

La tabella seguente illustra alcuni termini comuni utilizzati in questo documento:

| Termine | Definizione |
| --- | --- |
| [Experience Data Model (XDM)](../../xdm/home.md) | XDM è il framework fondamentale che consente a Adobe Experience Cloud, con tecnologia Adobe Experience Platform, di inviare il messaggio giusto alla persona giusta, sul canale giusto, nel momento esatto giusto. La metodologia su cui viene creato l’Experience Platform, XDM System, rende operativi gli schemi Experience Data Model per l’utilizzo da parte dei servizi di Platform. |
| Schema XDM | Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i sistemi, diventa più semplice mantenere un significato e quindi ottenere valore dai dati. Prima di poter acquisire i dati in Platform, è necessario comporre uno schema per descrivere la struttura dei dati e fornire vincoli al tipo di dati che possono essere contenuti all’interno di ciascun campo. Gli schemi sono costituiti da una classe XDM di base e da zero o più gruppi di campi schema. |
| Classe XDM | Tutti gli schemi XDM descrivono dati che possono essere classificati come record o serie temporali. Il comportamento dei dati di uno schema è definito dalla classe dello schema, che viene assegnata a uno schema al momento della creazione. Le classi XDM descrivono il minor numero di proprietà che uno schema deve contenere per rappresentare un particolare comportamento di dati. |
| [Gruppi di campi](../../xdm/schema/composition.md) | Componente che definisce uno o più campi in uno schema. I gruppi di campi impongono il modo in cui i loro campi vengono visualizzati nella gerarchia dello schema e pertanto presentano la stessa struttura in ogni schema in cui sono inclusi. I gruppi di campi sono compatibili solo con classi specifiche, identificate dalle rispettive `meta:intendedToExtend` attributo. |
| [Tipo di dati](../../xdm/schema/composition.md) | Componente che può anche fornire uno o più campi per uno schema. Tuttavia, a differenza dei gruppi di campi, i tipi di dati non sono vincolati a una particolare classe. Questo rende i tipi di dati un’opzione più flessibile per descrivere strutture di dati comuni riutilizzabili in più schemi con classi potenzialmente diverse. I tipi di dati descritti in questo documento sono supportati dagli schemi CEE e Adobe Analytics. |
| Abbandono | Misurazione della percentuale di account che annullano o scelgono di non rinnovare gli abbonamenti. Un tasso di abbandono elevato può avere un impatto negativo sui ricavi ricorrenti mensili (MRR, Monthly Recurring Revenue) e può anche indicare insoddisfazione per un prodotto o un servizio. |
| [Profilo cliente in tempo reale](../../profile/home.md) | Real-Time Customer Profile fornisce un profilo consumer centralizzato per una gestione mirata e personalizzata delle esperienze. Ogni profilo contiene dati aggregati in tutti i sistemi, nonché resoconti con marca temporale utilizzabili di eventi che hanno coinvolto l’individuo che si sono verificati in qualsiasi sistema utilizzato con Experience Platform. |

## Dati di input di IA per l’analisi dei clienti

>[!TIP]
>
> IA per l’analisi dei clienti determina automaticamente quali eventi sono utili per le previsioni e genera un avviso se i dati disponibili non sono sufficienti per generare previsioni di qualità.

IA per l’analisi dei clienti supporta i set di dati Adobe Analytics, Adobe Audience Manager, Experience Event (EE) e Consumer Experience Event (CEE). Lo schema CEE richiede l&#39;aggiunta di gruppi di campi durante il processo di creazione dello schema. Se utilizzi set di dati Adobe Analytics o Adobe Audience Manager, il connettore di origine mappa direttamente gli eventi standard (Commerce, Dettagli pagina web, Applicazione e Ricerca) elencati di seguito durante il processo di connessione. Puoi aggiungere più set di dati da origini diverse se ciascuno di essi condivide lo stesso tipo di identità (spazio dei nomi), ad esempio un ECID.

Per ulteriori informazioni sulla mappatura dei dati di Adobe Analytics o di Audienci Manager, visita [Mappature dei campi di Analytics](../../sources/connectors/adobe-applications/analytics.md) o [Audience Manager di mappature campi](../../sources/connectors/adobe-applications/mapping/audience-manager.md) guida.

### Eventi standard utilizzati da Customer AI {#standard-events}

Gli eventi esperienza XDM vengono utilizzati per determinare vari comportamenti dei clienti. A seconda della struttura dei dati, i tipi di evento elencati di seguito potrebbero non includere tutti i comportamenti del cliente. È compito dell’utente determinare quali campi dispongono dei dati necessari per identificare in modo chiaro e inequivocabile l’attività dell’utente web. A seconda dell’obiettivo predittivo, i campi obbligatori necessari possono cambiare.

IA per l’analisi dei clienti si basa su diversi tipi di eventi per la creazione delle funzioni dei modelli. Questi tipi di evento vengono aggiunti automaticamente allo schema utilizzando più gruppi di campi XDM.

>[!NOTE]
>
>Se utilizzi dati di Adobe Analytics o Adobe Audience Manager, lo schema viene creato automaticamente con gli eventi standard richiesti necessari per acquisire i dati. Se si sta creando uno schema CEE personalizzato per l&#39;acquisizione dei dati, è necessario considerare i gruppi di campi necessari per l&#39;acquisizione dei dati.

Non è necessario disporre di dati per ciascuno degli eventi standard elencati di seguito, ma per alcuni scenari sono richiesti determinati eventi. Se disponi di dati di eventi standard, è consigliabile includerli nello schema. Ad esempio, se desideri creare un’applicazione Customer AI per prevedere gli eventi di acquisto, sarebbe utile disporre di dati provenienti da `Commerce` e `Web page details` tipi di dati.

Per visualizzare un gruppo di campi nell’interfaccia utente di Platform, seleziona la **[!UICONTROL Schemi]** nella barra a sinistra, quindi seleziona il pulsante **[!UICONTROL Gruppi di campi]** scheda.

| Gruppo di campi | Tipo di evento | Percorso campo XDM |
| --- | --- | --- |
| [!UICONTROL Dettagli Commerce] | ordine | <li> commerce.order.purchaseID </li> <li> productListItems.SKU </li> |
|  | productListViews | <li> commerce.productListViews.value </li> <li> productListItems.SKU </li> |
|  | checkout | <li> commerce.checkouts.value </li> <li> productListItems.SKU </li> |
|  | acquisti | <li> commerce.purchases.value </li> <li> productListItems.SKU </li> |
|  | productListRemovals | <li> commerce.productListRemovals.value </li> <li> productListItems.SKU </li> |
|  | productListOpens | <li> commerce.productListOpens.value </li> <li> productListItems.SKU </li> |
|  | productViews | <li> commerce.productViews.value </li> <li> productListItems.SKU </li> |
| [!UICONTROL Dettagli web] | webVisit | web.webPageDetails.name |
|  | webInteraction | web.webInteraction.linkClicks.value |
| [!UICONTROL Dettagli applicazione] | applicationCloses | <li> application.applicationCloses.value </li> <li> application.name </li> |
|  | applicationCrashed | <li> application.crashes.value </li> <li> application.name </li> |
|  | applicationFeatureUsages | <li> application.featureUsages.value </li> <li> application.name </li> |
|  | applicationFirstLaunches | <li> application.firstLaunches.value </li> <li> application.name </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> application.name </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> application.name </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> application.name </li> |
| [!UICONTROL Dettagli di ricerca] | ricerca | search.keywords |

Inoltre, IA per l’analisi dei clienti può utilizzare i dati di abbonamento per generare modelli di abbandono migliori. I dati di abbonamento sono necessari per ogni profilo utilizzando [[!UICONTROL Abbonamento]](../../xdm/data-types/subscription.md) formato del tipo di dati. La maggior parte dei campi è facoltativa. Tuttavia, per un modello di abbandono ottimale, si consiglia vivamente di fornire dati per il maggior numero possibile di campi, ad esempio: `startDate`, `endDate`e ogni altro dettaglio pertinente.

### Aggiunta di eventi personalizzati e attributi di profilo

Se si dispone di informazioni che si desidera includere oltre al [campi evento standard](#standard-events) utilizzato da IA per l’analisi dei clienti, durante il ciclo di vita viene fornita un’opzione per l’evento personalizzato e l’attributo di profilo personalizzato [configurazione dell’istanza](./user-guide/configure.md#custom-events).

Se il set di dati selezionato include eventi personalizzati o attributi di profilo come &quot;prenotazione di un hotel&quot; o &quot;dipendente di X company&quot; definiti nello schema, puoi aggiungerli all’istanza. Questi eventi personalizzati aggiuntivi e attributi di profilo vengono utilizzati da IA per l’analisi dei clienti per migliorare la qualità del modello e fornire risultati più precisi.

### Dati storici {#data-requirements}

IA per l’analisi dei clienti richiede dati storici per la formazione dei modelli, ma la quantità di dati richiesti si basa su due elementi chiave: finestra dei risultati e popolazione ammissibile.

Per impostazione predefinita, IA per l’analisi dei clienti cerca un utente che abbia avuto attività negli ultimi 120 giorni se non viene fornita alcuna definizione di popolazione idonea durante la configurazione dell’applicazione. Inoltre, IA per l’analisi dei clienti richiede almeno 500 eventi di qualificazione e 500 eventi non qualificati (1000 in totale) di dati storici basati su una definizione di obiettivo prevista.

Gli esempi seguenti forniti utilizzano una formula semplice per determinare la quantità minima di dati richiesti. Se il requisito minimo è maggiore, è probabile che il modello fornisca risultati più precisi. Se la quantità di dati è inferiore a quella minima richiesta, il modello avrà esito negativo poiché non è disponibile una quantità sufficiente di dati per l’apprendimento del modello.

**Formula**:

Lunghezza minima dei dati richiesti = popolazione ammissibile + finestra dei risultati

>[!NOTE]
>
> 30 è il numero minimo di giorni richiesti per la popolazione ammissibile. In caso contrario, il valore predefinito è 120 giorni.

Esempi:

- Vuoi prevedere se è probabile che un cliente acquisti un orologio nei prossimi 30 giorni. Desideri inoltre valutare gli utenti che hanno svolto attività web negli ultimi 60 giorni. In questo caso la lunghezza minima dei dati richiesti è di 60 giorni + 30 giorni. La popolazione ammissibile è di 60 giorni e la finestra dei risultati è di 30 giorni per un totale di 90 giorni.

- Desideri prevedere se è probabile che l’utente acquisti un orologio nei prossimi 7 giorni. In questo caso la lunghezza minima dei dati richiesti è di 120 giorni + 7 giorni. Il valore predefinito della popolazione ammissibile è 120 giorni e la finestra dei risultati è di 7 giorni per un totale di 127 giorni.

- Vuoi prevedere se è probabile che il cliente acquisti un orologio nei prossimi 7 giorni. Desideri inoltre valutare gli utenti che hanno svolto attività web negli ultimi 7 giorni. In questo caso la lunghezza minima dei dati richiesti è di 30 giorni + 7 giorni. La popolazione ammissibile richiede un minimo di 30 giorni e la finestra del risultato è di 7 giorni totali per 37 giorni.

Oltre ai dati minimi richiesti, Customer AI funziona al meglio anche con i dati recenti. In questo caso d’uso, IA per l’analisi dei clienti esegue una previsione per il futuro sulla base dei dati comportamentali recenti di un utente. In altre parole, è probabile che i dati più recenti producano una previsione più accurata.

### Scenari di esempio

In questa sezione sono descritti diversi scenari per le istanze di IA per l’analisi dei clienti, nonché i tipi di evento richiesti e consigliati. Consulta la sezione [tabella eventi standard](#standard-events) per ulteriori informazioni sul gruppo di campi e sul relativo percorso.

>[!NOTE]
>
> I tipi di evento richiesti vengono utilizzati per identificare in modo chiaro e non ambiguo l’attività dell’utente web. Il numero di tipi di evento richiesti cambierà in base all’obiettivo predittivo e alla struttura dello schema. Se non si è sicuri che sia necessario un particolare tipo di evento, si consiglia di includerlo durante la creazione dello schema CEE. Se utilizzi dati Adobe Analytics o Adobe Audience Manager, gli eventi standard richiesti dovrebbero essere disponibili a seconda dei dati in streaming.

### Scenario 1: acquistare la conversione su un sito web di vendita al dettaglio e-commerce

**Obiettivo di previsione:** Prevedi la propensione di conversione per i profili idonei ad acquistare un determinato articolo di abbigliamento su un sito web.

**Tipi di evento standard richiesti:**

I tipi di evento elencati di seguito sono necessari per un output di IA per l’analisi dei clienti ottimale con questo particolare obiettivo di previsione. È possibile escludere un evento richiesto a seconda dell’obiettivo predittivo, tuttavia, l’esclusione di più eventi può portare a risultati insoddisfacenti.

- ordine
- checkout
- acquisti
- webVisit
- ricerca

**Ulteriori tipi di evento standard consigliati:**

Uno qualsiasi dei rimanenti [tipi di evento](#standard-events) potrebbe essere necessario in base alla complessità dell’obiettivo e della popolazione idonea durante la configurazione dell’istanza di Customer AI. Se i dati sono disponibili per un particolare tipo di dati, si consiglia di includerli nello schema.

### Scenario 2: conversione di abbonamento su un sito web di servizi di streaming multimediale

**Obiettivo di previsione:** Prevedi la propensione di conversione dell’abbonamento per i profili idonei a eseguire il commit a un determinato livello di abbonamento, ad esempio un piano standard o premium.

**Tipi di evento standard richiesti:**

I tipi di evento elencati di seguito sono necessari per un output di IA per l’analisi dei clienti ottimale con questo particolare obiettivo di previsione. È possibile escludere un evento richiesto a seconda dell’obiettivo predittivo, tuttavia, l’esclusione di più eventi può portare a risultati insoddisfacenti.

- ordine
- checkout
- acquisti
- webVisit
- ricerca

In questo esempio, `order`, `checkouts`, e `purchases` vengono utilizzati per indicare che un abbonamento è stato acquistato e il relativo tipo.

Inoltre, per un modello accurato si consiglia di utilizzare alcune delle proprietà disponibili nel [tipo di dati abbonamento](../../xdm/data-types/subscription.md).

**Ulteriori tipi di evento standard consigliati:**

Uno qualsiasi dei rimanenti [tipi di evento](#standard-events) potrebbe essere necessario in base alla complessità dell’obiettivo e della popolazione idonea durante la configurazione dell’istanza di Customer AI. Se i dati sono disponibili per un particolare tipo di dati, si consiglia di includerli nello schema.

### Scenario 3: abbandono di un sito web di commercio elettronico al dettaglio

**Obiettivo di previsione:** Prevedere la probabilità che non si verifichi un evento di acquisto.

**Tipi di evento standard richiesti:**

I tipi di evento elencati di seguito sono necessari per un output di IA per l’analisi dei clienti ottimale con questo particolare obiettivo di previsione. È possibile escludere un evento richiesto a seconda dell’obiettivo predittivo, tuttavia, l’esclusione di più eventi può portare a risultati insoddisfacenti.

- ordine
- checkout
- acquisti
- webVisit
- ricerca

**Ulteriori tipi di evento standard consigliati:**

Uno qualsiasi dei rimanenti [tipi di evento](#standard-events) potrebbe essere necessario in base alla complessità dell’obiettivo e della popolazione idonea durante la configurazione dell’istanza di Customer AI. Se i dati sono disponibili per un particolare tipo di dati, si consiglia di includerli nello schema.

### Scenario 4: conversione di upselling su un sito web di e-commerce retail

**Obiettivo di previsione:** Prevedere la propensione all&#39;acquisto della popolazione che ha acquistato un prodotto specifico per acquistare un nuovo prodotto correlato.

**Tipi di evento standard richiesti:**

I tipi di evento elencati di seguito sono necessari per un output di IA per l’analisi dei clienti ottimale con questo particolare obiettivo di previsione. È possibile escludere un evento richiesto a seconda dell’obiettivo predittivo, tuttavia, l’esclusione di più eventi può portare a risultati insoddisfacenti.

- ordine
- checkout
- acquisti
- webVisit
- ricerca

**Ulteriori tipi di evento standard consigliati:**

Uno qualsiasi dei rimanenti [tipi di evento](#standard-events) potrebbe essere necessario in base alla complessità dell’obiettivo e della popolazione idonea durante la configurazione dell’istanza di Customer AI. Se i dati sono disponibili per un particolare tipo di dati, si consiglia di includerli nello schema.

### Scenario 5: annullare l’abbonamento (abbandono) su un canale di notizie online

**Obiettivo di previsione:** Prevedere la propensione della popolazione ammissibile ad annullare l’abbonamento a un servizio il mese prossimo.

**Tipi di evento standard richiesti:**

I tipi di evento elencati di seguito sono necessari per un output di IA per l’analisi dei clienti ottimale con questo particolare obiettivo di previsione. È possibile escludere un evento richiesto a seconda dell’obiettivo predittivo, tuttavia, l’esclusione di più eventi può portare a risultati insoddisfacenti.

- webVisit
- ricerca

Inoltre, per un modello accurato si consiglia di utilizzare alcune delle proprietà disponibili nel [tipo di dati abbonamento](../../xdm/data-types/subscription.md).

**Ulteriori tipi di evento standard consigliati:**

Uno qualsiasi dei rimanenti [tipi di evento](#standard-events) potrebbe essere necessario in base alla complessità dell’obiettivo e della popolazione idonea durante la configurazione dell’istanza di Customer AI. Se i dati sono disponibili per un particolare tipo di dati, si consiglia di includerli nello schema.

### Scenario 6: avviare un’app mobile

**Obiettivo di previsione:** Prevedi la propensione dei profili idonei ad avviare un’app mobile a pagamento nei prossimi X giorni. È simile alla previsione dell’indicatore di prestazioni chiave (KPI, Key Performance Indicator) di &quot;Utenti attivi mensili&quot;.

**Tipi di evento standard richiesti:**

I tipi di evento elencati di seguito sono necessari per un output di IA per l’analisi dei clienti ottimale con questo particolare obiettivo di previsione. È possibile escludere un evento richiesto a seconda dell’obiettivo predittivo, tuttavia, l’esclusione di più eventi può portare a risultati insoddisfacenti.

- ordine
- checkout
- acquisti
- webVisit
- applicationCloses
- applicationCrashed
- applicationFeatureUsages
- applicationFirstLaunches
- applicationInstalls
- applicationLaunches
- applicationUpgrades

In questo esempio, `order`, `checkouts`, e `purchases` vengono utilizzati quando è necessario acquistare un’app mobile.

**Ulteriori tipi di evento standard consigliati:**

Uno qualsiasi dei rimanenti [tipi di evento](#standard-events) potrebbe essere necessario in base alla complessità dell’obiettivo e della popolazione idonea durante la configurazione dell’istanza di Customer AI. Se i dati sono disponibili per un particolare tipo di dati, si consiglia di includerli nello schema.

### Scenario 7: caratteristiche realizzate (Adobe Audience Manager)

**Obiettivo di previsione:** Prevedi la propensione per alcune caratteristiche da realizzare.

**Tipi di evento standard richiesti:**

Per utilizzare le caratteristiche da Adobe Audience Manager, è necessario creare una connessione sorgente utilizzando [Connettore sorgente in Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). Il connettore di origine crea automaticamente lo schema con i gruppi di campi appropriati. Non è necessario aggiungere manualmente altri tipi di evento affinché lo schema possa funzionare con IA per l’analisi dei clienti.

Quando configuri una nuova istanza di IA per l’analisi dei clienti, `audienceName` e `audienceID` può essere utilizzato per selezionare una particolare caratteristica per il punteggio durante la definizione dell’obiettivo.

## Dati di output di IA per l’analisi dei clienti

IA per l’analisi dei clienti genera diversi attributi per singoli profili ritenuti idonei. Esistono due modi per utilizzare il punteggio (output) in base al provisioning. Se disponi di un set di dati abilitato per Real-Time Customer Profile, puoi sfruttare le informazioni provenienti da Real-Time Customer Profile in [Generatore di segmenti](../../segmentation/ui/segment-builder.md). Se non hai un set di dati abilitato per il profilo, puoi [scaricare l’output di Customer AI](./user-guide/download-scores.md) set di dati disponibile nel data lake.

Puoi trovare il set di dati di output in **Set di dati** in Platform. Tutti i set di dati di output di IA per l’analisi dei clienti iniziano con il nome **Punteggi di Customer AI - Name_of_app**. Analogamente, tutti gli schemi di output di IA per l’analisi dei clienti iniziano con il nome **Schema di IA per l’analisi dei clienti - Name_of_app**.

![cai-schema-name-of-app](./images/user-guide/cai-schema-name-of-app.png)

>[!NOTE]
>
> I valori di output vengono utilizzati da Real-Time Customer Profile che può essere utilizzato per creare e definire segmenti.

La tabella seguente descrive i vari attributi trovati nell’output di Customer AI:

| Attributo | Descrizione |
| ----- | ----------- |
| Punteggio | La probabilità relativa che un cliente raggiunga l’obiettivo previsto entro l’intervallo di tempo definito. Questo valore non deve essere considerato come percentuale di probabilità, ma piuttosto la probabilità di un individuo rispetto alla popolazione complessiva. Questo punteggio è compreso tra 0 e 100. |
| Probabilità | Questo attributo rappresenta la reale probabilità che un profilo raggiunga l’obiettivo previsto entro l’intervallo di tempo definito. Quando confronti gli output tra obiettivi diversi, si consiglia di considerare la probabilità rispetto al percentile o al punteggio. La probabilità deve sempre essere utilizzata per determinare la probabilità media in tutta la popolazione ammissibile, poiché la probabilità tende a essere sul lato inferiore per gli eventi che non si verificano frequentemente. I valori di probabilità sono compresi tra 0 e 1. |
| Percentile | Questo valore fornisce informazioni sulle prestazioni di un profilo rispetto ad altri profili con punteggio simile. Ad esempio, un profilo con un livello percentile di 99 per abbandono indica che è a maggior rischio di abbandono rispetto al 99% di tutti gli altri profili valutati. I percentili sono compresi tra 1 e 100. |
| Tipo tendenza | Tipo di propensione selezionato. |
| Data punteggio | Data in cui si è verificato il punteggio. |
| Fattori di influenza | Motivi previsti sul motivo per cui è probabile che un profilo venga convertito o abbandonato. I fattori sono costituiti dai seguenti attributi:<ul><li>Codice: il profilo o l’attributo comportamentale che influenza positivamente il punteggio previsto di un profilo. </li><li>Valore: il valore del profilo o dell’attributo comportamentale.</li><li>Importanza: indica il peso del profilo o dell’attributo comportamentale sul punteggio previsto (basso, medio, alto)</li></ul> |

>[!NOTE]
>
> - IA per l’analisi dei clienti utilizza solo dati aggiornati per l’ulteriore formazione e il punteggio. Allo stesso modo, quando richiedi di eliminare i dati, IA per l’analisi dei clienti si astiene dall’utilizzare i dati eliminati.
> - IA per l’analisi dei clienti sfrutta i set di dati di Platform. Per supportare le richieste di diritti dei consumatori che un brand può ricevere, i brand devono utilizzare Platform Privacy Service per inviare ai consumatori le richieste di accesso e cancellazione per rimuovere i propri dati attraverso il data lake, il servizio Identity e il profilo cliente in tempo reale.
> - Tutti i set di dati utilizzati per l’input/output dei modelli seguiranno le linee guida di Platform. Platform Data Encryption si applica ai dati in transito e a riposo. Per ulteriori informazioni, consulta la documentazione di [crittografia dei dati](../../../help/landing/governance-privacy-security/encryption.md)


## Passaggi successivi {#next-steps}

Dopo aver preparato i dati e aver impostato tutte le credenziali e gli schemi, inizia seguendo la [Configurare un’istanza di Customer AI](./user-guide/configure.md) guida. Questa guida illustra come creare un’istanza per Customer AI.




