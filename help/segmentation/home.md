---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment service;segment;Segment;Segments;segments
solution: Experience Platform
title: Servizio di segmentazione Adobe Experience Platform
topic: overview
description: Questo documento fornisce una panoramica del servizio di segmentazione e del ruolo che esso svolge in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 5dd07bf9afe96be3a4c3f4a4d4e3b23aef4fde70
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 0%

---


# Adobe Experience Platform [!DNL Segmentation Service] overview

Adobe Experience Platform [!DNL Segmentation Service] fornisce un&#39;interfaccia utente e RESTful API che consente di creare segmenti e generare audience dai [!DNL Real-time Customer Profile] dati. Questi segmenti sono configurati e mantenuti a livello centrale [!DNL Platform]e sono facilmente accessibili da qualsiasi soluzione  Adobe.

Questo documento fornisce una panoramica [!DNL Segmentation Service] e il ruolo che esso svolge in Adobe Experience Platform.

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

Per informazioni su come creare e utilizzare i segmenti in [!DNL Segment Builder] (l’implementazione dell’interfaccia utente di [!DNL Segmentation Service]), consulta la guida [di](./ui/overview.md)Segment Builder (Generatore di segmenti).

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

Un percorso standard dell&#39;utente è sequenziale. Adobe Experience Platform consente di definire una serie ordinata di segmenti per riflettere questo percorso, acquisendo così le sequenze di eventi man mano che si verificano. Potete organizzare gli eventi nell&#39;ordine desiderato utilizzando la timeline dell&#39;evento visivo nella [!DNL Segment Builder].

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

Grazie alla funzionalità di segmentazione multi-entità avanzata, è possibile estendere [!DNL Real-time Customer Profile] i dati con dati aggiuntivi basati su prodotti, store o altre entità non associate, note anche come entità &quot;dimensione&quot;. Di conseguenza, [!DNL Segmentation Service] è possibile accedere a campi aggiuntivi durante la definizione del segmento, come se fossero nativi dell&#39;archivio [!DNL Profile] dati. La segmentazione multi-entità offre flessibilità nell&#39;identificazione delle audience in base ai dati pertinenti alle esigenze aziendali specifiche. Per ulteriori informazioni, compresi i casi di utilizzo e i flussi di lavoro, consultate la guida [alla segmentazione per](multi-entity-segmentation.md)più entità.

## [!DNL Segmentation Service] tipi di dati

[!DNL Segmentation Service] supporta una serie di tipi di dati primitivi e complessi. Informazioni dettagliate, incluso un elenco dei tipi di dati supportati, sono disponibili nella guida [ai tipi di dati](./data-types.md)supportati.

## Passaggi successivi

[!DNL Segmentation Service] fornisce un flusso di lavoro consolidato per creare segmenti dai [!DNL Real-time Customer Profile] dati. In sintesi:

- [!DNL Segmentation] è il processo di definizione di un sottoinsieme di profili dall&#39;archivio profili, che consente di caratterizzare il comportamento o gli attributi di un gruppo commerciabile desiderato. [!DNL Segmentation Service] rende possibile questo processo.
- Durante la pianificazione di un segmento, tenere presente che a un segmento può essere fatto riferimento e combinato con qualsiasi altro segmento.
- Un segmento può essere generato da regole basate sui dati del profilo, sui dati delle serie temporali correlati o su entrambi.
- I segmenti possono essere valutati su richiesta o in modo continuo. Quando viene valutato su richiesta, tutti i dati del profilo vengono passati attraverso le definizioni del segmento alla volta. Quando viene valutato in modo continuo, i dati scorrono le definizioni dei segmenti man mano che entrano [!DNL Platform].

Per informazioni su come definire i segmenti nell’interfaccia utente, consulta la guida [di Generatore di](./ui/overview.md)segmenti. Per informazioni sulla creazione di definizioni di segmenti tramite l&#39;API, consulta l&#39;esercitazione sulla [creazione di segmenti tramite l&#39;API](./tutorials/create-a-segment.md).