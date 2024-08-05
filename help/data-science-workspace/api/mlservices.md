---
keywords: Experience Platform; guida per sviluppatori; Endpoint; Data Science Area di lavoro; argomenti popolari; mlservices; API di Machine Learning di Sensei
solution: Experience Platform
title: MLServices API Endpoint
description: Un MLService è un modello addestrato pubblicato che fornisce alla tua organizzazione la possibilità di accesso e riutilizzare modelli sviluppati in precedenza. Un funzionalità chiave di MLServices è la capacità di automatizzare training e punteggio su base programmata. Le esecuzioni di training pianificate possono aiutare a mantenere l'efficienza e l'accuratezza di un modello, mentre le esecuzioni di punteggio pianificate possono garantire che vengano generate nuove informazioni in modo coerente.
role: Developer
exl-id: cd236e0b-3bfc-4d37-83eb-432f6ad5c5b6
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 2%

---

# Endpoint MLServices

>[!NOTE]
>
>Data Science Area di lavoro non è più disponibile per l&#39;acquisto.
>
>Questa documentazione è destinata ai clienti esistenti con precedenti diritti a Data Science Area di lavoro.

Un MLService è un modello addestrato pubblicato che fornisce alla tua organizzazione la possibilità di accesso e riutilizzare modelli sviluppati in precedenza. Un funzionalità chiave di MLServices è la capacità di automatizzare training e punteggio su base programmata. Le esecuzioni di training pianificate possono aiutare a mantenere l&#39;efficienza e l&#39;accuratezza di un modello, mentre le esecuzioni di punteggio pianificate possono garantire che vengano generate nuove informazioni in modo coerente.

Le pianificazioni automatizzate di formazione e punteggio sono definite con una marca temporale iniziale, una marca temporale finale e una frequenza rappresentata come [espressione cron](https://en.wikipedia.org/wiki/Cron). Le pianificazioni possono essere definite durante la [creazione di un MLService](#create-an-mlservice) o applicate da [aggiornamento di un MLService esistente](#update-an-mlservice).

## Creare un servizio MLS {#create-an-mlservice}

È possibile creare un servizio MLS eseguendo una richiesta POST e un payload che fornisca un nome per il servizio e un ID istanza MLS valido. L’istanza MLS utilizzata per creare un servizio MLS non deve necessariamente disporre di esperimenti di formazione esistenti, ma puoi scegliere di creare il servizio MLS con un modello addestrato esistente fornendo l’ID esperimento e l’ID esecuzione di formazione corrispondenti.

**Formato API**

```http
POST /mlServices
```

**Richiesta**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlServices \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingExperimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome desiderato per MLService. Il servizio corrispondente a questo servizio MLService erediterà questo valore da visualizzare nel interfaccia della raccolta servizi come nome del servizio. |
| `description` | Descrizione facoltativa per MLService. Il servizio corrispondente a questo MLService erediterà questo valore per essere visualizzato nell’interfaccia utente di Service Gallery come descrizione del servizio. |
| `mlInstanceId` | Un ID MLInstance valido. |
| `trainingDataSetId` | Un ID set di dati training che, se specificato, sostituirà l&#39;ID set di dati predefinito di MLInstance. Se MLInstance utilizzato per creare MLService non definisce un set di dati training, è necessario fornire un ID set di dati training appropriato. |
| `trainingExperimentId` | Un ID esperimento che puoi fornire facoltativamente. Se questo valore non viene fornito, creando MLService verrà creato anche un nuovo esperimento utilizzando le configurazioni predefinite di MLInstance. |
| `trainingExperimentRunId` | Un ID di esecuzione training che è possibile fornire facoltativamente. Se questo valore non viene fornito, la creazione di MLService creerà ed eseguirà anche un&#39;esecuzione training utilizzando i parametri di training predefiniti di MLInstance. |
| `trainingSchedule` | Un programmare per le esecuzioni automatizzate delle training. Se questa proprietà è definita, MLService eseguirà automaticamente le training esecuzioni su base pianificata. |
| `trainingSchedule.startTime` | Un timestamp per il quale inizieranno le esecuzioni training pianificate. |
| `trainingSchedule.endTime` | Un timestamp per il quale termineranno le esecuzioni training pianificate. |
| `trainingSchedule.cron` | Un&#39;espressione cron che definisce la frequenza delle esecuzioni automatiche delle training. |
| `scoringSchedule` | Un programmare per le esecuzioni automatiche dei punteggi. Se questa proprietà è definita, MLService eseguirà automaticamente le esecuzioni di punteggio in base alla pianificazione. |
| `scoringSchedule.startTime` | Un timestamp per il quale inizieranno le esecuzioni pianificate del punteggio. |
| `scoringSchedule.endTime` | Una marca temporale per la quale termineranno le esecuzioni pianificate del punteggio. |
| `scoringSchedule.cron` | Espressione cron che definisce la frequenza delle esecuzioni di punteggio automatizzate. |

**Risposta**

In caso di esito positivo, la risposta restituisce un payload contenente i dettagli del servizio MLS appena creato, inclusi l&#39;identificatore univoco (`id`), l&#39;ID esperimento per l&#39;addestramento (`trainingExperimentId`), l&#39;ID esperimento per il punteggio (`scoringExperimentId`) e l&#39;ID del set di dati di addestramento di input (`trainingDataSetId`).

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## Recupera un elenco di MLServices {#retrieve-a-list-of-mlservices}

È possibile recuperare un elenco di servizi MLServices eseguendo una singola richiesta GET. Per filtrare i risultati, è possibile specificare parametri di query nel percorso richiesta. Per un elenco delle query disponibili, fare riferimento alla sezione dell&#39;appendice sui [parametri di query per il recupero risorsa](./appendix.md#query).

**Formato API**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parametro | Descrizione |
| --- | --- |
| `{QUERY_PARAMETER}` | Uno dei parametri](./appendix.md#query) di query disponibili utilizzati per filtrare i [risultati. |
| `{VALUE}` | Valore del parametro di query precedente. |

**Richiesta**

Il seguente richiesta contiene una query e recupera un elenco di MLServices che condividono lo stesso ID MLInstance (`{MLINSTANCE_ID}`).

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di MLService e i relativi dettagli, inclusi il relativo ID MLService (`{MLSERVICE_ID}`), l&#39;ID esperimento per training (`{TRAINING_ID}`), l&#39;ID esperimento per il punteggio (`{SCORING_ID}`) e l&#39;ID set di dati del training di input (`{DATASET_ID}`).

```json
{
    "children": [
        {
            "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
            "name": "A service created in UI",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
            "trainingDataSetId": "5ee3cd7f2d34011913c56941",
            "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda,deleted==false",
        "count": 1
    }
}
```

## Recuperare un servizio MLS specifico {#retrieve-a-specific-mlservice}

Per recuperare i dettagli di un esperimento specifico, esegui una richiesta di GET che includa l’ID MLService desiderato nel percorso della richiesta.

**Formato API**

```http
GET /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: ID MLService valido.

**Richiesta**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli del servizio MLService richiesto.

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## Aggiornare un servizio MLService {#update-an-mlservice}

È possibile aggiornare un MLService esistente sovrascrivendone le proprietà tramite un richiesta PUT che include l&#39;ID del destinazione MLService nel percorso richiesta e fornendo un payload JSON contenente le proprietà aggiornate.

>[!TIP]
>
>Per garantire il successo di questa richiesta PUT, si consiglia innanzitutto di eseguire una richiesta GET per [recuperare MLService per ID](#retrieve-a-specific-mlservice). Quindi, modificare e aggiornare l&#39;oggetto JSON restituito e applicare l&#39;intero oggetto JSON modificato come payload per il richiesta PUT.

**Formato API**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: un ID MLService valido.

**Richiesta**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli aggiornati di MLService.

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-02T00:00:00.000Z"
}
```

## Elimina un MLService

È possibile eliminare un singolo MLService eseguendo una richiesta DELETE che include l&#39;ID del destinazione MLService nel percorso richiesta.

**Formato API**

```http
DELETE /mlServices/{MLSERVICE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MLSERVICE_ID}` | Un ID MLService valido. |

**Richiesta**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLService deletion was successful"
}
```

## Elimina MLServices per ID istanza

È possibile eliminare tutti i servizi MLS appartenenti a una particolare istanza MLInstance eseguendo una richiesta DELETE che specifica un ID istanza MLInstance come parametro query.

**Formato API**

```http
DELETE /mlServices?mlInstanceId={MLINSTANCE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MLINSTANCE_ID}` | Un ID MLInstance valido. |

**Richiesta**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "MLServices deletion was successful"
}
```
