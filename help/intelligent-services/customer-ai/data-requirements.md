---
keywords: Experience Platform;guida introduttiva;customer ai;argomenti più comuni;customer ai input;customer ai output; requisiti dei dati
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Requisiti dei dati in Customer AI
topic-legacy: Getting started
description: Scopri di più sugli eventi, gli input e gli output richiesti utilizzati da Customer AI.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '2484'
ht-degree: 1%

---


# Input e output in IA per l’analisi dei clienti

Il documento seguente illustra i diversi eventi, input e output richiesti utilizzati in Customer AI.

## Introduzione {#getting-started}

Di seguito sono riportati i passaggi per creare modelli di propensione e identificare i tipi di pubblico target per il marketing personalizzato in IA per l’analisi dei clienti:

1. Casi d’uso generali: in che modo i modelli di propensione aiutano a identificare i tipi di pubblico target per il marketing personalizzato? Quali sono i miei obiettivi aziendali e le tattiche corrispondenti per raggiungere l’obiettivo? Dove può rientrare la modellazione della propensione in questo processo?

2. Assegnare priorità ai casi d’uso: quali sono le priorità più alte per l’azienda?

3. Creare modelli in Customer AI: guarda questo [tutorial rapido](https://experienceleague.adobe.com/docs/platform-learn/tutorials/intelligent-services/configure-customer-ai.html?lang=it) e fai riferimento al nostro [Guida all’interfaccia utente](../customer-ai/user-guide/configure.md) un processo dettagliato per la creazione di un modello.

4. [Creare segmenti](../customer-ai/user-guide/create-segment.md) utilizzo dei risultati del modello.

5. Intraprendere azioni aziendali mirate in base a questi segmenti. Monitora i risultati e ripeti le azioni da migliorare.

Di seguito sono riportati alcuni esempi di configurazioni per il primo modello.  Il modello di esempio, incorporato in questo documento, utilizza un modello di IA per l’analisi dei clienti per prevedere chi sarà probabilmente convertito per un’attività di vendita al dettaglio nei successivi 30 giorni. Il set di dati di input è un set di dati di Adobe Analytics.

| Passaggio | Definizione | Esempio |
| ---- | ------ | ------- |
| Configurazione | Specifica le informazioni di base sul modello. | **Nome**: modello di propensione all’acquisto della matita <br> **Tipo di modello**: Conversione |
| Seleziona dati | Specifica i set di dati utilizzati per generare il modello. | **Set di dati**: set di dati di Adobe Analytics <br> **Identità**: assicurati che la colonna Identity per ogni set di dati sia impostata come identità comune. |
| Definisci obiettivo | Definisci l’obiettivo, la popolazione idonea, gli eventi personalizzati e gli attributi del profilo. | **Obiettivo di previsione**: Seleziona `commerce.purchases.value` è uguale a matita <br> **Finestra Risultato**: 30 giorni. |
| Imposta opzioni | Imposta la pianificazione per l’aggiornamento del modello e abilita i punteggi per il profilo | **Pianificazione**: Settimanale <br> **Abilita per profilo**: questo deve essere abilitato affinché l’output del modello possa essere utilizzato nella segmentazione. |

## Panoramica dei dati {#data-overview}

Le sezioni seguenti descrivono i diversi eventi richiesti, input e output utilizzati in Customer AI.

IA per l’analisi dei clienti funziona analizzando i seguenti set di dati per prevedere i punteggi di propensione di abbandono (quando è probabile che un cliente smetta di utilizzare il prodotto) o conversione (quando è probabile che un cliente effettui un acquisto):

- Dati di Adobe Analytics utilizzando [Connettore di origine di Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Adobe Audience Manager dati utilizzando [Connettore sorgente in Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- [Set di dati di Experience Event](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html)
- [Set di dati di Consumer Experience Event](https://experienceleague.adobe.com/docs/experience-platform/intelligent-services/data-preparation.html#cee-schema)

Puoi aggiungere più set di dati da origini diverse se ciascuno di essi condivide lo stesso tipo di identità (spazio dei nomi), ad esempio un ECID. Per ulteriori informazioni sull’aggiunta di più set di dati, consulta [Guida utente di Customer AI](../customer-ai/user-guide/configure.md).

>[!IMPORTANT]
>
>I connettori sorgente richiedono fino a quattro settimane per la retrocompilazione dei dati. Se hai impostato di recente un connettore, è necessario verificare che il set di dati abbia la lunghezza minima dei dati richiesta per IA per l’analisi dei clienti. Rivedi il [dati storici](#data-requirements) per verificare di disporre di dati sufficienti per l’obiettivo predittivo.

La tabella seguente illustra alcuni termini comuni utilizzati in questo documento:

| Termine | Definizione |
| --- | --- |
| [Experience Data Model (XDM)](../../xdm/home.md) | XDM è il framework fondamentale che consente a Adobe Experience Cloud, con tecnologia Adobe Experience Platform, di inviare il messaggio giusto alla persona giusta, sul canale giusto, nel momento esatto giusto. Platform utilizza il sistema XDM per organizzare i dati in un modo che ne semplifica l’utilizzo per i servizi Platform. |
| [Schema XDM](../../xdm/schema/composition.md) | Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i sistemi, diventa più semplice mantenere un significato e quindi ottenere valore dai dati. Prima di poter acquisire i dati in Platform, è necessario comporre uno schema per descrivere la struttura dei dati e fornire vincoli al tipo di dati che possono essere contenuti all’interno di ciascun campo. Gli schemi sono costituiti da una classe XDM di base e da zero o più gruppi di campi schema. |
| [Classe XDM](../../xdm/schema/field-constraints.md) | Tutti gli schemi XDM descrivono dati che possono essere classificati come `Experience Event`. Il comportamento dei dati di uno schema è definito dalla classe dello schema, che viene assegnata a uno schema al momento della creazione. Le classi XDM descrivono il minor numero di proprietà che uno schema deve contenere per rappresentare un particolare comportamento di dati. |
| [Gruppi di campi](../../xdm/schema/composition.md) | Componente che definisce uno o più campi in uno schema. I gruppi di campi impongono il modo in cui i loro campi vengono visualizzati nella gerarchia dello schema e pertanto presentano la stessa struttura in ogni schema in cui sono inclusi. I gruppi di campi sono compatibili solo con classi specifiche, identificate dalle rispettive `meta:intendedToExtend` attributo. |
| [Tipo di dati](../../xdm/schema/composition.md) | Componente che può anche fornire uno o più campi per uno schema. Tuttavia, a differenza dei gruppi di campi, i tipi di dati non sono vincolati a una particolare classe. Questo rende i tipi di dati un’opzione più flessibile per descrivere strutture di dati comuni riutilizzabili in più schemi con classi potenzialmente diverse. I tipi di dati descritti in questo documento sono supportati dagli schemi CEE e Adobe Analytics. |
| [Profilo cliente in tempo reale](../../profile/home.md) | Real-time Customer Profile fornisce un profilo consumer centralizzato per una gestione mirata e personalizzata delle esperienze. Ogni profilo contiene dati aggregati in tutti i sistemi, nonché resoconti con marca temporale utilizzabili di eventi che hanno coinvolto l’individuo che si sono verificati in qualsiasi sistema utilizzato con Experience Platform. |

## Dati di input di IA per l’analisi dei clienti {#customer-ai-input-data}

Per i set di dati di input, come Adobe Analytics e Adobe Audience Manager, i rispettivi connettori di origine mappano direttamente gli eventi in questi gruppi di campi standard (Commerce, Web, Application e Search) per impostazione predefinita durante il processo di connessione. La tabella seguente mostra i campi evento nei gruppi di campi standard predefiniti per IA per l’analisi dei clienti.

Per ulteriori informazioni sulla mappatura dei dati di Adobe Analytics o di Audienci Manager, consulta l’Audience Manager Mappature dei campi di Analytics [guida alle mappature dei campi](../../sources/connectors/adobe-applications/mapping/audience-manager.md).

Puoi utilizzare gli schemi XDM di Experience Event o Consumer Experience Event per set di dati di input che non vengono compilati tramite uno dei connettori precedenti. Durante il processo di creazione dello schema è possibile aggiungere altri gruppi di campi XDM. I gruppi di campi possono essere forniti per Adobe, come i gruppi di campi standard o i gruppi di campi personalizzati, che corrispondono alla rappresentazione dei dati in Platform.

>[!IMPORTANT]
>
>Devi accertarti che i dati vengano inseriti in questi set di dati di input. Se nei set di dati di input non vengono trovati eventi dai gruppi di campi standard, devi aggiungere eventi personalizzati durante il flusso di lavoro di configurazione. Vedi i dettagli sugli eventi personalizzati.

### Gruppi di campi standard utilizzati da IA per l’analisi dei clienti {#standard-events}

Gli Eventi di esperienza vengono utilizzati per determinare i vari comportamenti dei clienti. A seconda della struttura dei dati, i tipi di evento elencati di seguito potrebbero non includere tutti i comportamenti del cliente. È compito dell’utente determinare quali campi dispongono dei dati necessari per identificare in modo chiaro e inequivocabile l’attività dell’utente sul web o su altri canali specifici. A seconda dell’obiettivo predittivo, i campi obbligatori necessari possono cambiare.

>[!NOTE]
>
>Se utilizzi dati di Adobe Analytics o Adobe Audience Manager, lo schema viene creato automaticamente con gli eventi standard richiesti necessari per acquisire i dati. Se stai creando un tuo schema EE personalizzato per acquisire i dati, è necessario considerare quali gruppi di campi sono necessari per acquisire i dati.

IA per l’analisi dei clienti utilizza gli eventi in questi quattro gruppi di campi standard per impostazione predefinita: Commerce, Web, Application e Search. Non è necessario disporre di dati per ogni evento nei gruppi di campi standard elencati di seguito, ma per alcuni scenari sono richiesti determinati eventi. Se sono disponibili eventi nei gruppi di campi standard, si consiglia di includerli nello schema. Ad esempio, se desideri creare un modello di IA per l’analisi dei clienti per prevedere gli eventi di acquisto, è utile disporre di dati dai gruppi di campi Commerce e Dettagli pagina web.

Per visualizzare un gruppo di campi nell’interfaccia utente di Platform, seleziona la **[!UICONTROL Schemi]** nella barra a sinistra, quindi seleziona il pulsante **[!UICONTROL Gruppi di campi]** scheda.

| Gruppo di campi | Tipo di evento | Percorso campo XDM |
| --- | --- | --- |
| [!UICONTROL Dettagli Commerce] | ordine | <li> `commerce.order.purchaseID` </li> <li> `productListItems.SKU` </li> |
|  | productListViews | <li> `commerce.productListViews.value` </li> <li> `productListItems.SKU` </li> |
|  | checkout | <li> `commerce.checkouts.value` </li> <li> `productListItems.SKU` </li> |
|  | acquisti | <li> `commerce.purchases.value` </li> <li> `productListItems.SKU` </li> |
|  | productListRemovals | <li> `commerce.productListRemovals.value` </li> <li> `productListItems.SKU` </li> |
|  | productListOpens | <li> `commerce.productListOpens.value` </li> <li> `productListItems.SKU` </li> |
|  | productViews | <li> `commerce.productViews.value` </li> <li> `productListItems.SKU` </li> |
| [!UICONTROL Dettagli web] | webVisit | `web.webPageDetails.name` |
|  | webInteraction | `web.webInteraction.linkClicks.value` |
| [!UICONTROL Dettagli applicazione] | applicationCloses | <li> `application.applicationCloses.value` </li> <li> `application.name` </li> |
|  | applicationCrashed | <li> `application.crashes.value` </li> <li> `application.name` </li> |
|  | applicationFeatureUsages | <li> `application.featureUsages.value` </li> <li> `application.name` </li> |
|  | applicationFirstLaunches | <li> `application.firstLaunches.value` </li> <li> `application.name` </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> `application.name` </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> `application.name` </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> `application.name` </li> |
| [!UICONTROL Dettagli di ricerca] | ricerca | `search.keywords` |

Inoltre, IA per l’analisi dei clienti può utilizzare i dati di abbonamento per generare modelli di abbandono migliori. I dati di abbonamento sono necessari per ogni profilo utilizzando [[!UICONTROL Abbonamento]](../../xdm/data-types/subscription.md) formato del tipo di dati. La maggior parte dei campi è facoltativa. Tuttavia, per un modello di abbandono ottimale, si consiglia vivamente di fornire dati per il maggior numero possibile di campi, ad esempio: `startDate`, `endDate`e ogni altro dettaglio pertinente. Rivolgiti al team del tuo account per ulteriore supporto su questa funzione.

### Aggiunta di eventi personalizzati e attributi di profilo {#add-custom-events}

Se disponi di informazioni da includere oltre a quelle predefinite [campi evento standard](#standard-events) utilizzato da Customer AI, puoi utilizzare [configurazione evento personalizzata](./user-guide/configure.md#custom-events) per migliorare i dati utilizzati dal modello.

#### Quando utilizzare eventi personalizzati

Gli eventi personalizzati sono necessari quando i set di dati scelti nel passaggio di selezione del set di dati contengono *nessuno* dei campi evento predefiniti utilizzati da IA per l’analisi dei clienti. IA per l’analisi dei clienti necessita di informazioni su almeno un evento di comportamento dell’utente diverso dal risultato.

Gli eventi personalizzati sono utili per:

- Integrazione nel modello della conoscenza del dominio o delle competenze precedenti.

- Miglioramento della qualità del modello predittivo.

- Ottenere ulteriori informazioni e interpretazioni.

I migliori candidati per gli eventi personalizzati sono i dati che contengono conoscenze del dominio che possono essere predittive del risultato. Alcuni esempi generali di eventi personalizzati includono:

- Registrati per l&#39;account

- Iscriviti alla newsletter

- Effettuare una chiamata al servizio clienti

Di seguito sono riportati alcuni esempi di eventi personalizzati specifici del settore:

| Settore | Eventi personalizzati |
| --- | --- |
| Vendita al dettaglio | Transazione in-store<br>Iscriviti alla carta club<br>Clip coupon mobile. |
| Intrattenimento | Iscrizione alla stagione di acquisto <br> Trasmetti video. |
| Ricettività | Effettuare la prenotazione del ristorante <br> Acquista punti fedeltà. |
| Viaggi | Aggiungi informazioni sul viaggiatore conosciuto Acquista miglia. |
| Comunicazioni | Piano di aggiornamento/downgrade/annullamento. |

Per poter essere selezionati, gli eventi personalizzati devono rappresentare le azioni avviate dall&#39;utente. Ad esempio, &quot;Invia e-mail&quot; è un’azione avviata da un addetto marketing e non dall’utente, pertanto non deve essere utilizzata come evento personalizzato.

### Dati storici

IA per l’analisi dei clienti richiede dati storici per la formazione dei modelli. La durata richiesta per l’esistenza dei dati nel sistema è determinata da due elementi chiave: la finestra dei risultati e la popolazione ammissibile.

Per impostazione predefinita, IA per l’analisi dei clienti cerca un utente che abbia avuto attività negli ultimi 45 giorni se non viene fornita alcuna definizione di popolazione idonea durante la configurazione dell’applicazione. Inoltre, IA per l’analisi dei clienti richiede almeno 500 eventi di qualificazione e 500 eventi non qualificati (1000 in totale) da dati storici basati su una definizione di obiettivo prevista.

Gli esempi seguenti illustrano l&#39;utilizzo di una semplice formula che consente di determinare la quantità minima di dati richiesti. Se disponi di un numero di dati superiore al requisito minimo, è probabile che il modello fornisca risultati più precisi. Se la quantità di dati è inferiore a quella minima richiesta, il modello avrà esito negativo poiché non sono disponibili dati sufficienti per l&#39;apprendimento del modello.

**Formula**:

Per decidere la durata minima richiesta dei dati esistenti nel sistema:

- Per creare le funzioni sono necessari almeno 30 giorni. Confronta l’intervallo di lookback di idoneità con 30 giorni:

   - Se l’intervallo di lookback di idoneità è superiore a 30 giorni, il requisito di dati = intervallo di lookback di idoneità + intervallo di risultati.

   - In caso contrario, il fabbisogno di dati = 30 giorni + intervallo di risultati.

** Se per la definizione della popolazione idonea sono presenti più condizioni, l’intervallo di lookback di idoneità è quello più lungo.

>[!NOTE]
>
>30 è il numero minimo di giorni richiesti per la popolazione ammissibile. In caso contrario, il valore predefinito è 45 giorni.

**Esempi**:

- Desideri prevedere se un cliente acquisterà probabilmente un orologio nei prossimi 30 giorni per coloro che hanno un’attività web negli ultimi 60 giorni.

   - Intervallo di lookback di idoneità = 60 giorni

   - Finestra risultati = 30 giorni

   - Dati richiesti = 60 giorni + 30 giorni = 90 giorni

- Desideri prevedere se è probabile che l’utente acquisti un orologio nei prossimi 7 giorni **senza** fornendo una popolazione ammissibile esplicita. In questo caso, la popolazione ammissibile viene considerata automaticamente &quot;coloro che hanno avuto attività negli ultimi 45 giorni&quot; e la finestra di risultato è di 7 giorni.

   - Intervallo di lookback di idoneità = 45 giorni

   - Finestra risultati = 7 giorni

   - Dati richiesti = 45 giorni + 7 giorni = 52 giorni

- Vuoi prevedere se il cliente è probabile che acquisti un orologio nei prossimi 7 giorni per coloro che hanno alcune attività web negli ultimi 7 giorni.

   - Intervallo di lookback di idoneità = 7 giorni

   - Dati minimi necessari per creare funzionalità = 30 giorni

   - Finestra risultati = 7 giorni

   - Dati richiesti = 30 giorni + 7 giorni = 37 giorni

Anche se IA per l’analisi dei clienti richiede un periodo di tempo minimo per consentire l’esistenza dei dati nel sistema, funziona meglio anche con i dati recenti. Utilizzando dati comportamentali più recenti, IA per l’analisi dei clienti è probabile che generi una previsione più accurata del comportamento futuro di un utente.

## Dati di output di IA per l’analisi dei clienti {#customer-ai-output-data}

IA per l’analisi dei clienti genera diversi attributi per singoli profili ritenuti idonei. Esistono due modi per utilizzare il punteggio (output) in base al provisioning. Se disponi di un set di dati abilitato per Real-time Customer Profile, puoi sfruttare le informazioni provenienti da Real-time Customer Profile in [Generatore di segmenti](../../segmentation/ui/segment-builder.md). Se non hai un set di dati abilitato per il profilo, puoi [scaricare l’output di Customer AI](./user-guide/download-scores.md) set di dati disponibile nel data lake.

Puoi trovare il set di dati di output in Platform **Set di dati** Workspace. Tutti i set di dati di output di IA per l’analisi dei clienti iniziano con il nome **Punteggi di Customer AI - NAME_OF_APP**. Analogamente, tutti gli schemi di output di IA per l’analisi dei clienti iniziano con il nome **Schema di IA per l’analisi dei clienti - Name_of_app**.

![Nome dei set di dati di output in Customer AI](./images/user-guide/cai-schema-name-of-app.png)

La tabella seguente descrive i vari attributi trovati nell’output di Customer AI:

| Attributo | Descrizione |
| ----- | ----------- |
| [!UICONTROL Punteggio] | La probabilità relativa che un cliente raggiunga l’obiettivo previsto entro l’intervallo di tempo definito. Questo valore non deve essere considerato come percentuale di probabilità, ma piuttosto la probabilità di un individuo rispetto alla popolazione complessiva. Questo punteggio è compreso tra 0 e 100. |
| Probabilità | Questo attributo rappresenta la reale probabilità che un profilo raggiunga l’obiettivo previsto entro l’intervallo di tempo definito. Quando confronti gli output tra obiettivi diversi, ti consigliamo di considerare la probabilità rispetto al percentile o al punteggio. La probabilità deve sempre essere utilizzata per determinare la probabilità media in tutta la popolazione ammissibile, poiché la probabilità tende a essere sul lato inferiore per gli eventi che non si verificano frequentemente. I valori per l’intervallo di probabilità sono compresi tra 0 e 1. |
| Percentile | Questo valore fornisce informazioni sulle prestazioni di un profilo rispetto ad altri profili con punteggio simile. Ad esempio, un profilo con un livello percentile di 99 per abbandono indica che è a maggior rischio di abbandono rispetto al 99% di tutti gli altri profili valutati. I percentili sono compresi tra 1 e 100. |
| Tipo tendenza | Tipo di propensione selezionato. |
| Data punteggio | Data in cui si è verificato il punteggio. |
| Fattori di influenza | Questi sono i motivi previsti per cui un profilo ha probabilità di conversione o abbandono. Questi fattori sono costituiti dai seguenti attributi:<ul><li>Codice: il profilo o l’attributo comportamentale che influenza positivamente il punteggio previsto di un profilo. </li><li>Valore: il valore del profilo o dell’attributo comportamentale.</li><li>Importanza: indica il peso del profilo o dell’attributo comportamentale sul punteggio previsto (basso, medio, alto)</li></ul> |

## Passaggi successivi {#next-steps}

Una volta preparati i dati e assicurati che tutte le credenziali e gli schemi siano presenti, fai riferimento a [Configurare un’istanza di Customer AI](./user-guide/configure.md) guida, che illustra un tutorial dettagliato per creare un’istanza di Customer AI.