---
title: Scheda del modello per il punteggio tendenza di Customer AI
description: Scopri il modello di intelligenza artificiale utilizzato per IA per l’analisi dei clienti.
hide: true
hidefromtoc: true
source-git-commit: 21a95bd678cf83c72a08213b647ef778cfb49cfc
workflow-type: tm+mt
source-wordcount: '1629'
ht-degree: 0%

---

# Scheda del modello per il punteggio tendenza di Customer AI

Come parte di [Intelligent Services in Adobe Experience Platform](../../../intelligent-services/home.md), puoi utilizzare [IA per l&#39;analisi dei clienti](../../../intelligent-services/customer-ai/overview.md) per generare previsioni e spiegazioni sui clienti a livello individuale.

Con l’aiuto di fattori influenti, puoi utilizzare IA per l’analisi dei clienti per dirti cosa potrebbe fare un cliente e perché. Inoltre, puoi sfruttare le previsioni e le informazioni di Customer AI per personalizzare le esperienze dei clienti fornendo le offerte e i messaggi più appropriati.

Leggi questa scheda del modello per informazioni sul modello di intelligenza artificiale utilizzato per abilitare Customer AI.

## Panoramica del modello {#model-overview}

* IA per l’analisi dei clienti è un modello basato sull’intelligenza artificiale progettato per generare punteggi di tendenza per gli utenti in base ai comportamenti passati e alle interazioni con un’azienda. Utilizza IA per l’analisi dei clienti per prevedere la probabilità che un cliente intraprenda azioni specifiche, come effettuare un acquisto, partecipare a contenuti o abbandonarsi al cliente. Questo modello viene distribuito all’interno di Experience Platform e si integra con vari flussi di lavoro di marketing e analisi dei clienti.
* Il modello è progettato per fornire agli addetti al marketing e ai team di coinvolgimento dei clienti informazioni fruibili prevedendo la probabilità che un cliente esegua una determinata azione, ad esempio effettuando un acquisto, registrandosi a un abbonamento o partecipando a una campagna e-mail. Gli output consentono alle aziende di ottimizzare la segmentazione del pubblico e personalizzare le interazioni dei clienti in base ai comportamenti previsti.
* Si tratta di un **modello di classificazione di apprendimento supervisionato** che prevede la probabilità che si verifichi un evento (acquisto, abbandono, coinvolgimento) in base ai dati storici del cliente. Viene addestrato utilizzando alberi decisionali di potenziamento del gradiente (GBDT) con regressione logistica per modellare i punteggi di tendenza.
* Gli utenti principali di questo modello sono professionisti del marketing, analisti di dati e team di coinvolgimento dei clienti che sfruttano Experience Platform per promuovere strategie di marketing basate sui dati.
* IA per l’analisi dei clienti si integra direttamente nei servizi di IA di Experience Platform, consentendo agli utenti di accedere agli output dei modelli tramite API e dashboard predefiniti. I punteggi di tendenza generati dal modello possono essere utilizzati in [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/get-started) e [Real-Time CDP](../../../rtcdp/home.md) per perfezionare la segmentazione del pubblico e personalizzare le strategie di marketing.

## Uso previsto {#intended-use}

* Questo modello viene utilizzato principalmente per **la segmentazione dei clienti, il marketing mirato e la previsione di abbandono**. Le aziende sfruttano questo modello per **prevedere le intenzioni di acquisto dei clienti, ottimizzare le campagne di marketing e migliorare le attività di personalizzazione**. Ad esempio, un’azienda di e-commerce potrebbe utilizzare il modello per identificare gli acquirenti più propensi e offrire loro promozioni esclusive.
* Gli addetti al marketing spesso hanno difficoltà a **identificare i clienti giusti per eseguire il targeting** e **ottimizzare le attività di coinvolgimento**. Questo modello **riduce le supposizioni** fornendo un approccio basato sui dati per il targeting dei clienti, garantendo che le risorse di marketing siano allocate in modo efficiente.
* Il modello è applicabile in diversi settori, tra cui e-commerce, commercio al dettaglio, servizi finanziari, telecomunicazioni e media. Qualsiasi azienda che si basa sul coinvolgimento dei clienti e sul marketing personalizzato può beneficiare di questo modello.
* Il modello **non deve essere utilizzato per decisioni ad alto rischio**, ad esempio per il punteggio di credito finanziario, la diagnostica medica o le valutazioni legali. Inoltre, non è destinato a essere utilizzato per prevedere comportamenti personali sensibili (condizioni di salute, preferenze politiche) a causa di potenziali preoccupazioni etiche.

## Ingressi e uscite del modello {#model-inputs-and-outputs}

* Il modello elabora i dati comportamentali dei clienti, gli attributi demografici e le interazioni storiche. Ciò include dati come la frequenza delle visite al sito web, la cronologia degli acquisti passati, il coinvolgimento con le e-mail di marketing e informazioni demografiche.
* I dati di input devono essere strutturati come oggetti JSON contenenti attributi del cliente e segnali comportamentali. Per l’elaborazione in batch, il modello accetta file CSV formattati in base agli standard di acquisizione dei dati di Experience Platform.
* Il modello restituisce un punteggio di propensione compreso tra 0 e 1, dove valori più elevati indicano una maggiore probabilità che si verifichi l’evento previsto. Inoltre, fornisce punteggi di importanza delle funzioni, consentendo agli utenti di comprendere quali fattori hanno influenzato la previsione.

**Input di esempio**

```json
{
  "customer_id": 12345,
  "past_purchases": 3,
  "last_visit_days": 7,
  "email_click_rate": 0.4
}
```

**Output di esempio**

```json
{
  "customer_id": 12345,
  "propensity_score": 0.82
}
```

## Dati del corso di formazione

* Il modello è stato addestrato su **dati di interazione cliente anonimi di prime parti** raccolti tramite Experience Platform. Include dati comportamentali storici del cliente **, record di transazioni, interazioni e-mail e metriche di coinvolgimento** in più settori.
* Il set di dati di formazione è costituito da **10 milioni di record cliente** provenienti da un set diverso di clienti Experience Platform. Questi record includono **interazioni cronologiche con i clienti, dati sulle transazioni, registri di coinvolgimento comportamentale e informazioni demografiche** provenienti da vari settori, ad esempio vendita al dettaglio, commercio elettronico, telecomunicazioni e finanza. I dati sono stati raccolti per un periodo di 24 mesi, garantendo una rappresentazione sufficiente delle tendenze stagionali e dei modelli di impegno a lungo termine.
* Il set di dati proviene principalmente da utenti ad alto coinvolgimento, che può introdurre distorsioni nella selezione. Per attenuare questo problema, il modello applica tecniche di campionamento stratificato, tecniche di audit basate su distorsioni e strategie di potenziamento dei dati.
* Il set di dati viene sottoposto a un’ampia fase di pre-elaborazione per garantire la coerenza, la qualità e l’usabilità dei dati.
   * **Gestione dei valori mancanti**: i valori mancanti vengono gestiti utilizzando una combinazione di imputazione media (per i campi numerici), imputazione modalità (per i campi categorici) e modellazione predittiva (per i casi mancanti complessi).
   * **Codifica categorica**: le variabili categoriche, come i segmenti cliente e le categorie di acquisto, vengono convertite in rappresentazioni numeriche tramite tecniche di codifica a caldo e di destinazione.
   * **Ridimensionamento e normalizzazione delle funzionalità**: la scalatura min-max viene applicata per le variabili limitate (età, reddito), mentre la standardizzazione z-score viene utilizzata per le funzionalità distribuite normalmente.
   * **Elaborazione preliminare aggiuntiva**: la pipeline include rilevamento e rimozione dei valori anomali, filtri duplicati, standardizzazione dei timestamp e ingegneria delle funzionalità per migliorare la modellazione predittiva.

## Architettura del modello e formazione

* Il modello sfrutta **[!DNL Gradient Boosting Decision Trees](GBDT) utilizzando[!DNL XGBoost]**, ottimizzato per i dati strutturati. Viene addestrato sulle sequenze storiche di eventi dei clienti per identificare i modelli comportamentali predittivi.
* Il modello viene creato utilizzando un approccio di apprendimento supervisionato, sfruttando GBDT con [!DNL XGBoost] come algoritmo di apprendimento primario. Inoltre, la regressione logistica è incorporata come modello di base per il benchmarking della precisione predittiva.
* Il modello è stato sviluppato utilizzando **[!DNL TensorFlow]**, **[!DNL XGBoost]** e **[!DNL scikit-learn]**. La formazione viene eseguita sull&#39;infrastruttura cloud di Adobe AI utilizzando **[!DNL NVIDIA V100]GPU** e supporta set di dati su larga scala.
* [!DNL NVIDIA V100 GPUs], ha ricevuto il training sull&#39;infrastruttura Google Cloud.
* [!DNL AUC-ROC], precisione-richiamo e convalida incrociata.

## Prestazioni e valutazione

* Il modello è stato testato utilizzando un approccio di convalida di riserva, in cui l’80% dei dati è stato utilizzato per la formazione e il 20% è stato riservato alla valutazione.
* L&#39;efficacia del modello viene misurata utilizzando [!DNL AUC-ROC] (0,85), precisione-richiamo (0,78) e punteggio F1 (0,80). Queste metriche consentono di valutare la potenza predittiva del modello in diversi segmenti.
* Minore precisione per i nuovi segmenti di clienti con dati storici limitati.
* Il modello potrebbe avere prestazioni insoddisfacenti per i clienti con dati storici limitati (problema di avviamento a freddo). Inoltre, gli effetti stagionali (tendenze degli acquisti durante le feste) possono richiedere frequenti corsi di aggiornamento per mantenere l’accuratezza.

## Equità e parzialità

* Il modello è stato sottoposto a **test di parità demografica** e **valutazioni di imparzialità avversaria** per rilevare disparità di prestazioni tra segmenti di utenti diversi.
* L&#39;analisi ha rivelato un calo delle prestazioni del **5% per gli utenti con dati di interazione cronologici limitati**. Per risolvere questo problema, il modello include tecniche di riponderazione durante l&#39;addestramento.
* Il set di dati è stratificato per garantire una rappresentazione proporzionale dei diversi dati demografici dei clienti e durante la formazione vengono introdotti vincoli di correttezza per evitare che il modello favorisca un determinato gruppo. I controlli di distorsione regolari vengono eseguiti utilizzando l&#39;analisi della parità demografica, consentendo adeguamenti in caso di disparità di prestazioni.

## Spiegabilità e interpretabilità

* Il modello sfrutta **[!DNL SHapley Additive Explanations](SHAP)** per quantificare l&#39;impatto di ogni funzione di input sulle previsioni, fornendo trasparenza sul modo in cui gli attributi del cliente influenzano i punteggi di tendenza. I valori SHAP consentono sia l&#39;interpretabilità globale, identificando i fattori più influenti in tutte le previsioni, sia l&#39;interpretabilità locale, spiegando le previsioni individuali per clienti specifici.
* Il modello supporta **[!DNL Local Interpretable Model-Agnostic Explanations](LIME)** e SHAP per fornire informazioni dettagliate sul modo in cui le funzioni di input influenzano le previsioni. LIME genera spiegazioni locali creando versioni perturbate dei dati di input e osservando i cambiamenti nelle previsioni, mentre SHAP assegna valori di contributo a ogni funzione, offrendo sia l&#39;interpretabilità globale che locale delle decisioni dei modelli.

## Robustezza e generalizzazione

* Il modello mantiene l&#39;80% di [!DNL AUC-ROC] quando viene testato su set di dati non visti, dimostrando una forte generalizzazione ai nuovi record dei clienti. Le prestazioni rimangono stabili tra i diversi segmenti del cliente, ma mostrano un lieve deterioramento quando il comportamento dell’utente si discosta in modo significativo dai modelli storici.
* Il modello è stato valutato rispetto a input perturbati e avversi, inclusi dati mancanti, iniezione di outlier e etichettatura intenzionalmente errata. Mentre le prestazioni rimangono solide in condizioni normali, la minore accuratezza del peggioramento (circa il 3-5%) è stata osservata in caso di modifiche estreme.

## Considerazioni sulla sicurezza e sulla privacy

* Il modello **non elabora o conserva informazioni personali (PII)** e tutti i dati utilizzati per la formazione sono anonimi e aggregati. Aderisce alla rigorosa conformità con le politiche sulla privacy di Adobe e RGPD, per garantire un utilizzo responsabile dei dati.
* Il modello incorpora tecniche di privacy differenziale per aggiungere rumore controllato ai dati, impedendo la reidentificazione delle persone. Inoltre, **i metodi di hashing, anonimizzazione e tokenizzazione vengono utilizzati per rimuovere PII** prima dell&#39;apprendimento e dell&#39;inferenza del modello.

## Implementazione e integrazione

* Il modello è ospitato sui servizi di intelligenza artificiale di Adobe Experience Platform e integrato con varie applicazioni Adobe. È disponibile tramite endpoint API e consente di accedere facilmente a previsioni in tempo reale e all’elaborazione batch nei flussi di lavoro di marketing e coinvolgimento dei clienti.
* Il modello viene eseguito in una distribuzione basata su **[!DNL Kubernetes]** con funzionalità di ridimensionamento automatico per gestire in modo efficiente carichi di lavoro diversi. Le risorse di elaborazione includono [!DNL NVIDIA V100] GPU per la formazione e l&#39;inferenza ottimizzata basata su CPU per la scalabilità in tempo reale.

## Monitoraggio e manutenzione

* Il modello viene **monitorato in modo continuo tramite[!DNL WatsonX]**, tenendo traccia degli indicatori delle prestazioni chiave come la deriva di precisione, i cambiamenti di importanza delle funzionalità e la stabilità delle previsioni. I meccanismi di rilevamento delle anomalie e di avviso avvisano il team quando si verificano deviazioni significative dal comportamento previsto.
* Il modello viene riqualificato mensilmente utilizzando dati aggiornati sulle interazioni dei clienti per garantire una rilevanza costante. La riqualificazione periodica contribuisce a mitigare la deriva dei dati e le fluttuazioni stagionali che potrebbero influire sulla precisione predittiva

## Preoccupazioni etiche e IA responsabile

* Il modello potrebbe potenzialmente introdurre distorsioni nel processo decisionale se non monitorato correttamente. Ad esempio, se alcuni dati demografici sono sovrarappresentati nei dati di formazione, il modello potrebbe favorire ingiustamente gruppi di clienti specifici.
* Experience Platform segue le linee guida sull&#39;intelligenza artificiale responsabili, garantendo che i modelli siano sottoposti a **controlli di distorsione, test di correttezza e supervisione umana** prima della distribuzione.

## Limitazioni note

* Il modello potrebbe avere difficoltà a prevedere con precisione i risultati per i prodotti o i segmenti di clienti nuovi, in cui non sono disponibili dati storici sufficienti. Inoltre, le variazioni stagionali nel comportamento del cliente possono causare fluttuazioni nella precisione predittiva se non vengono prese in considerazione durante la riqualificazione.
* Le prestazioni si riducono quando la cronologia dei clienti è sparsa, ad esempio per i nuovi acquirenti o per gli utenti con dati di coinvolgimento minimi. Inoltre, se i comportamenti dei clienti **si spostano a causa di fattori esterni come le recessioni economiche o le tendenze del settore**, il modello potrebbe richiedere un rapido adattamento per mantenere l&#39;accuratezza.

## Miglioramenti futuri

* Le iterazioni future includeranno tecniche di apprendimento del trasferimento per migliorare le prestazioni per gli utenti con avviamento a freddo e migliorare la capacità di adattamento ai comportamenti dei clienti in continua evoluzione. Inoltre, verrà introdotta l’integrazione dei dati in tempo reale per migliorare i tempi di risposta e la precisione del modello negli ambienti di marketing dinamici.
