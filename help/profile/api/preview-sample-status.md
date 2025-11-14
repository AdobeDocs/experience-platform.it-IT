---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;anteprima;esempio
title: Anteprima endpoint API di stato campione (anteprima profilo)
description: L’endpoint per lo stato di anteprima del campione dell’API Real-Time Customer Profile ti consente di visualizzare in anteprima l’ultimo campione riuscito dei dati del profilo, di elencare la distribuzione del profilo per set di dati e per identità e di generare rapporti che mostrano la sovrapposizione dei set di dati, la sovrapposizione delle identità e i profili non uniti.
role: Developer
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: bb2cfb479031f9e204006ba489281b389e6c6c04
workflow-type: tm+mt
source-wordcount: '2306'
ht-degree: 1%

---

# Endpoint dello stato del campione di anteprima (anteprima profilo)

Adobe Experience Platform consente di acquisire i dati dei clienti da più origini per creare un profilo solido e unificato per ciascuno dei singoli clienti. Quando i dati vengono acquisiti in Experience Platform, viene eseguito un processo di esempio per aggiornare il conteggio dei profili e altre metriche relative ai dati del profilo cliente in tempo reale.

I risultati di questo processo di esempio possono essere visualizzati utilizzando l&#39;endpoint `/previewsamplestatus`, parte dell&#39;API Real-Time Customer Profile. Questo endpoint può essere utilizzato anche per elencare le distribuzioni di profilo per set di dati e spazio dei nomi delle identità, nonché per generare più rapporti al fine di ottenere visibilità nella composizione dell’archivio profili della tua organizzazione. Questa guida descrive i passaggi necessari per visualizzare queste metriche utilizzando l&#39;endpoint API `/previewsamplestatus`.

>[!NOTE]
>
>Nell’API del servizio di segmentazione di Adobe Experience Platform sono disponibili endpoint per la stima e l’anteprima che consentono di visualizzare informazioni di riepilogo sulle definizioni dei segmenti per poter isolare il pubblico previsto. Per informazioni dettagliate sull&#39;utilizzo degli endpoint di anteprima e stima, visitare la [guida delle anteprime e delle stime degli endpoint](../../segmentation/api/previews-and-estimates.md), parte della guida per gli sviluppatori API [!DNL Segmentation].

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39;[[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Prima di continuare, consulta la [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API [!DNL Experience Platform].

## Frammenti di profilo e profili uniti

Questa guida fa riferimento sia a &quot;frammenti di profilo&quot; che a &quot;profili uniti&quot;. È importante comprendere la differenza tra questi termini prima di procedere.

Ogni singolo profilo cliente è composto da più frammenti di profilo che sono stati uniti per formare un’unica vista di quel cliente. Ad esempio, se un cliente interagisce con il tuo marchio su più canali, è probabile che la tua organizzazione disponga di più frammenti di profilo relativi a quel singolo cliente che compaiono in più set di dati.

Quando i frammenti di profilo vengono acquisiti in Experience Platform, vengono uniti insieme (in base a un criterio di unione) per creare un singolo profilo per quel cliente. Pertanto, è probabile che il numero totale di frammenti di profilo sia sempre superiore al numero totale di profili uniti, in quanto ogni profilo è composto da più frammenti.

Per ulteriori informazioni sui profili e sul loro ruolo in Experience Platform, consulta la [Panoramica sul profilo cliente in tempo reale](../home.md).

## Modalità di attivazione del processo di esempio

Poiché i dati abilitati per Real-Time Customer Profile vengono acquisiti in [!DNL Experience Platform], vengono memorizzati nell&#39;archivio dati del profilo. Quando l’acquisizione dei record nell’archivio profili aumenta o diminuisce il conteggio totale dei profili di oltre il 3%, viene attivato un processo di campionamento per aggiornare il conteggio. Il modo in cui il campione viene attivato dipende dal tipo di acquisizione utilizzata:

* Per **flussi di lavoro di dati in streaming**, viene eseguito un controllo su base oraria per determinare se la soglia di aumento o di diminuzione del 3% è stata raggiunta. In caso affermativo, viene attivato automaticamente un processo di esempio per aggiornare il conteggio.
* Per l&#39;**acquisizione batch**, entro 15 minuti dalla corretta acquisizione di un batch nell&#39;archivio profili, se viene raggiunta la soglia di aumento o riduzione del 3%, viene eseguito un processo per aggiornare il conteggio. Utilizzando l’API di profilo è possibile visualizzare in anteprima l’ultimo processo di esempio riuscito, nonché elencare la distribuzione del profilo per set di dati e per spazio dei nomi dell’identità.

Il conteggio dei profili e i profili per metrica dello spazio dei nomi sono disponibili anche nella sezione [!UICONTROL Profiles] dell’interfaccia utente di Experience Platform. Per informazioni su come accedere ai dati del profilo tramite l&#39;interfaccia utente, visitare la [[!DNL Profile] guida dell&#39;interfaccia utente](../ui/user-guide.md).

## Visualizza ultimo stato del campione {#view-last-sample-status}

Per visualizzare i dettagli dell&#39;ultimo processo di esempio eseguito correttamente per l&#39;organizzazione, eseguire una richiesta GET all&#39;endpoint `/previewsamplestatus`. Questo rapporto include il numero totale di profili nel campione, nonché la metrica di conteggio dei profili o il numero totale di profili di cui dispone la tua organizzazione in Experience Platform.

Il conteggio dei profili viene generato dopo l’unione dei frammenti di profilo per formare un singolo profilo per ogni singolo cliente. In altre parole, quando i frammenti di profilo vengono uniti tra loro, viene restituito un conteggio di &quot;1&quot; profilo perché sono tutti correlati allo stesso individuo.

Il conteggio dei profili include anche profili con attributi (dati record) e profili contenenti solo dati di serie temporali (eventi), come i profili di Adobe Analytics. Il processo di esempio viene aggiornato regolarmente man mano che vengono acquisiti i dati del profilo, in modo da fornire un numero totale aggiornato di profili all’interno di Experience Platform.

**Formato API**

```http
GET /previewsamplestatus
```

**Richiesta**

+++ Richiesta di esempio per visualizzare lo stato dell’ultimo campione.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 e include i dettagli dell’ultimo processo di esempio eseguito correttamente per l’organizzazione.

+++ Risposta di esempio contenente lo stato dell’ultimo campione.

>[!NOTE]
>
>In questo esempio di risposta, `numRowsToRead` e `totalRows` sono uguali tra loro. Questo può accadere in base al numero di profili di cui dispone la tua organizzazione in Experience Platform. Tuttavia, in genere questi due numeri sono diversi, con `numRowsToRead` che è il numero minore perché rappresenta il campione come sottoinsieme del numero totale di profili (`totalRows`).

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
  "docCount": "\"300803\"",
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
| -------- | ----------- |
| `numRowsToRead` | Numero totale di profili uniti nel campione. |
| `sampleJobRunning` | Valore booleano che restituisce `true` quando è in corso un processo di esempio. Fornisce trasparenza nella latenza che si verifica quando un file batch viene caricato in quando viene effettivamente aggiunto all’archivio profili. |
| `docCount` | Numero totale di documenti nel database. |
| `totalFragmentCount` | Numero totale di frammenti di profilo nell’archivio Profili. |
| `lastSuccessfulBatchTimestamp` | Timestamp dell’ultima acquisizione batch riuscita. |
| `streamingDriven` | *Questo campo è stato dichiarato obsoleto e non contiene alcun significato per la risposta.* |
| `totalRows` | Numero totale di profili uniti in Experience Platform, noto anche come conteggio dei profili. |
| `lastBatchId` | ID dell’ultima acquisizione batch. |
| `status` | Stato dell’ultimo campione. |
| `samplingRatio` | Rapporto tra i profili uniti campionati (`numRowsToRead`) e i profili uniti totali (`totalRows`), espresso come percentuale in formato decimale. |
| `mergeStrategy` | Strategia di unione utilizzata nell&#39;esempio. |
| `lastSampledTimestamp` | Timestamp dell’ultimo esempio riuscito. |

+++

## Elenca distribuzione profilo per set di dati

Per visualizzare la distribuzione dei profili per set di dati, devi eseguire una richiesta GET all&#39;endpoint `/previewsamplestatus/report/dataset`.

**Formato API**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parametri query | Descrizione | Esempio |
| --------------- | ----------- | ------- |
| `date` | Specifica la data del rapporto da restituire. Se in tale data sono stati eseguiti più rapporti, viene restituito il rapporto più recente per tale data. Se non esiste un report per la data specificata, viene restituito un errore 404 (Non trovato). Se non viene specificata alcuna data, viene restituito il rapporto più recente. Formato: AAAA-MM-GG. | `date=2024-12-31` |

**Richiesta**

La richiesta seguente utilizza il parametro `date` per restituire il rapporto più recente per la data specificata.

+++ Una richiesta di esempio per recuperare la distribuzione del profilo per set di dati.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Risposta**

>[!NOTE]
>
>Se esistono più rapporti per la data, viene restituito solo l’ultimo rapporto. Se non esiste un rapporto di set di dati per la data specificata, viene restituito lo stato HTTP 404 (Non trovato).

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 e include un array `data`, contenente un elenco di oggetti set di dati.

+++ Risposta di esempio contenente gli oggetti set di dati più recenti.

>[!NOTE]
>
>La seguente risposta è stata troncata per mostrare tre set di dati.

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
| -------- | ----------- |
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

+++

## Distribuzione del profilo di elenco per spazio dei nomi delle identità

È possibile eseguire una richiesta GET all&#39;endpoint `/previewsamplestatus/report/namespace` per visualizzare la suddivisione per spazio dei nomi identità in tutti i profili uniti nell&#39;archivio profili. Sono incluse sia le identità standard fornite da Adobe, sia quelle personalizzate definite dalla tua organizzazione.

Gli spazi dei nomi di identità sono un componente importante del servizio Adobe Experience Platform Identity che fungono da indicatori del contesto a cui si riferiscono i dati dei clienti. Per ulteriori informazioni, leggere la [panoramica dello spazio dei nomi delle identità](../../identity-service/features/namespaces.md).

>[!NOTE]
>
>Il numero totale di profili per spazio dei nomi (sommando i valori mostrati per ciascuno spazio dei nomi) può essere maggiore della metrica del conteggio dei profili, perché un profilo può essere associato a più spazi dei nomi. Ad esempio, se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente verranno associati più spazi dei nomi.

**Formato API**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Parametri query | Descrizione | Esempio |
| --------------- | ----------- | ------- |
| `date` | Specifica la data del report da restituire. Se in tale data sono stati eseguiti più rapporti, viene restituito il rapporto più recente per tale data. Se non esiste un report per la data specificata, viene restituito un errore 404 (Non trovato). Se non viene specificata alcuna data, viene restituito il rapporto più recente. Formato: `YYYY-MM-DD`. | `date=2025-6-20` |

**Richiesta**

La richiesta seguente non specifica un parametro `date` e restituirà il report più recente.

+++ Una richiesta di esempio per restituire il rapporto più recente per la distribuzione del profilo per spazio dei nomi. 

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 e include un array `data`, con singoli oggetti contenenti i dettagli di ogni spazio dei nomi. La risposta mostrata è stata troncata per mostrare quattro spazi dei nomi.

+++ Una risposta di esempio contiene informazioni sulla distribuzione del profilo per spazio dei nomi.

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
| -------- | ----------- |
| `sampleCount` | Numero totale di profili uniti campionati nello spazio dei nomi. |
| `samplePercentage` | `sampleCount` come percentuale dei profili uniti campionati (il valore `numRowsToRead` restituito nel [ultimo stato campione](#view-last-sample-status)), espresso in formato decimale. |
| `reportTimestamp` | Il timestamp del rapporto. Se durante la richiesta è stato fornito un parametro `date`, il rapporto restituito si riferisce alla data specificata. Se non viene fornito alcun parametro `date`, viene restituito il report più recente. |
| `fullIDsFragmentCount` | Numero totale di frammenti di profilo nello spazio dei nomi. |
| `fullIDsCount` | Numero totale di profili uniti nello spazio dei nomi. |
| `fullIDsPercentage` | Il `fullIDsCount` come percentuale del totale dei profili uniti (il valore `totalRows` restituito nel [ultimo stato campione](#view-last-sample-status)), espresso in formato decimale. |
| `code` | `code` per lo spazio dei nomi. Questo si può trovare quando si lavora con gli spazi dei nomi utilizzando l&#39;[API del servizio Adobe Experience Platform Identity](../../identity-service/api/list-namespaces.md) ed è anche indicato come [!UICONTROL Identity symbol] nell&#39;interfaccia utente di Experience Platform. Per ulteriori informazioni, visita la [panoramica dello spazio dei nomi delle identità](../../identity-service/features/namespaces.md). |
| `value` | Il valore `id` per lo spazio dei nomi. Questo problema si verifica quando si lavora con spazi dei nomi utilizzando l&#39;[API del servizio Identity](../../identity-service/api/list-namespaces.md). |

+++

## Elencare le statistiche del set di dati {#dataset-stats}

È possibile generare un report che fornisca statistiche sul set di dati effettuando una richiesta GET all&#39;endpoint `/previewsamplestatus/report/dataset_stats`.

**Formato API**

```http
GET /previewsamplestatus/report/dataset_stats
```

**Richiesta**

+++ Richiesta di esempio per generare il rapporto sulle statistiche dei set di dati.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset_stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni sulle statistiche del set di dati.

+++ Una risposta di esempio che contiene informazioni sulle statistiche del set di dati.

>[!NOTE]
>
>La seguente risposta è stata troncata per mostrare tre set di dati.

```json
{
    "data": [
        {
            "120days": 4,
            "14days": 4,
            "30days": 4,
            "365days": 4,
            "60days": 4,
            "7days": 4,
            "90days": 4,
            "datasetId": "{DATASET_ID}",
            "datasetType": "ExperienceEvents",
            "percentEvents": 0.0,
            "percentProfiles": 0.0,
            "profileFragments": 1,
            "records": 4,
            "totalProfiles": 1
        },
        {
            "120days": 155435837,
            "14days": 32888631,
            "30days": 66496282,
            "365days": 155435837,
            "60days": 116433804,
            "7days": 18202004,
            "90days": 155435837,
            "datasetId": "{DATASET_ID}",
            "datasetType": "ExperienceEvents",
            "percentEvents": 16.0,
            "percentProfiles": 0.0,
            "profileFragments": 5410745,
            "records": 155435837,
            "totalProfiles": 4524723
        },
        {
            "120days": 0,
            "14days": 0,
            "30days": 0,
            "365days": 0,
            "60days": 0,
            "7days": 0,
            "90days": 0,
            "datasetId": "{DATASET_ID}",
            "datasetType": "Profiles",
            "percentEvents": 0.0,
            "percentProfiles": 0.0,
            "profileFragments": 3589,
            "records": 3589,
            "totalProfiles": 3589
        }
    ],
    "reportTimestamp": "2025-10-29T16:20:18.956"
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `120days` | Il numero di record che rimarranno nel set di dati dopo una scadenza di 120 giorni. |
| `14days` | Il numero di record che rimarranno nel set di dati dopo una scadenza di 14 giorni. |
| `30days` | Il numero di record che rimarranno nel set di dati dopo una scadenza di 30 giorni. |
| `365days` | Il numero di record che rimarranno nel set di dati dopo una scadenza dei dati di 365 giorni. |
| `60days` | Il numero di record che rimarranno nel set di dati dopo una scadenza dei dati di 60 giorni. |
| `7days` | Il numero di record che rimarranno nel set di dati dopo una scadenza di dati di 7 giorni. |
| `90days` | Il numero di record che rimarranno nel set di dati dopo una scadenza di 90 giorni. |
| `datasetId` | ID del set di dati. |
| `datasetType` | Il tipo di set di dati. Questo valore può essere `Profiles` o `ExperienceEvents`. |
| `percentEvents` | Percentuale di record Experience Events all’interno del set di dati. |
| `percentProfiles` | Percentuale di record Profilo all’interno del set di dati. |
| `profileFragments` | Numero totale di frammenti di profilo presenti nel set di dati. |
| `records` | Numero totale di record di profilo acquisiti nel set di dati. |
| `totalProfiles` | Numero totale di profili acquisiti nel set di dati. |

+++

## Ottieni la dimensione del set di dati {#character-count}

Puoi utilizzare questo endpoint per ottenere la dimensione del set di dati in byte settimana per settimana.

**Formato API**

```http
GET /previewsamplestatus/report/character_count
```

**Richiesta**

+++Richiesta di esempio per generare il rapporto sul conteggio dei caratteri.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/character_count \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni sulle dimensioni del set di dati nel corso delle settimane.

+++ Una risposta di esempio che contiene informazioni sulle dimensioni del set di dati dopo la scadenza dei dati.

>[!NOTE]
>
>La seguente risposta è stata troncata per mostrare tre set di dati.

```json
{
    "data": [
        {
            "datasetIds": [
                {
                    "datasetId": "67aba91a453f7d298cd2a643",
                    "recordType": "keyvalue",
                    "weeks": [
                        {
                            "size": 107773533894,
                            "week": "2025-10-26"
                        }
                    ]
                },
                {
                    "datasetId": "67aa6c867c3110298b017f0e",
                    "recordType": "timeseries",
                    "weeks": [
                        {
                            "size": 242902062440,
                            "week": "2025-10-26"
                        },
                        {
                            "size": 837539413062,
                            "week": "2025-10-19"
                        },
                        {
                            "size": 479253986484,
                            "week": "2025-10-12"
                        },
                        {
                            "size": 358911988990,
                            "week": "2025-10-05"
                        },
                        {
                            "size": 349701073042,
                            "week": "2025-09-28"
                        }
                    ]
                },
                {
                    "datasetId": "680c043667c0d7298c9ea275",
                    "recordType": "keyvalue",
                    "weeks": [
                        {
                            "size": 18392459832,
                            "week": "2025-10-26"
                        }
                    ]
                }
            ],
            "modelName": "_xdm.context.profile",
            "reportTimestamp": "2025-10-30T00:28:30.069Z"
        }
    ],
    "reportTimestamp": "2025-10-30T00:28:30.069Z"
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `datasetId` | ID del set di dati. |
| `recordType` | Tipo di dati all’interno del set di dati. Il tipo di record influisce sul valore della variabile `weeks`. I valori supportati includono `keyvalue` e `timeseries`. |
| `weeks` | Matrice contenente le informazioni sulle dimensioni del set di dati. Per i set di dati di tipo record `keyvalue`, contiene la settimana più recente e le dimensioni totali del set di dati in byte. Per i set di dati di tipo record `timeseries`, contiene ogni settimana dall&#39;acquisizione del set di dati alla settimana più recente e le dimensioni totali del set di dati in byte per ciascuna di tali settimane. |
| `modelName` | Nome del modello per il set di dati. I valori possibili includono `_xdm.context.profile` e `_xdm.context.experienceevent`. |
| `reportTimestamp` | La data e l’ora in cui è stato generato il rapporto. |

+++

## Passaggi successivi

Ora che sai come visualizzare in anteprima i dati di esempio nell’archivio Profili ed eseguire più rapporti sui dati, puoi anche utilizzare gli endpoint di stima e anteprima dell’API del servizio di segmentazione per visualizzare informazioni di riepilogo sulle definizioni dei segmenti. Queste informazioni sono utili per isolare il pubblico previsto. Per ulteriori informazioni sull&#39;utilizzo delle anteprime e delle stime tramite l&#39;API di segmentazione, consulta la [guida dell&#39;anteprima e degli endpoint di stima](../../segmentation/api/previews-and-estimates.md).

