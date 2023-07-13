---
solution: Experience Platform
title: Panoramica del servizio di segmentazione
description: Scopri il servizio di segmentazione di Adobe Experience Platform e il ruolo che svolge nell’ecosistema della piattaforma.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '1629'
ht-degree: 11%

---

# Panoramica di [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] fornisce un’interfaccia utente e un’API RESTful che consente di creare tipi di pubblico tramite le definizioni dei segmenti o altre origini dal tuo [!DNL Real-Time Customer Profile] dati. Questi tipi di pubblico sono configurati e gestiti centralmente su [!DNL Platform]e sono facilmente accessibili da qualsiasi soluzione Adobe.

Questo documento fornisce una panoramica di [!DNL Segmentation Service] e il ruolo che riveste in Adobe Experience Platform.

## Guida introduttiva a [!DNL Segmentation Service]

Devi comprendere i seguenti termini chiave usati in questo documento:

- **Segmentazione**: dividendo un ampio gruppo di individui (come clienti, potenziali clienti, utenti o organizzazioni) in gruppi più piccoli che condividono caratteristiche simili e risponderanno in modo simile alle strategie di marketing.
- **Pubblico**: una raccolta di persone che condividono comportamenti e/o caratteristiche simili. Questa raccolta di persone può essere generata da Adobe Experience Platform utilizzando le definizioni dei segmenti (pubblico generato da Platform) o da fonti esterne (pubblico generato esternamente).
- **Definizione del segmento**: set di regole utilizzato da Adobe Experience Platform per descrivere le caratteristiche o il comportamento chiave di un pubblico target.

## Come funziona la segmentazione

La segmentazione è il processo di definizione di attributi o comportamenti specifici condivisi da un sottoinsieme di profili dall’archivio dei profili, per distinguere un gruppo commerciabile di persone dalla base dei clienti. Ad esempio, in una campagna e-mail denominata &quot;Hai dimenticato di acquistare le tue scarpe da ginnastica?&quot;, potresti desiderare un pubblico di tutti gli utenti che hanno cercato scarpe da corsa negli ultimi 30 giorni, ma che non hanno completato un acquisto.

Una volta definito concettualmente un segmento, questo viene incorporato [!DNL Experience Platform]. In genere, i segmenti vengono creati dall’addetto al marketing o dallo specialista del pubblico, anche se alcune organizzazioni preferiscono che vengano creati dal proprio reparto di marketing, in collaborazione con i propri analisti di dati. Dopo aver esaminato i dati inviati a [!DNL Platform]L’analista dati compone la definizione del segmento selezionando i campi e i valori da utilizzare per creare le regole o le condizioni del segmento. Questa operazione viene eseguita utilizzando l’interfaccia o l’API.

## Creare segmenti

Se viene creato utilizzando l&#39;API o utilizzando [!DNL Segment Builder], i segmenti vengono in ultima analisi definiti utilizzando [!DNL Profile Query Language] (PQL) Qui viene descritta la definizione del segmento concettuale nel linguaggio generato per recuperare i profili che soddisfano i criteri. Per ulteriori informazioni, vedere [Panoramica di PQL](./pql/overview.md).

Per scoprire come creare e utilizzare i segmenti in [!DNL Segment Builder] (implementazione dell’interfaccia utente di [!DNL Segmentation Service]), vedere la [Guida al Generatore di segmenti](./ui/overview.md).

Per informazioni sulla creazione di definizioni dei segmenti utilizzando l’API, consulta l’esercitazione su [creazione di segmenti di pubblico tramite l’API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Se uno schema viene esteso, tutti i caricamenti futuri devono aggiornare di conseguenza i campi appena aggiunti. Per ulteriori informazioni sulla personalizzazione [!DNL Experience Data Model] (XDM), visita il [Esercitazione sull’editor di schemi](../xdm/tutorials/create-schema-ui.md).
>
>Inoltre, se nel set di dati è abilitato un valore di scadenza dell’evento esperienza, questo potrebbe influire sull’appartenenza del segmento creato. Leggere la guida su [Scadenze degli eventi esperienza](../profile/event-expirations.md) per ulteriori informazioni su come questa funzione può influenzare la segmentazione.

## Valutare segmenti {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="Metodi di valutazione"
>abstract="Platform supporta attualmente tre metodi di valutazione dei segmenti: segmentazione in streaming, segmentazione in batch e segmentazione Edge."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="Valutazione in streaming"
>abstract="La segmentazione in streaming è un processo continuo di selezione dei dati che aggiorna i segmenti in risposta all’attività dell’utente."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=it" text="Valutare gli eventi in tempo quasi reale con la segmentazione in streaming"

Platform supporta attualmente tre metodi di valutazione dei segmenti: segmentazione in streaming, segmentazione in batch e segmentazione Edge.

### Segmentazione in streaming {#streaming}

La segmentazione in streaming è un processo continuo di selezione dei dati che aggiorna i segmenti in risposta all’attività dell’utente. Una volta creato e salvato un segmento, la definizione del segmento viene applicata ai dati in arrivo in [!DNL Real-Time Customer Profile]. Le aggiunte e le rimozioni dei segmenti vengono elaborate regolarmente, garantendo la rilevanza del pubblico di destinazione.

Per ulteriori informazioni sulla segmentazione in streaming, consulta [documentazione sulla segmentazione in streaming](./api/streaming-segmentation.md).

### Segmentazione batch {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Valutazione in batch"
>abstract="In alternativa a un processo continuo di selezione dei dati, con la segmentazione in batch tutti i dati di profilo vengono valutati allo stesso tempo secondo le definizioni dei segmenti per produrre i segmenti di pubblico corrispondenti. Una volta creato, il segmento viene salvato e memorizzato, e potrai quindi esportarlo."

In alternativa a un processo continuo di selezione dei dati, con la segmentazione in batch tutti i dati di profilo vengono valutati allo stesso tempo secondo le definizioni dei segmenti per produrre i segmenti di pubblico corrispondenti. Una volta creato, il segmento viene salvato e memorizzato in modo da poterlo esportare per l’utilizzo.

I segmenti batch vengono valutati automaticamente ogni 24 ore. Se si desidera valutare un segmento batch su richiesta, è possibile utilizzare un processo di segmentazione. Per ulteriori informazioni sui processi di segmentazione, leggi [documentazione sui processi di segmentazione](./api/segment-jobs.md).

### Segmentazione Edge {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Valutazione Edge"
>abstract="La segmentazione Edge è la capacità di valutare all’istante i segmenti in Platform su Experience Edge, per casi d’uso di personalizzazione sulla stessa pagina e sulla pagina successiva."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=it" text="Guida all’interfaccia utente per la segmentazione Edge"

La segmentazione Edge consente di valutare i segmenti in Platform istantaneamente [su Experience Edge](../edge/home.md), abilitazione dei casi d’uso di personalizzazione della stessa pagina e della pagina successiva.

Per ulteriori informazioni sulla segmentazione Edge, leggi la sezione [Documentazione API](./api/edge-segmentation.md) o [Documentazione dell’interfaccia utente](./ui/edge-segmentation.md).

## Accedere ai risultati della segmentazione

Per informazioni su come accedere a un segmento esportato, consulta [tutorial sulla valutazione dei segmenti](./tutorials/evaluate-a-segment.md).

## Metadati del segmento

I metadati dei segmenti facilitano l’indicizzazione nel caso in cui uno qualsiasi dei segmenti debba essere riutilizzato e/o combinato.

Composizione dei segmenti (tramite l’API o [!DNL Segment Builder]) richiede di definire un nome di segmento e un criterio di unione.

### Nomi di segmenti

Quando crei un nuovo segmento, devi fornire un nome per il segmento. Il nome del segmento viene utilizzato per identificare un particolare segmento nella raccolta generata da [!DNL Segmentation Service]. I nomi dei segmenti devono quindi essere descrittivi, concisi e univoci.

>[!NOTE]
>
>Quando pianifichi un segmento, ricorda che è possibile fare riferimento ai segmenti da qualsiasi altro segmento e combinarli con essi. Quando selezioni un nome, considera la possibilità che il segmento contenga parti riutilizzabili.

### Criteri di unione

I criteri di unione sono regole utilizzate da [!DNL Profile] determinare in che modo i dati avranno priorità e verranno combinati in una vista unificata in determinate condizioni.
Se non è stato definito un criterio di unione, verrà utilizzato il valore predefinito [!DNL Platform] criterio di unione utilizzato. Se preferisci utilizzare un criterio di unione specifico per la tua organizzazione, puoi crearne uno personalizzato e contrassegnarlo come predefinito della tua organizzazione.

Ulteriori informazioni sui criteri di unione sono disponibili nella sezione [guida ai criteri di unione](../profile/api/merge-policies.md).

>[!NOTE]
>
>La stima delle dimensioni del pubblico si basa sul criterio di unione profili predefinito dell’organizzazione.

### Altri metadati di segmenti

Oltre al nome del segmento e al criterio di unione, [!DNL Segment Builder] ti offre un ulteriore campo di metadati &quot;descrizione del segmento&quot; in cui puoi riepilogare lo scopo della definizione del segmento.

## Funzioni di segmentazione avanzate

I segmenti possono essere configurati per generare continuamente un pubblico combinando [acquisizione di dati in streaming](../ingestion/streaming-ingestion/overview.md) con una delle seguenti funzioni di segmentazione avanzate:
- [Segmentazione sequenziale](#sequential)
- [Segmentazione dinamica](#dynamic)
- [Segmentazione di più entità](#multi-entity)

Queste feature avanzate vengono descritte più dettagliatamente nelle sezioni seguenti.

## Segmentazione sequenziale {#sequential}

Un percorso di utenti standard ha natura sequenziale. Adobe Experience Platform consente di definire una serie ordinata di segmenti per riflettere questo percorso, quindi di acquisire sequenze di eventi nel momento in cui si verificano. È possibile disporre gli eventi nell&#39;ordine desiderato utilizzando la timeline degli eventi visivi nella [!DNL Segment Builder].

Un esempio di percorso di clienti che richiederebbe una segmentazione sequenziale è product view > product add > checkout > No purchase (Visualizzazione prodotto > Aggiunta prodotto > Pagamento > Nessun acquisto).

## Segmentazione dinamica {#dynamic}

La segmentazione dinamica risolve i problemi di scalabilità che gli addetti al marketing devono tradizionalmente affrontare durante la creazione di segmenti per le campagne di marketing.

A differenza della segmentazione statica che richiede di acquisire in modo esplicito e ripetuto ogni caso d’uso possibile, la segmentazione dinamica utilizza le variabili per generare la logica della regola e le relazioni di espressione dinamiche.

### Caso d’uso: ricerca di clienti che effettuano acquisti al di fuori del proprio Stato membro d’origine

Per illustrare il valore di questa funzione di segmentazione avanzata, considera la collaborazione di un architetto di dati con un addetto al marketing per identificare i clienti che hanno effettuato acquisti al di fuori del proprio stato nazionale.

**Il problema**

La segmentazione statica richiede di definire singoli segmenti con un attributo univoco dello stato predefinito, prima di filtrare gli eventi di acquisto che non sono uguali allo stato predefinito. Un segmento esplicito di questo tipo recitava &quot;Sto cercando persone dello Utah in cui lo stato del loro acquisto non è lo Utah&quot;. Per creare un pubblico utilizzando questo metodo devi definire un segmento per ogni stato degli Stati Uniti, per un totale di 50 segmenti.

A causa delle diverse combinazioni di segmenti che inevitabilmente si presentano con la scalabilità, il processo manuale richiesto per la segmentazione statica diventa più dispendioso in termini di tempo, riducendo l’efficienza complessiva.

**La soluzione**

Assegnando una variabile all’attributo stato acquisto, il segmento dinamico si semplifica in modo da &quot;trovarmi un acquisto in cui lo stato di tale acquisto non è uguale allo stato iniziale del cliente&quot;. In questo modo puoi consolidare 50 segmenti statici in un singolo segmento dinamico.

## Segmentazione di più entità {#multi-entity}

Con la funzione di segmentazione avanzata con più entità, puoi estendere [!DNL Real-Time Customer Profile] dati con dati aggiuntivi basati su prodotti, archivi o altre entità non personali, noti anche come entità &quot;dimensionali&quot;. Di conseguenza, [!DNL Segmentation Service] può accedere a campi aggiuntivi durante la definizione del segmento come se fossero nativi per [!DNL Profile] archivio dati. La segmentazione multi-entità offre flessibilità per identificare i tipi di pubblico in base ai dati pertinenti per le tue esigenze aziendali specifiche. Per ulteriori informazioni, inclusi casi d’uso e flussi di lavoro, consulta [guida alla segmentazione di più entità](multi-entity-segmentation.md).

## [!DNL Segmentation Service] tipi di dati

[!DNL Segmentation Service] supporta diversi tipi di dati primitivi e complessi. Informazioni dettagliate, compreso un elenco dei tipi di dati supportati, sono disponibili nella [guida ai tipi di dati supportati](./data-types.md).

## Passaggi successivi

[!DNL Segmentation Service] fornisce un flusso di lavoro consolidato da cui creare segmenti [!DNL Real-Time Customer Profile] dati. In sintesi:

- [!DNL Segmentation] è il processo di definizione di un sottoinsieme di profili dall’archivio profili, che consente di caratterizzare il comportamento o gli attributi di un gruppo commerciabile desiderato. [!DNL Segmentation Service] rende possibile questo processo.
- Quando pianifichi un segmento, ricorda che è possibile fare riferimento a un segmento da qualsiasi altro segmento e combinarlo con esso.
- Un segmento può essere creato da regole basate su dati di profilo, dati di serie temporali correlate o entrambi.
- I segmenti possono essere valutati su richiesta o in modo continuo. Quando vengono valutati su richiesta, tutti i dati di profilo vengono trasmessi attraverso le definizioni dei segmenti contemporaneamente. Quando vengono valutati in modo continuo, i dati vengono trasmessi attraverso le definizioni dei segmenti mentre entrano [!DNL Platform].

Per informazioni su come definire i segmenti nell’interfaccia utente, consulta [Guida al Generatore di segmenti](./ui/overview.md). Per informazioni sulla creazione di definizioni dei segmenti utilizzando l’API, consulta l’esercitazione su [creazione di segmenti tramite l’API](./tutorials/create-a-segment.md).
