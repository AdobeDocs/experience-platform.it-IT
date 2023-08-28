---
keywords: Experience Platform;attivazione;risoluzione dei problemi;guardrail;linee guida;limite
title: Guardrail predefiniti per i dati di attivazione
solution: Experience Platform
product: experience platform
type: Documentation
description: Ulteriori informazioni sull’utilizzo predefinito dell’attivazione dei dati e sui limiti di tariffa.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 0835021523a7eb1642a6dbcb24334eac535aaa6d
workflow-type: tm+mt
source-wordcount: '1270'
ht-degree: 1%

---

# Guardrail per i dati di attivazione

Questa pagina fornisce i limiti predefiniti di utilizzo e tasso relativi al comportamento di attivazione. Quando si esaminano i seguenti guardrail, si presume che siano presenti correttamente [connesso alle destinazioni](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* La maggior parte dei clienti non supera questi limiti predefiniti. Per informazioni sui limiti personalizzati, contatta il rappresentante dell’assistenza clienti.
>* I limiti delineati nel presente documento vengono costantemente migliorati. Controlla regolarmente se ci sono aggiornamenti.
>* A seconda delle limitazioni individuali a valle, alcune destinazioni potrebbero avere guardrail più rigidi rispetto a quelle documentate in questa pagina. Assicurati anche di controllare il [catalogo](/help/destinations/catalog/overview.md) della destinazione a cui si sta effettuando la connessione e l&#39;attivazione dei dati.

## Tipi di limite {#limit-types}

In questo documento sono disponibili due tipi di limiti predefiniti:

* **Limite soft:** È possibile superare un limite soft, tuttavia i limiti soft forniscono una linea guida consigliata per le prestazioni del sistema.
* **Limite rigido:** Un limite rigido fornisce un massimo assoluto. L’interfaccia utente o l’API di Experienci Platform non consente di superare questo limite, oppure se superi questo limite, viene restituito un errore.


## Limiti di attivazione {#activation-limits}

I seguenti guardrail forniscono i limiti consigliati per l’attivazione dei dati Real-Time Customer Profile nelle destinazioni.

### Guardrail di attivazione generale {#general-activation-guardrails}

I guardrail di seguito si applicano generalmente all&#39;attivazione tramite [tutti i tipi di destinazione](/help/destinations/destination-types.md#destination-types).

| Guardrail | Limite | Tipo limite | Descrizione |
| --- | --- | --- | --- |
| Numero massimo di tipi di pubblico per una singola destinazione | 250 | Morbido | Si consiglia di mappare un massimo di 250 tipi di pubblico su una singola destinazione in un flusso di dati. <br><br> Se devi attivare più di 250 tipi di pubblico in una destinazione, puoi: <ul><li> Annullare la mappatura dei tipi di pubblico che non desideri più attivare oppure</li><li>Crea un nuovo flusso di dati nella destinazione desiderata e mappa i tipi di pubblico su questo nuovo flusso di dati.</li></ul> <br> Tieni presente che nel caso di alcune destinazioni, puoi essere limitato a meno di 250 tipi di pubblico mappati alla destinazione. Tali destinazioni sono richiamate più avanti nella pagina, nelle rispettive sezioni. |
| Numero massimo di attributi mappati a una destinazione | 50 | Morbido | Nel caso di più destinazioni e tipi di destinazione, puoi selezionare gli attributi e le identità del profilo da mappare per l’esportazione. Per prestazioni ottimali, è necessario mappare un massimo di 50 attributi in un flusso di dati su una destinazione. |
| Numero massimo di destinazioni | 100 | Rigido | Puoi creare un massimo di 100 destinazioni a cui connettersi e attivare i dati, *per sandbox*. [Destinazioni di personalizzazione Edge (personalizzazione personalizzata)](#edge-destinations-activation) può rappresentare un massimo di 10 delle 100 destinazioni consigliate. |
| Tipo di dati attivati nelle destinazioni | Dati profilo, comprese identità e mappa identità | Rigido | Attualmente, è possibile esportare solo *attributi record profilo* alle destinazioni. Al momento, gli attributi XDM che descrivono i dati dell’evento non sono supportati per l’esportazione. |
| Tipo di dati attivati nelle destinazioni: supporto degli attributi di array e mappa | Non disponibile | Rigido | In questo momento, è **non** possibile esportare *array o attributi mappa* alle destinazioni. L&#39;eccezione a questa regola è il [mappa identità](/help/xdm/field-groups/profile/identitymap.md), che viene esportato sia in streaming che nelle attivazioni basate su file. |

{style="table-layout:auto"}

### Attivazione streaming {#streaming-activation}

I guardrail di seguito si applicano all&#39;attivazione tramite [destinazioni di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md).

| Guardrail | Limite | Tipo limite | Descrizione |
| --- | --- | --- | --- |
| Numero di attivazioni (messaggi HTTP con esportazioni profilo) al secondo | N/D | - | Al momento non esiste alcun limite al numero di messaggi al secondo inviati dagli endpoint API di Experienci Platform alle destinazioni partner. <br> Eventuali limiti o latenze sono determinati dall’endpoint in cui Experienci Platform invia i dati. Assicurati anche di controllare il [catalogo](/help/destinations/catalog/overview.md) della destinazione a cui si sta effettuando la connessione e l&#39;attivazione dei dati. |

{style="table-layout:auto"}

### Attivazione batch (basata su file) {#batch-file-based-activation}

I guardrail di seguito si applicano all&#39;attivazione tramite [destinazioni batch (basate su file)](/help/destinations/ui/activate-batch-profile-destinations.md).

| Guardrail | Limite | Tipo limite | Descrizione |
| --- | --- | --- | --- |
| Frequenza di attivazione | Un’esportazione completa giornaliera o esportazioni incrementali più frequenti ogni 3, 6, 8 o 12 ore. | Rigido | Leggi le [esporta file completi](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) e [esportare file incrementali](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) sezioni della documentazione per ulteriori informazioni sugli incrementi di frequenza per le esportazioni batch. |
| Numero massimo di tipi di pubblico che possono essere esportati in una determinata ora | 100 | Morbido | Si consiglia di aggiungere un massimo di 100 tipi di pubblico ai flussi di dati di destinazione batch. |
| Numero massimo di righe (record) per file da attivare | 5 milioni | Rigido | Adobe Experience Platform divide automaticamente i file esportati in 5 milioni di record (righe) per file. Ogni riga rappresenta un profilo. Ai nomi dei file suddivisi viene aggiunto un numero che indica che il file fa parte di un’esportazione più grande: `filename.csv`, `filename_2.csv`, `filename_3.csv`. Per ulteriori informazioni, leggere [sezione pianificazione](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) dell’esercitazione attivare destinazioni batch. |

{style="table-layout:auto"}

### Attivazione ad hoc {#ad-hoc-activation}

I guardrail riportati di seguito si applicano al [attivazione ad hoc](/help/destinations/api/ad-hoc-activation-api.md) metodo.

| Guardrail | Limite | Tipo limite | Descrizione |
| --- | --- | --- | --- |
| Tipi di pubblico attivati per processo di attivazione ad hoc | 80 | Rigido | Attualmente, ogni processo di attivazione ad hoc può attivare fino a 80 tipi di pubblico. Se si tenta di attivare più di 80 tipi di pubblico per processo, il processo non riuscirà. Questo comportamento è soggetto a modifiche nelle versioni future. |
| Processi di attivazione ad-hoc simultanei per pubblico | 1 | Rigido | Non eseguire più di un processo di attivazione ad hoc simultaneo per pubblico. |

{style="table-layout:auto"}

### Attivazione delle destinazioni di personalizzazione Edge {#edge-destinations-activation}

I guardrail di seguito si applicano all&#39;attivazione tramite [destinazioni di personalizzazione edge](/help/destinations/destination-types.md#streaming-profile-export).

| Guardrail | Limite | Tipo limite | Descrizione |
| --- | --- | --- | --- |
| Numero massimo di [Personalizzazione personalizzata](/help/destinations/catalog/personalization/custom-personalization.md) destinazioni | 10 | Morbido | Puoi impostare flussi di dati su 10 destinazioni di personalizzazione personalizzate per sandbox. |
| Numero massimo di attributi mappati a una destinazione di personalizzazione per sandbox | 30 | Rigido | È possibile mappare un massimo di 30 attributi in un flusso di dati a una destinazione di personalizzazione, per sandbox. |
| Numero massimo di tipi di pubblico mappati su un singolo [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) destinazione | 50 | Morbido | Puoi attivare fino a 50 tipi di pubblico in un flusso di attivazione verso una singola destinazione di Adobe Target. |

{style="table-layout:auto"}

### [!BADGE Beta]Esportazioni di set di dati {type=Informative} {#dataset-exports}

Le esportazioni di set di dati sono attualmente supportate in una **[!UICONTROL Prima completo e poi incrementale]** [pattern](/help/destinations/ui/export-datasets.md#scheduling). Le protezioni descritte in questa sezione si applicano alla prima esportazione completa che si verifica dopo la configurazione di un flusso di lavoro di esportazione di un set di dati.

| Guardrail | Limite | Tipo limite | Descrizione |
| --- | --- | --- | --- |
| Dimensione dei set di dati esportati | 5 miliardi di record | Morbido | Il limite qui descritto per le esportazioni di set di dati è un *guardrail morbido*. Ad esempio, anche se l’interfaccia utente non blocca l’esportazione di set di dati superiori a 5 miliardi di record, il comportamento è imprevedibile e le esportazioni potrebbero non riuscire o avere una latenza di esportazione molto lunga. |

{style="table-layout:auto"}

<!--

### Dataset Types {#dataset-types}

Datasets exported from Experience Platform can be of two types, as described below:

**Timeseries**
Timeseries datasets are also known as *XDM Experience Events* datasets in Experience Platform terminology.
The dataset schema includes a top level *timestamp* column. Data is ingested in an append-only fashion.

**Record** 
Record datasets are also known as *XDM Individual Profile* datasets in Experience Platform terminology.
The dataset schema does not include a top level *timestamp* column. Data is ingested in upsert fashion.

The guardrails below are grouped by the format of the exported file, and then further by dataset type.

**Parquet output**

|Dataset type | Compression | Guardrail | Description |
|---------|----------|---------|-----------|
| Timeseries | N/A | Last seven days per file | The data from the last seven days only is exported. |
| Record | N/A | Five billion records per file | Only the data from the last seven days is exported. |

{style="table-layout:auto"}

**JSON output**

|Dataset type | Compression | Guardrail | Description |
|---------|----------|---------|-----------|
| Timeseries | N/A | Last seven days per file | The data from the last seven days only is exported. |
| <p>Record</p> | <p><ul><li>Yes</li><li>No</li></ul></p> | <p><ul><li>Five billion records per compressed file</li><li>One million records per uncompressed file</li></ul></p> | <p>The record count of the dataset must be less than five billion for compressed files and one million for uncompressed files, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</p> |

{style="table-layout:auto"}

-->

<!--

<table>
<thead>
  <tr>
    <th>Output format</th>
    <th>Dataset type</th>
    <th>Compression</th>
    <th>Guardrail</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">Parquet</td>
    <td>Timeseries</td>
    <td>-</td>
    <td>Last seven days per file</td>
    <td>Only the data from the last seven days is exported.</td>
  </tr>
  <tr>
    <td>Record</td>
    <td>-</td>
    <td>Five billion records per file</td>
    <td>The record count of the dataset must be less than five billion, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</td>
  </tr>
  <tr>
    <td rowspan="3">JSON</td>
    <td>Timeseries</td>
    <td>-</td>
    <td>Last seven days per file</td>
    <td>Only the data from the last seven days is exported.</td>
  </tr>
  <tr>
    <td rowspan="2">Record</td>
    <td>Yes</td>
    <td>Five billion records per file</td>
    <td>The record count of the dataset must be less than five billion, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</td>
  </tr>
  <tr>
    <td>No</td>
    <td>One million records per file</td>
    <td>The record count of the dataset must be less than one million, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</td>
  </tr>
</tbody>
</table>

-->

### Destination SDK guardrail {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) è una suite di API di configurazione che consente di configurare i modelli di integrazione delle destinazioni, ad Experience Platform per fornire dati di pubblico e profilo all’endpoint, in base ai formati di dati e autenticazione selezionati. I guardrail riportati di seguito si applicano alle destinazioni configurate mediante Destination SDK.

| Guardrail | Limite | Tipo limite | Descrizione |
| --- | --- | --- | --- |
| Numero massimo di [destinazioni personalizzate private](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Morbido | Puoi creare fino a 5 destinazioni private di flussi personalizzati o batch utilizzando Destination SDK. Se devi creare più di 5 di queste destinazioni, rivolgiti a un rappresentante dell’assistenza personalizzata. |
| Criterio di esportazione profilo per Destination SDK | <ul><li>`maxBatchAgeInSecs` (minimo 1,800 e massimo 3,600)</li><li>`maxNumEventsInBatch` (minimo 1.000, massimo 10.000)</li></ul> | Rigido | Quando si utilizza [aggregazione configurabile](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) per la destinazione, tieni presente i valori minimo e massimo che determinano la frequenza con cui i messaggi HTTP vengono inviati alla destinazione basata su API e il numero di profili da includere nei messaggi. |

{style="table-layout:auto"}

### Criterio di limitazione e nuovo tentativo della destinazione {#destination-throttling-and-retry-policy}

Dettagli sulle soglie o limitazioni di limitazione per determinate destinazioni. Questa sezione fornisce anche informazioni sui criteri per i nuovi tentativi per le destinazioni.

| Tipo di destinazione | Descrizione |
| --- | --- |
| Destinazioni Enterprise (API HTTP, Amazon Kinesis, Azure EventHubs) | Nel 95% del tempo, Experienci Platform tenta di offrire una latenza di velocità effettiva inferiore a 10 minuti per i messaggi inviati correttamente con una frequenza inferiore a 10.000 richieste al secondo per ogni flusso di dati verso una destinazione aziendale. <br> In caso di richieste non riuscite alla destinazione Enterprise, Experienci Platform memorizza le richieste non riuscite e tenta di inviarle all’endpoint due volte. |

{style="table-layout:auto"}

## Guardrail per altri servizi Experienci Platform {#guardrails-other-services}

Visualizza le informazioni sui guardrail per altri servizi Experienci Platform:

* Guardrail per [acquisizione dei dati](/help/ingestion/guardrails.md)
* Guardrail per [[!DNL Identity Service] dati](/help/identity-service/guardrails.md)
* Guardrail per [[!DNL Real-Time Customer Profile] dati](/help/profile/guardrails.md)
* Guardrail per [[!DNL Query Service] dati](/help/query-service/guardrails.md)
