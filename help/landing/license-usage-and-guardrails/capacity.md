---
title: Utilizzo licenze e capacità
description: Scopri i limiti di utilizzo delle licenze e di capacità in Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: b3b0792a1a1dd5270dec697539ed58d895814fc8
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 1%

---


# Utilizzo delle licenze e capacità

In Adobe Experience Platform, le funzionalità ti informano se l’organizzazione ha superato uno dei tuoi guardrail e ti forniscono informazioni su come risolvere questi problemi.

Per ulteriori informazioni sui guardrail in Experience Platform, leggere la [panoramica sui guardrail di Real-Time CDP](../../rtcdp/guardrails/overview.md).

## Comportamento capacità {#behavior}

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingthroughput"
>title="Velocità effettiva di streaming"
>abstract="Il valore della velocità effettiva di streaming misura i picchi di eventi in entrata combinati al secondo per l’acquisizione in streaming nel servizio Profilo, nelle sandbox di produzione e sviluppo."

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingaudiences"
>title="Conteggio del pubblico in streaming"
>abstract="Il numero massimo di tipi di pubblico in streaming per sandbox. Questo numero è comprensivo del numero di tipi di pubblico edge disponibili nella sandbox."

>[!CONTEXTUALHELP]
>id="platform_capacity_edgeaudiences"
>title="Tipi di pubblico di Edge"
>abstract="Il numero massimo di tipi di pubblico edge per sandbox."

Attualmente, Capacity supporta i seguenti servizi:

- Segmentazione in streaming
- Acquisizione in streaming

All’interno di questi servizi, vengono tracciati i seguenti guardrail:

- Il numero massimo di pubblici in streaming è 500
   - Di questi 500 tipi di pubblico in streaming, il numero massimo è 150
- Il throughput massimo combinato per la segmentazione in streaming è di 1500 record al secondo (rps)

La capacità del pubblico è al livello **sandbox**. Ciò significa che, per ogni sandbox presente nell’organizzazione, puoi avere 500 tipi di pubblico in streaming, di cui 150 Edge.

La capacità effettiva si trova a un livello **organizzazione** e può essere distribuita alle singole sandbox. Ad esempio, con 1500 rps per la velocità effettiva di segmentazione in streaming, puoi impostare la sandbox di produzione su 1500 rps e la sandbox di sviluppo su 150 rps.

Experience Platform calcola la velocità effettiva della sandbox in intervalli di rotazione di 15 minuti. Questo throughput viene misurato in tempo reale, con i dati aggiornati ogni 60 secondi.

Se l’utilizzo raggiunge l’80% e il 90% della capacità concessa in licenza, Experience Platform invierà un avviso per informarti che stai raggiungendo il massimo della capacità specificata. È possibile modificare le impostazioni per personalizzare la percentuale di capacità in modo da ricevere l&#39;avviso o rimuovere completamente l&#39;avviso.

Se l’utilizzo supera il 100% della capacità concessa in licenza, verrà considerata una violazione della capacità. A questo punto, si verificherà una latenza delle prestazioni e le destinazioni del livello di servizio (SLT) **non** saranno garantite.

## Domande frequenti

La sezione seguente illustra le domande frequenti sulle funzionalità di Capacity.

### Posso avere un limite massimo di velocità effettiva combinata che somma fino a meno del mio massimo target?

+++ Risposta

No. Il limite massimo di velocità effettiva combinata **deve** corrispondere al guardrail della tua organizzazione.

+++

### Cosa succede se supero le capacità massime?

+++ Risposta

Questo dipende dalla capacità superata.

Attualmente, se superi il numero massimo di tipi di pubblico consentiti, i tipi di pubblico in eccesso non verranno interessati. Tuttavia, la possibilità di creare nuovi tipi di pubblico potrebbe essere limitata in futuro.

Se superi la velocità effettiva di streaming, sperimenterai una latenza di prestazioni nell’acquisizione e nella segmentazione.

+++

### Perché devo rispettare le mie capacità massime?

+++ Risposta

Lavorare con le massime capacità garantisce la coerenza dei dati e l&#39;integrità dei dati.

Puoi garantire prestazioni coerenti durante gli eventi di picco, evitando problemi tecnici che potrebbero influire negativamente sulle prestazioni del sistema e influire sulle esperienze dei clienti a valle, migliorando in ultima analisi l’igiene dei dati e le prestazioni complessive del sistema.

+++

### Quali sono le best practice per gestire la velocità effettiva di segmentazione in streaming?

+++ Risposta

Per gestire al meglio la velocità effettiva di segmentazione dello streaming, è necessario valutare i set di dati per assicurarsi che stiano dando la priorità ai dati necessari per la personalizzazione.


Se non è richiesta l’elaborazione in tempo reale, è necessario utilizzare l’acquisizione in batch invece dell’acquisizione in streaming.

+++
