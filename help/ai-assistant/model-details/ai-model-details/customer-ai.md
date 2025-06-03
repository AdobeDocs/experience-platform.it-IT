---
title: Scheda del modello per il punteggio tendenza di Customer AI
description: Scopri il modello di intelligenza artificiale utilizzato per IA per l’analisi dei clienti.
hide: true
hidefromtoc: true
exl-id: b2eeb1d2-3c2b-40a0-b5cd-91e99d99a906
source-git-commit: dddd699f231d54ee44b33f86a5c9e59c0aedc30c
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 0%

---

# Scheda del modello per il punteggio tendenza di Customer AI

## Panoramica del modello {#model-overview}

* Il modello di punteggio tendenza di IA per l’analisi dei clienti è progettato per fornire agli addetti al marketing e ai team di coinvolgimento dei clienti informazioni actionable, prevedendo la probabilità che un cliente esegua una determinata azione, ad esempio effettuare un acquisto, iscriversi a un abbonamento o partecipare a una campagna e-mail. Gli output consentono alle aziende di ottimizzare la segmentazione del pubblico e personalizzare le interazioni dei clienti in base ai comportamenti previsti.
* Gli utenti principali di questo modello sono professionisti del marketing, analisti di dati e team di coinvolgimento dei clienti che sfruttano [Real-Time CDP](../../../rtcdp/home.md) per promuovere strategie di marketing basate sui dati.
* Questo modello viene utilizzato principalmente per la segmentazione dei clienti, il marketing mirato e la previsione dell’abbandono. Le aziende sfruttano questo modello per prevedere le intenzioni di acquisto dei clienti, ottimizzare le campagne di marketing e migliorare le attività di personalizzazione. Ad esempio, un’azienda di e-commerce potrebbe utilizzare il modello per identificare gli acquirenti più propensi e offrire loro promozioni esclusive.
* Gli addetti al marketing spesso hanno difficoltà a identificare i clienti giusti per eseguire il targeting e ottimizzare le attività di coinvolgimento. Questo modello riduce le supposizioni fornendo un approccio basato sui dati per il targeting dei clienti, garantendo che le risorse di marketing siano allocate in modo efficiente.
* Il modello non deve essere utilizzato per il processo decisionale ad alto rischio, come il punteggio di credito finanziario, la diagnostica medica o le valutazioni legali. Inoltre, non è destinato a essere utilizzato per prevedere comportamenti personali sensibili (ad esempio, condizioni di salute, preferenze politiche) a causa di potenziali preoccupazioni etiche.

## Dettagli modello {#model-details}

* Si tratta di un modello di classificazione di apprendimento supervisionato che prevede la probabilità che si verifichi un evento (acquisto, abbandono, coinvolgimento) in base ai dati storici del cliente. Viene addestrato utilizzando alberi decisionali di potenziamento del gradiente (GBDT) con regressione logistica per modellare i punteggi di tendenza.
* Il modello elabora i dati comportamentali dei clienti, gli attributi demografici e le interazioni storiche. Ciò include dati come la frequenza delle visite al sito web, la cronologia degli acquisti passati, il coinvolgimento con le e-mail di marketing e informazioni demografiche.
* Il modello restituisce un punteggio compreso tra 0 e 100, dove valori più elevati indicano una maggiore probabilità che l’evento previsto si verifichi nella coorte di popolazione con punteggio. Inoltre, fornisce punteggi di importanza delle funzioni, consentendo agli utenti di comprendere quali fattori hanno influenzato la previsione.

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
  "SCORE": 89 
}
```

## Formazione sui modelli {#model-training}

* I set di dati di formazione per ciascun cliente provengono direttamente dai propri dati in Experience Platform. Ciò include le interazioni storiche del cliente, i record transazionali, i registri di coinvolgimento comportamentale e le informazioni demografiche raccolte e memorizzate nella sua istanza di Experience Platform. Il set di dati sfrutta i dati specifici del cliente nell’arco temporale scelto, acquisendo le tendenze stagionali uniche e i pattern di coinvolgimento. Prima dell’utilizzo, il set di dati di ciascun cliente viene sottoposto a una pre-elaborazione personalizzata in base alle sue caratteristiche, che include la gestione del valore mancante, la codifica per categorie, la scalabilità delle funzioni, il rilevamento dei dati anomali e la progettazione delle funzioni per garantire una qualità e un’usabilità ottimali per il caso d’uso specifico.
* Il modello sfrutta [!DNL LightGBM] utilizzando [!DNL GBM], ottimizzato per i dati strutturati. Viene addestrato sulle sequenze storiche di eventi dei clienti per identificare i modelli comportamentali predittivi.
* Il modello è stato sviluppato utilizzando [!DNL LightGBM] e [!DNL scikit-learn] ed è addestrato sull&#39;infrastruttura cloud di Adobe AI.
* Le risorse del computer utilizzate per l&#39;apprendimento del modello sono [!DNL Databricks] cluster.

## Valutazione del modello {#model-evaluation}

* L&#39;efficacia del modello viene misurata utilizzando [!DNL AUC-ROC]. Poiché IA per l’analisi dei clienti si rivolge a una gamma molto ampia di casi di utilizzo da parte dei clienti, l’intervallo operativo non può essere noto. Pertanto, viene utilizzata la metrica [!DNL AUC] perché è indipendente da portata e budget.
* I dati di valutazione includono i record dei clienti di memorizzazione e vengono preelaborati in modo simile ai dati di formazione con passaggi di normalizzazione, codifica e pulizia delle funzioni per soddisfare le aspettative del formato di input. Una volta superata la finestra dei risultati, è possibile eseguire la valutazione finale delle prestazioni.

## Distribuzione del modello {#model-deployment}

* Il modello è ospitato sui servizi di intelligenza artificiale di Experience Platform e integrato con varie applicazioni Adobe. È disponibile tramite endpoint API e consente di accedere facilmente a previsioni in tempo reale e all’elaborazione batch nei flussi di lavoro di marketing e coinvolgimento dei clienti.
* Il modello viene continuamente monitorato tramite il monitoraggio del modello per vedere la deriva dalla configurazione di addestramento. I riavvolgimenti periodici (una volta ogni 3 mesi) vengono eseguiti automaticamente.
* Il modello viene riqualificato una volta ogni diversi mesi (il massimo una volta ogni 6 mesi) utilizzando dati aggiornati sulle interazioni dei clienti per garantire una rilevanza costante. La riqualificazione periodica aiuta a mitigare la deriva dei dati e le fluttuazioni stagionali che potrebbero influire sull’accuratezza predittiva.

## Spiegabilità {#explainability}

Il modello sfrutta [!DNL SHapley Additive Explanations] (SHAP) per quantificare l&#39;impatto di ogni funzione di input sulle previsioni, fornendo trasparenza sul modo in cui gli attributi del cliente influenzano i punteggi di tendenza. I valori SHAP consentono sia l&#39;interpretabilità globale, identificando i fattori più influenti in tutte le previsioni, sia l&#39;interpretabilità locale, spiegando le previsioni individuali per clienti specifici. Il modello supporta anche [!DNL Local Interpretable Model-Agnostic Explanations] (LIME).

## Equità e parzialità {#fairness-and-bias}

* Questo modello viene addestrato su dati comportamentali anonimi associati agli ID dei cookie, senza accesso ad attributi demografici protetti come età, genere o etnia. Di conseguenza, la misurazione diretta dell&#39;equità tra i gruppi sensibili non è fattibile. Gli sforzi di mitigazione includono la normalizzazione per la frequenza delle attività degli utenti, l&#39;eliminazione delle funzioni eccessivamente dominanti e l&#39;esecuzione di controlli di calibrazione dei punteggi tra coorti.
* Il modello tiene conto della distorsione di recency e monitora la distorsione di esposizione valutando le previsioni del modello sul traffico di sospensione randomizzato. Sono in corso valutazioni per rilevare e ridurre l’amplificazione delle distorsioni e i cicli di feedback durante la distribuzione dei modelli.
* Il set di dati proviene principalmente da utenti ad alto coinvolgimento, che può introdurre distorsioni nella selezione. Per attenuare questo problema, il modello applica strategie di campionamento.

## Robustezza {#robustness}

Il modello mantiene una forte generalizzazione ai nuovi record dei clienti. Le prestazioni rimangono stabili tra i diversi segmenti del cliente, ma mostrano un lieve deterioramento quando il comportamento dell’utente si discosta in modo significativo dai modelli storici.

## Considerazioni sulla privacy e sulla sicurezza {#privacy-and-security-considerations}

* Il modello non elabora né conserva informazioni personali identificabili (PII) e tutti i dati utilizzati per la formazione sono resi anonimi e aggregati. Rispetta la rigorosa conformità a GDPR, CCPA e alle politiche interne sulla privacy di Adobe. Il modello incorpora tecniche differenziali di privacy, hashing, anonimizzazione e tokenizzazione per garantire la privacy.
* IA per l’analisi dei clienti rispetta le preferenze di consenso. Dopo aver [configurato e abilitato i criteri di consenso](../../../data-governance/policies/user-guide.md#create-a-consent-policy), IA per l&#39;analisi dei clienti rispetterà i dati di consenso raccolti da te. Per il punteggio del modello nelle esecuzioni successive del modello vengono utilizzati solo i dati consentiti. I nuovi punteggi sostituiranno i punteggi precedenti e possono essere utilizzati nella segmentazione. Questa funzione è attualmente disponibile solo per i clienti di HealthCare Shield e per i clienti di Privacy and Security Shield.

## Considerazioni etiche {#ethical-considerations}

Il modello potrebbe potenzialmente introdurre distorsioni nel processo decisionale. Per evitare questo problema, Experience Platform segue le linee guida sull’intelligenza artificiale responsabile, garantendo che i modelli siano sottoposti ad audit basati su errori sistematici, test di imparzialità e supervisione umana prima della distribuzione.
