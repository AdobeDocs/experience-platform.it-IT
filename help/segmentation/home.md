---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Servizio Segmentazione Adobe Experience Platform '
topic: overview
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '1971'
ht-degree: 0%

---


# Adobe Experience Platform [!DNL Segmentation Service] overview

 Adobe Experience Platform [!DNL Segmentation Service] fornisce un&#39;interfaccia utente e RESTful API che consente di creare segmenti e generare audience dai [!DNL Real-time Customer Profile] dati. Questi segmenti sono configurati e mantenuti a livello centrale [!DNL Platform]e sono facilmente accessibili da qualsiasi soluzione Adobe.

Questo documento fornisce una panoramica [!DNL Segmentation Service] e il ruolo che svolge  Adobe Experience Platform.

## Getting started with [!DNL Segmentation Service]

È importante comprendere i seguenti termini chiave utilizzati in tutto il presente documento:

- **Segmentazione**: Dividere un gruppo di individui di grandi dimensioni (come clienti, potenziali, utenti o organizzazioni) in gruppi più piccoli che condividono caratteristiche simili e risponderanno in modo simile alle strategie di marketing.
- **Definizione** segmento: Set di regole utilizzato per descrivere le caratteristiche o il comportamento chiave di un&#39;audience target. Una volta concettualizzate, le regole delineate in una definizione di segmento vengono utilizzate per determinare i membri di pubblico idonei per un segmento.
- **Pubblico**: Set di profili risultante che soddisfano i criteri di una definizione di segmento.

## Funzionamento della segmentazione

La segmentazione è il processo di definizione di attributi o comportamenti specifici condivisi da un sottoinsieme di profili dall&#39;archivio profili per distinguere un gruppo commerciabile di persone dalla base cliente. Ad esempio, in una campagna e-mail intitolata &quot;Hai dimenticato di comprare le tue scarpe da ginnastica?&quot;, potresti voler avere un pubblico di tutti gli utenti che hanno cercato di correre scarpe negli ultimi 30 giorni, ma che non hanno completato un acquisto.

Una volta che un segmento è stato concettualmente definito, è integrato [!DNL Experience Platform]. In genere, i segmenti sono realizzati dagli esperti di marketing o dagli specialisti di audience, anche se alcune organizzazioni preferiscono essere creati dal loro reparto marketing, in collaborazione con i loro analisti di dati. Dopo aver rivisto i dati a cui si desidera inviare [!DNL Platform], l&#39;analista dei dati compone la definizione del segmento selezionando i campi e i valori da utilizzare per creare le regole o le condizioni del segmento. Questa operazione viene eseguita utilizzando l&#39;interfaccia utente o l&#39;API.

## Creare un segmento

Sia che vengano creati mediante l&#39;API o mediante l&#39; [!DNL Segment Builder], i segmenti vengono definiti in ultima analisi utilizzando [!DNL Profile Query Language] (PQL). Qui la definizione del segmento concettuale viene descritta nel linguaggio creato per recuperare i profili che soddisfano i criteri. Per ulteriori informazioni, consultate la panoramica [PQL](./pql/overview.md).

Per informazioni su come creare e utilizzare i segmenti in [!DNL Segment Builder] (l’implementazione dell’interfaccia utente di [!DNL Segmentation Service]), consulta la guida [di](./ui/overview.md)Generatore di segmenti.

Per informazioni sulla creazione di definizioni di segmenti tramite l&#39;API, consulta l&#39;esercitazione sulla [creazione di segmenti di pubblico tramite l&#39;API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Nel caso in cui uno schema venga esteso, tutti i caricamenti futuri devono aggiornare di conseguenza i campi aggiunti di recente. Per ulteriori informazioni sulla personalizzazione [!DNL Experience Data Model] (XDM), vedere l&#39;esercitazione [Editor](../xdm/tutorials/create-schema-ui.md)schema.

## Valutazione dei segmenti

### Segmentazione in streaming

La segmentazione in streaming è un processo continuo di selezione dei dati che aggiorna i segmenti in risposta all&#39;attività degli utenti. Una volta creato e salvato un segmento, la definizione del segmento viene applicata ai dati in arrivo a [!DNL Real-time Customer Profile]. L&#39;aggiunta e l&#39;eliminazione di segmenti vengono elaborati regolarmente, garantendo che il pubblico di destinazione rimanga rilevante.

Per ulteriori informazioni sulla segmentazione in streaming, consulta la documentazione [sulla segmentazione in](./api/streaming-segmentation.md)streaming.

### Segmentazione batch

In alternativa a un processo continuo di selezione dei dati, la segmentazione in batch sposta tutti i dati di profilo contemporaneamente attraverso le definizioni dei segmenti per produrre i tipi di pubblico corrispondenti. Una volta creato, questo segmento viene salvato e memorizzato in modo da poterlo esportare per l’uso.

Per informazioni su come valutare i segmenti, consulta l’esercitazione [sulla valutazione dei](./tutorials/evaluate-a-segment.md)segmenti.

## Accesso ai risultati della segmentazione

Per informazioni su come accedere a un segmento esportato, consulta l’esercitazione [sulla valutazione dei](./tutorials/evaluate-a-segment.md)segmenti.

## Metadati segmento

I metadati dei segmenti facilitano l’indicizzazione nel caso in cui uno dei segmenti venga riutilizzato e/o combinato.

Per comporre i segmenti (tramite API o [!DNL Segment Builder]) è necessario definire un nome di segmento e un criterio di unione.

### Nomi dei segmenti

Quando crei un nuovo segmento, devi fornire un nome di segmento. Il nome del segmento viene utilizzato per identificare un particolare segmento tra la raccolta generata da [!DNL Segmentation Service]. I nomi dei segmenti devono pertanto essere descrittivi, concisi e univoci.

>[!NOTE]
>
>Durante la pianificazione di un segmento, tieni presente che ai segmenti è possibile fare riferimento da qualsiasi altro segmento e che questi possono essere combinati con esso. Quando selezioni un nome, prendi in considerazione la possibilità che il segmento contenga porzioni riutilizzabili.

### Unisci criteri

I criteri di unione sono regole utilizzate [!DNL Profile] per determinare in che modo i dati verranno classificati in ordine di priorità e combinati in una visualizzazione unificata a determinate condizioni.
Se non è definito alcun criterio di unione, viene utilizzato il criterio di [!DNL Platform] unione predefinito. Se preferite utilizzare un criterio di unione specifico per l&#39;organizzazione, potete crearne uno personalizzato e contrassegnarlo come predefinito dell&#39;organizzazione.

Ulteriori informazioni sui criteri di unione sono disponibili nella guida [ai criteri di](../profile/api/merge-policies.md)unione.

>[!NOTE]
>
>La stima delle dimensioni del pubblico si basa sui criteri di unione dei profili predefiniti dell&#39;organizzazione.

### Altri metadati di segmento

Oltre al nome del segmento e ai criteri di unione, [!DNL Segment Builder] offre anche un campo di metadati &quot;descrizione del segmento&quot; in cui è possibile riepilogare lo scopo della definizione del segmento.

## Funzioni avanzate di segmentazione

I segmenti possono essere configurati in modo da generare continuamente un pubblico combinando l&#39;inserimento [dei dati di](../ingestion/streaming-ingestion/overview.md) streaming con una delle seguenti funzioni avanzate di segmentazione:
- [Segmentazione sequenziale](#sequential)
- [Segmentazione dinamica](#dynamic)
- [Segmentazione multi-entità](#multi-entity)

Queste funzioni avanzate sono descritte più dettagliatamente nelle sezioni seguenti.

## Segmentazione sequenziale {#sequential}

Un percorso standard dell&#39;utente è sequenziale.  Adobe Experience Platform consente di definire una serie ordinata di segmenti per riflettere questo percorso, acquisendo così le sequenze di eventi man mano che si verificano. Potete organizzare gli eventi nell&#39;ordine desiderato utilizzando la timeline dell&#39;evento visivo nella [!DNL Segment Builder].

Un esempio di percorso cliente che richiederebbe segmentazione sequenziale sarebbe la visualizzazione prodotto > aggiunta prodotto > checkout > Nessun acquisto.

## Segmentazione dinamica {#dynamic}

La segmentazione dinamica risolve i problemi di scalabilità che tradizionalmente incontrano i professionisti del marketing quando creano segmenti per campagne di marketing.

A differenza della segmentazione statica che richiede l&#39;acquisizione esplicita e ripetuta di ogni caso di utilizzo possibile, la segmentazione dinamica utilizza le variabili per creare la logica della regola ed esprimere in modo dinamico le relazioni.

### Caso di utilizzo: Ricerca di clienti che effettuano acquisti al di fuori del proprio stato

Per illustrare il valore di questa funzione di segmentazione avanzata, è consigliabile che un architetto dati collabori con un esperto di marketing per identificare i clienti che hanno effettuato acquisti al di fuori del proprio stato di origine.

**Il problema**

La segmentazione statica richiede di definire singoli segmenti con un attributo di stato iniziale univoco, prima di filtrare gli eventi di acquisto che non corrispondono allo stato iniziale. Un segmento esplicito di questo tipo avrebbe scritto &quot;Sto cercando persone dallo Utah dove lo stato del loro acquisto non è lo Utah&quot;. La creazione di un&#39;audience con questo metodo richiede la definizione di un segmento per ogni stato statunitense, per un totale di 50 segmenti.

A seguito delle diverse combinazioni di segmenti che inevitabilmente si verificano durante la scalabilità, il processo manuale richiesto per la segmentazione statica diventa più lungo, riducendo l&#39;efficienza complessiva.

**La soluzione**

Assegnando una variabile all&#39;attributo stato acquisto, il segmento dinamico semplifica la ricerca di un acquisto in cui lo stato dell&#39;acquisto non è uguale allo stato iniziale del cliente. In questo modo potrete consolidare 50 segmenti statici in un unico segmento dinamico.

## Segmentazione multi-entità {#multi-entity}

Con la funzione avanzata di segmentazione multi-entità, potete creare segmenti utilizzando più classi XDM, aggiungendo così estensioni agli schemi di persona. Di conseguenza, [!DNL Segmentation Service] è possibile accedere a campi aggiuntivi durante la definizione del segmento, come se fossero nativi dell&#39;archivio dati del profilo.

La segmentazione multi-entità offre la flessibilità necessaria per identificare i tipi di pubblico in base ai dati pertinenti alle esigenze aziendali. Questo processo può essere fatto in modo rapido e semplice senza richiedere la competenza nella query dei database. Questo consente di aggiungere dati chiave ai segmenti senza dover apportare costose modifiche ai flussi di dati o aspettare un&#39;unione di dati back-end.

Il seguente video è stato realizzato per consentire di comprendere meglio la segmentazione tra più entità e mostra sia la segmentazione multi-entità che il contesto del segmento (payload del segmento).

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

### Caso di utilizzo: Promozione basata sui prezzi

Per illustrare il valore di questa funzione di segmentazione avanzata, è consigliabile che un architetto dati collabori con un esperto di marketing.

In questo esempio, l&#39;architetto dei dati unisce i dati per una singola classe (costituita da schemi con [!DNL XDM Individual Profile] e [!DNL XDM ExperienceEvent] come classi di base) utilizzando una chiave a un&#39;altra classe. Una volta uniti, l&#39;architetto dei dati o l&#39;esperto di marketing possono utilizzare questi nuovi campi durante la definizione del segmento come se fossero nativi dello schema della classe base.

**Il problema**

L&#39;architetto dei dati e l&#39;esperto di marketing lavorano entrambi per lo stesso rivenditore di abbigliamento. Il rivenditore ha più di 1.000 punti vendita in Nord America e riduce periodicamente i prezzi dei prodotti per tutto il loro ciclo di vita. Di conseguenza, l&#39;esperto di marketing vuole eseguire una campagna speciale per dare agli acquirenti che hanno acquistato questi articoli la possibilità di acquistarli al prezzo scontato.

Le risorse dell&#39;architetto dati includono l&#39;accesso ai dati Web dalla navigazione dei clienti e ai dati di aggiunta del carrello contenenti identificatori SKU del prodotto. Hanno inoltre accesso a una classe &quot;prodotti&quot; separata, in cui vengono memorizzate informazioni aggiuntive sul prodotto (incluso il prezzo del prodotto). La loro guida è focalizzata sui clienti che hanno aggiunto un prodotto al loro carrello negli ultimi 14 giorni, ma non hanno acquistato l&#39;articolo, il cui prezzo è ora sceso.

**La soluzione**

>[!NOTE]
>
>In questo esempio si suppone che l&#39;architetto dei dati abbia già stabilito uno spazio dei nomi ID.

Utilizzando l&#39;API, l&#39;architetto dati collega la chiave dello [!DNL ExperienceEvent] schema alla classe &quot;products&quot;. In questo modo l&#39;architetto dei dati può utilizzare i campi aggiuntivi della classe &quot;products&quot; come se fossero nativi dello [!DNL ExperienceEvent] schema. Come fase finale del lavoro di configurazione, l&#39;architetto dei dati deve inserire i dati appropriati in [!DNL Real-time Customer Profile]. A questo scopo, abilita il dataset &quot;products&quot; da utilizzare con [!DNL Profile]. Una volta completata la configurazione, l&#39;architetto dei dati o l&#39;esperto di marketing possono creare il segmento di destinazione in [!DNL Segment Builder].

Vedere la panoramica [sulla composizione dello](../xdm/schema/composition.md#union) schema per apprendere come definire le relazioni tra le classi XDM.

<!-- ## Personalization payload

Segments can now carry a payload of contextual details to enable deep personalization of Adobe Solutions as well as external non-Adobe applications. These payloads can be added while defining your target segment.

With contextual data built into the segment itself, this advanced Segmentation Service feature allows you to better connect with your customer.

Segment Payload helps you answer questions surrounding your customer’s frame of reference such as:
- What: What product was purchased? What product should be recommended next?
- When: At what time and date did the purchase occur?
- Where: In which store or city did the customer make their purchase?

While this solution does not change the binary nature of segment membership, it does add additional context to each profile through an associated segment membership object. Each segment membership object has the capacity to include three kinds of contextual data:

- **Identifier**: this is the ID for the segment 
- **Attributes**: this would include information about the segment ID such as last qualification time, XDM version, status and so on.
- **Event data**: Specific aspects of experience events which resulted in the profile qualifying for the segment

Adding this specific data to the segment itself allows execution engines to personalize the experience for the customers in their target audience. -->

### Casi di utilizzo

Per illustrare il valore di questa funzione di segmentazione avanzata, prendete in considerazione tre casi d’uso standard che illustrano le sfide presenti nelle applicazioni di marketing prima del miglioramento del payload del segmento:
- Personalizzazione e-mail
- Ritargeting e-mail
- Ad retargeting

**Personalizzazione e-mail**

Un esperto di marketing che crea una campagna e-mail potrebbe aver tentato di creare un segmento per un pubblico target utilizzando gli acquisti recenti da parte dell&#39;archivio clienti negli ultimi tre mesi. Idealmente, questo segmento richiederebbe sia il nome dell&#39;articolo che il nome dello store in cui è stato effettuato l&#39;acquisto. Prima di questo miglioramento, la sfida era catturare l&#39;identificatore dello store dall&#39;evento di acquisto e assegnarlo al profilo del cliente.

**Ritargeting e-mail**

Spesso è complesso creare e qualificare segmenti per le campagne e-mail mirate all&#39;&quot;abbandono del carrello&quot;. Prima del miglioramento, sapere quali prodotti includere in un messaggio personalizzato era difficile a causa della disponibilità dei dati richiesti. I dati per i quali i prodotti sono stati abbandonati sono legati a eventi di esperienza che prima erano difficili da monitorare ed estrarre dati da.

**Ad retargeting**

Un&#39;altra sfida tradizionale per gli esperti di marketing è stata la creazione di annunci per ricompensare i clienti con articoli abbandonati del carrello. Mentre le definizioni dei segmenti affrontavano questa sfida, prima del miglioramento, non esisteva un metodo formale per distinguere tra prodotti acquistati e prodotti abbandonati. Ora è possibile eseguire il targeting di set di dati specifici durante la definizione del segmento.

## [!DNL Segmentation Service] tipi di dati

[!DNL Segmentation Service] supporta diversi tipi di dati, tra cui:

- Stringa
- Uniform Resource Identifier
- Enum
- Numero
- Long
- Intero
- Breve
- Byte
- Booleano
- Data
- Data-ora
- Matrice
- Oggetto
- Mappa
- Eventi

Informazioni più dettagliate su questi tipi di dati supportati sono disponibili nel documento [sui tipi di dati di](./data-types.md)supporto.

## Passaggi successivi

[!DNL Segmentation Service] fornisce un flusso di lavoro consolidato per creare segmenti dai [!DNL Real-time Customer Profile] dati. In sintesi:

- [!DNL Segmentation] è il processo di definizione di un sottoinsieme di profili dall&#39;archivio profili, che consente di caratterizzare il comportamento o gli attributi di un gruppo commerciabile desiderato. [!DNL Segmentation Service] rende possibile questo processo.
- Durante la pianificazione di un segmento, tenere presente che a un segmento può essere fatto riferimento e combinato con qualsiasi altro segmento.
- Un segmento può essere generato da regole basate sui dati del profilo, sui dati delle serie temporali correlati o su entrambi.
- I segmenti possono essere valutati su richiesta o in modo continuo. Quando viene valutato su richiesta, tutti i dati del profilo vengono passati attraverso le definizioni del segmento alla volta. Quando viene valutato in modo continuo, i dati scorrono le definizioni dei segmenti man mano che entrano [!DNL Platform].

Per informazioni su come definire i segmenti nell’interfaccia utente, consulta la guida [di Generatore di](./ui/overview.md)segmenti. Per informazioni sulla creazione di definizioni di segmenti tramite l&#39;API, consulta l&#39;esercitazione sulla [creazione di segmenti tramite l&#39;API](./tutorials/create-a-segment.md).