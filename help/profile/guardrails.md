---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;protezioni;linee guida;limite;entità;entità principale;entità dimensione;
title: Guardrail per i dati del profilo cliente in tempo reale
solution: Experience Platform
product: experience platform
type: Documentation
description: Adobe Experience Platform fornisce una serie di protezioni per aiutarti a evitare la creazione di modelli di dati non supportati da Profilo cliente in tempo reale. Questo documento delinea le best practice e i vincoli da tenere a mente durante la modellazione dei dati del profilo.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: 441c2978b90a4703874787b3ed8b94c4a7779aa8
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 1%

---

# Guardrail per i dati [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] fornisce profili individuali che ti consentono di fornire esperienze cross-channel personalizzate basate su approfondimenti comportamentali e attributi del cliente. Per raggiungere questo obiettivo, [!DNL Profile] e il motore di segmentazione all’interno di Adobe Experience Platform utilizzano un modello di dati ibrido altamente denormalizzato che offre un nuovo approccio allo sviluppo dei profili dei clienti. L’utilizzo di questo modello di dati ibridi rende importante che i dati raccolti siano modellati correttamente. Sebbene l’ archivio dati [!DNL Profile] che conserva i dati di profilo non sia un archivio relazionale, [!DNL Profile] consente l’integrazione con entità di piccole dimensioni per creare segmenti in modo semplificato e intuitivo. Questa integrazione è nota come segmentazione su più entità.

Adobe Experience Platform fornisce una serie di protezioni per evitare la creazione di modelli di dati che [!DNL Real-time Customer Profile] non è in grado di supportare. In questo documento vengono illustrate le protezioni, le best practice e i vincoli quando si utilizzano i dati di profilo per la segmentazione.

>[!NOTE]
>
>Le protezioni e i limiti descritti nel presente documento vengono costantemente migliorati. Controlla regolarmente la disponibilità di aggiornamenti.

## Introduzione

Prima di provare a generare modelli di dati da utilizzare in [!DNL Real-time Customer Profile], è consigliabile leggere la seguente documentazione sui servizi di Experience Platform. L&#39;utilizzo dei modelli di dati e delle protezioni descritte in questo documento richiede una comprensione dei vari servizi di Experience Platform coinvolti nella gestione delle entità [!DNL Real-time Customer Profile]:

* [[!DNL Real-time Customer Profile]](home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Servizio](../identity-service/home.md) Adobe Experience Platform Identity: Supporta la creazione di una &quot;visione unica del cliente&quot; attraverso il collegamento di identità provenienti da fonti di dati diverse che vengono acquisite in  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Il framework standardizzato tramite il quale Platform organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../xdm/schema/composition.md) dello schema: Introduzione agli schemi e alla modellazione dei dati in Experience Platform.
* [Servizio](../segmentation/home.md) di segmentazione di Adobe Experience Platform: Il motore di segmentazione all’interno  [!DNL Platform] utilizzato per creare segmenti di pubblico dai profili dei clienti in base ai comportamenti e agli attributi dei clienti.
   * [Segmentazione](../segmentation/multi-entity-segmentation.md) multi-entità: Guida alla creazione di segmenti che integrano entità dimensionali con dati di profilo.

## Tipi di entità

Il modello di dati di archivio [!DNL Profile] è costituito da due tipi di entità principali:

* **Entità principale:** un’entità primaria o un’entità profilo unisce i dati per formare una &quot;singola origine di verità&quot; per un singolo utente. Questi dati unificati vengono rappresentati utilizzando la cosiddetta &quot;visualizzazione unione&quot;. Una vista unione aggrega i campi di tutti gli schemi che implementano la stessa classe in un unico schema di unione. Lo schema di unione per [!DNL Real-time Customer Profile] è un modello dati ibrido denormalizzato che agisce come contenitore per tutti gli attributi di profilo e gli eventi comportamentali.

   Gli attributi indipendenti dalla data e dall’ora, noti anche come &quot;record data&quot; vengono modellati utilizzando [!DNL XDM Individual Profile], mentre i dati delle serie temporali, noti anche come &quot;event data&quot; (dati evento), vengono modellati utilizzando [!DNL XDM ExperienceEvent]. Man mano che i dati relativi a record e serie temporali vengono acquisiti in Adobe Experience Platform, si attiva [!DNL Real-time Customer Profile] per iniziare a acquisire i dati abilitati per l’utilizzo. Più interazioni e dettagli vengono acquisiti, più i profili individuali diventano solidi.

   ![](images/guardrails/profile-entity.png)

* **Entità Dimension:** la tua organizzazione può anche definire classi XDM per descrivere elementi diversi dai singoli utenti, ad esempio negozi, prodotti o proprietà. Questi schemi non[!DNL XDM Individual Profile] sono noti come &quot;entità dimensione&quot; e non contengono dati relativi alle serie temporali. Le entità di Dimension forniscono dati di ricerca che consentono e semplificano le definizioni di segmenti a più entità e devono essere sufficientemente piccole da consentire al motore di segmentazione di caricare l’intero set di dati in memoria per un’elaborazione ottimale (ricerca rapida dei punti).

   ![](images/guardrails/profile-and-dimension-entities.png)

## Frammenti di profilo

In questo documento sono presenti più protezioni che fanno riferimento a &quot;frammenti di profilo&quot;. Il Profilo cliente in tempo reale è composto da più frammenti di profilo. Ogni frammento rappresenta i dati per l’identità da un set di dati in cui è l’identità principale. Ciò significa che un frammento può contenere un ID principale e dati evento (serie temporale) in un set di dati XDM ExperienceEvent oppure può essere composto da un ID principale e da dati di record (attributi indipendenti dalla data e ora) in un set di dati XDM per profili individuali.

## Tipi di limite

Quando definisci il modello dati, si consiglia di rimanere entro le protezioni fornite per garantire le prestazioni corrette ed evitare errori di sistema.

Le protezioni fornite in questo documento comprendono due tipi di limiti:

* **Limite morbido:** un limite morbido fornisce un massimo consigliato per prestazioni di sistema ottimali. È possibile andare oltre un limite soft senza interrompere il sistema o ricevere messaggi di errore, ma andare oltre un limite soft comporterà un deterioramento delle prestazioni. Si consiglia di rimanere entro il limite soft per evitare riduzioni delle prestazioni complessive.

* **Limite rigido:** un limite rigido fornisce un massimo assoluto per il sistema. Superando un limite rigido si otterranno interruzioni ed errori, impedendo il funzionamento del sistema come previsto.

## Guardrail del modello dati

Durante la creazione di un modello dati da utilizzare con [!DNL Real-time Customer Profile] si consiglia di attenersi alle seguenti protezioni.

### Garanzie dell&#39;entità principale

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Numero di set di dati consigliati per contribuire allo schema di unione [!DNL Profile] | 20 | Morbido | **Si consiglia un massimo di 20 set di dati  [!DNL Profile]abilitati.** Per abilitare un altro set di dati per  [!DNL Profile], devi prima rimuovere o disabilitare un set di dati esistente. |
| Numero di relazioni con più entità consigliate | 5 | Morbido | **È consigliato un massimo di 5 relazioni tra più entità definite tra entità primarie ed entità dimensione.** Le mappature aggiuntive delle relazioni non devono essere effettuate finché non viene rimossa o disabilitata una relazione esistente. |
| Profondità JSON massima per il campo ID utilizzato nella relazione multi-entità | 4 | Morbido | **La profondità massima JSON consigliata per un campo ID utilizzato nelle relazioni tra più entità è 4.** Ciò significa che in uno schema altamente nidificato i campi nidificati con profondità superiore a 4 livelli non devono essere utilizzati come campo ID in una relazione. |
| Cardinalità array in un frammento di profilo | &lt;> | Morbido | **La cardinalità ottimale dell’array in un frammento di profilo (dati indipendenti dal tempo) è  &lt;>** |
| Cardinalità array in ExperienceEvent | &lt;=10 | Morbido | **La cardinalità ottimale dell’array in un ExperienceEvent (dati di serie temporali) è  &lt;>** |

### protezioni di entità Dimension

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Nessun dato relativo alle serie temporali consentito per entità non[!DNL XDM Individual Profile] | 0 | Duro | **I dati relativi alle serie temporali non sono consentiti per [!DNL XDM Individual Profile] le entità non incluse in Profile Service.** Se un set di dati della serie temporale è associato a un non-[!DNL XDM Individual Profile] ID, non deve essere abilitato per  [!DNL Profile]. |
| Nessuna relazione nidificata | 0 | Morbido | **Non creare una relazione tra due non [!DNL XDM Individual Profile] schemi.** La possibilità di creare relazioni non è consigliata per gli schemi che non fanno parte dello schema  [!DNL Profile] di unione. |
| Profondità JSON massima per il campo ID primario | 4 | Morbido | **La profondità massima JSON consigliata per il campo ID principale è 4.** Ciò significa che in uno schema altamente nidificato non devi selezionare un campo come ID primario se è nidificato con più di 4 livelli di profondità. Un campo al quarto livello nidificato può essere utilizzato come ID primario. |

## Protezione delle dimensioni dei dati

Le seguenti protezioni fanno riferimento alla dimensione dei dati e sono consigliate per garantire che i dati possano essere acquisiti, memorizzati e interrogati come previsto.

>[!NOTE]
>
>La dimensione dei dati viene misurata come dati non compressi in JSON al momento dell’acquisizione.

### Garanzie dell&#39;entità principale

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Dimensione massima di ExperienceEvent | 10 KB | Duro | **La dimensione massima di un evento è 10 KB.** L’acquisizione continuerà, ma tutti gli eventi di dimensioni superiori a 10 KB verranno eliminati. |
| Dimensione massima del record del profilo | 100 KB | Duro | **La dimensione massima di un record di profilo è 100 KB.** L’acquisizione continuerà, tuttavia i record di profilo di dimensioni superiori a 100 KB verranno eliminati. |
| Dimensione massima del frammento di profilo | 50 MB | Duro | **La dimensione massima di un frammento di profilo è 50 MB.** Segmentazione, esportazioni e ricerche potrebbero non riuscire per qualsiasi  [frammento di ](#profile-fragments) profilo maggiore di 50 MB. |
| Dimensioni massime di archiviazione del profilo | 50 MB | Morbido | **La dimensione massima di un profilo memorizzato è 50 MB.** L’aggiunta di nuovi  [frammenti di ](#profile-fragments) profilo a un profilo di dimensioni superiori a 50 MB influirà sulle prestazioni del sistema. |
| Numero di batch di profili o ExperienceEvent acquisiti al giorno | 90 | Morbido | **Il numero massimo di batch di profili o ExperienceEvent acquisiti al giorno è 90.** Ciò significa che il totale combinato dei batch di Profile ed ExperienceEvent acquisiti ogni giorno non può superare i 90. L’inserimento di batch aggiuntivi influisce sulle prestazioni del sistema. |

### protezioni di entità Dimension

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Dimensione totale massima per tutte le entità dimensionali | 5 GB | Morbido | **La dimensione totale massima consigliata per tutte le entità dimensionali è 5 GB.** L&#39;inserimento di entità di grandi dimensioni comporterà prestazioni di sistema scadenti. Ad esempio, non è consigliato caricare un catalogo di prodotti da 10 GB come entità dimensione. |
| Set di dati per schema entità dimensionale | 5 | Morbido | **È consigliato un massimo di 5 set di dati associati a ogni schema di entità dimensionale.** Ad esempio, se crei uno schema per &quot;prodotti&quot; e aggiungi cinque set di dati che contribuiscono, non devi creare un sesto set di dati associato allo schema dei prodotti. |
| Numero di batch di entità dimensione acquisiti al giorno | 4 per entità | Morbido | **Il numero massimo di batch di entità dimensione acquisiti al giorno è 4 per entità.** Ad esempio, puoi inserire gli aggiornamenti di un catalogo di prodotti fino a 4 volte al giorno. L’inserimento di batch di entità dimensione aggiuntivi per la stessa entità influisce sulle prestazioni del sistema. |

## Garanzie di segmentazione

Le protezioni descritte in questa sezione si riferiscono al numero e alla natura dei segmenti che un’organizzazione può creare all’interno di un Experience Platform, nonché alla mappatura e all’attivazione dei segmenti sulle destinazioni.

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Numero massimo di segmenti per sandbox | 10.000 | Morbido | **Il numero massimo di segmenti che un&#39;organizzazione può creare è 10.000 per sandbox.** Un’organizzazione può avere più di 10.000 segmenti in totale, purché ci siano meno di 10.000 segmenti in ogni singolo sandbox. Il tentativo di creare ulteriori segmenti comporterà prestazioni di sistema ridotte. |
| Numero massimo di segmenti di streaming per sandbox | 500 | Morbido | **Il numero massimo di segmenti di streaming che un&#39;organizzazione può creare è 500 per sandbox.** Un’organizzazione può disporre di più di 500 segmenti di streaming in totale, purché ci siano meno di 500 segmenti di streaming in ogni singolo sandbox. Il tentativo di creare ulteriori segmenti di streaming si tradurrà in prestazioni di sistema degradate. |
| Numero massimo di segmenti batch per sandbox | 10.000 | Morbido | **Il numero massimo di segmenti batch che un&#39;organizzazione può creare è 10.000 per sandbox.** Un&#39;organizzazione può avere più di 10.000 segmenti batch in totale, purché ci siano meno di 10.000 segmenti batch in ogni singolo sandbox. Il tentativo di creare ulteriori segmenti batch provocherà un deterioramento delle prestazioni del sistema. |
