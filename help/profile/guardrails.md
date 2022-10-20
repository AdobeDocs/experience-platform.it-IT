---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;protezioni;linee guida;limite;entità;entità principale;entità dimensione;
title: Guardrail predefiniti per i dati del profilo cliente in tempo reale
solution: Experience Platform
product: experience platform
type: Documentation
description: Adobe Experience Platform utilizza un modello di dati ibridi altamente denormalizzati che differisce dal modello tradizionale di dati relazionali. In questo documento trovi informazioni sui limiti predefiniti di utilizzo e tasso, che ti aiuteranno a modellare i dati profilo in modo da ottenere prestazioni di sistema ottimali.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: d6100f58b8ffd6251c3a58576a41dbfb75c3bb0c
workflow-type: tm+mt
source-wordcount: '1902'
ht-degree: 5%

---

# Guardrail predefiniti per [!DNL Real-time Customer Profile] dati

Adobe Experience Platform consente di fornire esperienze cross-channel personalizzate basate su insights comportamentali e attributi del cliente sotto forma di profili cliente in tempo reale. Per supportare questo nuovo approccio ai profili, Experience Platform utilizza un modello dati ibrido altamente denormalizzato che differisce dal modello dati relazionale tradizionale.

In questo documento trovi informazioni sui limiti predefiniti di utilizzo e tasso, che ti aiuteranno a modellare i dati profilo in modo da ottenere prestazioni di sistema ottimali. Quando si esaminano le seguenti protezioni, si presume che i dati siano stati modellati correttamente. Se hai domande su come modellare i tuoi dati, contatta il tuo rappresentante del servizio clienti.

>[!NOTE]
>
>La maggior parte dei clienti non supera questi limiti predefiniti. Per informazioni sui limiti personalizzati, contatta il rappresentante dell’Assistenza clienti.

## Introduzione

I seguenti servizi di Experience Platform sono coinvolti nella modellazione dei dati del profilo cliente in tempo reale:

* [[!DNL Real-time Customer Profile]](home.md): Crea profili di consumatore unificati utilizzando dati provenienti da più sorgenti.
* [Identità](../identity-service/home.md): Collega le identità di diverse origini dati durante l’acquisizione in Platform.
* [Schemi](../xdm/home.md): Gli schemi Experience Data Model (XDM) sono il framework standardizzato tramite il quale Platform organizza i dati sulla customer experience.
* [Segmenti](../segmentation/home.md): Il motore di segmentazione all’interno di Platform viene utilizzato per creare segmenti dai profili dei clienti in base ai comportamenti e agli attributi dei clienti.

## Tipi di limite

Questo documento contiene due tipi di limiti predefiniti:

* **Limite morbido:** È possibile superare un limite soft, tuttavia i limiti soft forniscono una linea guida consigliata per le prestazioni del sistema.

* **Limite rigido:** Un limite rigido fornisce un massimo assoluto.

>[!NOTE]
>
>I limiti delineati in questo documento vengono costantemente migliorati. Controlla regolarmente la disponibilità di aggiornamenti. Se sei interessato a conoscere i limiti personalizzati, contatta il tuo rappresentante di assistenza clienti.

## Limiti del modello dati

Le seguenti protezioni forniscono i limiti consigliati durante la modellazione dei dati del profilo cliente in tempo reale. Per ulteriori informazioni sulle entità principali e le entità dimensione, consulta la sezione su [tipi di entità](#entity-types) nell&#39;appendice.

### Garanzie dell&#39;entità principale

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Set di dati per classi di profili individuali XDM | 20 | Morbido | Si consiglia un massimo di 20 set di dati che sfruttano la classe Profilo individuale XDM. |
| Set di dati della classe ExperienceEvent XDM | 20 | Morbido | Si consiglia un massimo di 20 set di dati che sfruttano la classe ExperienceEvent XDM. |
| Set di dati suite di rapporti Adobe Analytics abilitati per Profilo | 1 | Morbido | Per Profilo deve essere abilitato un massimo di un set di dati della suite di rapporti di Analytics (1). Il tentativo di abilitare più set di dati della suite di rapporti di Analytics per il profilo potrebbe avere conseguenze indesiderate per la qualità dei dati. Per ulteriori informazioni, consulta la sezione su [Set di dati Adobe Analytics](#aa-datasets) nell&#39;appendice. |
| Relazioni tra più entità | 5 | Morbido | È consigliato un massimo di 5 relazioni tra più entità definite tra entità primarie ed entità dimensione. Le mappature aggiuntive delle relazioni non devono essere effettuate finché non viene rimossa o disabilitata una relazione esistente. |
| Profondità JSON per il campo ID utilizzato nelle relazioni con più entità | 4 | Morbido | La profondità massima JSON consigliata per un campo ID utilizzato nelle relazioni tra più entità è 4. Ciò significa che in uno schema altamente nidificato i campi nidificati con profondità superiore a 4 livelli non devono essere utilizzati come campo ID in una relazione. |
| Cardinalità array in un frammento di profilo | &lt;=500 | Morbido | La cardinalità ottimale dell’array in un frammento di profilo (dati indipendenti dal tempo) è &lt;=500. |
| Cardinalità array in ExperienceEvent | &lt;=10 | Morbido | La cardinalità ottimale dell&#39;array in un ExperienceEvent (dati delle serie temporali) è &lt;=10. |
| Numero di identità per grafico di identità per profilo singolo | 50 | Duro | **Il numero massimo di identità in un grafico di identità per un singolo profilo è 50.** Eventuali profili con più di 50 identità sono esclusi da segmentazione, esportazioni e ricerche. |

{style=&quot;table-layout:auto&quot;}

### protezioni di entità Dimension

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Non sono consentiti dati per serie temporali per non[!DNL XDM Individual Profile] entità | 0 | Duro | **I dati relativi alle serie temporali non sono consentiti per i[!DNL XDM Individual Profile] entità nel servizio profili.** Se un set di dati della serie temporale è associato a un[!DNL XDM Individual Profile] ID, il set di dati non deve essere abilitato per [!DNL Profile]. |
| Nessuna relazione nidificata | 0 | Morbido | Non creare una relazione tra due non-[!DNL XDM Individual Profile] schemi. La possibilità di creare relazioni non è consigliata per gli schemi che non fanno parte del [!DNL Profile] schema di unione. |
| Profondità JSON per il campo ID primario | 4 | Morbido | La profondità massima JSON consigliata per il campo ID principale è 4. Ciò significa che in uno schema altamente nidificato non devi selezionare un campo come ID primario se è nidificato con più di 4 livelli di profondità. Un campo al quarto livello nidificato può essere utilizzato come ID primario. |

{style=&quot;table-layout:auto&quot;}

## Limiti di dimensione dei dati

Le seguenti protezioni fanno riferimento alla dimensione dei dati e forniscono i limiti consigliati per i dati che possono essere acquisiti, memorizzati e interrogati come previsto. Per ulteriori informazioni sulle entità principali e le entità dimensione, consulta la sezione su [tipi di entità](#entity-types) nell&#39;appendice.

>[!NOTE]
>
>La dimensione dei dati viene misurata come dati non compressi in JSON al momento dell’acquisizione.

### Garanzie dell&#39;entità principale

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Dimensione massima di ExperienceEvent | 10 KB | Duro | **La dimensione massima di un evento è 10 KB.** L’acquisizione continuerà, ma tutti gli eventi di dimensioni superiori a 10 KB verranno eliminati. |
| Dimensione massima del record del profilo | 100 KB | Duro | **La dimensione massima di un record di profilo è 100 KB.** L’acquisizione continuerà, tuttavia i record di profilo di dimensioni superiori a 100 KB verranno eliminati. |
| Dimensione massima del frammento di profilo | 50 MB | Duro | **La dimensione massima di un singolo frammento di profilo è 50 MB.** Segmentazione, esportazioni e ricerche potrebbero non riuscire per qualsiasi [frammento di profilo](#profile-fragments) è più grande di 50 MB. |
| Dimensioni massime di archiviazione del profilo | 50 MB | Morbido | **La dimensione massima di un profilo memorizzato è 50 MB.** Aggiunta di nuovi [frammenti di profilo](#profile-fragments) In un profilo di dimensioni superiori a 50 MB, le prestazioni del sistema risulteranno compromesse. Ad esempio, un profilo potrebbe contenere un singolo frammento di 50 MB oppure più frammenti in più set di dati con una dimensione totale combinata di 50 MB. Il tentativo di memorizzare un profilo con un singolo frammento di dimensioni superiori a 50 MB o più frammenti di dimensioni totali superiori a 50 MB in una dimensione combinata influisce sulle prestazioni del sistema. |
| Numero di batch di profili o ExperienceEvent acquisiti al giorno | 90 | Morbido | **Il numero massimo di batch di profili o ExperienceEvent acquisiti al giorno è 90.** Ciò significa che il totale combinato dei batch di Profile ed ExperienceEvent acquisiti ogni giorno non può superare i 90. L’inserimento di batch aggiuntivi influisce sulle prestazioni del sistema. |

{style=&quot;table-layout:auto&quot;}

### protezioni di entità Dimension

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Dimensione totale per tutte le entità dimensionali | 5 GB | Morbido | La dimensione totale consigliata per tutte le entità dimensionali è 5 GB. L&#39;inserimento di entità di grandi dimensioni può influire sulle prestazioni del sistema. Ad esempio, non è consigliato caricare un catalogo di prodotti da 10 GB come entità dimensione. |
| Set di dati per schema entità dimensionale | 5 | Morbido | È consigliato un massimo di 5 set di dati associati a ogni schema di entità dimensionale. Ad esempio, se crei uno schema per &quot;prodotti&quot; e aggiungi cinque set di dati che contribuiscono, non devi creare un sesto set di dati associato allo schema dei prodotti. |
| batch di entità Dimension acquisiti al giorno | 4 per entità | Morbido | Il numero massimo consigliato di batch di entità dimensione acquisiti al giorno è 4 per entità. Ad esempio, puoi inserire gli aggiornamenti di un catalogo di prodotti fino a 4 volte al giorno. L’inserimento di batch di entità dimensione aggiuntivi per la stessa entità può influire sulle prestazioni del sistema. |

{style=&quot;table-layout:auto&quot;}

## Garanzie di segmentazione

Le protezioni descritte in questa sezione si riferiscono al numero e alla natura dei segmenti che un’organizzazione può creare all’interno di un Experience Platform, nonché alla mappatura e all’attivazione dei segmenti sulle destinazioni.

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Segmenti per sandbox | 4000 | Morbido | Un’organizzazione può avere più di 4000 segmenti in totale, purché ci siano meno di 4000 segmenti in ogni singolo sandbox. Il tentativo di creare ulteriori segmenti può influire sulle prestazioni del sistema. |
| Segmenti edge per sandbox | 150 | Morbido | Un’organizzazione può avere più di 150 segmenti edge in totale, purché vi siano meno di 150 segmenti edge in ogni singolo sandbox. Il tentativo di creare ulteriori segmenti edge può influire sulle prestazioni del sistema. |
| Segmenti in streaming per sandbox | 500 | Morbido | Un’organizzazione può disporre di più di 500 segmenti di streaming in totale, purché ci siano meno di 500 segmenti di streaming in ogni singolo sandbox. Il tentativo di creare ulteriori segmenti di streaming potrebbe influire sulle prestazioni del sistema. |
| Segmenti batch per sandbox | 4000 | Morbido | Un’organizzazione può avere più di 4000 segmenti batch in totale, purché ci siano meno di 4000 segmenti batch in ogni singolo sandbox. Il tentativo di creare ulteriori segmenti batch può influire sulle prestazioni del sistema. |

{style=&quot;table-layout:auto&quot;}

## Appendice

Questa sezione fornisce ulteriori dettagli sui limiti contenuti in questo documento.

### Tipi di entità

La [!DNL Profile] il modello di dati store è costituito da due tipi di entità principali:

* **Entità principale:** Un’entità primaria o un’entità di profilo unisce i dati per formare una &quot;singola origine di verità&quot; per un singolo utente. Questi dati unificati vengono rappresentati utilizzando la cosiddetta &quot;visualizzazione unione&quot;. Una vista unione aggrega i campi di tutti gli schemi che implementano la stessa classe in un unico schema di unione. Schema dell&#39;unione per [!DNL Real-time Customer Profile] è un modello dati ibrido denormalizzato che agisce come contenitore per tutti gli attributi del profilo e gli eventi comportamentali.

   Gli attributi indipendenti dal tempo, noti anche come &quot;dati di record&quot; vengono modellati utilizzando [!DNL XDM Individual Profile], mentre i dati delle serie temporali, noti anche come &quot;dati evento&quot; vengono modellati utilizzando [!DNL XDM ExperienceEvent]. Quando i dati di record e serie temporali vengono acquisiti in Adobe Experience Platform, si attiva [!DNL Real-time Customer Profile] per iniziare l’acquisizione dei dati abilitati per il relativo utilizzo. Più interazioni e dettagli vengono acquisiti, più i profili individuali diventano solidi.

   ![](images/guardrails/profile-entity.png)

* **entità Dimension:** Anche se l’archivio dati del profilo in cui vengono conservati i dati del profilo non è un archivio relazionale, il profilo consente l’integrazione con entità di dimensioni ridotte per creare segmenti in modo semplice e intuitivo. Questa integrazione è nota come [segmentazione su più entità](../segmentation/multi-entity-segmentation.md). La tua organizzazione può inoltre definire classi XDM per descrivere elementi diversi da singoli utenti, ad esempio negozi, prodotti o proprietà. Tali[!DNL XDM Individual Profile] Gli schemi sono noti come &quot;entità dimensione&quot; e non contengono dati relativi alle serie temporali. Le entità di Dimension forniscono dati di ricerca che consentono e semplificano le definizioni di segmenti a più entità e devono essere sufficientemente piccole da consentire al motore di segmentazione di caricare l’intero set di dati in memoria per un’elaborazione ottimale (ricerca rapida dei punti).

   ![](images/guardrails/profile-and-dimension-entities.png)

### Frammenti di profilo

In questo documento sono presenti diverse protezioni che fanno riferimento a &quot;frammenti di profilo&quot;. Ad Experience Platform, più frammenti di profilo vengono uniti per formare il Profilo cliente in tempo reale. Ciascun frammento rappresenta un’identità principale univoca e i dati corrispondenti del record o dell’evento per tale ID all’interno di un dato set di dati. Per ulteriori informazioni sui frammenti di profilo, consulta [Panoramica del profilo](home.md#profile-fragments-vs-merged-profiles).

### Unisci criteri {#merge-policies}

Quando si riuniscono dati provenienti da più origini, i criteri di unione sono le regole utilizzate da Platform per determinare in che modo i dati verranno definiti come prioritari e quali dati verranno combinati per creare tale visualizzazione unificata. Ad esempio, se un cliente interagisce con il tuo marchio su più canali, la tua organizzazione avrà più frammenti di profilo relativi al singolo cliente che compaiono in più set di dati. Quando questi frammenti vengono acquisiti in Platform, vengono uniti per creare un singolo profilo per quel cliente. Quando i dati provenienti da più origini sono in conflitto, il criterio di unione determina quali informazioni includere nel profilo dell&#39;utente. È consentito un massimo di cinque (5) criteri di unione per organizzazione. Per ulteriori informazioni sui criteri di unione, consulta la sezione [panoramica dei criteri di unione](merge-policies/overview.md).

### Set di dati suite di rapporti Adobe Analytics in Platform {#aa-datasets}

È possibile abilitare più suite di rapporti per il profilo purché tutti i conflitti di dati siano risolti. Puoi utilizzare la funzionalità Preparazione dati per risolvere i conflitti di dati tra eVar, Elenchi e Prop. Per ulteriori informazioni su come utilizzare la funzionalità di preparazione dei dati, consulta la sezione [Guida all’interfaccia utente del connettore Adobe Analytics](../sources/tutorials/ui/create/adobe-applications/analytics.md).
