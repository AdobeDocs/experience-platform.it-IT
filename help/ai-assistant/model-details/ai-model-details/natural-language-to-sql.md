---
title: Dettagli sul modello SQL dal linguaggio naturale dell’Assistente IA
description: Scopri il modello di IA per l’Assistente all’intelligenza artificiale per SQL AI.
exl-id: ca157945-5f74-45d0-9d40-c65d09a8e80d
source-git-commit: 3d870c367317d73bba8b75b38f7b2a93ab6b5bbd
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# Informazioni operative sull&#39;Assistente ai linguaggio naturale per i dettagli del modello SQL

>[!IMPORTANT]
>
>Adobe sta attivamente pubblicando ulteriori dettagli del modello; man mano che sarà disponibile, verrà aggiunta ulteriore documentazione ad Experience League.

## Panoramica del modello {#model-overview}

* **Nome modello e versione**: Adobe Experience Platform AI Assistant Operational Insights Natural Language to SQL Model ([!DNL NL2SQL]).
* **Data di rilascio modello**: febbraio 2025
* **Scopo del modello**: il modello è progettato per tradurre in query SQL le query in linguaggio naturale dei clienti sulle informazioni operative. Queste query SQL vengono eseguite tramite il grafo delle conoscenze di Adobe Experience Platform, che contiene metadati sulle entità Experience Platform dei clienti, come schemi, set di dati, tipi di pubblico, destinazioni e percorsi. I risultati delle query SQL vengono quindi utilizzati per generare risposte alle domande originali sul linguaggio naturale dei clienti.
* **Utenti previsti**: gli utenti principali di questo modello sono professionisti del marketing, analisti di dati o responsabili di percorsi di clienti che desiderano comprendere e agire in base a informazioni operative all&#39;interno di Experience Platform utilizzando un linguaggio naturale. Potrebbero non essere esperti di SQL o ingegneria dei dati, ma hanno bisogno di risposte rapide e precise sulle loro entità Experience Platform per prendere decisioni informate e ottimizzare le esperienze dei clienti.
* **Casi d&#39;uso**: questo modello consente agli utenti di accedere ai metadati delle loro entità Experience Platform, come tipi di pubblico, percorsi, schemi, attributi, set di dati e destinazioni. Gli utenti possono porre domande nel linguaggio naturale, ad esempio quali tipi di pubblico vengono attivati o quali tipi di pubblico utilizzano uno schema specifico, e il modello le traduce in query SQL attraverso il Knowledge Graph di Experience Platform. Questo consente agli utenti di ottenere rapidamente visibilità operativa e prendere decisioni informate senza dover esplorare o interrogare manualmente il sistema.
* **Perplessità**: questo modello risolve le principali perplessità riscontrate dagli utenti aziendali e dagli analisti che lavorano con Experience Platform, ad esempio la complessità di navigare in grandi volumi di metadati interconnessi, la necessità di scrivere manualmente query SQL per recuperare informazioni operative e la mancanza di visibilità sulle modalità di connessione o esecuzione delle entità Experience Platform come tipi di pubblico, set di dati e percorsi. Consentendo l&#39;accesso ai metadati in linguaggio naturale e automatizzando la generazione di SQL, il modello riduce la dipendenza dalle risorse tecniche, riduce i tempi di discovery di insight e consente agli utenti di prendere decisioni più rapide e basate sui dati.

## Dettagli modello {#model-details}

* **Tipo di modello**: richiesta LLM con apprendimento dinamico nel contesto
* **Input**: query del linguaggio naturale dell&#39;utente.
* **Output**: il modello restituisce le query SQL con sintassi [!DNL Snowflake], che verrà eseguita tramite il grafico della conoscenza di Experience Platform.

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

## Valutazione del modello {#model-evaluation}

* **Metriche e procedure di valutazione**: il modello viene valutato esaminando le [!DNL NL2SQL] richieste e valutando quante di esse producono i risultati SQL corretti. Il processo di valutazione è una combinazione di corrispondenza basata su regole (standardizzazione SQL e quindi corrispondenza diretta delle stringhe SQL), risolutore SQL basato su LLM e valutazione umana.
* **Dati di valutazione e pre-elaborazione**: utilizziamo set aperti per il test di regressione e abbiamo anche progetti di annotazione settimanali per monitorare le prestazioni del modello attraverso il traffico cliente reale campionato.

## Distribuzione del modello {#model-deployment}

* **Monitoraggio del modello**: il modello base è ospitato da [!DNL Azure].
* **Aggiornamento modello**: Adobe Experience Platform AI Assistant Operational Insights Natural Language to SQL Model viene aggiornato regolarmente (settimanalmente) tramite l&#39;espansione della banca domande. Il modello viene aggiornato anche attraverso nuove strategie e istruzioni di richiesta, quando necessario.

## Equità e parzialità {#fairness-and-bias}

* **Correttezza del modello**: per garantire che il modello interpreti e generi query in modo coerente tra diversi intenti dell&#39;utente e varianti linguistiche senza introdurre pregiudizi o rafforzare gli stereotipi, Adobe utilizza controlli rapidi, spiegabilità e protezioni contro la generazione di output distorti o non etici.
* **Disturbi dei dati**: l&#39;output del modello è interessato dagli esempi di apprendimento in contesto e da ciò che il modulo di recupero seleziona nel prompt. Gli esempi delle banche delle domande contengono esempi considerati rappresentativi dal punto di vista della gestione del prodotto. A seconda del caso d’uso, i clienti devono considerare in che modo le potenziali distorsioni negli output dei modelli possono allinearsi o avere un impatto sull’applicazione a cui sono destinati.

## Considerazioni etiche {#ethical-considerations}

**Considerazioni etiche associate al modello**: per evitare di esporre attributi PII o sensibili, il modello è stato progettato per evitare il rafforzamento delle distorsioni dei dati esistenti e rispettare i limiti di controllo dell&#39;accesso. Ciò include il filtraggio, l’assegnazione di tag e il controllo dei campi dello schema per un utilizzo responsabile.
