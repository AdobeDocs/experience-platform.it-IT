---
title: Dettagli del modello di punteggio tendenza di Customer AI
description: Scopri il modello di intelligenza artificiale utilizzato per IA per l’analisi dei clienti.
hide: true
hidefromtoc: true
exl-id: b2eeb1d2-3c2b-40a0-b5cd-91e99d99a906
source-git-commit: 8230c71c9b7896dfb71506632754d48583d0dc21
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 0%

---

# Dettagli del modello di punteggio tendenza di Customer AI

## Panoramica del modello {#model-overview}

* **Nome modello e versione**: modello punteggio tendenza IA per l&#39;analisi dei clienti
* **Scopo del modello**: il modello è progettato per fornire agli addetti al marketing e ai team di coinvolgimento dei clienti informazioni actionable, prevedendo la probabilità che un consumatore esegua una determinata azione, ad esempio effettuare un acquisto, iscriversi a un abbonamento o partecipare a una campagna e-mail. Gli output consentono alle aziende di ottimizzare la segmentazione del pubblico e personalizzare le interazioni dei consumatori in base ai comportamenti previsti.
* **Utenti previsti**: gli utenti principali di questo modello sono professionisti del marketing, analisti di dati e team di coinvolgimento dei clienti che sfruttano [Real-Time CDP](../../../rtcdp/home.md) per gestire strategie di marketing basate sui dati.
* **Casi d&#39;uso**: questo modello viene utilizzato principalmente per la segmentazione del consumatore, il marketing mirato e la previsione di abbandono. Le aziende sfruttano questo modello per prevedere le intenzioni di acquisto dei consumatori, ottimizzare le campagne di marketing e migliorare le attività di personalizzazione. Ad esempio, un’azienda di e-commerce potrebbe utilizzare il modello per identificare gli acquirenti più propensi e offrire loro promozioni esclusive.
* **Punti critici**: gli addetti al marketing hanno spesso difficoltà a identificare i consumatori giusti per eseguire il targeting e ottimizzare le attività di coinvolgimento. Questo modello riduce le supposizioni fornendo un approccio basato sui dati per il targeting dei consumatori, garantendo che le risorse di marketing siano allocate in modo efficiente.
* **Possibile uso improprio**: il modello non deve essere utilizzato per casi di utilizzo ad alto rischio, come il punteggio di credito finanziario, la diagnostica medica o le valutazioni legali. Inoltre, il modello non deve essere utilizzato per prevedere i comportamenti personali sensibili (come le condizioni di salute, le preferenze politiche).

## Dettagli modello {#model-details}

* **Tipo di modello**: si tratta di un modello di classificazione di apprendimento supervisionato che prevede la probabilità che si verifichi un evento (ad esempio acquisto, abbandono, coinvolgimento) in base ai dati storici dei consumatori. Viene addestrato utilizzando alberi decisionali di potenziamento del gradiente (GBDT) con regressione logistica per modellare i punteggi di tendenza.
* **Input**: il modello elabora i dati comportamentali dei consumatori, gli attributi demografici e le interazioni cronologiche. Ciò include dati come la frequenza delle visite al sito web, la cronologia degli acquisti passati, il coinvolgimento con le e-mail di marketing e informazioni demografiche.
* **Output**: il modello restituisce un punteggio compreso tra 0 e 100, dove valori più elevati indicano una maggiore probabilità che l&#39;evento previsto si verifichi nella coorte di popolazione con punteggio. Inoltre, fornisce punteggi di importanza delle funzioni, consentendo agli esperti di marketing di comprendere quali fattori hanno influenzato la previsione.

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

* **Dati di formazione e pre-elaborazione**: il set di dati di formazione per ciascun cliente proviene direttamente dai propri dati in Adobe Experience Platform. Ciò include le interazioni storiche del cliente, i record transazionali, i registri di coinvolgimento comportamentale e le informazioni demografiche raccolte e memorizzate nell’istanza Adobe Experience Platform. Il set di dati sfrutta i dati specifici del cliente nell’arco temporale scelto, acquisendo le tendenze stagionali uniche e i pattern di coinvolgimento. Prima dell’utilizzo, il set di dati di ciascun cliente viene sottoposto a una pre-elaborazione personalizzata in base alle sue caratteristiche, che include la gestione del valore mancante, la codifica per categorie, la scalabilità delle funzioni, il rilevamento dei dati anomali e la progettazione delle funzioni per garantire una qualità e un’usabilità ottimali per il caso d’uso specifico.
   * I dati dei consumatori utilizzati per la formazione non vengono utilizzati per diversi clienti.
* **Specifiche di formazione**: il modello sfrutta [!DNL LightGBM] utilizzando [!DNL GBM], ottimizzato per i dati strutturati. Viene addestrato sulle sequenze storiche di eventi dei clienti per identificare i modelli comportamentali predittivi.
* **Framework di formazione**: il modello è stato sviluppato utilizzando [!DNL LightGBM] e [!DNL scikit-learn] ed è ospitato nell&#39;infrastruttura cloud di Adobe AI.
* **Infrastruttura di formazione**: [!DNL Databricks] cluster.

## Valutazione del modello {#model-evaluation}

* **Metriche e procedure di valutazione**: l&#39;efficacia del modello viene misurata utilizzando [!DNL AUC-ROC]. Poiché IA per l’analisi dei clienti si rivolge a una gamma molto ampia di casi di utilizzo da parte dei clienti, l’intervallo operativo non può essere noto. Pertanto, viene utilizzata una metrica [!DNL AUC] indipendente dalla portata e dal budget.
* **Dati di valutazione e pre-elaborazione**: i dati di valutazione includono record consumer di memorizzazione e vengono preelaborati in modo simile ai dati di formazione con i passaggi di normalizzazione, codifica e pulizia delle funzionalità per soddisfare le aspettative del formato di input. Una volta superata la finestra dei risultati, possiamo eseguire una valutazione finale delle prestazioni.

## Distribuzione del modello {#model-deployment}

* **Distribuzione del modello**: il modello è ospitato sui servizi di intelligenza artificiale di Adobe Experience Platform e integrato con varie applicazioni Adobe. È disponibile tramite endpoint API e consente di accedere facilmente a previsioni in tempo reale ed elaborazione batch attraverso i flussi di lavoro di marketing e coinvolgimento dei consumatori.
* **Monitoraggio del modello**: il modello viene monitorato continuamente tramite il monitoraggio del modello per visualizzare la deriva dalla configurazione dell&#39;addestramento. I riavvolgimenti periodici (una volta ogni 3 mesi) vengono eseguiti automaticamente.
* **Aggiornamento modello**: il modello viene riqualificato una volta ogni diversi mesi (al massimo una volta ogni 6 mesi) utilizzando dati aggiornati sulle interazioni con il consumatore per garantire una rilevanza costante. La riqualificazione periodica aiuta a mitigare la deriva dei dati e le fluttuazioni stagionali che potrebbero influire sull’accuratezza predittiva.

## Spiegabilità {#explainability}

**Spiegazione del modello**: il modello sfrutta [!DNL SHapley Additive Explanations] (SHAP) per quantificare l&#39;impatto di ogni funzione di input sulle previsioni, fornendo trasparenza sul modo in cui gli attributi del consumatore influenzano i punteggi di tendenza. I valori SHAP consentono sia l&#39;interpretabilità globale, identificando i fattori più influenti in tutte le previsioni, sia l&#39;interpretabilità locale, spiegando le singole previsioni per specifici consumatori. Il modello supporta anche [!DNL Local Interpretable Model-Agnostic Explanations] (LIME).

## Equità e parzialità {#fairness-and-bias}

* **Correttezza del modello**: questo modello viene addestrato su dati comportamentali anonimi associati agli ID dei cookie, senza accesso ad attributi demografici protetti come età, genere o etnia. Di conseguenza, la misurazione diretta dell&#39;equità tra i gruppi sensibili non è fattibile. Gli sforzi di mitigazione includono la normalizzazione per la frequenza delle attività degli utenti, l&#39;eliminazione delle funzioni eccessivamente dominanti e l&#39;esecuzione di controlli di calibrazione dei punteggi tra coorti. Teniamo conto della distorsione di recency e monitoriamo la distorsione di esposizione valutando le previsioni dei modelli sul traffico di sospensione randomizzato. Sono in corso valutazioni per rilevare e ridurre l’amplificazione delle distorsioni e i cicli di feedback durante la distribuzione dei modelli.
* **Distorsioni dei dati**: il set di dati proviene principalmente da utenti con un coinvolgimento maggiore, il che può introdurre distorsioni nella selezione. Per attenuare questo problema, il modello applica strategie di campionamento. A seconda del caso d’uso, i clienti devono considerare in che modo le potenziali distorsioni negli output dei modelli possono allinearsi o avere un impatto sull’applicazione a cui sono destinati.

## Robustezza {#robustness}

**Robustezza del modello**: il modello mantiene una forte generalizzazione per i nuovi record consumer. Le prestazioni rimangono stabili tra i diversi segmenti di consumatori, ma mostrano un lieve deterioramento quando il comportamento dell’utente si discosta in modo significativo dai modelli storici.

## Considerazioni etiche {#ethical-considerations}

**Considerazioni etiche associate al modello**: questo modello è destinato a casi di utilizzo di marketing e i clienti devono prestare maggiore cautela se lo applicano a domini sensibili o regolamentati come il credito o l&#39;occupazione. I risultati sono probabilistici e derivano da dati comportamentali, che possono riflettere distorsioni storiche o di rappresentazione. I clienti sono incoraggiati ad applicare la supervisione umana. Adobe Experience Platform segue le linee guida sull’intelligenza artificiale responsabile, garantendo che i modelli siano sottoposti a controlli di parzialità, test di imparzialità e supervisione umana prima della distribuzione. Per ulteriori informazioni, consulta i [Principi etici di Adobe AI](https://www.adobe.com/content/dam/cc/en/ai-ethics/pdfs/Adobe-AI-Ethics-Principles.pdf?msockid=0d85c8269eb36f0801d0ddb49fd16ebc).