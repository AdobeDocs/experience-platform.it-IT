---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;servizio segmenti;segmento;Segmento;Segmenti;segmenti
solution: Experience Platform
title: Panoramica del servizio di segmentazione
topic-legacy: overview
description: Scopri il servizio di segmentazione di Adobe Experience Platform e il ruolo che svolge nell’ecosistema di Platform.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 52197a6c009fb5b0b6037a4fef3c98ad7c327e2e
workflow-type: tm+mt
source-wordcount: '1632'
ht-degree: 0%

---

# [!DNL Segmentation Service] panoramica

Adobe Experience Platform [!DNL Segmentation Service] fornisce un’interfaccia utente e l’API RESTful che ti consentono di creare segmenti e generare tipi di pubblico dal tuo [!DNL Real-time Customer Profile] dati. Questi segmenti sono configurati e mantenuti a livello centrale su [!DNL Platform]e sono facilmente accessibili da qualsiasi soluzione di Adobe.

Questo documento fornisce una panoramica di [!DNL Segmentation Service] e il ruolo che gioca in Adobe Experience Platform.

## Guida introduttiva a [!DNL Segmentation Service]

È importante comprendere i seguenti termini chiave utilizzati in questo documento:

- **Segmentazione**: Dividere un grande gruppo di individui (come clienti, potenziali, utenti o organizzazioni) in gruppi più piccoli che condividono caratteristiche simili e risponderanno in modo simile alle strategie di marketing.
- **Definizione del segmento**: Set di regole utilizzato per descrivere le caratteristiche o il comportamento chiave di un pubblico target. Una volta concettualizzate, le regole descritte in una definizione di segmento vengono utilizzate per determinare i membri del pubblico qualificati per un segmento.
- **Pubblico**: Il set risultante di profili che soddisfano i criteri di una definizione di segmento.

## Come funziona la segmentazione

La segmentazione è il processo di definizione di attributi o comportamenti specifici condivisi da un sottoinsieme di profili dall’archivio dei profili per distinguere un gruppo commerciabile di persone dalla base dei clienti. Ad esempio, in una campagna e-mail intitolata &quot;Ti sei dimenticato di comprare le scarpe da ginnastica?&quot;, potresti volere un pubblico di tutti gli utenti che hanno cercato di correre scarpe negli ultimi 30 giorni, ma che non hanno completato un acquisto.

Una volta definito concettualmente un segmento, viene incorporato in [!DNL Experience Platform]. In genere, i segmenti sono generati dagli addetti al marketing o dagli specialisti di pubblico, anche se alcune organizzazioni preferiscono essere creati dal loro reparto marketing, in collaborazione con i loro analisti di dati. Dopo aver esaminato i dati inviati a [!DNL Platform], l’analista di dati compone la definizione del segmento selezionando quali campi e valori verranno utilizzati per creare le regole o le condizioni del segmento. Questa operazione viene eseguita utilizzando l’interfaccia utente o l’API.

## Creare segmenti

Creato utilizzando l’API o [!DNL Segment Builder], i segmenti vengono definiti in ultima analisi utilizzando [!DNL Profile Query Language] (PQL). In questa sezione viene descritta la definizione del segmento concettuale nel linguaggio creato per recuperare i profili che soddisfano i criteri. Per ulteriori informazioni, consulta la sezione [Panoramica di PQL](./pql/overview.md).

Per scoprire come creare e utilizzare i segmenti nel [!DNL Segment Builder] (l’implementazione dell’interfaccia utente di [!DNL Segmentation Service]), vedi [Guida al Generatore di segmenti](./ui/overview.md).

Per informazioni sulla creazione di definizioni di segmenti utilizzando l’API, consulta l’esercitazione su [creazione di segmenti di pubblico tramite API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Nel caso in cui uno schema venga esteso, tutti i caricamenti futuri devono aggiornare di conseguenza i campi appena aggiunti. Per ulteriori informazioni sulla personalizzazione [!DNL Experience Data Model] (XDM), visita [Esercitazione sull’Editor di schema](../xdm/tutorials/create-schema-ui.md).
>
>Inoltre, se il valore TTL (time-to-live) è abilitato nel set di dati, ciò potrebbe influenzare l’appartenenza del segmento creato. Per ulteriori informazioni su TTL e su come può influenzare la segmentazione, consulta la sezione [Guida TTL del servizio profili](../profile/apply-ttl.md).

## Valutare i segmenti {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="Metodi di valutazione"
>abstract="Platform supporta attualmente tre metodi di valutazione dei segmenti: segmentazione in streaming, segmentazione in batch e segmentazione edge."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="Valutazione in streaming"
>abstract="La segmentazione in streaming è un processo continuo di selezione dei dati che aggiorna i segmenti in risposta all’attività dell’utente."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html" text="Valutare gli eventi in tempo quasi reale con la segmentazione in streaming"

Platform supporta attualmente tre metodi di valutazione dei segmenti: segmentazione in streaming, segmentazione in batch e segmentazione edge.

### Segmentazione streaming {#streaming}

La segmentazione in streaming è un processo continuo di selezione dei dati che aggiorna i segmenti in risposta all’attività dell’utente. Una volta generato e salvato un segmento, la definizione del segmento viene applicata ai dati in arrivo a [!DNL Real-time Customer Profile]. Gli aggiornamenti e le rimozioni dei segmenti vengono elaborati regolarmente, garantendo che il pubblico di destinazione rimanga rilevante.

Per ulteriori informazioni sulla segmentazione in streaming, consulta la sezione [documentazione sulla segmentazione in streaming](./api/streaming-segmentation.md).

### Segmentazione in batch {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Valutazione batch"
>abstract="In alternativa a un processo continuo di selezione dei dati, la segmentazione in batch sposta tutti i dati di profilo contemporaneamente attraverso le definizioni dei segmenti per produrre i tipi di pubblico corrispondenti. Una volta creato, il segmento viene salvato e memorizzato in modo da poterlo esportare per l’uso."

In alternativa a un processo continuo di selezione dei dati, la segmentazione in batch sposta tutti i dati di profilo contemporaneamente attraverso le definizioni dei segmenti per produrre i tipi di pubblico corrispondenti. Una volta creato, questo segmento viene salvato e memorizzato in modo da poterlo esportare per l’uso.

I segmenti batch vengono valutati automaticamente ogni 24 ore. Se si desidera valutare un segmento batch su richiesta, è possibile utilizzare un processo di segmento. Per ulteriori informazioni sui processi dei segmenti, consulta la sezione [documentazione sui processi di segmento](./api/segment-jobs.md).

### Segmentazione degli spigoli {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Valutazione Edge"
>abstract="La segmentazione dei bordi è la capacità di valutare istantaneamente i segmenti in Platform su Experience Edge, consentendo casi d’uso di personalizzazione per pagine uguali e successive."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html" text="Guida all’interfaccia utente per la segmentazione dei bordi"

La segmentazione dei bordi è la capacità di valutare istantaneamente i segmenti in Platform [su Experience Edge](../edge/home.md), abilitare i casi d’uso per la personalizzazione della pagina e di quella successiva.

Per ulteriori informazioni sulla segmentazione dei bordi, consulta la sezione [Documentazione API](./api/edge-segmentation.md) o [Documentazione dell’interfaccia utente](./ui/edge-segmentation.md).

## Accedere ai risultati della segmentazione

Per scoprire come accedere a un segmento esportato, consulta la sezione [esercitazione sulla valutazione dei segmenti](./tutorials/evaluate-a-segment.md).

## Metadati del segmento

I metadati del segmento facilitano l’indicizzazione nel caso in cui uno qualsiasi dei tuoi segmenti debba essere riutilizzato e/o combinato.

Composizione dei segmenti (tramite API o [!DNL Segment Builder]) richiede di definire un nome di segmento e un criterio di unione.

### Nomi dei segmenti

Quando crei un nuovo segmento, devi fornire un nome di segmento. Il nome del segmento viene utilizzato per identificare un particolare segmento tra la raccolta creata da [!DNL Segmentation Service]. I nomi dei segmenti devono quindi essere descrittivi, concisi e univoci.

>[!NOTE]
>
>Quando pianifichi un segmento, ricorda che ai segmenti può essere fatto riferimento da qualsiasi altro segmento e combinato con esso. Quando selezioni un nome, prendi in considerazione la possibilità che il segmento contenga parti riutilizzabili.

### Unisci criteri

I criteri di unione sono regole utilizzate da [!DNL Profile] determinare in che modo i dati verranno classificati in base alle priorità e combinati in una visualizzazione unificata in determinate condizioni.
Se un criterio di unione non è definito, l&#39;impostazione predefinita [!DNL Platform] viene utilizzato il criterio di unione. Se si preferisce utilizzare un criterio di unione specifico per l&#39;organizzazione, è possibile crearne uno personalizzato e contrassegnarlo come predefinito dell&#39;organizzazione.

Ulteriori informazioni sui criteri di unione sono disponibili nella sezione [guida ai criteri di unione](../profile/api/merge-policies.md).

>[!NOTE]
>
>La stima delle dimensioni del pubblico si basa sul criterio di unione profili predefinito dell’organizzazione.

### Altri metadati dei segmenti

Oltre al nome del segmento e ai criteri di unione, [!DNL Segment Builder] offre un ulteriore campo di metadati &quot;descrizione segmento&quot; in cui puoi riepilogare lo scopo della definizione del segmento.

## Funzioni avanzate di segmentazione

I segmenti possono essere configurati in modo da generare continuamente un pubblico combinando [acquisizione dati in streaming](../ingestion/streaming-ingestion/overview.md) con una delle seguenti funzioni avanzate di segmentazione:
- [Segmentazione sequenziale](#sequential)
- [Segmentazione dinamica](#dynamic)
- [Segmentazione su più entità](#multi-entity)

Queste funzioni avanzate sono descritte più dettagliatamente nelle sezioni seguenti.

## Segmentazione sequenziale {#sequential}

Un percorso di utenti standard è sequenziale in natura. Adobe Experience Platform consente di definire una serie ordinata di segmenti per riflettere questo percorso, acquisendo quindi sequenze di eventi man mano che si verificano. Puoi organizzare gli eventi nell’ordine desiderato utilizzando la timeline dell’evento visivo nella [!DNL Segment Builder].

Un esempio di percorso di clienti che richiederebbe la segmentazione sequenziale sarebbe la visualizzazione del prodotto > aggiunta del prodotto > pagamento > Nessun acquisto.

## Segmentazione dinamica {#dynamic}

La segmentazione dinamica risolve i problemi di scalabilità che tradizionalmente incontrano gli addetti al marketing durante la creazione di segmenti per le campagne di marketing.

A differenza della segmentazione statica che richiede di acquisire in modo esplicito e ripetuto ogni possibile caso d’uso, la segmentazione dinamica utilizza le variabili per generare la logica della regola ed esprimere in modo dinamico le relazioni.

### Caso di utilizzo: Ricerca di clienti che effettuano acquisti al di fuori del proprio stato

Per illustrare il valore di questa funzione di segmentazione avanzata, considera la collaborazione di un architetto di dati con un addetto al marketing per identificare i clienti che hanno effettuato acquisti al di fuori del proprio stato iniziale.

**Il problema**

La segmentazione statica richiede di definire singoli segmenti con un attributo di stato iniziale univoco, prima di filtrare gli eventi di acquisto che non corrispondono allo stato iniziale. Un segmento esplicito di questo tipo avrebbe scritto &quot;Sto cercando persone dallo Utah dove lo stato del loro acquisto non è lo Utah&quot;. La creazione di un pubblico utilizzando questo metodo richiede di definire un segmento per ogni stato US, per un totale di 50 segmenti.

A causa delle diverse combinazioni di segmenti che inevitabilmente si presentano durante la scalabilità, il processo manuale richiesto per la segmentazione statica diventa più lungo, riducendo l’efficienza complessiva.

**La soluzione**

Assegnando una variabile all&#39;attributo dello stato di acquisto, il segmento dinamico semplifica la &quot;ricerca di un acquisto in cui lo stato di tale acquisto non è uguale allo stato di origine del cliente&quot;. In questo modo puoi consolidare 50 segmenti statici in un unico segmento dinamico.

## Segmentazione su più entità {#multi-entity}

Con la funzione avanzata di segmentazione multi-entità, puoi estendere [!DNL Real-time Customer Profile] dati con dati aggiuntivi basati su prodotti, archivi o altre persone, noti anche come entità &quot;dimension&quot;. Di conseguenza, [!DNL Segmentation Service] può accedere a campi aggiuntivi durante la definizione del segmento, come se fossero nativi [!DNL Profile] archivio dati. La segmentazione su più entità offre flessibilità nell’identificazione dei tipi di pubblico in base ai dati pertinenti alle tue esigenze aziendali specifiche. Per ulteriori informazioni, compresi i casi d’uso e i flussi di lavoro, consulta [guida alla segmentazione su più entità](multi-entity-segmentation.md).

## [!DNL Segmentation Service] tipi di dati

[!DNL Segmentation Service] supporta una varietà di tipi di dati primitivi e complessi. Informazioni dettagliate, compreso un elenco dei tipi di dati supportati, sono disponibili nella sezione [guida ai tipi di dati supportati](./data-types.md).

## Passaggi successivi

[!DNL Segmentation Service] fornisce un flusso di lavoro consolidato da cui creare i segmenti [!DNL Real-time Customer Profile] dati. In sintesi:

- [!DNL Segmentation] è il processo di definizione di un sottoinsieme di profili dall’archivio profili, che ti consente di caratterizzare il comportamento o gli attributi di un gruppo commercializzabile desiderato. [!DNL Segmentation Service] rende possibile questo processo.
- Durante la pianificazione di un segmento, ricorda che un segmento può essere referenziato da qualsiasi altro segmento e combinato con esso.
- Un segmento può essere generato da regole basate sui dati di profilo, sui dati relativi a serie temporali o su entrambi.
- I segmenti possono essere valutati on-demand o in modo continuo. Quando viene valutato on-demand, tutti i dati di profilo vengono trasmessi attraverso le definizioni dei segmenti contemporaneamente. Quando viene valutato continuamente, i dati scorrono attraverso le definizioni dei segmenti mentre immettono [!DNL Platform].

Per scoprire come definire i segmenti nell’interfaccia utente, vedi [Guida al Generatore di segmenti](./ui/overview.md). Per informazioni sulla creazione di definizioni di segmenti utilizzando l’API, consulta l’esercitazione su [creazione di segmenti utilizzando l’API](./tutorials/create-a-segment.md).
