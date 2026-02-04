---
title: Convalida del pubblico
description: Scopri come Experience Platform convalida i tipi di pubblico per garantire che funzionino bene anche più a valle.
source-git-commit: 52439e55d3c48631488b17b6b04256bcbbe37bcb
workflow-type: tm+mt
source-wordcount: '1630'
ht-degree: 1%

---


# Convalida del pubblico

Quando scrivi una definizione di pubblico in Adobe Experience Platform, la convalida del pubblico fornisce convalide e protezioni integrate per garantire che i tipi di pubblico siano non solo accurati, ma anche stabili e scalabili.

Attenendoti alle best practice per la definizione del pubblico, assicurati che i tipi di pubblico possano valutare più rapidamente, assicurati che la logica rimanga efficiente anche quando le dimensioni del pubblico aumentano e riduci il rischio di errori di valutazione durante periodi di traffico elevato. I tipi di pubblico ottimizzati migliorano inoltre la velocità di attivazione verso le destinazioni, riducono la latenza di personalizzazione in tempo reale e mantengono la stabilità generale della sandbox.

Experience Platform esegue queste convalide in tempo reale mentre crei il pubblico in Segment Builder. Quando aggiungi eventi o attributi che superano le soglie di convalida, ricevi un feedback immediato all’interno dell’interfaccia di Segment Builder.

## Tipi di convalida {#validation-types}

Quando la convalida del pubblico viene eseguita sui tipi di pubblico, è possibile violare due diversi tipi di costrutti: costrutti di convalida critici e costrutti di ottimizzazione delle prestazioni.

Se viene violato un costrutto di convalida critico, il sistema impedisce di salvare il pubblico per proteggere la stabilità della sandbox. Se viene violato un costrutto di ottimizzazione delle prestazioni, potrai salvare il pubblico, ma è *vivamente consigliato* aggiornare la definizione del pubblico per evitare problemi di prestazioni.

## Controlli di convalida {#validation-checks}

Attualmente, sono supportate le seguenti convalide:

| Verifica di convalida | Tipo | Soglia |
| ---------------- | ---- | --------- |
| Complessità logica | Convalida critica | La definizione del pubblico contiene troppe query, con conseguente complessità logica non necessaria. |
| Eventi sequenziali | Convalida critica | All’interno di una definizione di pubblico sono presenti più di 6 eventi sequenziali. |
| Conteggio aggregato | Ottimizzazione delle prestazioni | All’interno di una definizione di pubblico sono presenti più di 3 funzioni di aggregazione. |
| Dati nidificati | Ottimizzazione delle prestazioni | All’interno di una definizione di pubblico sono presenti più di 2 livelli di profondità dei dati nidificati (tipi di dati array o mappa). |
| Dimensione del pubblico | Ottimizzazione delle prestazioni | La dimensione di qualificazione del pubblico è maggiore del 30% del numero totale di profili nella sandbox. |

### [!BADGE Convalida critica]{type=Negative} Complessità logica {#logical-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_rewritescheck"
>title="Avviso sull’efficienza delle query"
>abstract="Il pubblico contiene troppe query, che generano una complessità logica non necessaria. Semplifica la definizione del pubblico prima di continuare."

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_cnfcomplexitycheck"
>title="Complessità logica"
>abstract="Il pubblico contiene troppe query, che generano una complessità logica non necessaria. Semplifica la definizione del pubblico prima di continuare."

La convalida della complessità logica analizza la struttura delle istruzioni logiche (AND, OR, NOT) all’interno della definizione del pubblico. In particolare, cerca definizioni di pubblico che forzino il sistema a eseguire un numero eccessivo di confronti per profilo.

Se la definizione del pubblico presenta un numero eccessivo di confronti per profilo, questa maggiore complessità comporta una valutazione più lenta in base al profilo. Di conseguenza, questo aumenta il tempo complessivo necessario per la valutazione del pubblico.

Per evitare di attivare questa convalida, utilizza una definizione di pubblico semplice. Se non riesci a comprendere la tua definizione di pubblico, è troppo complicata e Experience Platform potrebbe richiedere più tempo per valutare il pubblico.

**Esempio**

Supponiamo che tu voglia trovare clienti che vivono in determinati stati. _potrebbe_ scrivere questo elemento in modo inefficiente controllando se il profilo ha il valore per uno stato che corrisponde a uno dei 45 valori elencati, come segue:

+++ Definizione di pubblico inefficiente

```
State.equals("AL", "AK", "AZ", "AR", "CA", "CO", "CT", "DE", "FL", "GA","HI", "ID", "IL", "IN", "IA", "KS", "KY", "LA", "ME", "MD", "MA", "MI", "MN", "MS", "MO", "MT", "NE", "NV", "NH", "NJ", "NM", "NY", "NC", "ND", "OH", "OK", "OR", "PA", "RI", "SC", "SD", "TN", "TX", "UT")
```

+++

Tuttavia, utilizzando un segno di non spunta, devi solo verificare se il profilo non ha uno dei 5 valori elencati, dando luogo a una query molto più efficiente.

+++ Definizione di pubblico efficiente

```
not(State.equals("VT", "VA", "WA", "WV", "WI", "WY" ))
```

+++

In alternativa, supponiamo che tu voglia trovare i clienti canadesi nel tuo piano di prova. Un approccio meno efficiente consisterebbe nel cercare canadesi nel piano di prova escludendo manualmente ogni altro piano, uno per uno, e verificando che il profilo non sia in nessuno di essi.

+++ Definizione di pubblico inefficiente

```
NOT(
    plan.equals("basic") OR
    plan.equals("standard") OR
    plan.equals("premium") OR
    plan.equals("enterprise")
) AND NOT (
    region.equals("us-east") OR
    region.equals("us-west") OR
    region.equals("eu-central") OR
    region.equals("apac")
)
```

+++

Dovresti invece essere diretto e indirizzato al piano specifico che desideri includere.

+++ Definizione di pubblico efficiente

```
plan.equals("trial") AND region.equals("canada")
```

+++

### [!BADGE Convalida critica]{type=Negative} Complessità degli eventi sequenziali {#sequential-event-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_chaincountcheck"
>title="Limite sequenza di eventi"
>abstract="Il pubblico contiene troppi eventi sequenziali. All’interno della definizione del pubblico, puoi avere solo un massimo di 6 eventi sequenziali. Prima di continuare, rimuovi alcuni eventi sequenziali dalla definizione del pubblico."

La convalida della complessità degli eventi sequenziali limita a 6 il numero di eventi sequenziali in una sequenza.

La segmentazione sequenziale è una delle operazioni più complicate dal punto di vista computazionale all’interno di Experience Platform, in quanto il sistema deve analizzare l’intera cronologia degli eventi esperienza di un cliente, ordinarli per marca temporale e verificare se l’ordine specificato corrisponde alla query. Di conseguenza, quando la catena cresce, aumenta drasticamente il numero di permutazioni necessarie per il calcolo.

Per evitare di attivare questa convalida, è necessario concentrarsi sulle nozioni di base della catena sequenziale definendo l&#39;inizio, il centro e la fine del percorso. I passaggi immediati sono spesso impliciti nella conversione finale.

**Esempio**

Supponiamo che tu voglia eseguire il targeting degli utenti che hanno visualizzato un prodotto, aggiungerlo al carrello e acquistarlo. Un approccio meno efficiente controllerebbe ogni singolo stato del percorso dell’utente. Ad esempio, la seguente query passa attraverso questa sequenza di eventi: Accedi al sito web -> Cerca il prodotto -> Visualizza una pagina di prodotto -> Aggiunte al carrello -> Passa al pagamento -> Evento di acquisto

+++ Definizione di pubblico inefficiente

```
chain(xEvent, timestamp, [ A: WHAT(eventType = "login"), B: WHAT(eventType = "search"), C: WHAT(eventType = "productView"), D: WHAT(eventType = "addToCart"), E: WHAT(eventType = "checkout"), F: WHAT(eventType = "purchase") ])
```

+++

Tuttavia, riducendo la sequenza all’inizio, al centro e alla fine, è sufficiente disporre di una sequenza di eventi lunga 3 eventi, per ottenere una query più efficiente. Ad esempio, la seguente query esamina questa sequenza di eventi: Visualizza una pagina di prodotto -> Aggiunte al carrello -> Evento di acquisto

+++ Definizione di pubblico efficiente

```
chain(xEvent, timestamp, [ A: WHAT(eventType = "productView"), B: WHAT(eventType = "addToCart"), C: WHAT(eventType = "purchase") ])
```

+++

### [!BADGE Ottimizzazione delle prestazioni]{type=Caution} Conteggio aggregato {#aggregated-count}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_countaggregationcheck"
>title="Avviso filtro conteggio"
>abstract="Troppi eventi di aggregazione per il pubblico. Dovresti utilizzare un massimo di 3 eventi di aggregazione all’interno del pubblico. Per evitare problemi di prestazioni, rimuovi alcuni eventi di aggregazione dalla definizione del pubblico."

Il controllo del conteggio aggregato limita a 3 condizioni il numero di eventi di aggregazione utilizzati nel pubblico.

Un evento standard deve trovare un solo evento corrispondente per qualificare un utente. Tuttavia, un evento di aggregazione deve leggere e analizzare l&#39;**intera cronologia** di eventi di un utente prima di poter prendere una decisione, rallentando i tempi di elaborazione con un maggior numero di eventi di aggregazione utilizzati.

Per evitare di attivare questa convalida, utilizza solo conteggi specifici quando è strettamente necessario per la definizione del pubblico. Se devi sapere solo se un utente si è attivato una volta, ad esempio, puoi utilizzare la logica standard &quot;Esiste&quot;, anziché l’evento &quot;Conteggio > 0&quot;.

### [!BADGE Ottimizzazione delle prestazioni]{type=Caution} Complessità dei dati nidificati {#nested-data-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_arraydepthcheck"
>title="Avviso dati nidificati"
>abstract="Il pubblico ha troppi livelli di dati nidificati. Dovresti utilizzare un massimo di 2 livelli di dati all’interno del pubblico. Per evitare problemi di prestazioni, è necessario appiattire la definizione del pubblico."

La convalida della complessità dei dati nidificati limita a 2 livelli il numero di dati nidificati all’interno di una definizione di pubblico.

Sebbene Experience Platform supporti l’utilizzo di oggetti array e map per memorizzare tipi di dati complessi, la decompressione delle strutture nidificate per trovare un valore richiede una logica di attraversamento più complessa. Più i dati sono profondi e nidificati in un array, più tempo richiede per essere recuperati per la convalida.

Se esegui frequentemente la segmentazione su un attributo profondamente nidificato, per un accesso più semplice potresti dover contattare il team di progettazione dati per copiare l’attributo a un livello più alto nello schema del profilo.

### [!BADGE Ottimizzazione delle prestazioni]{type=Caution} Dimensione pubblico {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_profilestorecheck"
>title="Avvertenza sulla dimensione del pubblico"
>abstract="Il pubblico è scritto in modo troppo ampio. Evita di scrivere una definizione di pubblico che qualifichi più del 30% dei profili totali nella sandbox. Per evitare problemi di prestazioni, devi stringere la definizione del pubblico."

La convalida della dimensione del pubblico controlla se la definizione del pubblico è così ampia che più del 30% dei profili totali nella sandbox siano idonei per il pubblico.

Anche se Experience Platform è in grado di gestire tipi di pubblico di grandi dimensioni, una definizione di pubblico troppo vaga (come Tutti i clienti attivi) può aumentare il tempo di valutazione e la latenza di attivazione.

Se devi creare un pubblico che qualifichi più del 30% dell’archivio profili, assicurati che la prima valutazione del pubblico venga eseguita utilizzando una valutazione flessibile del pubblico. Valutare il pubblico con una valutazione on-demand può ridurre l’impatto complessivo di un pubblico di grandi dimensioni sul processo di segmentazione giornaliero.

## Passaggi successivi

Dopo aver letto questa guida, hai una migliore comprensione di come Experience Platform esegue le convalide automatiche per migliorare la valutazione, la stabilità e la scalabilità. Per ulteriori informazioni sulla creazione di tipi di pubblico tramite l&#39;interfaccia utente, consulta la [documentazione del Generatore di segmenti](./ui/segment-builder.md).

## Appendice

Nell’appendice seguente sono elencate le domande frequenti sulla convalida del pubblico in Experience Platform.

### Domande frequenti {#faq}

**Cosa succede se ignoro gli avvisi e salvo il pubblico?**

+++ Risposta

Per gli avvisi di ottimizzazione delle prestazioni, il pubblico verrà salvato e il sistema tenterà di valutarlo. Tuttavia, i tempi di elaborazione potrebbero risultare notevolmente più lenti. In situazioni estreme, se il volume di dati è sufficientemente elevato, il processo di segmentazione potrebbe non riuscire o scadere, costringendoti a riprogettare il pubblico.

In caso di errori critici di convalida, non potrai salvare il pubblico.

+++

**Posso richiedere un aumento del limite &quot;Evento sequenziale&quot;?**

+++ Risposta

No, non puoi. Si tratta di un rigido guardrail progettato per proteggere la stabilità dell’intero ambiente Experience Platform. Se la sequenza richiede più di 6 passaggi, è un forte indicatore del fatto che la logica deve essere semplificata o suddivisa in due tipi di pubblico diversi (ad esempio, un pubblico di &quot;Coinvolgimento&quot; e un pubblico di &quot;Conversione&quot;).

+++

**Queste nuove convalide interromperanno i tipi di pubblico esistenti?**

+++ Risposta

Queste convalide vengono eseguite al momento dell&#39;**authoring**. Di conseguenza, i tipi di pubblico esistenti continueranno a essere eseguiti così come sono. Tuttavia, se tenti di modificare un pubblico esistente che viola queste regole, ti verrà richiesto di ottimizzarlo prima di poter salvare le modifiche.

+++

**Ho requisiti di dati complessi. Come posso evitare l&#39;avviso &quot;Nested Data&quot;?**

+++ Risposta

È meglio evitare l’avviso &quot;Dati nidificati&quot; a livello di modellazione dei dati. Alcuni suggerimenti includono l&#39;utilizzo del team di progettazione dati per appiattire lo schema XDM e portare gli attributi critici (come `subscriptionStatus` e `loyaltyTier`) al livello superiore del profilo.

+++

**Questi controlli verranno applicati sia ai tipi di pubblico Bozza che Pubblicato?**

+++ Risposta

Sì, questi controlli si applicano a *tutti* i tipi di pubblico valutati in Experience Platform.

+++
