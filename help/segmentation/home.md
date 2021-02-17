---
keywords: ' Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Segmento;Segmento;Segmento;Segmenti;Segmenti;Segmenti;segmenti'
solution: Experience Platform
title: Panoramica del servizio di segmentazione
topic: overview
description: Informazioni su Adobe Experience Platform Segmentation Service e sul ruolo che gioca nell'ecosistema della piattaforma.
translation-type: tm+mt
source-git-commit: c0c42f872666323bfb3bdbdf5fb02475d3b5bc79
workflow-type: tm+mt
source-wordcount: '1407'
ht-degree: 0%

---


# [!DNL Segmentation Service]panoramica

Adobe Experience Platform [!DNL Segmentation Service] fornisce un&#39;interfaccia utente e RESTful API che consente di creare segmenti e generare audience dai dati [!DNL Real-time Customer Profile]. Questi segmenti sono configurati e mantenuti a livello centrale su [!DNL Platform] e sono facilmente accessibili da qualsiasi soluzione  Adobe.

Questo documento fornisce una panoramica di [!DNL Segmentation Service] e del ruolo che esso svolge in Adobe Experience Platform.

## Guida introduttiva di [!DNL Segmentation Service]

È importante comprendere i seguenti termini chiave utilizzati in tutto il presente documento:

- **Segmentazione**: Dividere un gruppo di individui di grandi dimensioni (come clienti, potenziali, utenti o organizzazioni) in gruppi più piccoli che condividono caratteristiche simili e risponderanno in modo simile alle strategie di marketing.
- **Definizione** segmento: Set di regole utilizzato per descrivere le caratteristiche o il comportamento chiave di un&#39;audience target. Una volta concettualizzate, le regole delineate in una definizione di segmento vengono utilizzate per determinare i membri di pubblico idonei per un segmento.
- **Pubblico**: Set di profili risultante che soddisfano i criteri di una definizione di segmento.

## Funzionamento della segmentazione

La segmentazione è il processo di definizione di attributi o comportamenti specifici condivisi da un sottoinsieme di profili dall&#39;archivio profili per distinguere un gruppo commerciabile di persone dalla base cliente. Ad esempio, in una campagna e-mail intitolata &quot;Hai dimenticato di comprare le tue scarpe da ginnastica?&quot;, potresti voler avere un pubblico di tutti gli utenti che hanno cercato di correre scarpe negli ultimi 30 giorni, ma che non hanno completato un acquisto.

Una volta concettualmente definito un segmento, questo viene integrato in [!DNL Experience Platform]. In genere, i segmenti sono realizzati dagli esperti di marketing o dagli specialisti di audience, anche se alcune organizzazioni preferiscono essere creati dal loro reparto marketing, in collaborazione con i loro analisti di dati. Dopo aver rivisto i dati inviati a [!DNL Platform], l&#39;analista dei dati compone la definizione del segmento selezionando quali campi e valori verranno utilizzati per creare le regole o le condizioni del segmento. Questa operazione viene eseguita utilizzando l&#39;interfaccia utente o l&#39;API.

## Creare un segmento

Sia che vengano creati utilizzando l&#39;API o utilizzando [!DNL Segment Builder], i segmenti vengono definiti in ultima istanza utilizzando [!DNL Profile Query Language] (PQL). Qui la definizione del segmento concettuale viene descritta nel linguaggio creato per recuperare i profili che soddisfano i criteri. Per ulteriori informazioni, vedere la [panoramica PQL](./pql/overview.md).

Per informazioni su come creare e utilizzare i segmenti in [!DNL Segment Builder] (l&#39;implementazione dell&#39;interfaccia utente di [!DNL Segmentation Service]), consulta la [Guida al Generatore di segmenti](./ui/overview.md).

Per informazioni sulla creazione di definizioni di segmenti mediante l&#39;API, vedete l&#39;esercitazione sulla [creazione di segmenti di pubblico mediante l&#39;API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Nel caso in cui uno schema venga esteso, tutti i caricamenti futuri devono aggiornare di conseguenza i campi aggiunti di recente. Per ulteriori informazioni sulla personalizzazione di [!DNL Experience Data Model] (XDM), fare clic sull&#39;esercitazione [Editor di schema](../xdm/tutorials/create-schema-ui.md).

## Valutazione dei segmenti

Piattaforma supporta attualmente due metodi di valutazione dei segmenti: segmentazione in streaming e segmentazione batch.

### Segmentazione in streaming

La segmentazione in streaming è un processo continuo di selezione dei dati che aggiorna i segmenti in risposta all&#39;attività degli utenti. Una volta creato e salvato un segmento, la definizione del segmento viene applicata rispetto ai dati in arrivo a [!DNL Real-time Customer Profile]. L&#39;aggiunta e l&#39;eliminazione di segmenti vengono elaborati regolarmente, garantendo che il pubblico di destinazione rimanga rilevante.

Per ulteriori informazioni sulla segmentazione in streaming, consulta la [documentazione sulla segmentazione in streaming](./api/streaming-segmentation.md).

### Segmentazione batch

In alternativa a un processo continuo di selezione dei dati, la segmentazione in batch sposta tutti i dati di profilo contemporaneamente attraverso le definizioni dei segmenti per produrre i tipi di pubblico corrispondenti. Una volta creato, questo segmento viene salvato e memorizzato in modo da poterlo esportare per l’uso.

Per informazioni su come valutare i segmenti, consulta l&#39; [tutorial sulla valutazione dei segmenti](./tutorials/evaluate-a-segment.md).

## Accesso ai risultati della segmentazione

Per informazioni su come accedere a un segmento esportato, consulta l&#39; [esercitazione sulla valutazione dei segmenti](./tutorials/evaluate-a-segment.md).

## Metadati segmento

I metadati dei segmenti facilitano l’indicizzazione nel caso in cui uno dei segmenti venga riutilizzato e/o combinato.

Per comporre i segmenti (tramite API o [!DNL Segment Builder]) è necessario definire un nome di segmento e un criterio di unione.

### Nomi dei segmenti

Quando crei un nuovo segmento, devi fornire un nome di segmento. Il nome del segmento viene utilizzato per identificare un particolare segmento tra la raccolta creata da [!DNL Segmentation Service]. I nomi dei segmenti devono pertanto essere descrittivi, concisi e univoci.

>[!NOTE]
>
>Durante la pianificazione di un segmento, tieni presente che ai segmenti è possibile fare riferimento da qualsiasi altro segmento e che questi possono essere combinati con esso. Quando selezioni un nome, prendi in considerazione la possibilità che il segmento contenga porzioni riutilizzabili.

### Unisci criteri

I criteri di unione sono regole utilizzate da [!DNL Profile] per determinare in che modo i dati verranno classificati in ordine di priorità e combinati in una visualizzazione unificata a determinate condizioni.
Se non è definito alcun criterio di unione, viene utilizzato il criterio di unione predefinito [!DNL Platform]. Se preferite utilizzare un criterio di unione specifico per l&#39;organizzazione, potete crearne uno personalizzato e contrassegnarlo come predefinito dell&#39;organizzazione.

Ulteriori informazioni sui criteri di unione sono disponibili nella [guida ai criteri di unione](../profile/api/merge-policies.md).

>[!NOTE]
>
>La stima delle dimensioni del pubblico si basa sui criteri di unione dei profili predefiniti dell&#39;organizzazione.

### Altri metadati di segmento

Oltre al nome del segmento e ai criteri di unione, [!DNL Segment Builder] offre anche un campo di metadati &quot;descrizione del segmento&quot; in cui potete riepilogare lo scopo della definizione del segmento.

## Funzioni avanzate di segmentazione

I segmenti possono essere configurati per generare continuamente un pubblico combinando [l&#39;inserimento dei dati di streaming](../ingestion/streaming-ingestion/overview.md) con una delle seguenti funzioni di segmentazione avanzate:
- [Segmentazione sequenziale](#sequential)
- [Segmentazione dinamica](#dynamic)
- [Segmentazione multi-entità](#multi-entity)

Queste funzioni avanzate sono descritte più dettagliatamente nelle sezioni seguenti.

## Segmentazione sequenziale {#sequential}

Un percorso di utenti standard è sequenziale. Adobe Experience Platform consente di definire una serie ordinata di segmenti in base a questo percorso, acquisendo così le sequenze di eventi man mano che si verificano. È possibile organizzare gli eventi nell&#39;ordine desiderato utilizzando la timeline dell&#39;evento visivo in [!DNL Segment Builder].

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

Grazie alla funzionalità di segmentazione multi-entità avanzata, è possibile estendere i dati [!DNL Real-time Customer Profile] con dati aggiuntivi basati su prodotti, store o altre entità non associate, note anche come entità &quot;dimensione&quot;. Di conseguenza, [!DNL Segmentation Service] può accedere a campi aggiuntivi durante la definizione del segmento, come se fossero nativi dell&#39;archivio dati [!DNL Profile]. La segmentazione multi-entità offre flessibilità nell&#39;identificazione delle audience in base ai dati pertinenti alle esigenze aziendali specifiche. Per ulteriori informazioni, compresi i casi di utilizzo e i flussi di lavoro, fare riferimento alla [guida alla segmentazione multi-entità](multi-entity-segmentation.md).

## [!DNL Segmentation Service] tipi di dati

[!DNL Segmentation Service] supporta una serie di tipi di dati primitivi e complessi. Informazioni dettagliate, incluso un elenco dei tipi di dati supportati, sono disponibili nella guida [ai tipi di dati supportati](./data-types.md).

## Passaggi successivi

[!DNL Segmentation Service] fornisce un flusso di lavoro consolidato per creare segmenti dai  [!DNL Real-time Customer Profile] dati. In sintesi:

- [!DNL Segmentation] è il processo di definizione di un sottoinsieme di profili dall&#39;archivio profili, che consente di caratterizzare il comportamento o gli attributi di un gruppo commerciabile desiderato. [!DNL Segmentation Service] rende possibile questo processo.
- Durante la pianificazione di un segmento, tenere presente che a un segmento può essere fatto riferimento e combinato con qualsiasi altro segmento.
- Un segmento può essere generato da regole basate sui dati del profilo, sui dati delle serie temporali correlati o su entrambi.
- I segmenti possono essere valutati su richiesta o in modo continuo. Quando viene valutato su richiesta, tutti i dati del profilo vengono passati attraverso le definizioni del segmento alla volta. Quando viene valutato in modo continuo, i dati scorrono le definizioni dei segmenti mentre entrano in [!DNL Platform].

Per informazioni su come definire i segmenti nell&#39;interfaccia utente, consulta la guida [Segment Builder guide](./ui/overview.md). Per informazioni sulla creazione di definizioni di segmenti mediante l&#39;API, vedete l&#39;esercitazione sulla [creazione di segmenti mediante l&#39;API](./tutorials/create-a-segment.md).