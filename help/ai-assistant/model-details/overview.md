---
title: Dettagli Del Modello Per La Trasparenza Del Modello Di Intelligenza Artificiale In Adobe Experience Platform
description: Scopri i dettagli del modello in Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: 74a8ef82-cff9-4a7e-95c8-f915eb664eda
source-git-commit: 6623c7dad0fc4ddb7cb79e8f474b824915f130fc
workflow-type: tm+mt
source-wordcount: '3171'
ht-degree: 0%

---

# Dettagli del modello per la trasparenza del modello di IA in Adobe Experience Platform

Un dettaglio del modello di IA è il formato standard tramite il quale viene comunicata la trasparenza del modello di IA. I dettagli del modello forniscono informazioni complete sul modello sottostante su cui è basato un determinato strumento di intelligenza artificiale. I dettagli del modello includono informazioni quali lo scopo di uno strumento di intelligenza artificiale, i dati di formazione, le metriche delle prestazioni, le limitazioni e le considerazioni etiche. Puoi utilizzare la trasparenza fornita dai dettagli del modello per comprendere meglio le funzionalità e i limiti del modello, nonché per promuovere in modo migliore un uso responsabile ed equo dell’intelligenza artificiale.

I dettagli del modello sono pubblici e sono intesi a migliorare la comprensione, sia attuale che futura, dei modelli di intelligenza artificiale utilizzati da Adobe. I dettagli del modello sono generalmente statici. Tuttavia, esistono diversi aspetti dei modelli di intelligenza artificiale che possono cambiare nel tempo, tra cui derivazione, parzialità e altri attributi di trasparenza.

Leggi questo documento per scoprire i dettagli del modello in Adobe Experience Platform.

## Sezioni dei dettagli del modello {#model-detail-sections}

Un dettaglio del modello è composto da una varietà di sezioni diverse, ciascuna incentrata su un particolare aspetto del modello di intelligenza artificiale.

Leggete quanto segue per una guida sulle diverse sezioni di un modello, incluse le informazioni sulle domande che trattano.

### Panoramica del modello {#model-overview}

La panoramica del modello contiene informazioni generali su un modello di intelligenza artificiale. Utilizza questa sezione per fornire informazioni quali il nome, lo scopo e il tipo del modello di intelligenza artificiale. Inoltre, puoi utilizzare questa sezione per identificare gli utenti desiderati ed approfondire il modo in cui il modello si integra con Experience Platform.

+++Visualizza domande e risposte di esempio

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Qual è il nome del modello? | Il nome ufficiale e la versione del modello di IA | **CustomerAI Propensity Scoring Model v2.0** <br>CustomerAI è un modello basato sull&#39;intelligenza artificiale progettato per generare punteggi di tendenza per gli utenti in base ai comportamenti passati e alle interazioni con un&#39;azienda. Consente di prevedere la probabilità che un cliente intraprenda azioni specifiche, ad esempio effettuare un acquisto, partecipare a contenuti o abbandonarsi al cliente. Questo modello viene distribuito all&#39;interno di Adobe Experience Platform e si integra con vari flussi di lavoro di marketing e analisi dei clienti.</br> |
| Qual è lo scopo del modello? | Breve descrizione di ciò che il modello è progettato per fare. | Il modello è progettato per fornire agli addetti al marketing e ai team di coinvolgimento dei clienti informazioni fruibili prevedendo la probabilità che un cliente esegua una determinata azione, ad esempio effettuando un acquisto, registrandosi a un abbonamento o partecipando a una campagna e-mail. Gli output consentono alle aziende di ottimizzare la segmentazione del pubblico e personalizzare le interazioni dei clienti in base ai comportamenti previsti. |
| Che tipo di modello è? | Il tipo di modello, ad esempio classificazione, regressione, generativo e così via. | Si tratta di un s **modello di classificazione di apprendimento supervisionato** che prevede la probabilità che si verifichi un evento (ad esempio, acquisto, abbandono, coinvolgimento) in base ai dati storici del cliente. Viene addestrato utilizzando alberi decisionali di potenziamento del gradiente (GBDT) con regressione logistica per modellare i punteggi di tendenza. |
| Chi sono gli utenti previsti? | I gruppi di utenti interni ed esterni a cui è destinato il modello. | Gli utenti principali di questo modello sono professionisti del marketing, analisti di dati e team di coinvolgimento dei clienti che sfruttano Adobe Experience Platform per promuovere strategie di marketing basate sui dati. |
| In che modo questo modello si integra con Adobe Experience Platform? | Dettagli dell’integrazione e API utilizzate, nonché come si adattano ai flussi di lavoro. | CustomerAI si integra direttamente nei **servizi di intelligenza artificiale di Adobe Experience Platform**, consentendo agli utenti di accedere agli output dei modelli tramite API e dashboard predefiniti. I punteggi di tendenza generati dal modello possono essere utilizzati in **Adobe Journey Optimizer**, **e Adobe Real-Time CDP**, per perfezionare la segmentazione del pubblico e personalizzare le strategie di marketing. |

{style="table-layout:auto"}

+++

### Uso previsto {#intended-use}

La sezione dell’uso previsto contiene informazioni sui casi d’uso principali del modello di intelligenza artificiale. Puoi utilizzare questa sezione per approfondire i problemi che il modello intende risolvere, i settori e/o i domini a cui il modello è pertinente e i casi di utilizzo errato che devono essere evitati quando si utilizza il modello di intelligenza artificiale.

+++Visualizza domande e risposte di esempio

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Quali sono i casi d’uso principali? | Gli scenari in cui è previsto l’utilizzo del modello. | Questo modello viene utilizzato principalmente per **la segmentazione dei clienti, il marketing mirato e la previsione di abbandono**. Le aziende sfruttano questo modello per **prevedere le intenzioni di acquisto dei clienti, ottimizzare le campagne di marketing e migliorare le attività di personalizzazione**. Ad esempio, un’azienda di e-commerce potrebbe utilizzare il modello per identificare gli acquirenti più propensi e offrire loro promozioni esclusive. |
| Quali problemi risolve questo modello? | I punti critici affrontati dal modello. | Gli addetti al marketing spesso hanno difficoltà a **identificare i clienti giusti per eseguire il targeting** e **ottimizzare le attività di coinvolgimento**. Questo modello **riduce le supposizioni** fornendo un **approccio basato sui dati** al targeting dei clienti, garantendo che le risorse di marketing siano allocate in modo efficiente. |
| A quali settori o domini si riferisce questo modello? | Un elenco dei settori applicabili. | Il modello è applicabile a più settori, tra cui **e-commerce, vendita al dettaglio, servizi finanziari, telecomunicazioni e media**. Qualsiasi azienda che si basa sul coinvolgimento dei clienti e sul marketing personalizzato può beneficiare di questo modello. |
| Come non utilizzare questo modello? | Eventuali casi di uso improprio da evitare. | Il modello **non deve essere utilizzato per decisioni ad alto rischio**, ad esempio **valutazione del credito finanziario, diagnostica medica o valutazioni legali**. Inoltre, non è destinato all&#39;uso in **previsione di comportamenti personali sensibili** (come condizioni di salute, preferenze politiche) a causa di potenziali preoccupazioni etiche. |

{style="table-layout:auto"}

+++

### Ingressi e uscite del modello {#model-inputs-and-outputs}

La sezione input e output del modello contiene informazioni sui tipi di dati supportati che il modello assume come input e restituisce come output. Puoi utilizzare questa sezione per fornire esempi degli input e degli output di dati rilevanti per il modello di intelligenza artificiale.

+++Visualizza domande e risposte di esempio

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Quali tipi di dati assume il modello come input? | I tipi di dati utilizzati dal modello come input, inclusi: caratteristiche dei dati, formati e origini. | Il modello elabora **dati comportamentali dei clienti, attributi demografici e interazioni cronologiche**. Ciò include dati come la frequenza delle visite al sito web, la cronologia degli acquisti passati, il coinvolgimento con le e-mail di marketing e informazioni demografiche. |
| Che formato devono essere gli input? | I formati di input accettati. | I dati di input devono essere strutturati come **oggetti JSON** contenenti attributi del cliente e segnali comportamentali. Per l&#39;elaborazione in batch, il modello accetta **file CSV** formattati in base agli standard di acquisizione dei dati di Adobe Experience Platform. |
| Cosa produce il modello? | Tipo di output generato dal modello. | Il modello restituisce un punteggio di propensione compreso tra 0 e 1, dove valori più elevati indicano una maggiore probabilità che si verifichi l’evento previsto. Inoltre, fornisce punteggi di importanza delle funzioni, consentendo agli utenti di comprendere quali fattori hanno influenzato la previsione. |
| Quali sono gli input e gli output di esempio? | Un input campione e un output corrispondente. | <ul><li>**Input di esempio:** json { &quot;customer_id&quot;: 12345, &quot;last_purchases&quot;: 3, &quot;last_visit_days&quot;: 7, &quot;email_click_rate&quot;: 0,4 }</li><li>**Output di esempio:** json { &quot;customer_id&quot;: 12345, &quot;propensity_score&quot;: 0.82 }</li></ul> |

{style="table-layout:auto"}

+++

### Dati del corso di formazione {#training-data}

La sezione dei dati di formazione contiene informazioni sui set di dati utilizzati per addestrare un determinato modello di intelligenza artificiale. Puoi utilizzare questa sezione per approfondire le dimensioni e l’origine dei dati di apprendimento, i pregiudizi identificati nel set di dati e il modo in cui i dati sono stati preelaborati.

+++Visualizza domande e risposte di esempio

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Quali set di dati sono stati utilizzati per addestrare il modello? | Una descrizione delle origini dati. | Il modello è stato addestrato sui dati di prime parti anonimi relativi all’interazione con il cliente raccolti tramite Adobe Experience Platform. Include dati comportamentali storici sui clienti, record delle transazioni, interazioni e-mail e metriche di coinvolgimento in più settori. |
| Quali sono le dimensioni e l&#39;origine dei dati? | Volume e origine del set di dati di formazione. | Il set di dati di formazione è costituito da 10 milioni di record di clienti provenienti da diversi clienti Adobe Experience Platform. Questi record includono interazioni storiche con i clienti, dati sulle transazioni, registri di coinvolgimento comportamentale e informazioni demografiche provenienti da vari settori come il commercio al dettaglio, l’e-commerce, le telecomunicazioni e la finanza. I dati sono stati raccolti per un periodo di 24 mesi, garantendo una rappresentazione sufficiente delle tendenze stagionali e dei modelli di impegno a lungo termine. |
| Esistono distorsioni note nel set di dati? | Considerazioni sulla distorsione e sforzi di mitigazione. | Il set di dati proviene principalmente da utenti ad alto coinvolgimento, che può introdurre distorsioni nella selezione. Per attenuare questo problema, il modello applica tecniche di campionamento stratificato, tecniche di audit basate su distorsioni e strategie di potenziamento dei dati. |
| Come vengono preelaborati i dati? | Passaggi intrapresi per pulire e preparare i dati. | Il set di dati viene sottoposto a un’ampia fase di pre-elaborazione per garantire la coerenza, la qualità e l’usabilità dei dati. <ol><li>**Gestione dei valori mancanti**: i valori mancanti vengono gestiti utilizzando una combinazione di imputazione media (per i campi numerici), imputazione modalità (per i campi categorici) e modellazione predittiva (per i casi mancanti complessi).</li><li>**Codifica categorica:** Le variabili categoriche, quali i segmenti cliente e le categorie di acquisto, vengono convertite in rappresentazioni numeriche mediante tecniche di codifica a caldo e di destinazione.</li><li>**Scalabilità e normalizzazione funzionalità:** la scalabilità min-max viene applicata per le variabili limitate (ad esempio età, reddito), mentre la standardizzazione z-score viene utilizzata per le funzionalità distribuite normalmente.</li><li>**Elaborazione preliminare aggiuntiva:** la pipeline include rilevamento e rimozione dei valori anomali, filtri duplicati, standardizzazione delle marche temporali e progettazione delle funzionalità per migliorare la predittività.</li></ol> |

{style="table-layout:auto"}

+++

### Architettura del modello e formazione {#model-architecture-and-training}

La sezione Architettura del modello e formazione descrive il blueprint del modello di intelligenza artificiale. Questa sezione si riferisce alla struttura e alla progettazione del modello di IA, compresi dettagli sul tipo di algoritmo e sui metodi di valutazione utilizzati. Puoi inoltre utilizzare questa sezione per fornire informazioni sui framework di formazione utilizzati, nonché sulle risorse di calcolo utilizzate nella formazione.

+++Visualizza domande e risposte di esempio

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Quale architettura utilizza il modello? | Il tipo di rete neurale, il metodo del gruppo, ecc. | Il modello sfrutta gli alberi decisionali di incremento delle sfumature (GBDT) utilizzando XGBoost, ottimizzati per i dati strutturati. Viene addestrato sulle sequenze storiche di eventi dei clienti per identificare i modelli comportamentali predittivi. |
| Quali algoritmi sono stati applicati? | Le tecniche di apprendimento automatico utilizzate. | Il modello è costruito utilizzando un approccio di apprendimento supervisionato, sfruttando gli alberi decisionali di incremento del gradiente (GBDT) con XGBoost come algoritmo di apprendimento principale. Inoltre, la regressione logistica è incorporata come modello di base per il benchmarking della precisione predittiva. |
| Quali framework di formazione sono stati utilizzati? | Le librerie o le piattaforme utilizzate per la formazione. | Il modello è stato sviluppato utilizzando TensorFlow, XGBoost e scikit-learn. La formazione viene eseguita sull’infrastruttura cloud Adobe AI utilizzando le GPU NVIDIA V100 e supportando set di dati su larga scala. |
| Quali risorse di elaborazione sono state utilizzate per la formazione? | Risorse hardware e cloud utilizzate per la formazione. | GPU NVIDIA V100, formazione sull&#39;infrastruttura Google Cloud. |
| Quali metodi di valutazione sono stati utilizzati? | Le metriche e le procedure di test utilizzate per la valutazione. | AUC-ROC, precisione-richiamo e validazione incrociata. |

{style="table-layout:auto"}

+++

### Prestazioni e valutazione {#performance-and-evaluation}

La sezione prestazioni e valutazione contiene informazioni sulle metriche e sui metodi utilizzati per valutare il livello di esecuzione delle attività previste da parte del modello. Puoi utilizzare questa sezione per fornire informazioni sulle metriche di valutazione utilizzate, nonché sui punti deboli o i casi di errore identificati.

+++Visualizza domande e risposte di esempio

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Come è stato testato il modello? | Metodi utilizzati per convalidare le prestazioni. | Il modello è stato testato utilizzando un approccio di convalida di riserva, in cui l’80% dei dati è stato utilizzato per la formazione e il 20% è stato riservato alla valutazione. |
| Quali metriche di valutazione sono state utilizzate? | Gli indicatori chiave di prestazione. | L&#39;efficacia del modello viene misurata utilizzando **AUC-ROC (0,85)**, **precision-recall (0,78)** e **F1-score (0,80)**. Queste metriche consentono di valutare la potenza predittiva del modello in diversi segmenti. |
| In che modo le prestazioni variano nei diversi scenari? | Le varianti di prestazioni specifiche del contesto. | Minore precisione per i nuovi segmenti di clienti con dati storici limitati. |
| Ci sono debolezze note o casi di fallimento? | Eventuali limiti o punti di errore. | Il modello potrebbe avere prestazioni insoddisfacenti per i clienti con dati storici limitati (problema di avviamento a freddo). Inoltre, gli effetti stagionali, come le tendenze degli acquisti durante le feste, possono richiedere frequenti corsi di aggiornamento per mantenere l’accuratezza. |

{style="table-layout:auto"}

+++

### Equità e parzialità {#fairness-and-bias}

La sezione equità e distorsione contiene informazioni sulle prestazioni del modello di IA per quanto riguarda le metriche di equità e distorsione. L&#39;equità si riferisce alla capacità del modello di fornire risultati equi tra diversi gruppi demografici e casi d&#39;uso, mentre la distorsione si riferisce a errori sistematici che portano a risultati ingiusti. Utilizza questa sezione per approfondire i controlli di correttezza eseguiti e per discutere in che modo il modello attenui i pregiudizi.

+++Visualizza domande e risposte di esempio

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Quali controlli di correttezza sono stati eseguiti? | Analisi di distorsione e processi di mitigazione eseguiti. | Il modello è stato sottoposto a test di parità demografica e a valutazioni di imparzialità avversarie per rilevare le disparità di prestazioni tra i diversi segmenti di utenti. |
| Il modello influisce in modo sproporzionato su alcuni gruppi? | Eventuali disparità nelle prestazioni identificate. | L’analisi ha rivelato un calo del 5% delle prestazioni per gli utenti con dati cronologici di interazione limitati. Per risolvere questo problema, il modello include tecniche di riponderazione durante l&#39;addestramento. |
| In che modo il modello attenua i pregiudizi? | Tecniche utilizzate per risolvere i pregiudizi. | Il set di dati è stratificato per garantire una rappresentazione proporzionale dei diversi dati demografici dei clienti e durante la formazione vengono introdotti vincoli di correttezza per evitare che il modello favorisca un determinato gruppo. I controlli di distorsione regolari vengono eseguiti utilizzando l&#39;analisi della parità demografica, consentendo adeguamenti in caso di disparità di prestazioni. |

{style="table-layout:auto"}

+++

### Spiegabilità e interpretabilità {#explainability-and-interpretability}

La sezione spiegabilità e interpretabilità contiene informazioni sulla capacità di un modello di intelligenza artificiale di fornire spiegazioni chiare e comprensibili e sulla facilità con cui un utente umano può capire in che modo le funzioni di input influiscono sulle previsioni e sulle risposte. Usa questa sezione per spiegare come gli utenti possono comprendere meglio perché il tuo modello prende determinate decisioni e quali strumenti o tecniche sono disponibili per l’interpretabilità.

+++Visualizza domande e risposte di esempio

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Gli utenti possono capire perché il modello prende determinate decisioni? | I metodi di interpretabilità utilizzati dal modello. | Il modello sfrutta le **Spiegazioni aggiuntive di SHapley (SHAP)** per quantificare l&#39;impatto di ogni funzione di input sulle relative previsioni, fornendo trasparenza sul modo in cui gli attributi del cliente influenzano i punteggi di tendenza. I valori SHAP consentono sia l&#39;interpretabilità globale, identificando i fattori più influenti in tutte le previsioni, sia l&#39;interpretabilità locale, spiegando le previsioni individuali per clienti specifici. |
| Quali strumenti o tecniche sono disponibili per l&#39;interpretabilità? | Gli strumenti di spiegabilità disponibili. | Il modello supporta **Local Interpretable Model-Agnostic Explanations (LIME)** e SHAP per fornire informazioni sul modo in cui le funzioni di input influenzano le previsioni. LIME genera spiegazioni locali creando versioni perturbate dei dati di input e osservando i cambiamenti nelle previsioni, mentre SHAP assegna valori di contributo a ogni funzione, offrendo sia l&#39;interpretabilità globale che locale delle decisioni dei modelli. |

{style="table-layout:auto"}

+++

### Robustezza e generalizzazione {#robustness-and-generalization}

La sezione relativa alla robustezza e alla generalizzazione contiene informazioni sulle prestazioni del modello di intelligenza artificiale in caso di dati non visualizzati. Inoltre, puoi utilizzare questa sezione per approfondire in che modo il modello mantiene le prestazioni e l’accuratezza, dati gli input imprevisti o impegnativi.

>[!TIP]
>
>Nell’intelligenza artificiale, per &quot;dati non visualizzati&quot; si intendono i dati diversi da quelli su cui è stato addestrato un determinato modello.

+++Visualizza domande e risposte di esempio

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Quali sono le prestazioni del modello sui dati non visualizzati? | I risultati sul test delle prestazioni di generalizzazione. | Il modello mantiene il **80% AUC-ROC** quando viene testato su set di dati non visti, dimostrando una forte generalizzazione ai nuovi record dei clienti. Le prestazioni rimangono stabili tra i diversi segmenti del cliente, ma mostrano un lieve deterioramento quando il comportamento dell’utente si discosta in modo significativo dai modelli storici. |
| Il modello è stato sottoposto a prove di stress per gli input avversari? | Dettagli della valutazione di robustezza. | Il modello è stato valutato rispetto a input perturbati e avversi, inclusi dati mancanti, iniezione di outlier e etichettatura intenzionalmente errata. Mentre le prestazioni rimangono solide in condizioni normali, la minore accuratezza del peggioramento (circa il 3-5%) è stata osservata in caso di modifiche estreme. |

{style="table-layout:auto"}

+++

### Considerazioni sulla sicurezza e sulla privacy {#security-and-privacy-considerations}

La sezione relativa alla sicurezza e alla privacy contiene informazioni sulle misure e le pratiche implementate per proteggere i dati sensibili e garantire l’utilizzo sicuro del modello. Puoi utilizzare questa sezione per rispondere a domande su come il modello gestisce i dati sensibili.

+++Visualizza domande e risposte di esempio

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Il modello gestisce dati sensibili? | Qualsiasi informazione conforme alle leggi sulla privacy. | Il modello non elabora né conserva informazioni personali identificabili (PII) e tutti i dati utilizzati per la formazione sono resi anonimi e aggregati. Aderisce alla rigorosa conformità con le politiche sulla privacy di Adobe e RGPD, per garantire un utilizzo responsabile dei dati. |
| Quali tecniche di tutela della privacy sono state utilizzate? | Le tecniche utilizzate per garantire le misure sulla privacy. | Il modello incorpora tecniche di privacy differenziale per aggiungere rumore controllato ai dati, impedendo la reidentificazione delle persone. Inoltre, i metodi di hashing, anonimizzazione e tokenizzazione vengono utilizzati per rimuovere i dati PII prima dell&#39;apprendimento e dell&#39;inferenza dei modelli. |

{style="table-layout:auto"}

+++

### Monitoraggio e manutenzione {#monitoring-and-maintenance}

La sezione relativa al monitoraggio e alla manutenzione contiene informazioni sul modo in cui le prestazioni del modello vengono monitorate nel tempo e sulla frequenza con cui il modello viene riaddestrato. È possibile utilizzare questa sezione per fornire informazioni sul modo in cui vengono tracciate metriche quali precisione, precisione, richiamo e latenza.

+++Visualizza domande e risposte di esempio

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Come vengono monitorate le prestazioni del modello nel tempo? | Dettagli sui meccanismi di tracciamento utilizzati per il modello. | Il modello viene costantemente monitorato tramite WatsonX, tenendo traccia degli indicatori di prestazioni chiave come la deriva di precisione, i cambiamenti di importanza delle caratteristiche e la stabilità predittiva. I meccanismi di rilevamento delle anomalie e di avviso avvisano il team quando si verificano deviazioni significative dal comportamento previsto. |
| Con quale frequenza viene riaddestrato il modello? | La frequenza degli aggiornamenti sul modello. | Il modello viene riqualificato mensilmente utilizzando dati aggiornati sulle interazioni dei clienti per garantire una rilevanza costante. La riqualificazione periodica aiuta a mitigare la deriva dei dati e le fluttuazioni stagionali che potrebbero influire sull’accuratezza predittiva. |

{style="table-layout:auto"}

+++

### Considerazioni etiche e IA responsabile {#ethical-considerations-and-responsible-ai}

La sezione Considerazioni etiche e IA responsabile contiene informazioni su qualsiasi dubbio etico associato al modello di IA. Questa sezione contiene anche il livello di aderenza del modello ai principi di intelligenza artificiale responsabili. Utilizza questa sezione per fornire informazioni sui potenziali impatti etici dell&#39;utilizzo del modello, tra cui il riconoscimento dei pregiudizi, la garanzia di correttezza e la prevenzione di danni a individui o gruppi.

+++Visualizza domande e risposte di esempio

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Quali preoccupazioni di natura etica sono associate a questo modello? | I rischi potenziali che sono stati identificati. | Il modello potrebbe potenzialmente introdurre distorsioni nel processo decisionale se non monitorato correttamente. Ad esempio, se alcuni dati demografici sono sovrarappresentati nei dati di formazione, il modello potrebbe favorire ingiustamente gruppi di clienti specifici. |
| In che modo il modello si allinea ai principi di IA responsabile? | Informazioni su come il modello è conforme alle linee guida sull’etica dell’intelligenza artificiale. | Adobe Experience Platform segue le linee guida sull’intelligenza artificiale responsabile, garantendo che i modelli siano sottoposti a controlli di parzialità, test di imparzialità e supervisione umana prima della distribuzione. |

{style="table-layout:auto"}

+++

### Limitazioni note {#known-limitations}

La sezione limitazioni note contiene informazioni sulle limitazioni esistenti identificate per il modello di intelligenza artificiale. Usa questa sezione per sottolineare le condizioni in cui il modello di intelligenza artificiale potrebbe funzionare male e per delineare eventuali limitazioni di cui gli utenti devono essere a conoscenza.

+++Visualizza domande e risposte di esempio

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Quali sono le limitazioni note del modello? | Qualsiasi vincolo di prestazioni o caso d’uso identificato. | Il modello potrebbe avere difficoltà a prevedere con precisione i risultati per i prodotti o i segmenti di clienti nuovi, in cui non sono disponibili dati storici sufficienti. Inoltre, le variazioni stagionali nel comportamento del cliente possono causare fluttuazioni nella precisione predittiva se non vengono prese in considerazione durante la riqualificazione. |
| In quali condizioni il modello funziona male? | Eventuali debolezze identificate in relazione al modello. | Le prestazioni si riducono quando la cronologia dei clienti è sparsa, ad esempio per i nuovi acquirenti o per gli utenti con dati di coinvolgimento minimi. Inoltre, se i comportamenti dei clienti cambiano a causa di fattori esterni come le recessioni economiche o le tendenze del settore, il modello può richiedere un rapido adattamento per mantenere l’accuratezza. |

{style="table-layout:auto"}

+++

### Miglioramenti futuri {#future-improvements}

La sezione sui miglioramenti futuri contiene informazioni sugli aggiornamenti delle funzioni pianificati per il modello di intelligenza artificiale. Utilizza questa sezione per sviluppare la roadmap dei miglioramenti.

+++Visualizza domande e risposte di esempio

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Quali miglioramenti sono pianificati per le iterazioni future? | La roadmap dei miglioramenti. | Le iterazioni future includeranno tecniche di apprendimento del trasferimento per migliorare le prestazioni per gli utenti con avviamento a freddo e migliorare la capacità di adattamento ai comportamenti dei clienti in continua evoluzione. Inoltre, verrà introdotta l’integrazione dei dati in tempo reale per migliorare i tempi di risposta e la precisione del modello negli ambienti di marketing dinamici. |

{style="table-layout:auto"}

+++
