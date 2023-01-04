---
keywords: Experience Platform;attivazione;risoluzione dei problemi;protezioni;linee guida;limite
title: Garanzie predefinite per i dati di attivazione
solution: Experience Platform
product: experience platform
type: Documentation
description: Ulteriori informazioni sui limiti di utilizzo e di tasso predefiniti per l’attivazione dei dati.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1198'
ht-degree: 3%

---

# Guardrail per i dati di attivazione

Questa pagina fornisce limiti di utilizzo e di frequenza predefiniti per quanto riguarda il comportamento di attivazione. Quando si esaminano le seguenti protezioni, si presume che tu abbia eseguito correttamente [connesso a destinazioni](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* La maggior parte dei clienti non supera questi limiti predefiniti. Per informazioni sui limiti personalizzati, contatta il rappresentante dell’Assistenza clienti.
>* I limiti delineati in questo documento vengono costantemente migliorati. Controlla regolarmente la disponibilità di aggiornamenti.
>* A seconda delle limitazioni a valle individuali, alcune destinazioni potrebbero avere protezioni più restrittive rispetto a quelle documentate in questa pagina. Assicurati anche di controllare il [catalogo](/help/destinations/catalog/overview.md) pagina della destinazione a cui si desidera collegare e attivare i dati.


## Tipi di limite {#limit-types}

Questo documento contiene due tipi di limiti predefiniti:

* **Limite morbido:** È possibile superare un limite soft, tuttavia i limiti soft forniscono una linea guida consigliata per le prestazioni del sistema.
* **Limite rigido:** Un limite rigido fornisce un massimo assoluto. L’interfaccia utente o l’API di Experience Platform non ti consente di superare questo limite, oppure viene restituito un errore se superi questo limite.


## Limiti di attivazione {#activation-limits}

Le seguenti protezioni forniscono i limiti consigliati quando si attivano i dati del profilo cliente in tempo reale nelle destinazioni.

### Guardrail di attivazione generale {#general-activation-guardrails}

Le protezioni sotto riportate si applicano generalmente all&#39;attivazione attraverso [tutti i tipi di destinazione](/help/destinations/destination-types.md#destination-types).

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Numero massimo di segmenti in una singola destinazione | 250 | Morbido | Si consiglia di mappare un massimo di 250 segmenti su una singola destinazione in un flusso di dati. <br><br> Se devi attivare più di 250 segmenti su una destinazione, puoi: <ul><li> Annulla la mappatura di segmenti che non desideri più attivare oppure</li><li>Crea un nuovo flusso di dati per la destinazione desiderata e mappa i segmenti su questo nuovo flusso di dati.</li></ul> <br> Tieni presente che in alcune destinazioni puoi essere limitato a meno di 250 segmenti mappati sulla destinazione. Tali destinazioni sono chiamate più avanti nella pagina, nelle rispettive sezioni. |
| Numero massimo di destinazioni | 100 | Morbido | Si consiglia di creare un massimo di 100 destinazioni a cui è possibile collegare e attivare i dati *per sandbox*. [Destinazioni di personalizzazione Edge (personalizzazione personalizzata)](#edge-destinations-activation) può rappresentare un massimo di 10 delle 100 destinazioni consigliate. |
| Numero massimo di attributi mappati a una destinazione | 50 | Morbido | Nel caso di più destinazioni e tipi di destinazione, puoi selezionare gli attributi e le identità di profilo da mappare per l’esportazione. Per prestazioni ottimali, in un flusso di dati è necessario mappare a una destinazione un massimo di 50 attributi. |
| Tipo di dati attivati nelle destinazioni | Dati del profilo, comprese identità e mappa di identità | Duro | Attualmente è possibile esportare solo *attributi del record del profilo* verso le destinazioni. Gli attributi XDM che descrivono i dati dell’evento non sono al momento supportati per l’esportazione. |
| Tipo di dati attivati nelle destinazioni - supporto degli attributi di matrice e mappa | Non disponibile | Duro | A questo punto è **not** possibile esportazione *attributi di matrice o mappa* verso le destinazioni. L&#39;eccezione a questa regola è il [mappa identità](/help/xdm/field-groups/profile/identitymap.md), che viene esportato sia in streaming che in attivazioni basate su file. |

{style=&quot;table-layout:auto&quot;}

### Attivazione in streaming {#streaming-activation}

Le protezioni sotto riportate si applicano all&#39;attivazione tramite [destinazioni di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md).

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Numero di attivazioni (messaggi HTTP con esportazioni di profilo) al secondo | N/D | - | Attualmente non esiste alcun limite al numero di messaggi al secondo inviati da Experience Platform agli endpoint API delle destinazioni partner. <br> Eventuali limiti o latenze sono determinati dall’endpoint in cui l’Experience Platform invia i dati. Assicurati anche di controllare il [catalogo](/help/destinations/catalog/overview.md) pagina della destinazione a cui si desidera collegare e attivare i dati. |

{style=&quot;table-layout:auto&quot;}

### Attivazione batch (basata su file) {#batch-file-based-activation}

Le protezioni sotto riportate si applicano all&#39;attivazione tramite [destinazioni batch (basate su file)](/help/destinations/ui/activate-batch-profile-destinations.md).

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Frequenza di attivazione | Esportazione completa giornaliera o esportazioni incrementali più frequenti ogni 3, 6, 8 o 12 ore. | Duro | Leggi la sezione [esportare file completi](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) e [esportare file incrementali](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) sezioni di documentazione per ulteriori informazioni sugli incrementi di frequenza per le esportazioni batch. |
| Numero massimo di segmenti che possono essere esportati a un’ora specifica | 100 | Morbido | Si consiglia di aggiungere un massimo di 100 segmenti ai flussi di dati di destinazione batch. |
| Numero massimo di righe (record) per file da attivare | 5 milioni | Duro | Adobe Experience Platform divide automaticamente i file esportati a 5 milioni di record (righe) per file. Ogni riga rappresenta un profilo. I nomi dei file divisi vengono aggiunti con un numero che indica che il file fa parte di un’esportazione più grande, in quanto tale: `filename.csv`, `filename_2.csv`, `filename_3.csv`. Per ulteriori informazioni, consulta la sezione [sezione programmazione](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) del tutorial di attivazione delle destinazioni batch. |

{style=&quot;table-layout:auto&quot;}

### Attivazione ad hoc {#ad-hoc-activation}

Le protezioni sotto riportate si applicano al [attivazione ad hoc](/help/destinations/api/ad-hoc-activation-api.md) metodo .

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Segmenti attivati per processo di attivazione ad hoc | 80 | Duro | Attualmente, ogni processo di attivazione ad-hoc può attivare fino a 80 segmenti. Se si tenta di attivare più di 80 segmenti per processo, il processo non riuscirà. Questo comportamento è soggetto a modifiche nelle versioni future. |
| Processi di attivazione simultanea ad hoc per segmento | 1 | Duro | Non eseguire più di un processo di attivazione ad hoc simultaneo per segmento. |

{style=&quot;table-layout:auto&quot;}

### Attivazione di destinazioni di personalizzazione Edge {#edge-destinations-activation}

Le protezioni sotto riportate si applicano all&#39;attivazione tramite [destinazioni di personalizzazione edge](/help/destinations/destination-types.md#streaming-profile-export).

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Numero massimo di [Personalizzazione personalizzata](/help/destinations/catalog/personalization/custom-personalization.md) destinazioni | 10 | Morbido | Puoi impostare i flussi di dati su 10 destinazioni di personalizzazione personalizzate per sandbox. |
| Numero massimo di attributi mappati a una destinazione di personalizzazione per sandbox | 20 | Duro | È possibile mappare un massimo di 20 attributi in un flusso di dati a una destinazione di personalizzazione, per sandbox. |
| Numero massimo di segmenti mappati a un singolo [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) destinazione | 50 | Morbido | Puoi attivare un massimo di 50 segmenti in un flusso di attivazione per una singola destinazione Adobe Target. |

{style=&quot;table-layout:auto&quot;}

### Destination SDK {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) è una suite di API di configurazione che ti consentono di configurare pattern di integrazione di destinazione, ad Experience Platform per distribuire i dati di pubblico e profilo all’endpoint, in base ai dati e ai formati di autenticazione scelti. Le protezioni riportate di seguito si applicano alle destinazioni configurate utilizzando Destination SDK.

| Guardrail | Limite | Tipo di limite | Descrizione |
| --- | --- | --- | --- |
| Numero massimo di [destinazioni personalizzate private](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Morbido | Puoi creare un massimo di 5 destinazioni personalizzate di streaming o batch private utilizzando Destination SDK. Rivolgiti a un rappresentante dell’Assistenza clienti personalizzato se hai bisogno di creare più di 5 destinazioni di questo tipo. |
| Criteri di esportazione profilo per Destination SDK | <ul><li>`maxBatchAgeInSecs` (minimo 1 800 e massimo 3 600)</li><li>`maxNumEventsInBatch` (minimo 1.000, massimo 10.000)</li></ul> | Duro | Quando utilizzi [aggregazione configurabile](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation) Per la destinazione , fai attenzione ai valori minimo e massimo che determinano la frequenza con cui i messaggi HTTP vengono inviati alla destinazione basata su API e quanti profili devono includere nei messaggi. |

{style=&quot;table-layout:auto&quot;}

### Criterio di limitazione della destinazione e nuovo tentativo {#destination-throttling-and-retry-policy}

Dettagli sulle soglie di limitazione o limitazioni per determinate destinazioni. Questa sezione fornisce inoltre informazioni sui criteri per i nuovi tentativi per le destinazioni.

| Tipo di destinazione | Descrizione |
| --- | --- |
| Destinazioni Enterprise (API HTTP, Amazon Kinesis, Azure EventHubs) | Nel 95% del tempo, Experience Platform tenta di offrire una latenza di throughput inferiore a 10 minuti per i messaggi inviati con successo con un tasso di meno di 10 mila richieste al secondo per ogni flusso di dati a una destinazione aziendale. <br> In caso di richieste non riuscite alla destinazione enterprise, Experience Platform memorizza le richieste non riuscite e tenta nuovamente due volte di inviare le richieste all’endpoint. |

{style=&quot;table-layout:auto&quot;}

## Garanzie per altri servizi di Experience Platform {#guardrails-other-services}

Visualizza informazioni sulle protezioni per altri servizi di Experience Platform:

* Guardrail per [inserimento dati](/help/ingestion/guardrails.md)
* Guardrail per [[!DNL Identity Service] dati](/help/identity-service/guardrails.md)
* Guardrail per [[!DNL Real-Time Customer Profile] dati](/help/profile/guardrails.md)
* Guardrail per [[!DNL Query Service] dati](/help/query-service/guardrails.md)
