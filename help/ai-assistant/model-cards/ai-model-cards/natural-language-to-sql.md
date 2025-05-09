---
title: Scheda modello SQL con linguaggio naturale dell'Assistente IA
description: Scopri il modello di IA per l’Assistente all’intelligenza artificiale per SQL AI.
hide: true
hidefromtoc: true
source-git-commit: 70b705a7c6df24ad9549c46832ff4898253670ac
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Scheda linguaggio naturale per modello SQL dell&#39;Assistente all&#39;intelligenza artificiale

## Panoramica del modello {#model-overview}

* Il nome ufficiale del modello è AI Assistant Operational Insights Natural Language to SQL Model ([!DNL NL2SQL]) ed è stato rilasciato nella sua ultima versione GA nel febbraio 2025.
* Il modello è progettato per tradurre in query SQL le query in linguaggio naturale dei clienti sulle informazioni operative. Queste query SQL vengono eseguite tramite il grafo delle conoscenze di Adobe Experience Platform, che contiene metadati sulle entità Experience Platform dei clienti, come schemi, set di dati, tipi di pubblico, destinazioni e percorsi. I risultati delle query SQL vengono quindi utilizzati per generare risposte alle domande originali sul linguaggio naturale dei clienti.
* Gli utenti principali di questo modello sono professionisti del marketing, analisti di dati o responsabili di percorsi di clienti che desiderano comprendere e agire in base alle informazioni operative all’interno di Experience Platform utilizzando un linguaggio naturale. Potrebbero non essere esperti di SQL o ingegneria dei dati, ma hanno bisogno di risposte rapide e precise sulle loro entità Experience Platform per prendere decisioni informate e ottimizzare le esperienze dei clienti.
* Questo modello fa parte dell’Assistente AI per informazioni operative, dove consente agli utenti di accedere ai metadati delle loro entità Experience Platform come pubblico, percorsi, schemi, attributi, set di dati e destinazioni. Gli utenti possono porre domande nel linguaggio naturale, ad esempio quali tipi di pubblico vengono attivati o quali tipi di pubblico utilizzano uno schema specifico, e il modello le traduce in query SQL attraverso il Knowledge Graph di Experience Platform. Questo consente agli utenti di ottenere rapidamente visibilità operativa e prendere decisioni informate senza dover esplorare o interrogare manualmente il sistema.
* Questo modello affronta i punti critici che gli utenti e gli analisti aziendali che lavorano con Experience Platform devono affrontare, ad esempio la complessità di navigare in grandi volumi di metadati interconnessi, la necessità di scrivere manualmente query SQL per recuperare informazioni operative e la mancanza di visibilità sul modo in cui le entità di Experience Platform, come i tipi di pubblico, i set di dati e i percorsi, sono connessi o funzionano. Consentendo l&#39;accesso ai metadati in linguaggio naturale e automatizzando la generazione di SQL, il modello riduce la dipendenza dalle risorse tecniche, riduce i tempi di discovery di insight e consente agli utenti di prendere decisioni più rapide e basate sui dati.
* Il modello non deve essere utilizzato per accedere o dedurre dati personali (PII, Personally Identifiable Information) come nomi di clienti, indirizzi e-mail o numeri di telefono, anche se tali dati esistono nella piattaforma.
* Inoltre, non deve essere utilizzato per i controlli di conformità o governance, come la convalida dei criteri di conservazione dei dati, le regole di controllo dell’accesso o lo stato del consenso. Queste attività richiedono sistemi e strategie specializzati.

## Dettagli modello {#model-details}

* Il tipo di modello è Chiedi conferma LLM con apprendimento dinamico nel contesto.
* L’input del modello è costituito da query in linguaggio naturale dell’utente.
* Il modello restituisce le query SQL con sintassi [!DNL Snowflake], che vengono eseguite tramite Knowledge Graph di Experience Platform.

**Input di esempio**

```console
How many datasets were created within the last 10 days?
```

**Output di esempio**

```SQL
SELECT
    COUNT(*) AS datasetCount 
FROM hkg_dim_dataset 
WHERE
    createdTime >= DATEADD(day, -10, CURRENT_DATE);
```

## Formazione sui modelli {#model-training}

* [!DNL NL2SQL] ha utilizzato [!DNL OpenAI] modelli basati su GPT per l&#39;apprendimento nel contesto.
* La banca domande [!DNL NL2SQL] contiene 428 query del team [!DNL Operational Insights] e 524 di team esterni per casi d&#39;uso alfa.

## Valutazione del modello {#model-evaluation}

* Il modello viene valutato utilizzando la precisione. Ad esempio, su tutte le [!DNL NL2SQL] richieste, quante restituiscono i risultati SQL corretti.
* Il processo di valutazione è una combinazione di corrispondenza basata su regole (standardizzazione SQL e quindi corrispondenza diretta delle stringhe SQL), risolutore SQL basato su LLM e valutazione umana
* I set aperti vengono utilizzati per il test di regressione e i progetti di annotazione settimanali monitorano le prestazioni del modello attraverso il traffico reale del cliente campionato.
* Per quanto riguarda la valutazione in contraddittorio, esiste un modello separato esterno e interno all&#39;ambito che funge da guardrail per [!DNL NL2SQL].

## Distribuzione del modello {#model-deployment}

* Il modello LLM è un modello basato su GPT ospitato da [!DNL Azure OpenAI] API.
* Il modello base è ospitato da [!DNL Azure].
* Il modello viene aggiornato regolarmente, su base settimanale, attraverso l&#39;espansione della banca delle domande. L’elenco delle modalità viene aggiornato anche tramite nuove strategie e istruzioni di richiesta, quando necessario.

## Spiegabilità {#explainability}

Il modello utilizza un modello di spiegazione distinto per SQL.

## Equità e parzialità {#fairness-and-bias}

* Per garantire che il modello interpreti e generi query in modo coerente tra diversi intenti dell’utente e varianti linguistiche senza introdurre pregiudizi o rafforzare gli stereotipi, Adobe utilizza controlli rapidi, spiegabilità e protezioni contro la generazione di output distorti o non etici.
* L’output del modello è interessato dagli esempi di apprendimento in contesto e da ciò che il modulo di recupero seleziona nel prompt. Gli esempi delle banche delle domande contengono esempi considerati rappresentativi dal punto di vista del Primo Ministro e stiamo anche ampliando le banche delle domande in base al traffico reale dei clienti.

## Robustezza {#robustness}

Poiché la maggior parte delle query che riceve non sono coperte dalla banca domande, la precisione del traffico di produzione riflette la robustezza del modello.

## Considerazioni sulla privacy e sulla sicurezza {#privacy-and-security-considerations}

Il modello non elabora o conserva informazioni personali identificabili (PII, personally identifiable information) e tali informazioni sono nascoste per la generazione SQL. Per il controllo delle autorizzazioni di controllo degli accessi basato su attributi, l’istruzione SQL generata verrà ulteriormente elaborata dal team del Knowledge Graph di Experience Platform per garantire la qualità della governance.

## Considerazioni etiche {#ethical-considerations}

Per evitare di esporre PII o attributi sensibili, il modello è stato progettato per supportare la privacy, evitare di rafforzare le distorsioni dei dati esistenti e rispettare i limiti di controllo degli accessi. Ciò include il filtraggio, l’assegnazione di tag e il controllo dei campi dello schema per un utilizzo responsabile.

