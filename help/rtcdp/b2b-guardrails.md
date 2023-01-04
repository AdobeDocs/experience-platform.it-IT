---
keywords: profilo;profilo cliente in tempo reale;risoluzione dei problemi;protezioni;linee guida;limite;entità;entità primaria;entità dimensione;RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;piattaforma dati cliente in tempo reale;cdp in tempo reale;b2b;cdp;
title: Guardrail predefiniti per Real-time Customer Data Platform B2B Edition
type: Documentation
description: Adobe Experience Platform utilizza un modello di dati ibridi altamente denormalizzati che differisce dal modello tradizionale di dati relazionali. Questo documento fornisce limiti di utilizzo e di tasso predefiniti per aiutarti a modellare i tuoi dati in modo da ottenere prestazioni di sistema ottimali utilizzando Adobe Real-time Customer Data Platform B2B Edition.
exl-id: 8eff8c3f-a250-4aec-92a1-719ce4281272
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1602'
ht-degree: 2%

---

# Guardrail predefiniti per Real-time Customer Data Platform B2B Edition

>[!NOTE]
>
>I limiti descritti in questo documento rappresentano le modifiche abilitate da Real-time Customer Data Platform B2B Edition. Per un elenco completo dei limiti predefiniti per Real-Time CDP B2B Edition, combina questi limiti con i limiti generali di Adobe Experience Platform descritti in [protezioni per la documentazione dei dati del profilo cliente in tempo reale](../profile/guardrails.md).

Real-time Customer Data Platform B2B Edition consente di offrire esperienze cross-channel personalizzate basate su insights comportamentali e attributi del cliente sotto forma di profili cliente e profili account in tempo reale. Per supportare questo nuovo approccio ai profili, Experience Platform utilizza un modello dati ibrido altamente denormalizzato che differisce dal modello dati relazionale tradizionale.

Questo documento fornisce limiti di utilizzo e di tasso predefiniti per aiutarti a modellare i tuoi dati in modo da ottenere prestazioni di sistema ottimali. Quando si esaminano le seguenti protezioni, si presume che i dati siano stati modellati correttamente. Se hai domande su come modellare i tuoi dati, contatta il tuo rappresentante del servizio clienti.

>[!INFO]
>
>La maggior parte dei clienti non supera questi limiti predefiniti. Per informazioni sui limiti personalizzati, contatta il rappresentante dell’Assistenza clienti.

## Tipi di limite

Questo documento contiene due tipi di limiti predefiniti:

* **Limite morbido:** È possibile superare un limite soft, tuttavia i limiti soft forniscono una linea guida consigliata per le prestazioni del sistema.

* **Limite rigido:** Un limite rigido fornisce un massimo assoluto.

>[!INFO]
>
>I limiti delineati in questo documento vengono costantemente migliorati. Controlla regolarmente la disponibilità di aggiornamenti. Se sei interessato a conoscere i limiti personalizzati, contatta il tuo rappresentante di assistenza clienti.

## Limiti del modello dati

Le seguenti protezioni forniscono i limiti consigliati durante la modellazione dei dati del profilo cliente in tempo reale. Per ulteriori informazioni sulle entità principali e le entità dimensione, consulta la sezione su [tipi di entità](#entity-types) nell&#39;appendice.

### Garanzie dell&#39;entità principale

>[!NOTE]
>
>I limiti del modello dati descritti in questa sezione rappresentano le modifiche abilitate da Real-time Customer Data Platform B2B Edition. Per un elenco completo dei limiti predefiniti per Real-Time CDP B2B Edition, combina questi limiti con i limiti generali di Adobe Experience Platform descritti in [protezioni per la documentazione dei dati del profilo cliente in tempo reale](../profile/guardrails.md).

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Set di dati di classe XDM standard Real-Time CDP B2B Edition | 60 | Morbido | Si consiglia un massimo di 60 set di dati che sfruttano le classi standard Experience Data Model (XDM) fornite da Real-Time CDP B2B Edition. Per un elenco completo delle classi XDM standard per i casi d’uso B2B, fai riferimento al [Schemi nella documentazione di Real-Time CDP B2B Edition](schemas/b2b.md). <br/><br/>*Nota: A causa della natura del modello dati ibrido denormalizzato di Experience Platform, la maggior parte dei clienti non supera questo limite. Per domande su come modellare i dati o se desideri saperne di più sui limiti personalizzati, contatta il tuo rappresentante di Assistenza clienti.* |
| Relazioni legacy tra più entità | 20 | Morbido | È consigliato un massimo di 20 relazioni tra più entità definite tra entità primarie ed entità dimensione. Le mappature aggiuntive delle relazioni non devono essere effettuate finché non viene rimossa o disabilitata una relazione esistente. |
| Relazioni molti-a-uno per classe XDM | 2 | Morbido | Si consiglia un massimo di 2 relazioni molti-a-uno definite per classe XDM. È necessario creare una relazione aggiuntiva solo dopo aver rimosso o disabilitato una relazione esistente. Per i passaggi su come creare una relazione tra due schemi, consulta l’esercitazione su [definizione delle relazioni dello schema B2B](../xdm/tutorials/relationship-b2b.md). |

### protezioni di entità Dimension

>[!NOTE]
>
>I limiti del modello dati descritti in questa sezione rappresentano le modifiche abilitate da Real-time Customer Data Platform B2B Edition. Per un elenco completo dei limiti predefiniti per Real-Time CDP B2B Edition, combina questi limiti con i limiti generali di Adobe Experience Platform descritti in [protezioni per la documentazione dei dati del profilo cliente in tempo reale](../profile/guardrails.md).

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Nessuna relazione legacy nidificata | 0 | Morbido | Non creare una relazione tra due non-[!DNL XDM Individual Profile] schemi. La possibilità di creare relazioni non è consigliata per gli schemi che non fanno parte del [!DNL Profile] schema di unione. |
| Solo gli oggetti B2B possono partecipare a relazioni molti-a-uno | 0 | Duro | Il sistema supporta solo relazioni molti-a-uno tra gli oggetti B2B. Per ulteriori informazioni sulle relazioni molti-a-uno, consulta l’esercitazione su [definizione delle relazioni dello schema B2B](../xdm/tutorials/relationship-b2b.md). |
| Profondità massima delle relazioni nidificate tra oggetti B2B | 3 | Duro | La profondità massima delle relazioni nidificate tra gli oggetti B2B è 3. Questo significa che in uno schema altamente nidificato non dovrebbe esistere una relazione tra oggetti B2B nidificati con più di 3 livelli di profondità. |

## Limiti di dimensione dei dati

Le seguenti protezioni fanno riferimento alla dimensione dei dati e forniscono i limiti consigliati per i dati che possono essere acquisiti, memorizzati e interrogati come previsto. Per ulteriori informazioni sulle entità principali e le entità dimensione, consulta la sezione su [tipi di entità](#entity-types) nell&#39;appendice.

>[!INFO]
>
>La dimensione dei dati viene misurata come dati non compressi in JSON al momento dell’acquisizione.

### Garanzie dell&#39;entità principale

>[!NOTE]
>
>I limiti di dimensione dei dati descritti in questa sezione rappresentano le modifiche abilitate da Real-time Customer Data Platform B2B Edition. Per un elenco completo dei limiti predefiniti per Real-Time CDP B2B Edition, combina questi limiti con i limiti generali di Adobe Experience Platform descritti in [protezioni per la documentazione dei dati del profilo cliente in tempo reale](../profile/guardrails.md).

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Batch acquisiti per classe XDM al giorno | 45 | Morbido | Il numero totale di batch acquisiti ogni giorno per classe XDM non deve superare i 45. L’inserimento di batch aggiuntivi può impedire prestazioni ottimali. |

### protezioni di entità Dimension

>[!NOTE]
>
>I limiti di dimensione dei dati descritti in questa sezione rappresentano le modifiche abilitate da Real-time Customer Data Platform B2B Edition. Per un elenco completo dei limiti predefiniti per Real-Time CDP B2B Edition, combina questi limiti con i limiti generali di Adobe Experience Platform descritti in [protezioni per la documentazione dei dati del profilo cliente in tempo reale](../profile/guardrails.md).

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Dimensione totale per tutte le entità dimensionali | 5 GB | Morbido | La dimensione totale consigliata per tutte le entità dimensionali è 5 GB. L&#39;inserimento di entità di grandi dimensioni può influire sulle prestazioni del sistema. Ad esempio, non è consigliato caricare un catalogo di prodotti da 10 GB come entità dimensione. |
| Set di dati per schema entità dimensionale | 5 | Morbido | È consigliato un massimo di 5 set di dati associati a ogni schema di entità dimensionale. Ad esempio, se crei uno schema per &quot;prodotti&quot; e aggiungi cinque set di dati che contribuiscono, non devi creare un sesto set di dati associato allo schema dei prodotti. |
| batch di entità Dimension acquisiti al giorno | 4 per entità | Morbido | Il numero massimo consigliato di batch di entità dimensione acquisiti al giorno è 4 per entità. Ad esempio, puoi inserire gli aggiornamenti di un catalogo di prodotti fino a 4 volte al giorno. L’inserimento di batch di entità dimensione aggiuntivi per la stessa entità può influire sulle prestazioni del sistema. |

## Garanzie di segmentazione

Le protezioni descritte in questa sezione si riferiscono al numero e alla natura dei segmenti che un’organizzazione può creare all’interno di un Experience Platform, nonché alla mappatura e all’attivazione dei segmenti sulle destinazioni.

>[!NOTE]
>
>I limiti di segmentazione descritti in questa sezione rappresentano le modifiche abilitate da Real-time Customer Data Platform B2B Edition. Per un elenco completo dei limiti predefiniti per Real-Time CDP B2B Edition, combina questi limiti con i limiti generali di Adobe Experience Platform descritti in [protezioni per la documentazione dei dati del profilo cliente in tempo reale](../profile/guardrails.md).

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Segmenti per sandbox B2B | 400 | Morbido | Un’organizzazione può avere più di 400 segmenti in totale, purché ci siano meno di 400 segmenti in ogni singolo sandbox B2B. Il tentativo di creare ulteriori segmenti può influire sulle prestazioni del sistema. |

## Passaggi successivi

I limiti descritti in questo documento rappresentano le modifiche abilitate da Real-time Customer Data Platform B2B Edition. Per un elenco completo dei limiti predefiniti per Real-Time CDP B2B Edition, combina questi limiti con i limiti generali di Adobe Experience Platform descritti in [protezioni per la documentazione dei dati del profilo cliente in tempo reale](../profile/guardrails.md).

## Appendice

Questa sezione fornisce ulteriori dettagli sui limiti contenuti in questo documento.

### Tipi di entità

La [!DNL Profile] il modello di dati store è costituito da due tipi di entità principali:

* **Entità principale:** Un’entità primaria o un’entità di profilo unisce i dati per formare una &quot;singola origine di verità&quot; per un singolo utente. Questi dati unificati vengono rappresentati utilizzando la cosiddetta &quot;visualizzazione unione&quot;. Una vista unione aggrega i campi di tutti gli schemi che implementano la stessa classe in un unico schema di unione. Schema dell&#39;unione per [!DNL Real-Time Customer Profile] è un modello dati ibrido denormalizzato che agisce come contenitore per tutti gli attributi del profilo e gli eventi comportamentali.

   Gli attributi indipendenti dal tempo, noti anche come &quot;dati di record&quot; vengono modellati utilizzando [!DNL XDM Individual Profile], mentre i dati delle serie temporali, noti anche come &quot;dati evento&quot; vengono modellati utilizzando [!DNL XDM ExperienceEvent]. Quando i dati di record e serie temporali vengono acquisiti in Adobe Experience Platform, si attiva [!DNL Real-Time Customer Profile] per iniziare l’acquisizione dei dati abilitati per il relativo utilizzo. Più interazioni e dettagli vengono acquisiti, più i profili individuali diventano solidi.

   ![](../profile/images/guardrails/profile-entity.png)

* **entità Dimension:** Anche se l’archivio dati del profilo in cui vengono conservati i dati del profilo non è un archivio relazionale, il profilo consente l’integrazione con entità di dimensioni ridotte per creare segmenti in modo semplice e intuitivo. Questa integrazione è nota come [segmentazione su più entità](../segmentation/multi-entity-segmentation.md). La tua organizzazione può inoltre definire classi XDM per descrivere elementi diversi da singoli utenti, ad esempio negozi, prodotti o proprietà. Tali[!DNL XDM Individual Profile] Gli schemi sono noti come &quot;entità dimensione&quot; e non contengono dati relativi alle serie temporali. Le entità di Dimension forniscono dati di ricerca che consentono e semplificano le definizioni di segmenti a più entità e devono essere sufficientemente piccole da consentire al motore di segmentazione di caricare l’intero set di dati in memoria per un’elaborazione ottimale (ricerca rapida dei punti).

   ![](../profile/images/guardrails/profile-and-dimension-entities.png)
