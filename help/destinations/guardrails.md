---
keywords: Experience Platform;attivazione;risoluzione dei problemi;guardrail;linee guida;limite
title: Guardrail predefiniti per l'attivazione dei dati
solution: Experience Platform
product: experience platform
type: Documentation
description: Ulteriori informazioni sull’utilizzo predefinito dell’attivazione dei dati e sui limiti di tariffa.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 322510055bd8b8803292a2b4af9df9e1dbee7ffb
workflow-type: tm+mt
source-wordcount: '1685'
ht-degree: 2%

---

# Guardrail per l&#39;attivazione dei dati

>[!IMPORTANT]
>
>Controlla i diritti di licenza nell&#39;ordine di vendita e la corrispondente [descrizione del prodotto](https://helpx.adobe.com/it/legal/product-descriptions.html) sui limiti di utilizzo effettivi, oltre a questa pagina di guardrail.

Questa pagina fornisce i limiti predefiniti di utilizzo e tasso relativi al comportamento di attivazione. Durante la revisione dei seguenti guardrail, si presume che tu abbia [connesso correttamente alle destinazioni](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* La maggior parte dei clienti non supera questi limiti predefiniti. Per informazioni sui limiti personalizzati, contatta il rappresentante dell’assistenza clienti.
>* I limiti delineati nel presente documento vengono costantemente migliorati. Controlla regolarmente la disponibilità di aggiornamenti.
>* A seconda delle limitazioni individuali a valle, alcune destinazioni potrebbero avere guardrail più rigidi rispetto a quelle documentate in questa pagina. Verificare anche la pagina del [catalogo](/help/destinations/catalog/overview.md) della destinazione a cui si sta effettuando la connessione e l&#39;attivazione dei dati.

## Tipi di guardrail {#limit-types}

In questo documento sono disponibili due tipi di limiti predefiniti:

| Tipo di guardrail | Descrizione |
|----------|---------|
| **Guardrail delle prestazioni (limite software)** | I guardrail di prestazioni sono limiti di utilizzo relativi all’ambito dei tuoi casi d’uso. Quando si superano i guardrail delle prestazioni, è possibile che si verifichi un peggioramento delle prestazioni e della latenza. L’Adobe non è responsabile di tale degrado delle prestazioni. I clienti che superano costantemente il limite di prestazioni possono scegliere di concedere licenze aggiuntive per evitare il degrado delle prestazioni. |
| **Guardrail applicati dal sistema (limite rigido)** | I guardrail applicati dal sistema vengono applicati dall’interfaccia utente o dall’API di Real-Time CDP. Questi sono i limiti che non puoi superare, poiché l’interfaccia utente e l’API ti impediranno di farlo o restituiranno un errore. |

{style="table-layout:auto"}


## Limiti di attivazione {#activation-limits}

I seguenti guardrail forniscono i limiti consigliati per l’attivazione dei dati Real-Time Customer Profile nelle destinazioni.

### Guardrail di attivazione generale {#general-activation-guardrails}

I guardrail di seguito si applicano generalmente all&#39;attivazione tramite [tutti i tipi di destinazione](/help/destinations/destination-types.md#destination-types).

| Guardrail | Limite | Tipo limite | Descrizione |
| --- | --- | --- | --- |
| Numero massimo di tipi di pubblico per una singola destinazione | 250 | Guardrail delle prestazioni | Si consiglia di mappare un massimo di 250 tipi di pubblico su una singola destinazione in un flusso di dati. <br><br> Se devi attivare più di 250 tipi di pubblico in una destinazione, puoi: <ul><li> Annullare la mappatura dei tipi di pubblico che non desideri più attivare oppure</li><li>Crea un nuovo flusso di dati nella destinazione desiderata e mappa i tipi di pubblico su questo nuovo flusso di dati.</li></ul> <br> Tieni presente che nel caso di alcune destinazioni, puoi essere limitato a meno di 250 tipi di pubblico mappati alla destinazione. Tali destinazioni sono richiamate più avanti nella pagina, nelle rispettive sezioni. |
| Numero massimo di attributi mappati a una destinazione | 50 | Guardrail delle prestazioni | Nel caso di più destinazioni e tipi di destinazione, puoi selezionare gli attributi e le identità del profilo da mappare per l’esportazione. Per prestazioni ottimali, è necessario mappare un massimo di 50 attributi in un flusso di dati su una destinazione. |
| Numero massimo di destinazioni | 100 | Guarddrail imposto dal sistema | Puoi creare un massimo di 100 destinazioni a cui connetterti e attivare i dati, *per sandbox*. [Le destinazioni di personalizzazione di Edge (Personalizzazione personalizzata)](#edge-destinations-activation) possono rappresentare un massimo di 10 delle 100 destinazioni consigliate. |
| Tipo di dati attivati nelle destinazioni | Dati profilo, comprese identità e mappa identità | Guarddrail imposto dal sistema | Attualmente, è possibile esportare solo *attributi record profilo* nelle destinazioni. Al momento, gli attributi XDM che descrivono i dati dell’evento non sono supportati per l’esportazione. |
| Tipo di dati attivati nelle destinazioni: supporto degli attributi di array e mappa | Non disponibile | Guarddrail imposto dal sistema | Al momento, è **impossibile** esportare *gli attributi di matrice o mappa* nelle destinazioni. L&#39;eccezione a questa regola è la [mappa identità](/help/xdm/field-groups/profile/identitymap.md), che viene esportata sia nello streaming che nelle attivazioni basate su file. |

{style="table-layout:auto"}

### Attivazione streaming {#streaming-activation}

I guardrail di seguito si applicano all&#39;attivazione tramite [destinazioni di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md).

| Guardrail | Limite | Tipo limite | Descrizione |
| --- | --- | --- | --- |
| Numero di attivazioni (messaggi HTTP con esportazioni profilo) al secondo | N/D | - | Al momento non esiste alcun limite al numero di messaggi al secondo inviati dagli endpoint API di Experience Platform alle destinazioni partner. <br> Eventuali limiti o latenze sono determinati dall&#39;endpoint in cui Experience Platform invia i dati. Verificare anche la pagina del [catalogo](/help/destinations/catalog/overview.md) della destinazione a cui si sta effettuando la connessione e l&#39;attivazione dei dati. |

{style="table-layout:auto"}

### Attivazione batch (basata su file) {#batch-file-based-activation}

I guardrail riportati di seguito si applicano all&#39;attivazione tramite [destinazioni batch (basate su file)](/help/destinations/ui/activate-batch-profile-destinations.md).

| Guardrail | Limite | Tipo limite | Descrizione |
| --- | --- | --- | --- |
| Frequenza di attivazione | Un’esportazione completa giornaliera o esportazioni incrementali più frequenti ogni 3, 6, 8 o 12 ore. | Guarddrail imposto dal sistema | Per ulteriori informazioni sugli incrementi di frequenza per le esportazioni batch, leggere le sezioni della documentazione [esporta file completi](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) e [esporta file incrementali](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files). |
| Numero massimo di tipi di pubblico che possono essere esportati in una determinata ora | 100 | Guardrail delle prestazioni | Si consiglia di aggiungere un massimo di 100 tipi di pubblico ai flussi di dati di destinazione batch. |
| Numero massimo di righe (record) per file da attivare | 5 milioni | Guarddrail imposto dal sistema | Adobe Experience Platform divide automaticamente i file esportati in 5 milioni di record (righe) per file. Ogni riga rappresenta un profilo. Ai nomi dei file suddivisi viene aggiunto un numero che indica che il file fa parte di un&#39;esportazione più grande: `filename.csv`, `filename_2.csv`, `filename_3.csv`. Per ulteriori informazioni, leggere la [sezione di pianificazione](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) dell&#39;esercitazione attivare destinazioni batch. |

{style="table-layout:auto"}

### Attivazione ad hoc {#ad-hoc-activation}

I guardrail seguenti si applicano al metodo [ad-hoc activation](/help/destinations/api/ad-hoc-activation-api.md).

| Guardrail | Limite | Tipo limite | Descrizione |
| --- | --- | --- | --- |
| Tipi di pubblico attivati per processo di attivazione ad hoc | 80 | Guarddrail imposto dal sistema | Attualmente, ogni processo di attivazione ad hoc può attivare fino a 80 tipi di pubblico. Se si tenta di attivare più di 80 tipi di pubblico per processo, il processo non riuscirà. Questo comportamento è soggetto a modifiche nelle versioni future. |
| Processi di attivazione ad-hoc simultanei per pubblico | 1 | Guarddrail imposto dal sistema | Non eseguire più di un processo di attivazione ad hoc simultaneo per pubblico. |

{style="table-layout:auto"}

### Attivazione delle destinazioni di personalizzazione Edge {#edge-destinations-activation}

I guardrail riportati di seguito si applicano all&#39;attivazione tramite [destinazioni di personalizzazione edge](/help/destinations/destination-types.md#advanced-enterprise-destinations).

| Guardrail | Limite | Tipo limite | Descrizione |
| --- | --- | --- | --- |
| Numero massimo di [destinazioni Personalizzazione personalizzata](/help/destinations/catalog/personalization/custom-personalization.md) | 10 | Guardrail delle prestazioni | Puoi impostare flussi di dati su 10 destinazioni di personalizzazione personalizzate per sandbox. |
| Numero massimo di attributi mappati a una destinazione di personalizzazione per sandbox | 30 | Guarddrail imposto dal sistema | È possibile mappare un massimo di 30 attributi in un flusso di dati a una destinazione di personalizzazione, per sandbox. |
| Numero massimo di tipi di pubblico mappati a una singola destinazione [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) | 50 | Guardrail delle prestazioni | Puoi attivare fino a 50 tipi di pubblico in un flusso di attivazione verso una singola destinazione di Adobe Target. |

{style="table-layout:auto"}

### Esportazioni di set di dati {#dataset-exports}

Le esportazioni di set di dati sono attualmente supportate in un **[!UICONTROL Primo modello completo e quindi incrementale]** [pattern](/help/destinations/ui/export-datasets.md#scheduling). I guardrail descritti in questa sezione *si applicano alla prima esportazione completa* che si verifica dopo la configurazione di un flusso di lavoro di esportazione del set di dati.

<!--

| Guardrail | Limit | Limit Type | Description |
| --- | --- | --- | --- |
| Size of exported datasets | 5 billion records | Soft | The limit described here for dataset exports is a *soft guardrail*. For example, while the user interface will not block you from exporting datasets larger than 5 billion records, the behavior is unpredictable and exports might either fail or have very long export latency. |

{style="table-layout:auto"}

-->

#### Tipi di set di dati {#dataset-types}

I guardrail di esportazione dei set di dati si applicano a due tipi di set di dati esportati da Experience Platform, come descritto di seguito:

**Set di dati basati sullo schema XDM Experience Events**
Nel caso di set di dati basati sullo schema XDM Experience Events, lo schema del set di dati include una colonna *timestamp* di livello principale. I dati vengono acquisiti in modalità di sola aggiunta.

**Set di dati basati sullo schema Profilo individuale XDM**
Nel caso di set di dati basati sullo schema Profilo individuale XDM, lo schema del set di dati non include una colonna *timestamp* di livello principale. I dati vengono acquisiti in modalità upsert.

Il soft guardrail riportato di seguito si applica a tutti i set di dati esportati da Experience Platform. Consulta anche i guardrail rigidi riportati di seguito, specifici per set di dati e tipi di compressione diversi.

| Guardrail | Limite | Tipo limite | Descrizione |
| --- | --- | --- | --- |
| Dimensione dei set di dati esportati | 5 miliardi di record | Guardrail delle prestazioni | Il limite qui descritto per le esportazioni di set di dati è un *guardrail soft*. Ad esempio, anche se l’interfaccia utente non blocca l’esportazione di set di dati superiori a 5 miliardi di record, il comportamento è imprevedibile e le esportazioni potrebbero non riuscire o avere una latenza di esportazione molto lunga. |

{style="table-layout:auto"}

#### Guardrail per esportazioni di set di dati pianificate

Per le esportazioni di set di dati pianificate o ricorrenti, i guardrail riportati di seguito sono identici per i due formati del file esportato (JSON o parquet) e sono raggruppati per tipo di set di dati.

>[!WARNING]
>
>Le esportazioni in file JSON sono supportate solo in modalità compressa.

| Tipo di set di dati | Guardrail | Tipo di guardrail | Descrizione |
---------|----------|---------|-------|
| Set di dati basati sullo schema **XDM Experience Events** | Ultimi 365 giorni di dati | Guarddrail imposto dal sistema | Vengono esportati i dati dell&#39;ultimo anno di calendario. |
| Set di dati basati sullo schema **Profilo individuale XDM** | Dieci miliardi di record in tutti i file esportati in un flusso di dati | Guarddrail imposto dal sistema | Il numero di record del set di dati deve essere inferiore a dieci miliardi per i file JSON o parquet compressi e a un milione per i file parquet non compressi, altrimenti l’esportazione non riesce. Riduci le dimensioni del set di dati che stai tentando di esportare se è più grande della soglia consentita. |

{style="table-layout:auto"}

<!--

#### Ad-hoc dataset exports

Exporting datasets in an-hoc manner is currently supported via API only. For ad-hoc dataset exports, you must use the backfill parameter in the API to limit the timeframe of exported data. 

The guardrails below are the same whether you are exporting parquet of JSON files ad-hoc. 

**Parquet and JSON output**

|Dataset type | Backfill parameter provided | Guardrail | Guardrail type | Description |
|---------|---------|-----------|-----------|------------|
| Datasets based on the **XDM Experience Events schema** |  <p><ul><li>Both start and end date provided in `backfill` parameter in API call</li><li>Incomplete `backfill` parameter provided in API call</li></ul></p> | <p><ul><li>Last 30 days</li><li>Last 365 days</li></ul></p> | Hard | <p><ul><li>The export fails if the `startDate - endDate` interval is over 30 days</li><li>Either the `startDate` or `endDate` are missing or  incorrectly formatted in the API call. Expected format: `yyyy-MM-dd'T'HH:mm:ss.SSS'Z'`</li></ul></p> |
| Datasets based on the **XDM Individual Profile schema** |  - | Ten billion records across all files exported in a dataflow | Hard | The record count of the dataset must be less than ten billion for compressed JSON or parquet files and one million for uncompressed parquet files, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold. |

{style="table-layout:auto"}

-->

Ulteriori informazioni sull&#39;esportazione di [set di dati](/help/destinations/ui/export-datasets.md).


### Destination SDK guardrail {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) è una suite di API di configurazione che ti consente di configurare i modelli di integrazione delle destinazioni, ad Experience Platform per fornire i dati di pubblico e profilo all&#39;endpoint, in base ai formati di dati e autenticazione scelti. I guardrail riportati di seguito si applicano alle destinazioni configurate mediante Destination SDK.

| Guardrail | Limite | Tipo limite | Descrizione |
| --- | --- | --- | --- |
| Numero massimo di [destinazioni personalizzate private](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Guardrail delle prestazioni | Puoi creare fino a 5 destinazioni private di flussi personalizzati o batch utilizzando Destination SDK. Se devi creare più di 5 di queste destinazioni, rivolgiti a un rappresentante dell’assistenza personalizzata. |
| Criterio di esportazione profilo per Destination SDK | <ul><li>`maxBatchAgeInSecs` (minimo 1.800 e massimo 3.600)</li><li>`maxNumEventsInBatch` (minimo 1.000, massimo 10.000)</li></ul> | Guarddrail imposto dal sistema | Quando utilizzi l&#39;opzione di [aggregazione configurabile](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) per la destinazione, tieni presente i valori minimo e massimo che determinano la frequenza con cui i messaggi HTTP vengono inviati alla destinazione basata su API e il numero di profili che i messaggi devono includere. |

{style="table-layout:auto"}

### Criterio di limitazione e nuovo tentativo della destinazione {#destination-throttling-and-retry-policy}

Dettagli sulle soglie o limitazioni di limitazione per determinate destinazioni. Questa sezione fornisce anche informazioni sui criteri per i nuovi tentativi per le destinazioni.

| Tipo di destinazione | Descrizione |
| --- | --- |
| Destinazioni Enterprise (API HTTP, Amazon Kinesis, Azure EventHubs) | Nel 95% del tempo, Experience Platform tenta di offrire una latenza di velocità effettiva inferiore a 10 minuti per i messaggi inviati correttamente con una frequenza inferiore a 10.000 richieste al secondo per ogni flusso di dati verso una destinazione aziendale. <br> In caso di richieste non riuscite alla destinazione Enterprise, Experience Platform memorizza le richieste non riuscite e tenta di inviarle all&#39;endpoint due volte. |

{style="table-layout:auto"}

## Passaggi successivi

Consulta la seguente documentazione per ulteriori informazioni su altri guardrail dei servizi Experience Platform, informazioni sulla latenza end-to-end e informazioni sulle licenze dai documenti di descrizione del prodotto Real-Time CDP:

* [Guardrail Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagrammi di latenza end-to-end](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) per vari servizi Experience Platform.
* [Real-time Customer Data Platform (Edizione B2C - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
