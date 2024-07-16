---
solution: Experience Platform
title: Panoramica del servizio di segmentazione
description: Scopri il servizio di segmentazione di Adobe Experience Platform e il ruolo che svolge nell’ecosistema della piattaforma.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 12%

---

# Panoramica di [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] fornisce un&#39;interfaccia utente e un&#39;API RESTful che consentono di creare tipi di pubblico tramite definizioni di segmenti o altre origini dai dati di [!DNL Real-Time Customer Profile]. Questi tipi di pubblico sono configurati e gestiti centralmente in [!DNL Platform] e sono facilmente accessibili da qualsiasi soluzione Adobe.

Questo documento fornisce una panoramica di [!DNL Segmentation Service] e del ruolo che svolge in Adobe Experience Platform.

## Guida introduttiva a [!DNL Segmentation Service]

Devi comprendere i seguenti termini chiave usati in questo documento:

- **Pubblico**: un insieme di persone che condividono comportamenti e/o caratteristiche simili. Questa raccolta di persone può essere generata da Adobe Experience Platform utilizzando le definizioni dei segmenti (pubblico generato da Platform) o da fonti esterne (pubblico generato esternamente).
- **Definizione del segmento**: il set di regole utilizzato da Adobe Experience Platform per descrivere le caratteristiche o il comportamento chiave di un pubblico di destinazione.
- **Segmento**: azione di separazione dei profili in tipi di pubblico.

## Come funziona la segmentazione

La segmentazione è il processo di definizione di attributi o comportamenti specifici condivisi da un sottoinsieme di profili dall’archivio Profili per distinguere un gruppo commerciabile di persone dalla base clienti. Ad esempio, in una campagna e-mail denominata &quot;Hai dimenticato di acquistare le tue scarpe da ginnastica?&quot;, potresti desiderare un pubblico di tutti gli utenti che hanno cercato scarpe da corsa negli ultimi 30 giorni, ma che non hanno completato un acquisto.

Una volta definito concettualmente un pubblico, questo viene generato in [!DNL Experience Platform]. In genere, i tipi di pubblico vengono creati dall’addetto al marketing o dallo specialista del pubblico, anche se alcune organizzazioni preferiscono che vengano creati dal proprio reparto di marketing, in collaborazione con i propri analisti di dati. Dopo aver esaminato i dati inviati a [!DNL Platform], l&#39;analista dati può creare il pubblico in due modi: creando una definizione di segmento selezionando i campi e i valori da utilizzare per creare le regole o le condizioni del pubblico oppure componendo un pubblico utilizzando la Composizione pubblico.

## Creare tipi di pubblico

I tipi di pubblico possono essere creati in due modi diversi su Adobe Experience Platform: direttamente composti come tipi di pubblico o tramite definizioni di segmenti derivate da Platform.

### Composizione del pubblico

Quando componi direttamente un pubblico su Platform, puoi utilizzare la Composizione del pubblico. Per informazioni su come utilizzare la composizione del pubblico per creare un pubblico, consulta la [guida alla composizione del pubblico](./ui/audience-composition.md) per ulteriori informazioni.

### Definizioni dei segmenti

Sia che vengano create utilizzando l&#39;API che utilizzando [!DNL Segment Builder], le definizioni dei segmenti vengono in ultima analisi definite utilizzando [!DNL Profile Query Language] (PQL). Qui viene descritta la definizione del segmento concettuale nel linguaggio generato per recuperare i profili che soddisfano i criteri. Per ulteriori informazioni, vedere [Panoramica di PQL](./pql/overview.md).

Per informazioni su come creare e utilizzare i segmenti in [!DNL Segment Builder] (implementazione dell&#39;interfaccia utente di [!DNL Segmentation Service]), consulta la [guida per il Generatore di segmenti](./ui/segment-builder.md).

Per informazioni sulla creazione di definizioni di segmenti utilizzando l&#39;API, consulta l&#39;esercitazione sulla [creazione di definizioni di segmenti utilizzando l&#39;API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Se uno schema viene esteso, tutti i caricamenti futuri devono aggiornare di conseguenza i campi appena aggiunti. Per ulteriori informazioni sulla personalizzazione di [!DNL Experience Data Model] (XDM), visitare l&#39;esercitazione [Editor schema](../xdm/tutorials/create-schema-ui.md).
>
>Inoltre, se nel set di dati è abilitato un valore di scadenza di evento esperienza, questo potrebbe influire sull’appartenenza della definizione di segmento creata. Per ulteriori informazioni su come questa funzione può influenzare la segmentazione, consulta la guida in [Scadenze evento esperienza](../profile/event-expirations.md).

## Valutare i tipi di pubblico {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="Metodi di valutazione"
>abstract="Platform supporta attualmente tre metodi di valutazione dei tipi di pubblico: segmentazione in streaming, segmentazione in batch e segmentazione Edge."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="Valutazione in streaming"
>abstract="La segmentazione in streaming è un processo continuo di selezione di dati che aggiorna i tipi di pubblico in risposta all’attività dell’utente."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=it" text="Valutare gli eventi in tempo quasi reale con la segmentazione in streaming"

Platform supporta attualmente tre metodi di valutazione dei tipi di pubblico: segmentazione in streaming, segmentazione in batch e segmentazione Edge.

### Segmentazione in streaming {#streaming}

La segmentazione in streaming è un processo continuo di selezione di dati che aggiorna i tipi di pubblico in risposta all’attività dell’utente. Una volta creato e salvato un pubblico, la definizione del segmento viene applicata ai dati in arrivo in [!DNL Real-Time Customer Profile]. Le aggiunte e le rimozioni al pubblico vengono elaborate regolarmente, in modo da garantire che il pubblico di destinazione rimanga pertinente.

Per ulteriori informazioni sulla segmentazione streaming, consulta la [documentazione sulla segmentazione streaming](./api/streaming-segmentation.md).

### Segmentazione in batch {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Valutazione in batch"
>abstract="In alternativa a un processo continuo di selezione dei dati, con la segmentazione in batch tutti i dati di profilo vengono valutati allo stesso tempo secondo le definizioni dei segmenti per produrre i segmenti di pubblico corrispondenti. Una volta creato, il pubblico viene salvato e memorizzato, in modo che tu possa esportarlo per l’uso."

In alternativa a un processo continuo di selezione dei dati, con la segmentazione in batch tutti i dati di profilo vengono valutati allo stesso tempo secondo le definizioni dei segmenti per produrre i segmenti di pubblico corrispondenti. Una volta creato, il pubblico risultante viene salvato e memorizzato in modo da poterlo esportare per l’utilizzo.

I tipi di pubblico in batch vengono valutati automaticamente ogni 24 ore. Se desideri valutare un pubblico batch su richiesta, puoi utilizzare un processo di segmentazione. Per ulteriori informazioni sui processi di segmentazione, consulta la [documentazione sui processi di segmentazione](./api/segment-jobs.md).

### Segmentazione Edge {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Valutazione Edge"
>abstract="La segmentazione Edge è la capacità di valutare all’istante i segmenti in Platform sulla reta Edge, per casi d’uso di personalizzazione sulla stessa pagina e sulla pagina successiva."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=it" text="Guida all’interfaccia utente per la segmentazione Edge"

La segmentazione di Edge consente di valutare i segmenti in Platform [ istantaneamente nell’Edge Network](../web-sdk/home.md), abilitando casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva.

Per ulteriori informazioni sulla segmentazione Edge, consulta la [documentazione API](./api/edge-segmentation.md) o la [documentazione interfaccia utente](./ui/edge-segmentation.md).

## Accedere ai risultati della segmentazione

Per informazioni su come accedere a un pubblico esportato, consulta l&#39;esercitazione sulla valutazione della definizione del segmento [](./tutorials/evaluate-a-segment.md).

## Metadati di definizione del segmento

I metadati di definizione del segmento facilitano l’indicizzazione nel caso in cui un pubblico debba essere riutilizzato e/o combinato.

Per comporre una definizione di segmento (tramite l&#39;API o [!DNL Segment Builder]) è necessario definire un nome e un criterio di unione.

### Nomi di definizione del segmento

Quando crei una nuova definizione di segmento, devi fornire un nome. Il nome della definizione del segmento viene utilizzato per identificare una particolare definizione di segmento nella raccolta generata da [!DNL Segmentation Service]. I nomi delle definizioni dei segmenti devono quindi essere descrittivi, concisi e univoci.

>[!NOTE]
>
>Quando pianifichi una definizione di segmento, ricorda che è possibile fare riferimento alle definizioni di segmento da qualsiasi altra definizione di segmento e combinarle con esse. Quando selezioni un nome, considera la possibilità che la definizione del segmento possa contenere parti riutilizzabili.

### Criteri di unione

I criteri di unione sono regole utilizzate da [!DNL Profile] per determinare come assegnare la priorità ai dati e combinarli in una visualizzazione unificata in determinate condizioni.

Se non è definito alcun criterio di unione, verrà utilizzato il criterio di unione predefinito [!DNL Platform]. Se preferisci utilizzare un criterio di unione specifico per la tua organizzazione, puoi crearne uno personalizzato e contrassegnarlo come predefinito della tua organizzazione.

Ulteriori informazioni sui criteri di unione sono disponibili nella [guida dei criteri di unione](../profile/api/merge-policies.md).

>[!NOTE]
>
>La stima delle dimensioni del pubblico si basa sul criterio di unione profili predefinito dell’organizzazione.

### Metadati di definizione di altri segmenti

Oltre al nome e al criterio di unione, [!DNL Segment Builder] offre un campo di metadati di descrizione aggiuntivo in cui è possibile riepilogare lo scopo della definizione del segmento.

## Funzioni di segmentazione avanzate

Le definizioni dei segmenti possono essere configurate in modo da generare continuamente un pubblico combinando [l&#39;acquisizione di dati in streaming](../ingestion/streaming-ingestion/overview.md) con una delle seguenti funzioni di segmentazione avanzate:
- [Segmentazione sequenziale](#sequential)
- [Segmentazione dinamica](#dynamic)
- [Segmentazione di più entità](#multi-entity)

Queste feature avanzate vengono descritte più dettagliatamente nelle sezioni seguenti.

### Segmentazione sequenziale {#sequential}

Un percorso di utenti standard ha natura sequenziale. Adobe Experience Platform consente di definire una serie ordinata di tipi di pubblico per riflettere questo percorso, quindi di acquisire sequenze di eventi nel momento in cui si verificano. È possibile disporre gli eventi nell&#39;ordine desiderato utilizzando la sequenza temporale degli eventi visivi in [!DNL Segment Builder].

Un esempio di percorso di clienti che richiederebbe una segmentazione sequenziale è product view > product add > checkout > No purchase (Visualizzazione prodotto > Aggiunta prodotto > Pagamento > Nessun acquisto).

### Segmentazione dinamica {#dynamic}

La segmentazione dinamica risolve i problemi di scalabilità che gli addetti al marketing devono tradizionalmente affrontare durante la creazione di tipi di pubblico per le campagne di marketing.

A differenza della segmentazione statica che richiede di acquisire in modo esplicito e ripetuto ogni caso d’uso possibile, la segmentazione dinamica utilizza le variabili per generare la logica della regola e le relazioni di espressione dinamiche.

Per illustrare il valore di questa funzione di segmentazione avanzata, considera la collaborazione di un architetto di dati con un addetto al marketing per identificare i clienti che hanno effettuato acquisti al di fuori del proprio stato.

La segmentazione statica richiede di definire singoli segmenti con un attributo univoco dello stato predefinito, prima di filtrare gli eventi di acquisto che non sono uguali allo stato predefinito. Una definizione esplicita di questo tipo di segmento sarebbe &quot;Sto cercando persone dallo Utah dove lo stato del loro acquisto non è lo Utah&quot;. Per creare un pubblico utilizzando questo metodo devi definire un segmento per ogni stato degli Stati Uniti, per un totale di 50 segmenti.

A causa delle diverse combinazioni di definizione dei segmenti che inevitabilmente si presentano con la scalabilità, il processo manuale richiesto per la segmentazione statica diventa più dispendioso in termini di tempo, riducendo l’efficienza complessiva.

Assegnando una variabile all’attributo &quot;purchase state&quot;, la definizione del segmento dinamico si semplifica in quanto &quot;trova un acquisto il cui stato non è uguale a quello dell’abitazione del cliente&quot;. In questo modo è possibile consolidare 50 segmenti statici in una singola definizione di segmento dinamico.

### Segmentazione di più entità {#multi-entity}

Con la funzione di segmentazione avanzata di più entità, è possibile estendere i dati di [!DNL Real-Time Customer Profile] con dati aggiuntivi basati su prodotti, archivi o altre entità non personali, note anche come entità &quot;dimensionali&quot;. Di conseguenza, [!DNL Segmentation Service] può accedere a campi aggiuntivi durante la definizione del segmento come se fossero nativi dell&#39;archivio dati [!DNL Profile]. La segmentazione multi-entità offre flessibilità per identificare i tipi di pubblico in base ai dati pertinenti per le tue esigenze aziendali specifiche. Per ulteriori informazioni, inclusi casi d&#39;uso e flussi di lavoro, consulta la [guida alla segmentazione di più entità](multi-entity-segmentation.md).

## [!DNL Segmentation Service] tipi di dati

[!DNL Segmentation Service] supporta diversi tipi di dati primitivi e complessi. Informazioni dettagliate, incluso un elenco dei tipi di dati supportati, sono disponibili nella [guida dei tipi di dati supportati](./data-types.md).

## Passaggi successivi

[!DNL Segmentation Service] fornisce un flusso di lavoro consolidato per generare tipi di pubblico dai dati di [!DNL Real-Time Customer Profile].

Per ulteriori informazioni sull&#39;utilizzo dell&#39;interfaccia utente del servizio di segmentazione, leggere la [Panoramica dell&#39;interfaccia utente del servizio di segmentazione](./ui/overview.md).

Per informazioni su come comporre i tipi di pubblico nell&#39;interfaccia utente, consulta la [guida alla composizione dei tipi di pubblico](./ui/audience-composition.md). Per informazioni su come definire le definizioni dei segmenti nell&#39;interfaccia utente, consulta la [guida del Generatore di segmenti](./ui/overview.md). Per informazioni sulla creazione di definizioni di segmenti utilizzando l&#39;API, consulta l&#39;esercitazione sulla [creazione di definizioni di segmenti utilizzando l&#39;API](./tutorials/create-a-segment.md).
