---
keywords: ' Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;tutorial;linee guida;limite;entità;entità primaria;entità dimensione;'
title: ' Experienci Platform per i dati del profilo cliente in tempo reale'
solution: Experience Platform
product: experience platform
topic: guide
type: Documentation
description: 'Adobe Experience Platform offre una serie di garanzie per evitare di creare modelli di dati che il profilo cliente in tempo reale non supporta. In questo documento vengono illustrate le procedure ottimali e i vincoli da tenere presenti nella modellazione dei dati del profilo. '
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '1457'
ht-degree: 1%

---


# [!DNL Platform] corrimano  [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] fornisce profili individuali che consentono di fornire esperienze multicanale personalizzate basate su informazioni comportamentali e attributi del cliente. Per raggiungere questo obiettivo, [!DNL Profile] e il motore di segmentazione all&#39;interno di Adobe Experience Platform utilizzano un modello dati ibrido altamente denormalizzato che offre un nuovo approccio allo sviluppo dei profili cliente. L&#39;utilizzo di questo modello di dati ibridi rende estremamente importante che i dati raccolti siano modellati correttamente. Mentre l&#39;archivio di dati [!DNL Profile] che conserva i dati del profilo non è uno store relazionale, [!DNL Profile] consente l&#39;integrazione con entità di piccole dimensioni per creare segmenti in modo semplificato e intuitivo. Questa integrazione è nota come segmentazione multi-entità.

Adobe Experience Platform offre una serie di guardrail per evitare la creazione di modelli di dati che [!DNL Real-time Customer Profile] non è in grado di supportare. In questo documento vengono delineati sia i reggilibri che le procedure ottimali e i vincoli quando si utilizzano i dati di profilo per la segmentazione.

>[!NOTE]
>
>I guardrail e i limiti delineati in questo documento sono costantemente migliorati. Verificare regolarmente la disponibilità di aggiornamenti.

## Introduzione

Prima di provare a creare modelli di dati da utilizzare in [!DNL Real-time Customer Profile], è consigliabile leggere la seguente documentazione sui servizi  Experience Platform. L&#39;utilizzo dei modelli di dati e dei custodi descritti in questo documento richiede la comprensione dei vari servizi di Experience Platform  coinvolti nella gestione delle entità [!DNL Real-time Customer Profile]:

* [[!DNL Real-time Customer Profile]](home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Servizio](../identity-service/home.md) identità Adobe Experience Platform: Supporta la creazione di una &quot;singola vista del cliente&quot;, collegando le identità provenienti da origini dati diverse durante l&#39;assimilazione  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Il framework standardizzato tramite il quale la piattaforma organizza i dati sull&#39;esperienza cliente.
   * [Nozioni di base sulla composizione](../xdm/schema/composition.md) dello schema: Introduzione agli schemi e alla modellazione dei dati all&#39;interno  Experience Platform.
* [Servizio](../segmentation/home.md) di segmentazione Adobe Experience Platform: Il motore di segmentazione  [!DNL Platform] utilizzato per creare segmenti di pubblico dai profili cliente in base ai comportamenti e agli attributi del cliente.
   * [Segmentazione](../segmentation/multi-entity-segmentation.md) multi-entità: Guida alla creazione di segmenti che integrano entità dimensionali con dati di profilo.

## Tipi di entità

Il modello di dati dello store [!DNL Profile] è costituito da due tipi di entità di base:

* **Entità principale:** un&#39;entità primaria, o un&#39;entità di profilo, unisce i dati per formare una &quot;singola origine di verità&quot; per un individuo. Questi dati unificati vengono rappresentati utilizzando la cosiddetta &quot;visualizzazione unione&quot;. Una vista unione aggrega i campi di tutti gli schemi che implementano la stessa classe in un unico schema di unione. Lo schema unione per [!DNL Real-time Customer Profile] è un modello dati ibrido denormalizzato che agisce come contenitore per tutti gli attributi di profilo e gli eventi comportamentali.

   Gli attributi indipendenti dal tempo, noti anche come &quot;record data&quot;, vengono modellati utilizzando [!DNL XDM Individual Profile], mentre i dati delle serie temporali, noti anche come &quot;event data&quot;, vengono modellati utilizzando [!DNL XDM ExperienceEvent]. Quando i dati di record e serie temporali vengono acquisiti in Adobe Experience Platform, viene attivato [!DNL Real-time Customer Profile] per iniziare l&#39;acquisizione dei dati che sono stati attivati per il loro utilizzo. Più interazioni e dettagli vengono acquisiti, più solidi diventano i profili individuali.

   ![](images/guardrails/profile-entity.png)

* **entità Dimension:** l&#39;organizzazione può anche definire classi XDM per descrivere elementi diversi da individui, ad esempio store, prodotti o proprietà. Questi schemi non[!DNL XDM Individual Profile] sono noti come &quot;entità dimensione&quot; e non contengono dati relativi alle serie temporali. Le entità di Dimension forniscono dati di ricerca che agevolano e semplificano le definizioni di segmenti multi-entità e devono essere sufficientemente piccole da consentire al motore di segmentazione di caricare l&#39;intero set di dati in memoria per un&#39;elaborazione ottimale (ricerca rapida).

   ![](images/guardrails/profile-and-dimension-entities.png)

## Tipi di limite

Quando si definisce il modello dati, si consiglia di rimanere all&#39;interno dei custodie forniti per garantire le prestazioni corrette ed evitare errori di sistema. I guardrail forniti in questo documento includono due tipi di limite:

* **Soft limit:** un limite morbido fornisce un massimo consigliato per prestazioni ottimali del sistema. È possibile andare oltre un limite software senza interrompere il sistema o ricevere messaggi di errore, ma andando oltre un limite software si tradurrà in un deterioramento delle prestazioni. Si consiglia di rimanere entro il limite soft per evitare riduzioni delle prestazioni complessive.

* **Limite rigido:** un limite rigido fornisce un massimo assoluto per il sistema. Andando oltre un limite difficile si verificheranno interruzioni ed errori, impedendo al sistema di funzionare come previsto.

## Guardrail modello dati

Durante la creazione di un modello dati da utilizzare con [!DNL Real-time Customer Profile] si consiglia di attenersi alle seguenti strutture.

### Garanzie dell&#39;entità principale

| Guardrail | Limite | Tipo limite | Descrizione |
| --- | --- | --- | --- |
| Numero di set di dati consigliati per contribuire allo schema di unione [!DNL Profile] | 20 | Morbido | **È consigliabile un massimo di 20 set di dati  [!DNL Profile]abilitati.** Per abilitare un altro set di dati per  [!DNL Profile], un set di dati esistente deve prima essere rimosso o disabilitato. |
| Numero di relazioni con più entità consigliate | 5 | Morbido | **È consigliabile un massimo di 5 relazioni tra più entità definite tra entità primarie ed entità dimensione.** Non è possibile eseguire mappature aggiuntive delle relazioni finché una relazione esistente non viene rimossa o disabilitata. |
| Profondità JSON massima per il campo ID utilizzato nella relazione tra più entità | 4 | Morbido | **La profondità JSON massima consigliata per un campo ID utilizzato nelle relazioni tra più entità è 4.** Ciò significa che in uno schema altamente nidificato, i campi nidificati con profondità superiore a 4 livelli non devono essere utilizzati come campo ID in una relazione. |
| Cardinalità degli array in un frammento di profilo | &lt;> | Morbido | **La cardinalità ottimale dell&#39;array in un frammento di profilo (dati indipendenti dall&#39;ora) è  &lt;>** |
| Cardinalità degli array in ExperienceEvent | &lt;=10 | Morbido | **La cardinalità ottimale dell&#39;array in un ExperienceEvent (dati delle serie temporali) è  &lt;>** |

### Dimension di garanzie

| Guardrail | Limite | Tipo limite | Descrizione |
| --- | --- | --- | --- |
| Nessun dato della serie temporale consentito per entità non-[!DNL XDM Individual Profile] | 0 | Rigido | **I dati delle serie temporali non sono consentiti per [!DNL XDM Individual Profile] le entità non incluse nel servizio profilo.** Se un set di dati della serie temporale è associato a un non-[!DNL XDM Individual Profile] ID, il set di dati non deve essere abilitato per  [!DNL Profile]. |
| Nessuna relazione nidificata | 0 | Morbido | **Non creare una relazione tra due non [!DNL XDM Individual Profile] schemi.** La capacità di creare relazioni non è consigliata per gli schemi che non fanno parte dello schema  [!DNL Profile] unione. |
| Profondità JSON massima per il campo ID principale | 4 | Morbido | **La profondità JSON massima consigliata per il campo ID principale è 4.** Questo significa che in uno schema altamente nidificato non è necessario selezionare un campo come ID primario se nidificato con più di 4 livelli di profondità. Un campo al quarto livello nidificato può essere utilizzato come ID principale. |

## Garanzie dimensioni dati

I seguenti trattini di sicurezza fanno riferimento alla dimensione dei dati e sono consigliati per garantire che i dati possano essere acquisiti, memorizzati e interrogati come previsto.

>[!NOTE]
>
>La dimensione dei dati sarà misurata come dati non compressi in JSON al momento dell&#39;assimilazione.

### Garanzie dell&#39;entità principale

| Guardrail | Limite | Tipo limite | Descrizione |
| --- | --- | --- | --- |
| Dimensione massima per frammento di profilo | 10 KB | Morbido | **La dimensione massima consigliata per un frammento di profilo è 10 KB.** L&#39;inserimento di frammenti di profilo più grandi influirà sulle prestazioni del sistema. Ad esempio, il caricamento di un set di dati CRM pesante in cui alcuni frammenti di profilo hanno dimensioni pari a 50 kB comporterà un peggioramento delle prestazioni del sistema. |
| Dimensioni massime assolute per frammento di profilo | 1 MB | Rigido | **La dimensione massima assoluta di un frammento di profilo è 1 MB.** L&#39;inserimento non riesce se si tenta di caricare un frammento di profilo maggiore di 1 MB. |

### Dimension di garanzie

| Guardrail | Limite | Tipo limite | Descrizione |
| --- | --- | --- | --- |
| Dimensione totale massima per tutte le entità dimensionali | 5 GB | Morbido | **La dimensione totale massima consigliata per tutte le entità dimensionali è 5 GB.** L&#39;inserimento di entità di grandi dimensioni comporterà un peggioramento delle prestazioni del sistema. Ad esempio, non è consigliabile tentare di caricare un catalogo di prodotti da 10 GB come entità dimensione. |
| Set di dati per schema entità dimensionale | 5 | Morbido | **È consigliabile un massimo di 5 set di dati associati a ogni schema di entità dimensionale.** Ad esempio, se si crea uno schema per &quot;products&quot; e si aggiungono cinque dataset contributivi, non creare un sesto dataset associato allo schema di prodotti. |

## Garanzie di segmentazione

Le guardrail descritte in questa sezione si riferiscono al numero e alla natura dei segmenti che un&#39;organizzazione può creare all&#39;interno  Experience Platform, nonché alla mappatura e all&#39;attivazione dei segmenti alle destinazioni.

| Guardrail | Limite | Tipo limite | Descrizione |
| --- | --- | --- | --- |
| Numero massimo di segmenti per sandbox | 10.000 | Morbido | **Il numero massimo di segmenti che un&#39;organizzazione può creare è 10.000 per sandbox.** Un&#39;organizzazione può avere più di 10.000 segmenti in totale, purché in ogni sandbox ci siano meno di 10.000 segmenti. Se si tenta di creare segmenti aggiuntivi, le prestazioni del sistema risulteranno ridotte. |
| Numero massimo di segmenti di streaming per sandbox | 500 | Morbido | **Il numero massimo di segmenti di streaming che un&#39;organizzazione può creare è 500 per sandbox.** Un&#39;organizzazione può disporre di più di 500 segmenti di streaming in totale, a condizione che vi siano meno di 500 segmenti di streaming in ciascuna sandbox. Se si tenta di creare ulteriori segmenti di streaming, le prestazioni del sistema risulteranno ridotte. |
| Numero massimo di segmenti batch per sandbox | 10.000 | Morbido | **Il numero massimo di segmenti batch che un&#39;organizzazione può creare è 10.000 per sandbox.** Un&#39;organizzazione può avere più di 10.000 segmenti batch in totale, a condizione che vi siano meno di 10.000 segmenti batch in ogni singolo sandbox. Se si tenta di creare segmenti batch aggiuntivi, le prestazioni del sistema risulteranno ridotte. |