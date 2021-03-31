---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;servizio segmenti;segmento;Segmento;Segmenti;segmenti
solution: Experience Platform
title: Panoramica del servizio di segmentazione
topic: ' - Panoramica'
description: Scopri il servizio di segmentazione di Adobe Experience Platform e il ruolo che svolge nell’ecosistema di Platform.
translation-type: tm+mt
source-git-commit: 738256021fb583e7dc14fd33f5df193813a6e0bb
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 0%

---


# [!DNL Segmentation Service]panoramica

Adobe Experience Platform [!DNL Segmentation Service] fornisce un’interfaccia utente e RESTful API che consente di creare segmenti e generare tipi di pubblico dai dati [!DNL Real-time Customer Profile]. Questi segmenti sono configurati e mantenuti a livello centrale su [!DNL Platform] e sono facilmente accessibili da qualsiasi soluzione di Adobe.

Questo documento fornisce una panoramica di [!DNL Segmentation Service] e del ruolo che svolge in Adobe Experience Platform.

## Guida introduttiva a [!DNL Segmentation Service]

È importante comprendere i seguenti termini chiave utilizzati in questo documento:

- **Segmentazione**: Dividere un grande gruppo di individui (come clienti, potenziali, utenti o organizzazioni) in gruppi più piccoli che condividono caratteristiche simili e risponderanno in modo simile alle strategie di marketing.
- **Definizione** del segmento: Set di regole utilizzato per descrivere le caratteristiche o il comportamento chiave di un pubblico target. Una volta concettualizzate, le regole descritte in una definizione di segmento vengono utilizzate per determinare i membri del pubblico qualificati per un segmento.
- **Pubblico**: Il set risultante di profili che soddisfano i criteri di una definizione di segmento.

## Come funziona la segmentazione

La segmentazione è il processo di definizione di attributi o comportamenti specifici condivisi da un sottoinsieme di profili dall’archivio dei profili per distinguere un gruppo commerciabile di persone dalla base dei clienti. Ad esempio, in una campagna e-mail intitolata &quot;Ti sei dimenticato di comprare le scarpe da ginnastica?&quot;, potresti volere un pubblico di tutti gli utenti che hanno cercato di correre scarpe negli ultimi 30 giorni, ma che non hanno completato un acquisto.

Una volta definito concettualmente un segmento, questo viene generato in [!DNL Experience Platform]. In genere, i segmenti sono generati dagli addetti al marketing o dagli specialisti di pubblico, anche se alcune organizzazioni preferiscono essere creati dal loro reparto marketing, in collaborazione con i loro analisti di dati. Dopo aver esaminato i dati inviati a [!DNL Platform], l’analista dei dati compone la definizione del segmento selezionando quali campi e valori verranno utilizzati per creare le regole o le condizioni del segmento. Questa operazione viene eseguita utilizzando l’interfaccia utente o l’API.

## Creare un segmento

I segmenti vengono definiti in ultima analisi utilizzando [!DNL Profile Query Language] (PQL), sia che siano creati utilizzando l’API o utilizzando il tag [!DNL Segment Builder]. In questa sezione viene descritta la definizione del segmento concettuale nel linguaggio creato per recuperare i profili che soddisfano i criteri. Per ulteriori informazioni, consulta la [Panoramica PQL](./pql/overview.md).

Per scoprire come creare e utilizzare i segmenti in [!DNL Segment Builder] (l’implementazione dell’interfaccia utente di [!DNL Segmentation Service]), consulta la [guida al generatore di segmenti](./ui/overview.md).

Per informazioni sulla creazione di definizioni di segmenti utilizzando l&#39;API, consulta l&#39;esercitazione su [creazione di segmenti di pubblico utilizzando l&#39;API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Nel caso in cui uno schema venga esteso, tutti i caricamenti futuri devono aggiornare di conseguenza i campi appena aggiunti. Per ulteriori informazioni sulla personalizzazione di [!DNL Experience Data Model] (XDM), visita il tutorial [Editor di schema](../xdm/tutorials/create-schema-ui.md).

## Valutare i segmenti

Platform supporta attualmente due metodi di valutazione dei segmenti: segmentazione in streaming e segmentazione in batch.

### Segmentazione streaming

La segmentazione in streaming è un processo continuo di selezione dei dati che aggiorna i segmenti in risposta all’attività dell’utente. Una volta generato e salvato un segmento, la definizione del segmento viene applicata ai dati in arrivo a [!DNL Real-time Customer Profile]. Gli aggiornamenti e le rimozioni dei segmenti vengono elaborati regolarmente, garantendo che il pubblico di destinazione rimanga rilevante.

Per ulteriori informazioni sulla segmentazione in streaming, consulta la [documentazione sulla segmentazione in streaming](./api/streaming-segmentation.md).

### Segmentazione in batch

In alternativa a un processo continuo di selezione dei dati, la segmentazione in batch sposta tutti i dati di profilo contemporaneamente attraverso le definizioni dei segmenti per produrre i tipi di pubblico corrispondenti. Una volta creato, questo segmento viene salvato e memorizzato in modo da poterlo esportare per l’uso.

I segmenti valutati utilizzando la segmentazione batch vengono valutati ogni 24 ore. Tuttavia, per i segmenti esistenti, la segmentazione incrementale mantiene i segmenti valutati utilizzando la segmentazione batch freschi per un massimo di un&#39;ora. Eventuali segmenti nuovi o modificati di recente dovranno attendere l’esecuzione del successivo processo di segmentazione batch completa per sfruttare la segmentazione incrementale.

Per scoprire come valutare i segmenti, consulta l’ [esercitazione sulla valutazione dei segmenti](./tutorials/evaluate-a-segment.md).

### Segmentazione degli spigoli

La segmentazione dei bordi è la capacità di valutare istantaneamente i segmenti in Platform sul bordo, abilitando casi d’uso di personalizzazione della pagina e della stessa pagina.

Per ulteriori informazioni sulla segmentazione edge, consulta la [documentazione API](./api/edge-segmentation.md) o la [documentazione dell’interfaccia utente](./ui/edge-segmentation.md).

## Accedere ai risultati della segmentazione

Per informazioni su come accedere a un segmento esportato, consulta l’ [esercitazione sulla valutazione dei segmenti](./tutorials/evaluate-a-segment.md).

## Metadati del segmento

I metadati del segmento facilitano l’indicizzazione nel caso in cui uno qualsiasi dei tuoi segmenti debba essere riutilizzato e/o combinato.

La composizione dei segmenti (tramite l’API o [!DNL Segment Builder]) richiede la definizione di un nome di segmento e di un criterio di unione.

### Nomi dei segmenti

Quando crei un nuovo segmento, devi fornire un nome di segmento. Il nome del segmento viene utilizzato per identificare un particolare segmento tra la raccolta creata da [!DNL Segmentation Service]. I nomi dei segmenti devono quindi essere descrittivi, concisi e univoci.

>[!NOTE]
>
>Quando pianifichi un segmento, ricorda che ai segmenti può essere fatto riferimento da qualsiasi altro segmento e combinato con esso. Quando selezioni un nome, prendi in considerazione la possibilità che il segmento contenga parti riutilizzabili.

### Unisci criteri

I criteri di unione sono regole utilizzate da [!DNL Profile] per determinare come assegnare priorità ai dati e combinarli in una visualizzazione unificata in determinate condizioni.
Se non è definito un criterio di unione, viene utilizzato il criterio di unione predefinito [!DNL Platform]. Se si preferisce utilizzare un criterio di unione specifico per l&#39;organizzazione, è possibile crearne uno personalizzato e contrassegnarlo come predefinito dell&#39;organizzazione.

Ulteriori informazioni sui criteri di unione sono disponibili nella [guida ai criteri di unione](../profile/api/merge-policies.md).

>[!NOTE]
>
>La stima delle dimensioni del pubblico si basa sul criterio di unione profili predefinito dell’organizzazione.

### Altri metadati dei segmenti

Oltre al nome del segmento e ai criteri di unione, [!DNL Segment Builder] offre un campo di metadati aggiuntivo per la &quot;descrizione del segmento&quot; in cui è possibile riepilogare lo scopo della definizione del segmento.

## Funzioni avanzate di segmentazione

I segmenti possono essere configurati per generare continuamente un pubblico combinando [streaming data ingestion](../ingestion/streaming-ingestion/overview.md) con una delle seguenti funzioni avanzate di segmentazione:
- [Segmentazione sequenziale](#sequential)
- [Segmentazione dinamica](#dynamic)
- [Segmentazione su più entità](#multi-entity)

Queste funzioni avanzate sono descritte più dettagliatamente nelle sezioni seguenti.

## Segmentazione sequenziale {#sequential}

Un percorso di utenti standard è sequenziale in natura. Adobe Experience Platform consente di definire una serie ordinata di segmenti per riflettere questo percorso, acquisendo quindi sequenze di eventi man mano che si verificano. Puoi organizzare gli eventi nell’ordine desiderato utilizzando la timeline dell’evento visivo in [!DNL Segment Builder].

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

## Segmentazione multi-entità {#multi-entity}

Con la funzione avanzata di segmentazione multi-entità, puoi estendere i dati [!DNL Real-time Customer Profile] con dati aggiuntivi basati su prodotti, store o altre entità non personali, note anche come entità &quot;dimensione&quot;. Di conseguenza, [!DNL Segmentation Service] può accedere a campi aggiuntivi durante la definizione del segmento come se fossero nativi nell’ archivio dati [!DNL Profile]. La segmentazione su più entità offre flessibilità nell’identificazione dei tipi di pubblico in base ai dati pertinenti alle tue esigenze aziendali specifiche. Per ulteriori informazioni, inclusi casi d&#39;uso e flussi di lavoro, consulta la [guida alla segmentazione su più entità](multi-entity-segmentation.md).

## [!DNL Segmentation Service] tipi di dati

[!DNL Segmentation Service] supporta una varietà di tipi di dati primitivi e complessi. Informazioni dettagliate, incluso un elenco dei tipi di dati supportati, sono disponibili nella [guida sui tipi di dati supportati](./data-types.md).

## Passaggi successivi

[!DNL Segmentation Service] fornisce un flusso di lavoro consolidato per creare segmenti dai  [!DNL Real-time Customer Profile] dati. In sintesi:

- [!DNL Segmentation] è il processo di definizione di un sottoinsieme di profili dall’archivio profili, che ti consente di caratterizzare il comportamento o gli attributi di un gruppo commercializzabile desiderato. [!DNL Segmentation Service] rende possibile questo processo.
- Durante la pianificazione di un segmento, ricorda che un segmento può essere referenziato da qualsiasi altro segmento e combinato con esso.
- Un segmento può essere generato da regole basate sui dati di profilo, sui dati relativi alle serie temporali o su entrambi.
- I segmenti possono essere valutati on-demand o in modo continuo. Quando viene valutato on-demand, tutti i dati di profilo vengono trasmessi attraverso le definizioni dei segmenti contemporaneamente. Quando viene valutato continuamente, i dati scorrono attraverso le definizioni dei segmenti mentre immette [!DNL Platform].

Per scoprire come definire i segmenti nell’interfaccia utente, consulta la [guida al Generatore di segmenti](./ui/overview.md). Per informazioni sulla creazione di definizioni di segmenti utilizzando l&#39;API, consulta l&#39;esercitazione su [creazione di segmenti utilizzando l&#39;API](./tutorials/create-a-segment.md).