---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;anteprima;esempio
title: Anteprima endpoint API di stato campione (anteprima profilo)
description: L’endpoint per lo stato di anteprima del campione dell’API Real-Time Customer Profile ti consente di visualizzare in anteprima l’ultimo campione riuscito dei dati del profilo, di elencare la distribuzione del profilo per set di dati e per identità e di generare rapporti che mostrano la sovrapposizione dei set di dati, la sovrapposizione delle identità e i profili non uniti.
role: Developer
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '2906'
ht-degree: 1%

---

# Endpoint dello stato del campione di anteprima (anteprima profilo)

Adobe Experience Platform consente di acquisire i dati dei clienti da più origini per creare un profilo solido e unificato per ciascuno dei singoli clienti. Quando i dati vengono acquisiti in Platform, viene eseguito un processo di esempio per aggiornare il conteggio dei profili e altre metriche relative ai dati del profilo cliente in tempo reale.

I risultati di questo processo di esempio possono essere visualizzati utilizzando l&#39;endpoint `/previewsamplestatus`, parte dell&#39;API Real-Time Customer Profile. Questo endpoint può essere utilizzato anche per elencare le distribuzioni di profilo per set di dati e spazio dei nomi delle identità, nonché per generare più rapporti al fine di ottenere visibilità nella composizione dell’archivio profili della tua organizzazione. Questa guida descrive i passaggi necessari per visualizzare queste metriche utilizzando l&#39;endpoint API `/previewsamplestatus`.

>[!NOTE]
>
>Nell’API del servizio di segmentazione di Adobe Experience Platform sono disponibili endpoint per la stima e l’anteprima che consentono di visualizzare informazioni di riepilogo sulle definizioni dei segmenti per poter isolare il pubblico previsto. Per informazioni dettagliate sull&#39;utilizzo degli endpoint di anteprima e stima, visitare la [guida delle anteprime e delle stime degli endpoint](../../segmentation/api/previews-and-estimates.md), parte della guida per gli sviluppatori API [!DNL Segmentation].

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39;[[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Prima di continuare, consulta la [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API [!DNL Experience Platform].

## Frammenti di profilo e profili uniti

Questa guida fa riferimento sia a &quot;frammenti di profilo&quot; che a &quot;profili uniti&quot;. È importante comprendere la differenza tra questi termini prima di procedere.

Ogni singolo profilo cliente è composto da più frammenti di profilo che sono stati uniti per formare un’unica vista di quel cliente. Ad esempio, se un cliente interagisce con il tuo marchio su più canali, è probabile che la tua organizzazione disponga di più frammenti di profilo relativi a quel singolo cliente che compaiono in più set di dati.

Quando i frammenti di profilo vengono acquisiti in Platform, vengono uniti insieme (in base a un criterio di unione) per creare un singolo profilo per quel cliente. Pertanto, è probabile che il numero totale di frammenti di profilo sia sempre superiore al numero totale di profili uniti, in quanto ogni profilo è composto da più frammenti.

Per ulteriori informazioni sui profili e sul loro ruolo in Experience Platform, consulta la [Panoramica del profilo cliente in tempo reale](../home.md).

## Modalità di attivazione del processo di esempio

Poiché i dati abilitati per Real-Time Customer Profile vengono acquisiti in [!DNL Platform], vengono memorizzati nell&#39;archivio dati del profilo. Quando l’acquisizione dei record nell’archivio profili aumenta o diminuisce il conteggio totale dei profili di oltre il 5%, viene attivato un processo di campionamento per aggiornare il conteggio. Il modo in cui il campione viene attivato dipende dal tipo di acquisizione utilizzata:

* Per **flussi di lavoro di dati in streaming**, viene eseguito un controllo su base oraria per determinare se la soglia di aumento o di diminuzione del 5% è stata raggiunta. In caso affermativo, viene attivato automaticamente un processo di esempio per aggiornare il conteggio.
* Per l&#39;**acquisizione batch**, entro 15 minuti dalla corretta acquisizione di un batch nell&#39;archivio profili, se viene raggiunta la soglia di aumento o riduzione del 5%, viene eseguito un processo per aggiornare il conteggio. Utilizzando l’API di profilo è possibile visualizzare in anteprima l’ultimo processo di esempio riuscito, nonché elencare la distribuzione del profilo per set di dati e per spazio dei nomi dell’identità.

Il conteggio dei profili e i profili per metrica dello spazio dei nomi sono disponibili anche nella sezione [!UICONTROL Profiles] dell&#39;interfaccia utente di Experience Platform. Per informazioni su come accedere ai dati del profilo tramite l&#39;interfaccia utente, visitare la [[!DNL Profile] guida dell&#39;interfaccia utente](../ui/user-guide.md).

## Visualizza ultimo stato del campione {#view-last-sample-status}

È possibile eseguire una richiesta di GET all&#39;endpoint `/previewsamplestatus` per visualizzare i dettagli dell&#39;ultimo processo di esempio eseguito correttamente per l&#39;organizzazione. Ciò include il numero totale di profili nel campione, nonché la metrica di conteggio dei profili o il numero totale di profili di cui dispone la tua organizzazione in Experience Platform.

Il conteggio dei profili viene generato dopo l’unione dei frammenti di profilo per formare un singolo profilo per ogni singolo cliente. In altre parole, quando i frammenti di profilo vengono uniti tra loro, viene restituito un conteggio di &quot;1&quot; profilo perché sono tutti correlati allo stesso individuo.

Il conteggio dei profili include anche profili con attributi (dati record) e profili contenenti solo dati di serie temporali (eventi), come i profili di Adobe Analytics. Il processo di esempio viene aggiornato regolarmente man mano che i dati di profilo vengono acquisiti, in modo da fornire un numero totale aggiornato di profili in Platform.

**Formato API**

```http
GET /previewsamplestatus
```

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

La risposta include i dettagli dell’ultimo processo di esempio riuscito eseguito per l’organizzazione.

>[!NOTE]
>
>In questo esempio di risposta, `numRowsToRead` e `totalRows` sono uguali tra loro. A seconda del numero di profili di cui dispone l’organizzazione, questo può accadere in Experience Platform. Tuttavia, in genere questi due numeri sono diversi, con `numRowsToRead` che è il numero minore perché rappresenta il campione come sottoinsieme del numero totale di profili (`totalRows`).

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
  "cosmosDocCount": "\"300803\"",
  "totalFragmentCount": 47429,
  "lastSuccessfulBatchTimestamp": "\"null\"",
  "streamingDriven": "\"false\"",
  "totalRows": "41003",
  "lastBatchId": "\"null\"",
  "status": "TASK_FINISHED",
  "samplingRatio": 1.0,
  "mergeStrategy": "timestampOrdered_auto",
  "lastSampledTimestamp": "2020-08-01 17:57:57.0"
}
```

| Proprietà | Descrizione |
|---|---|
| `numRowsToRead` | Numero totale di profili uniti nel campione. |
| `sampleJobRunning` | Valore booleano che restituisce `true` quando è in corso un processo di esempio. Fornisce trasparenza nella latenza che si verifica quando un file batch viene caricato in quando viene effettivamente aggiunto all’archivio profili. |
| `cosmosDocCount` | Numero totale di documenti in Cosmos. |
| `totalFragmentCount` | Numero totale di frammenti di profilo nell’archivio Profili. |
| `lastSuccessfulBatchTimestamp` | Timestamp dell’ultima acquisizione batch riuscita. |
| `streamingDriven` | *Questo campo è stato dichiarato obsoleto e non contiene alcun significato per la risposta.* |
| `totalRows` | Numero totale di profili uniti in Experience Platform, noto anche come &quot;conteggio dei profili&quot;. |
| `lastBatchId` | ID dell’ultima acquisizione batch. |
| `status` | Stato dell’ultimo campione. |
| `samplingRatio` | Rapporto tra i profili uniti campionati (`numRowsToRead`) e i profili uniti totali (`totalRows`), espresso come percentuale in formato decimale. |
| `mergeStrategy` | Strategia di unione utilizzata nell&#39;esempio. |
| `lastSampledTimestamp` | Timestamp dell’ultimo esempio riuscito. |

## Elenca distribuzione profilo per set di dati

Per visualizzare la distribuzione dei profili per set di dati, è possibile eseguire una richiesta GET all&#39;endpoint `/previewsamplestatus/report/dataset`.

**Formato API**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parametro | Descrizione |
|---|---|
| `date` | Specifica la data del rapporto da restituire. Se in tale data sono stati eseguiti più rapporti, viene restituito il rapporto più recente per tale data. Se non esiste un report per la data specificata, viene restituito un errore 404 (Non trovato). Se non viene specificata alcuna data, viene restituito il rapporto più recente. Formato: AAAA-MM-GG. Esempio: `date=2024-12-31` |

**Richiesta**

La richiesta seguente utilizza il parametro `date` per restituire il rapporto più recente per la data specificata.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

La risposta include un array `data`, contenente un elenco di oggetti set di dati. La risposta mostrata è stata troncata per mostrare tre set di dati.

>[!NOTE]
>
>Se esistono più rapporti per la data, viene restituito solo l’ultimo rapporto. Se non esiste un rapporto di set di dati per la data specificata, viene restituito lo stato HTTP 404 (Non trovato).

```json
{
  "data": [
    {
      "sampleCount": 12577,
      "samplePercentage": 0.306734,
      "fullIDsCount": 20988,
      "fullIDsPercentage": 0.511865,
      "name": "CRM Profiles",
      "description": "Profiles from the CRM.",
      "value": "5f160106be34361915754b9c",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697",
    },
    {
      "sampleCount": 12938,
      "samplePercentage": 0.315538,
      "fullIDsCount": 21796,
      "fullIDsPercentage": 0.531571,
      "name": "AAM Authenticated Profiles",
      "description": "This data set contains AAM authenticated profiles.",
      "value": "5dc77ec6eed47f18a796ca90",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    },
    {
      "sampleCount": 22725,
      "samplePercentage": 0.554228,
      "fullIDsCount": 41003,
      "fullIDsPercentage": 1.0,
      "name": "Loyalty Program Members",
      "description": "Members of the loyalty program at all levels.",
      "value": "5d0fda92274e55144d4de620",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| Proprietà | Descrizione |
|---|---|
| `sampleCount` | Numero totale di profili uniti campionati con questo ID set di dati. |
| `samplePercentage` | `sampleCount` come percentuale del numero totale di profili uniti campionati (il valore `numRowsToRead` restituito nel [ultimo stato campione](#view-last-sample-status)), espresso in formato decimale. |
| `fullIDsCount` | Numero totale di profili uniti con questo ID set di dati. |
| `fullIDsPercentage` | `fullIDsCount` come percentuale del numero totale di profili uniti (il valore `totalRows` restituito nell&#39;[ultimo stato campione](#view-last-sample-status)), espresso in formato decimale. |
| `name` | Nome del set di dati, fornito durante la creazione del set di dati. |
| `description` | Descrizione del set di dati, fornita durante la creazione del set di dati. |
| `value` | ID del set di dati. |
| `streamingIngestionEnabled` | Se il set di dati è abilitato per l’acquisizione in streaming. |
| `createdUser` | ID utente dell’utente che ha creato il set di dati. |
| `reportTimestamp` | Il timestamp del rapporto. Se durante la richiesta è stato fornito un parametro `date`, il rapporto restituito si riferisce alla data specificata. Se non viene fornito alcun parametro `date`, viene restituito il report più recente. |

## Distribuzione del profilo di elenco per spazio dei nomi delle identità

È possibile eseguire una richiesta di GET all&#39;endpoint `/previewsamplestatus/report/namespace` per visualizzare la suddivisione per spazio dei nomi identità in tutti i profili uniti nell&#39;archivio profili. Sono incluse sia le identità standard fornite da Adobe, sia le identità personalizzate definite dall’organizzazione.

Gli spazi dei nomi di identità sono un componente importante del servizio Adobe Experience Platform Identity che fungono da indicatori del contesto a cui si riferiscono i dati dei clienti. Per ulteriori informazioni, leggere la [panoramica dello spazio dei nomi delle identità](../../identity-service/features/namespaces.md).

>[!NOTE]
>
>Il numero totale di profili per spazio dei nomi (sommando i valori mostrati per ciascuno spazio dei nomi) può essere maggiore della metrica del conteggio dei profili, perché un profilo può essere associato a più spazi dei nomi. Ad esempio, se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente verranno associati più spazi dei nomi.

**Formato API**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Parametro | Descrizione |
|---|---|
| `date` | Specifica la data del rapporto da restituire. Se in tale data sono stati eseguiti più rapporti, viene restituito il rapporto più recente per tale data. Se non esiste un report per la data specificata, viene restituito un errore 404 (Non trovato). Se non viene specificata alcuna data, viene restituito il rapporto più recente. Formato: AAAA-MM-GG. Esempio: `date=2024-12-31` |

**Richiesta**

La richiesta seguente non specifica un parametro `date` e pertanto restituirà il report più recente.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

La risposta include un array `data`, con singoli oggetti contenenti i dettagli di ogni spazio dei nomi. La risposta mostrata è stata troncata per mostrare quattro spazi dei nomi.

```json
{
  "data": [
    {
      "sampleCount": 12148,
      "samplePercentage": 0.296271,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 13141,
      "fullIDsCount": 12631,
      "fullIDsPercentage": 0.308051,
      "code": "Email",
      "value": "6"
    },
    {
      "sampleCount": 6989,
      "samplePercentage": 0.170451,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 7543,
      "fullIDsCount": 7042,
      "fullIDsPercentage": 0.171744,
      "code": "ECID",
      "value": "4"
    },
    {
      "sampleCount": 888,
      "samplePercentage": 0.021657,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 3801,
      "fullIDsCount": 3206,
      "fullIDsPercentage": 0.078189,
      "code": "AAID",
      "value": "10"
    },
    {
      "sampleCount": 21809,
      "samplePercentage": 0.531888,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 27023,
      "fullIDsCount": 21936,
      "fullIDsPercentage": 0.534985,
      "code": "Phone",
      "value": "7"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| Proprietà | Descrizione |
|---|---|
| `sampleCount` | Numero totale di profili uniti campionati nello spazio dei nomi. |
| `samplePercentage` | `sampleCount` come percentuale dei profili uniti campionati (il valore `numRowsToRead` restituito nel [ultimo stato campione](#view-last-sample-status)), espresso in formato decimale. |
| `reportTimestamp` | Il timestamp del rapporto. Se durante la richiesta è stato fornito un parametro `date`, il rapporto restituito si riferisce alla data specificata. Se non viene fornito alcun parametro `date`, viene restituito il report più recente. |
| `fullIDsFragmentCount` | Numero totale di frammenti di profilo nello spazio dei nomi. |
| `fullIDsCount` | Numero totale di profili uniti nello spazio dei nomi. |
| `fullIDsPercentage` | Il `fullIDsCount` come percentuale del totale dei profili uniti (il valore `totalRows` restituito nel [ultimo stato campione](#view-last-sample-status)), espresso in formato decimale. |
| `code` | `code` per lo spazio dei nomi. Questo si trova quando si lavora con spazi dei nomi utilizzando l&#39;[API del servizio Adobe Experience Platform Identity](../../identity-service/api/list-namespaces.md) ed è anche indicato come [!UICONTROL simbolo di identità] nell&#39;interfaccia utente di Experience Platform. Per ulteriori informazioni, visita la [panoramica dello spazio dei nomi delle identità](../../identity-service/features/namespaces.md). |
| `value` | Il valore `id` per lo spazio dei nomi. Questo problema si verifica quando si lavora con spazi dei nomi utilizzando l&#39;[API del servizio Identity](../../identity-service/api/list-namespaces.md). |

## Generare il rapporto di sovrapposizione del set di dati

Il rapporto di sovrapposizione dei set di dati fornisce visibilità sulla composizione dell’archivio profili della tua organizzazione esponendo i set di dati che contribuiscono maggiormente al pubblico indirizzabile (profili uniti). Oltre a fornire informazioni approfondite sui dati, questo rapporto può aiutarti a intraprendere azioni per ottimizzare l’utilizzo della licenza, ad esempio impostare le scadenze per determinati set di dati.

È possibile generare il report di sovrapposizione del set di dati eseguendo una richiesta di GET all&#39;endpoint `/previewsamplestatus/report/dataset/overlap`.

Per istruzioni dettagliate su come generare il report di sovrapposizione dei set di dati utilizzando la riga di comando o l&#39;interfaccia utente di Postman, consulta l&#39;[esercitazione sulla generazione del report di sovrapposizione dei set di dati](../tutorials/dataset-overlap-report.md).

**Formato API**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| Parametro | Descrizione |
|---|---|
| `date` | Specifica la data del rapporto da restituire. Se più rapporti sono stati eseguiti nella stessa data, viene restituito il rapporto più recente per tale data. Se non esiste un report per la data specificata, viene restituito un errore 404 (Non trovato). Se non viene specificata alcuna data, viene restituito il rapporto più recente. Formato: AAAA-MM-GG. Esempio: `date=2024-12-31` |

**Richiesta**

La richiesta seguente utilizza il parametro `date` per restituire il rapporto più recente per la data specificata.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Risposta**

In caso di esito positivo, la richiesta restituisce lo stato HTTP 200 (OK) e il rapporto di sovrapposizione dei set di dati.

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-12-29T19:55:31.147"
}
```

| Proprietà | Descrizione |
|---|---|
| `data` | L&#39;oggetto `data` contiene elenchi separati da virgole di set di dati e i rispettivi conteggi dei profili. |
| `reportTimestamp` | Il timestamp del rapporto. Se durante la richiesta è stato fornito un parametro `date`, il rapporto restituito si riferisce alla data specificata. Se non viene fornito alcun parametro `date`, viene restituito il report più recente. |

### Interpretazione del rapporto di sovrapposizione dei set di dati

I risultati del rapporto possono essere interpretati dai set di dati e dai conteggi dei profili nella risposta. Considerare l&#39;oggetto report `data` di esempio seguente:

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Questo rapporto fornisce le seguenti informazioni:

* Sono presenti 123 profili composti da dati provenienti dai seguenti set di dati: `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Sono presenti 454.412 profili composti da dati provenienti da questi due set di dati: `5d92921872831c163452edc8` e `5eb2cdc6fa3f9a18a7592a98`.
* Esistono 107 profili composti solo da dati del set di dati `5eeda0032af7bb19162172a7`.
* Nell’organizzazione sono presenti in totale 454.642 profili.

## Genera il report di sovrapposizione dello spazio dei nomi delle identità {#identity-overlap-report}

Il rapporto di sovrapposizione dello spazio dei nomi delle identità fornisce visibilità sulla composizione dell’archivio profili della tua organizzazione esponendo gli spazi dei nomi delle identità che contribuiscono maggiormente al pubblico indirizzabile (profili uniti). Sono inclusi sia gli spazi dei nomi di identità standard forniti da Adobe, sia gli spazi dei nomi di identità personalizzati definiti dalla tua organizzazione.

È possibile generare il report di sovrapposizione dello spazio dei nomi delle identità eseguendo una richiesta GET all&#39;endpoint `/previewsamplestatus/report/namespace/overlap`.

**Formato API**

```http
GET /previewsamplestatus/report/namespace/overlap
GET /previewsamplestatus/report/namespace/overlap?{QUERY_PARAMETERS}
```

| Parametro | Descrizione |
|---|---|
| `date` | Specifica la data del rapporto da restituire. Se più rapporti sono stati eseguiti nella stessa data, viene restituito il rapporto più recente per tale data. Se non esiste un report per la data specificata, viene restituito un errore 404 (Non trovato). Se non viene specificata alcuna data, viene restituito il rapporto più recente. Formato: AAAA-MM-GG. Esempio: `date=2024-12-31` |

**Richiesta**

La richiesta seguente utilizza il parametro `date` per restituire il rapporto più recente per la data specificata.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Risposta**

In caso di esito positivo, la richiesta restituisce lo stato HTTP 200 (OK) e il rapporto di sovrapposizione dello spazio dei nomi dell’identità.

```json
{
    "data": {
        "Email,crmid,loyal": 2,
        "ECID,Email,crmid": 7,
        "ECID,Email,mobilenr": 12,
        "AAID,ECID,loyal": 1,
        "mobilenr": 25,
        "AAID,ECID": 1508,
        "ECID,crmid": 1,
        "AAID,ECID,crmid": 2,
        "Email,crmid": 328,
        "CORE": 49,
        "AAID": 446,
        "crmid,loyal": 20988,
        "Email": 10904,
        "crmid": 249,
        "ECID,Email": 74,
        "Phone": 40,
        "Email,Phone,loyal": 48,
        "AAID,AVID,ECID": 85,
        "Email,loyal": 1002,
        "AAID,ECID,Email,Phone,crmid": 5,
        "AAID,ECID,Email,crmid,loyal": 23,
        "AAID,AVID,ECID,Email,crmid": 2,
        "AVID": 3,
        "AAID,ECID,Phone": 1,
        "loyal": 43,
        "ECID,Email,crmid,loyal": 6,
        "AAID,ECID,Email,Phone,crmid,loyal": 1,
        "AAID,ECID,Email": 2,
        "AAID,ECID,Email,crmid": 142,
        "AVID,ECID": 24,
        "ECID": 6565
    },
    "reportTimestamp": "2021-12-29T16:55:03.624"
}
```

| Proprietà | Descrizione |
|---|---|
| `data` | L&#39;oggetto `data` contiene elenchi separati da virgole con combinazioni univoche di codici dello spazio dei nomi delle identità e dei rispettivi conteggi dei profili. |
| Codici dello spazio dei nomi | `code` è un formato breve per ogni nome spazio dei nomi delle identità. È possibile trovare una mappatura di ogni `code` al relativo `name` utilizzando [API del servizio Adobe Experience Platform Identity](../../identity-service/api/list-namespaces.md). `code` è anche indicato come [!UICONTROL simbolo di identità] nell&#39;interfaccia utente Experience Platform. Per ulteriori informazioni, visita la [panoramica dello spazio dei nomi delle identità](../../identity-service/features/namespaces.md). |
| `reportTimestamp` | Il timestamp del rapporto. Se durante la richiesta è stato fornito un parametro `date`, il rapporto restituito si riferisce alla data specificata. Se non viene fornito alcun parametro `date`, viene restituito il report più recente. |

### Interpretazione del rapporto di sovrapposizione dello spazio dei nomi delle identità

I risultati del rapporto possono essere interpretati dalle identità e dai conteggi dei profili nella risposta. Il valore numerico di ogni riga indica il numero di profili composti dall’esatta combinazione di spazi dei nomi di identità standard e personalizzati.

Considerare l&#39;estratto seguente dell&#39;oggetto `data`:

```json
  "AAID,ECID,Email,crmid": 142,
  "AVID,ECID": 24,
  "ECID": 6565
```

Questo rapporto fornisce le seguenti informazioni:

* Sono disponibili 142 profili composti da `AAID`, `ECID` e `Email` identità standard, nonché da uno spazio dei nomi di identità `crmid` personalizzato.
* Ci sono 24 profili composti da `AAID` e `ECID` spazi dei nomi di identità.
* Sono presenti 6.565 profili che includono solo un&#39;identità `ECID`.

## Generare il rapporto sui profili non uniti

Puoi ottenere ulteriore visibilità sulla composizione dell’archivio profili della tua organizzazione tramite il rapporto sui profili non uniti. Un profilo &quot;non unito&quot; è un profilo che contiene un solo frammento di profilo. Un profilo &quot;sconosciuto&quot; è un profilo associato a spazi dei nomi di identità pseudonimi come `ECID` e `AAID`. I profili sconosciuti sono inattivi, il che significa che non hanno aggiunto nuovi eventi per il periodo di tempo specificato. Il rapporto dei profili non uniti fornisce un raggruppamento dei profili per un periodo di 7, 30, 60, 90 e 120 giorni.

È possibile generare il report dei profili non uniti eseguendo una richiesta GET all&#39;endpoint `/previewsamplestatus/report/unstitchedProfiles`.

**Formato API**

```http
GET /previewsamplestatus/report/unstitchedProfiles
```

**Richiesta**

La richiesta seguente restituisce il rapporto dei profili non uniti.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/unstitchedProfiles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Risposta**

In caso di esito positivo, la richiesta restituisce lo stato HTTP 200 (OK) e il rapporto sui profili non uniti.

>[!NOTE]
>
>Ai fini di questa guida, il report è stato troncato per includere solo `"120days"` e &quot;`7days`&quot; periodi di tempo. Il rapporto completo dei profili non uniti fornisce un raggruppamento dei profili per un periodo di 7, 30, 60, 90 e 120 giorni.

```json
{
  "data": {
      "totalNumberOfProfiles": 63606,
      "totalNumberOfEvents": 130977,
      "unstitchedProfiles": {
          "120days": {
              "countOfProfiles": 1644,
              "eventsAssociated": 26824,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 18,
                      "eventsAssociated": 95
                  },
                  "loyal": {
                      "countOfProfiles": 26,
                      "eventsAssociated": 71
                  },
                  "ECID": {
                      "countOfProfiles": 1600,
                      "eventsAssociated": 26658
                  }
              }
          },
          "7days": {
              "countOfProfiles": 1782,
              "eventsAssociated": 29151,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 19,
                      "eventsAssociated": 97
                  },
                  "ECID": {
                      "countOfProfiles": 1734,
                      "eventsAssociated": 28591
                  },
                  "loyal": {
                      "countOfProfiles": 29,
                      "eventsAssociated": 463
                  }
              }
          }
      }
  },
  "reportTimestamp": "2025-08-25T22:14:55.186"
}
```

| Proprietà | Descrizione |
|---|---|
| `data` | L&#39;oggetto `data` contiene le informazioni restituite per il report dei profili non uniti. |
| `totalNumberOfProfiles` | Numero totale di profili univoci nell’archivio Profili. Equivale al conteggio del pubblico indirizzabile. Include profili noti e non uniti. |
| `totalNumberOfEvents` | Il numero totale di ExperienceEvents nell’archivio dei profili. |
| `unstitchedProfiles` | Oggetto contenente una suddivisione dei profili non uniti per periodo di tempo. Il rapporto dei profili non uniti fornisce un raggruppamento dei profili per periodi di tempo di 7, 30, 60, 90 e 120 giorni. |
| `countOfProfiles` | Il conteggio dei profili non uniti per il periodo di tempo o il conteggio dei profili non uniti per lo spazio dei nomi. |
| `eventsAssociated` | Il numero di ExperienceEvents per l’intervallo di tempo o il numero di eventi per lo spazio dei nomi. |
| `nsDistribution` | Oggetto contenente spazi dei nomi di identità individuali con la distribuzione di profili ed eventi non uniti per ogni spazio dei nomi. Nota: l&#39;aggiunta del totale di `countOfProfiles` per ogni spazio dei nomi delle identità nell&#39;oggetto `nsDistribution` è uguale a `countOfProfiles` per il periodo di tempo. Lo stesso vale per `eventsAssociated` per spazio dei nomi e il totale di `eventsAssociated` per periodo di tempo. |
| `reportTimestamp` | Il timestamp del rapporto. |

### Interpretazione del rapporto sui profili non uniti

I risultati del rapporto possono fornire informazioni sul numero di profili non uniti e inattivi presenti nell’archivio profili della tua organizzazione.

Considerare l&#39;estratto seguente dell&#39;oggetto `data`:

```json
  "7days": {
    "countOfProfiles": 1782,
    "eventsAssociated": 29151,
    "nsDistribution": {
      "Email": {
        "countOfProfiles": 19,
        "eventsAssociated": 97
      },
      "ECID": {
        "countOfProfiles": 1734,
        "eventsAssociated": 28591
      },
      "loyal": {
        "countOfProfiles": 29,
        "eventsAssociated": 463
      }
    }
  }
```

Questo rapporto fornisce le seguenti informazioni:

* Sono presenti 1.782 profili che contengono un solo frammento di profilo e non hanno nuovi eventi per gli ultimi sette giorni.
* Ci sono 29.151 ExperienceEvents associati ai 1.782 profili non uniti.
* Esistono 1.734 profili non uniti contenenti un singolo frammento di profilo dallo spazio dei nomi dell’identità di ECID.
* Esistono 28.591 eventi associati ai 1.734 profili non uniti che contengono un singolo frammento di profilo dallo spazio dei nomi dell’identità di ECID.

## Passaggi successivi

Ora che sai come visualizzare in anteprima i dati di esempio nell’archivio Profili ed eseguire più rapporti sui dati, puoi anche utilizzare gli endpoint di stima e anteprima dell’API del servizio di segmentazione per visualizzare informazioni di riepilogo sulle definizioni dei segmenti. Queste informazioni sono utili per isolare il pubblico previsto. Per ulteriori informazioni sull&#39;utilizzo delle anteprime e delle stime tramite l&#39;API di segmentazione, consulta la [guida dell&#39;anteprima e degli endpoint di stima](../../segmentation/api/previews-and-estimates.md).

