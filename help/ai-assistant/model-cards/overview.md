---
title: Schede Modello Per Trasparenza Modello IA In Adobe Experience Platform
description: Scopri di più sui modelli di schede in Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 21a95bd678cf83c72a08213b647ef778cfb49cfc
workflow-type: tm+mt
source-wordcount: '2386'
ht-degree: 0%

---

# Schede modello per trasparenza modello AI in Adobe Experience Platform

Le schede modello sono i formati standard con cui viene comunicata la trasparenza del modello di IA. Le schede modello sono pubbliche e hanno lo scopo di migliorare la comprensione da parte dei clienti attuali e potenziali dei modelli di intelligenza artificiale utilizzati da Adobe. Le schede modello sono generalmente statiche. Tuttavia, esistono diversi aspetti dei modelli di intelligenza artificiale che possono cambiare nel tempo, tra cui derivazione, parzialità e altri attributi di trasparenza.

Leggi questo documento per scoprire di più sui modelli di schede in Adobe Experience Platform.

## Sezioni modello scheda {#model-card-sections}

Leggi quanto segue per una guida sulle diverse sezioni di una scheda modello, incluse le informazioni sulle domande a cui sono indirizzati.

### Panoramica del modello {#model-overview}

+++Visualizza domande e risposte di esempio

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Qual è il nome del modello? | Il nome ufficiale e la versione del modello di intelligenza artificiale | **CustomerAI Propensity Scoring Model v2.0** <br>CustomerAI è un modello basato sull&#39;intelligenza artificiale progettato per generare punteggi di propensione per gli utenti in base ai loro comportamenti passati e alle interazioni con un&#39;azienda. Consente di prevedere la probabilità che un cliente intraprenda azioni specifiche, ad esempio effettuare un acquisto, partecipare a contenuti o abbandonarsi al cliente. Questo modello viene distribuito all&#39;interno di Adobe Experience Platform e si integra con vari flussi di lavoro marketing e analisi del cliente.</br> |
| Qual è lo scopo del modello? | Breve descrizione dello scopo per cui è stato progettato il modello. | Il modello è progettato per fornire ai professionisti del marketing e ai team di coinvolgimento dei clienti informazioni fruibili prevedendo la probabilità che un cliente esegua una determinata azione, ad esempio effettuare un acquisto, iscriversi a un abbonamento o interagire con una campagna e-mail. I risultati consentono alle aziende di ottimizzare le segmentazione del pubblico e personalizzare le interazioni con i clienti in base ai comportamenti previsti. |
| Che tipo di modello è? | Il tipo di modello, ad esempio classificazione, regressione, generativo e così via. | Si tratta di un s **modello di classificazione di apprendimento supervisionato** che prevede la probabilità che si verifichi un evento (ad esempio, acquisto, abbandono, coinvolgimento) in base ai dati storici del cliente. Viene addestrato utilizzando alberi decisionali di potenziamento del gradiente (GBDT) con regressione logistica per modellare i punteggi di tendenza. |
| Chi sono gli utenti previsti? | I gruppi di utente interni ed esterni a cui è destinato il modello. | Gli utenti principali di questo modello sono professionisti del marketing, analisti di dati e team di coinvolgimento dei clienti che sfruttano Adobe Experience Platform per promuovere strategie di marketing basate sui dati. |
| In che modo questo modello si integra con Adobe Experience Platform? | Dettagli dell’integrazione e API utilizzate, nonché come si adattano ai flussi di lavoro. | CustomerAI si integra direttamente nei **servizi di intelligenza artificiale di Adobe Experience Platform**, consentendo agli utenti di accedere agli output dei modelli tramite API e dashboard predefiniti. I punteggi di tendenza generati dal modello possono essere utilizzati in **Adobe Journey Optimizer**, **e Adobe Real-Time CDP**, per perfezionare la segmentazione del pubblico e personalizzare le strategie di marketing. |

{style="table-layout:auto"}

+++

### Uso previsto {#intended-use}

+++Visualizza domande ed esempi di risposte

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Quali sono i casi d&#39;uso principali? | Gli scenari in cui è previsto l&#39;utilizzo del modello. | Questo modello viene utilizzato principalmente per la Segmentazione del cliente, le **marketing mirate e la previsione dell&#39;abbandono**. Le aziende sfruttare questo modello per **prevedere l&#39;intenzione di acquisto dei clienti, ottimizzare le campagne di marketing e migliorare le personalizzazione attività**. Ad esempio, un&#39;azienda e-commerce potrebbe utilizzare il modello per identificare gli acquirenti con grandi intenzioni e offrire loro promozioni esclusive. |
| Quali problemi risolve questo modello? | I principali punti dolenti affrontati dal modello. | Gli addetti al marketing spesso hanno difficoltà a **identificare i clienti giusti da destinazione** e **ottimizzare gli sforzi** di coinvolgimento. Questo modello **riduce le congetture** fornendo un **approccio** basato sui dati al targeting dei clienti, garantendo che le marketing risorse siano allocate in modo efficiente. |
| Per quali settori o domini è rilevante questo modello? | Un elenco dei settori applicabili. | Il modello è applicabile in più settori, tra cui **e-commerce, vendita al dettaglio, servizi finanziari, telecomunicazioni e media**. Qualsiasi azienda che si affida al coinvolgimento dei clienti e a marketing personalizzati può trarre vantaggio da questo modello. |
| Come non dovrebbe essere utilizzato questo modello? | Qualsiasi caso di uso improprio che dovrebbe essere evitato. | Il modello **non deve essere utilizzato per processi** decisionali ad alto rischio, come **il punteggio di credito finanziario, la diagnostica medica o le valutazioni** legali. Inoltre, non è destinato all&#39;uso nella **previsione di comportamenti personalmente sensibili (come condizioni di** salute, preferenze politiche) a causa di potenziali preoccupazioni etiche. |

{style="table-layout:auto"}

+++

### Modellare ingressi e uscite {#model-inputs-and-outputs}

+++Visualizza domande ed esempi di risposte

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Quali tipi di dati accetta il modello come input? | I tipi di dati che il modello accetta come input, inclusi i dati, le feature, i formati e le origini. | Il modello elabora **i dati comportamentali dei clienti, gli attributi demografici e le interazioni** storiche. Ciò include dati come la frequenza visita del sito Web, la cronologia degli acquisti passati, il coinvolgimento con le e-mail marketing e le informazioni demografiche. |
| In che formato devono essere gli input? | I formati di input accettati. | I dati di input devono essere strutturati come **oggetti JSON** contenenti attributi del cliente e segnali comportamentali. Per l&#39;elaborazione in batch, il modello accetta **file CSV** formattati in base agli standard di acquisizione dei dati di Adobe Experience Platform. |
| Cosa produce il modello? | Tipo di output generato dal modello. | Il modello restituisce un punteggio di propensione compreso tra 0 e 1, dove valori più elevati indicano una maggiore probabilità che si verifichi l’evento previsto. Inoltre, fornisce punteggi di importanza delle funzioni, consentendo agli utenti di comprendere quali fattori hanno influenzato la previsione. |
| Quali sono gli input e gli output di esempio? | Un input campione e un output corrispondente. | <ul><li>**Input di esempio:** json { &quot;customer_id&quot;: 12345, &quot;last_purchases&quot;: 3, &quot;last_visit_days&quot;: 7, &quot;email_click_rate&quot;: 0,4 }</li><li>**Output di esempio:** json { &quot;customer_id&quot;: 12345, &quot;propensity_score&quot;: 0.82 }</li></ul> |

{style="table-layout:auto"}

+++

### Dati del corso di formazione {#training-data}

+++Visualizza domande ed esempi di risposte

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Quali set di dati sono stati utilizzati per eseguire il training del modello? | Una descrizione delle origini dati. | Il modello è stato addestrato su dati di interazione con il cliente di prime parti e anonimizzati raccolti tramite Adobe Experience Platform. Include dati comportamentali storici dei clienti, record delle transazioni, interazioni e-mail e metriche di coinvolgimento in più settori. |
| Qual è la dimensione e l&#39;origine dei dati? | Volume e origine dell&#39;training dataset. | Il set di dati training è costituito da 10 milioni di record di clienti provenienti da una serie diversificata di Adobe Experience Platform clienti. Questi record includono interazioni storiche con i clienti, dati transazionali, registri di coinvolgimento comportamentale e informazioni demografiche di vari settori come vendita al dettaglio, e-commerce, telecomunicazioni e finanza. I dati sono stati raccolti per un periodo di 24 mesi, garantendo una rappresentazione sufficiente delle tendenze stagionali e dei modelli di impegno a lungo termine. |
| Esistono distorsioni note nel set di dati? | Considerazioni sulla distorsione e sforzi di mitigazione. | Il set di dati proviene principalmente da utenti ad alto coinvolgimento, che può introdurre distorsioni nella selezione. Per mitigare questo problema, il modello applica tecniche di campionamento stratificato, bias auditing e strategie di aumento dei dati. |
| Come vengono preelaborati i dati? | Passaggi intrapresi per pulire e preparare i dati. | Il set di dati viene sottoposto a un’ampia fase di pre-elaborazione per garantire la coerenza, la qualità e l’usabilità dei dati. <ol><li>**Gestione dei valori mancanti**: i valori mancanti vengono gestiti utilizzando una combinazione di imputazione media (per i campi numerici), imputazione modalità (per i campi categorici) e modellazione predittiva (per i casi mancanti complessi).</li><li>**Codifica categorica:** Le variabili categoriche, quali i segmenti cliente e le categorie di acquisto, vengono convertite in rappresentazioni numeriche mediante tecniche di codifica a caldo e di destinazione.</li><li>**Scalabilità e normalizzazione funzionalità:** la scalabilità min-max viene applicata per le variabili limitate (ad esempio età, reddito), mentre la standardizzazione z-score viene utilizzata per le funzionalità distribuite normalmente.</li><li>**Elaborazione preliminare aggiuntiva:** la pipeline include rilevamento e rimozione dei valori anomali, filtri duplicati, standardizzazione delle marche temporali e progettazione delle funzionalità per migliorare la predittività.</li></ol> |

{style="table-layout:auto"}

+++

### Architettura e training dei modelli {#model-architecture-and-training}

+++Visualizza domande ed esempi di risposte

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Quale architettura utilizza il modello? | Il tipo di rete neurale, il metodo del gruppo, ecc. | Il modello sfrutta gli alberi decisionali di incremento delle sfumature (GBDT) utilizzando XGBoost, ottimizzati per i dati strutturati. Viene addestrato sulle sequenze storiche di eventi dei clienti per identificare i modelli comportamentali predittivi. |
| Quali algoritmi sono stati applicati? | Le tecniche di apprendimento automatico utilizzate. | Il modello è costruito utilizzando un approccio di apprendimento supervisionato, sfruttando gli alberi decisionali di incremento del gradiente (GBDT) con XGBoost come algoritmo di apprendimento principale. Inoltre, la regressione logistica è incorporata come modello di base per il benchmarking dell&#39;accuratezza predittiva. |
| Quali training framework sono stati utilizzati? | I librerie o le piattaforme utilizzate per training. | Il modello è stato sviluppato utilizzando TensorFlow, XGBoost e scikit-learn. La formazione viene eseguita sull’infrastruttura cloud Adobe AI utilizzando le GPU NVIDIA V100 e supportando set di dati su larga scala. |
| Quali risorse di elaborazione sono state utilizzate per la formazione? | Hardware e risorse cloud utilizzate per training. | GPU NVIDIA V100, addestrate sull&#39;infrastruttura Google Cloud. |
| Quali metodi di valutazione sono stati utilizzati? | Metriche e procedure di test utilizzate per la valutazione. | AUC-ROC, richiamo di precisione e cross-convalida. |

{style="table-layout:auto"}

+++

### Prestazioni e valutazione {#performance-and-evaluation}

+++Visualizza domande ed esempi di risposte

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Come è stato testato il modello? | Metodi utilizzati per convalidare le prestazioni. | Il modello è stato testato utilizzando un approccio di convalida di riserva, in cui l’80% dei dati è stato utilizzato per la formazione e il 20% è stato riservato alla valutazione. |
| Quali metriche di valutazione sono state utilizzate? | Gli indicatori chiave di prestazione. | L&#39;efficacia del modello viene misurata utilizzando **AUC-ROC (0,85)**, **precision-recall (0,78)** e **F1-score (0,80)**. Queste metriche consentono di valutare la potenza predittiva del modello in diversi segmenti. |
| In che modo le prestazioni variano nei diversi scenari? | Le varianti di prestazioni specifiche del contesto. | Minore precisione per i nuovi segmenti di clienti con dati storici limitati. |
| Ci sono debolezze note o casi di fallimento? | Eventuali limiti o punti di errore. | Il modello potrebbe sottoperformare per i clienti con dati cronologici limitati (problema di avvio a freddo). Inoltre, gli effetti stagionali, come le tendenze dello shopping natalizio, possono richiedere frequenti interventi di riqualificazione per mantenere l&#39;accuratezza. |

{style="table-layout:auto"}

+++

### Equità e parzialità {#fairness-and-bias}

+++Visualizza domande ed esempi di risposte

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Quali controlli di equità sono stati effettuati? | Analisi della distorsione e processi di mitigazione eseguiti. | Il modello è stato sottoposto a test di parità demografica e valutazioni di equità contraddittoria per rilevare disparità di performance tra diversi segmenti utente. |
| Il modello influisce in modo sproporzionato su determinati gruppi? | Eventuali disparità nelle prestazioni che sono state identificate. | L’analisi ha rivelato un calo del 5% delle prestazioni per gli utenti con dati cronologici di interazione limitati. Per risolvere questo problema, il modello include tecniche di riponderazione durante l&#39;addestramento. |
| In che modo il modello attenua il bis? | Le tecniche utilizzate per affrontare i pregiudizi. | Il set di dati è stratificato per garantire la rappresentazione proporzionale di diversi dati demografici dei clienti e durante la training vengono introdotti vincoli di equità per impedire al modello di favorire un particolare gruppo. Vengono condotti audit periodici di distorsione utilizzando l&#39;analisi della parità demografica, consentendo adeguamenti se vengono rilevate disparità di prestazioni. |

{style="table-layout:auto"}

+++

### Spiegabilità e interpretabilità {#explainability-and-interpretability}

+++Visualizza domande e risposte di esempio

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Gli utenti possono capire perché il modello prende determinate decisioni? | I metodi di interpretabilità utilizzati dal modello. | Il modello sfrutta le **Spiegazioni aggiuntive di SHapley (SHAP)** per quantificare l&#39;impatto di ogni funzione di input sulle relative previsioni, fornendo trasparenza sul modo in cui gli attributi del cliente influenzano i punteggi di tendenza. I valori SHAP consentono sia l&#39;interpretabilità globale, identificando i fattori più influenti in tutte le previsioni, sia l&#39;interpretabilità locale, spiegando le previsioni individuali per clienti specifici. |
| Quali strumenti o tecniche sono disponibili per l&#39;interpretabilità? | Gli strumenti di spiegabilità disponibili. | Il modello supporta **Local Interpretable Model-Agnostic Explanations (LIME)** e SHAP per fornire informazioni sul modo in cui le funzioni di input influenzano le previsioni. LIME genera spiegazioni locali creando versioni perturbate dei dati di input e osservando i cambiamenti nelle previsioni, mentre SHAP assegna valori di contributo a ogni funzione, offrendo sia l&#39;interpretabilità globale che locale delle decisioni dei modelli. |

{style="table-layout:auto"}

+++

### Robustezza e generalizzazione {#robustness-and-generalization}

+++Visualizza domande e risposte di esempio

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Qual è la performance del modello su dati non visualizzati? | I risultati sui test delle prestazioni di generalizzazione. | Il modello mantiene **l&#39;80% di AUC-ROC** quando testato su set di dati non visualizzati, dimostrando una forte generalizzazione ai nuovi record dei clienti. Le prestazioni rimangono stabili tra i diversi segmenti del cliente, ma mostrano un lieve deterioramento quando il comportamento dell’utente si discosta in modo significativo dai modelli storici. |
| Il modello è stato sottoposto a prove di stress per gli input avversari? | Dettagli della valutazione di robustezza. | Il modello è stato valutato rispetto a input perturbati e contraddittori, inclusi dati mancanti, iniezione di valori anomali e etichettatura errata intenzionale. Mentre le prestazioni rimangono robuste in condizioni normali, è stato osservato un lieve degrado dell&#39;accuratezza (circa il 3-5%) in caso di modifiche estreme del contraddittorio. |

{style="table-layout:auto"}

+++

### Considerazioni sulla sicurezza e sulla privacy {#security-and-privacy-considerations}

+++Visualizza domande ed esempi di risposte

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Il modello gestisce dati sensibili? | Qualsiasi conformità informativa alle leggi sulla privacy. | Il modello non elabora né conserva alcuna informazione di identificazione personale (PII) e tutti i dati utilizzati per training sono resi anonimi e aggregati. Aderisce al rigoroso rispetto delle politiche GDPR, CCPA e interne Adobe Systems sulla privacy per garantire un utilizzo responsabile dei dati. |
| Quali tecniche di tutela della privacy sono state utilizzate? | Le tecniche utilizzate per garantire le misure sulla privacy. | Il modello incorpora tecniche di privacy differenziale per aggiungere rumore controllato ai dati, impedendo la reidentificazione delle persone. Inoltre, i metodi di hashing, anonimizzazione e tokenizzazione vengono utilizzati per rimuovere i dati PII prima dell&#39;apprendimento e dell&#39;inferenza dei modelli. |

{style="table-layout:auto"}

+++

### Monitoraggio e manutenzione {#monitoring-and-maintenance}

+++Visualizza domande e risposte di esempio

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Come vengono monitorate le prestazioni del modello nel tempo? | Dettagli sui meccanismi di tracciamento utilizzati per il modello. | Il modello viene costantemente monitorato tramite WatsonX, tenendo traccia degli indicatori di prestazioni chiave come la deriva di precisione, i cambiamenti di importanza delle caratteristiche e la stabilità predittiva. I meccanismi di rilevamento delle anomalie e di avviso avvisano il team quando si verificano deviazioni significative dal comportamento previsto. |
| Con quale frequenza viene ripetuto il training del modello? | Frequenza degli aggiornamenti nel modello. | Il modello viene riqualificato mensilmente utilizzando dati interazione con il cliente aggiornati per garantire la continua pertinenza. La riqualificazione periodica aiuta a mitigare la deriva dei dati e le fluttuazioni stagionali che potrebbero influire sull&#39;accuratezza predittiva. |

{style="table-layout:auto"}

+++

### Considerazioni etiche e IA responsabile {#ethical-considerations-and-responsible-ai}

+++Visualizza domande ed esempi di risposte

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Quali preoccupazioni etiche sono associate a questo modello? | I potenziali rischi che sono stati identificati. | Il modello potrebbe potenzialmente introdurre pregiudizi nel processo decisionale se non monitorato correttamente. Ad esempio, se alcuni dati demografici sono sovrarappresentati nei dati training, il modello potrebbe favorire ingiustamente gruppi di clienti specifici. |
| In che modo il modello si allinea con i principi dell&#39;IA responsabile? | Informazioni su come il modello è conforme alle linee guida etiche dell&#39;IA. | Adobe Experience Platform segue le linee guida dell&#39;IA responsabile, garantendo che i modelli siano sottoposti a verifiche di parzialità, test di equità e supervisione umana prima della distribuzione. |

{style="table-layout:auto"}

+++

### Limitazioni note {#known-limitations}

+++Visualizza domande ed esempi di risposte

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Quali sono le limitazioni note del modello? | Qualsiasi vincolo di prestazioni o caso d’uso identificato. | Il modello potrebbe avere difficoltà a prevedere con precisione i risultati per i prodotti appena lanciati o i segmenti di clienti in cui sono disponibili dati storici insufficienti. Inoltre, le variazioni stagionali nel comportamento del cliente possono causare fluttuazioni nella precisione predittiva se non vengono prese in considerazione durante la riqualificazione. |
| In quali condizioni il modello funziona male? | Eventuali debolezze identificate in relazione al modello. | Le prestazioni si riducono quando la cronologia dei clienti è sparsa, ad esempio per i nuovi acquirenti o per gli utenti con dati di coinvolgimento minimi. Inoltre, se i comportamenti dei clienti cambiano a causa di fattori esterni come le recessioni economiche o le tendenze del settore, il modello può richiedere un rapido adattamento per mantenere l’accuratezza. |

{style="table-layout:auto"}

+++

### Miglioramenti futuri {#future-improvements}

+++Visualizza domande e risposte di esempio

| Domanda | Informazioni necessarie | Esempio di risposta |
| --- | --- | --- |
| Quali miglioramenti sono pianificati per le iterazioni future? | Roadmap per i miglioramenti. | Le iterazioni future includeranno tecniche di apprendimento del trasferimento per migliorare le prestazioni per gli utenti cold-start e migliorare l&#39;adattabilità ai mutevoli comportamenti dei clienti. Inoltre, verrà introdotta l’integrazione dei dati in tempo reale per migliorare i tempi di risposta e la precisione del modello negli ambienti di marketing dinamici. |

{style="table-layout:auto"}

+++