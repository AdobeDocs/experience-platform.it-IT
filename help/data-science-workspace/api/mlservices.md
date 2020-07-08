---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Servizi
topic: Developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 2%

---


# MLServices

Un servizio MLService è un modello di formazione pubblicato che consente alla vostra azienda di accedere e riutilizzare modelli sviluppati in precedenza. Una caratteristica chiave di MLServices è la capacità di automatizzare la formazione e il punteggio su base programmata. Le sessioni di formazione pianificate possono contribuire a mantenere l&#39;efficienza e l&#39;accuratezza di un modello, mentre le esecuzioni di punteggio pianificate possono garantire la generazione coerente di nuove informazioni.

I programmi di formazione e valutazione automatizzati sono definiti con una marca temporale iniziale, una marca temporale finale e una frequenza rappresentata come espressione [](https://en.wikipedia.org/wiki/Cron)cron. Le pianificazioni possono essere definite durante la [creazione di un servizio MLService](#create-an-mlservice) o applicate [aggiornando un servizio MLService](#update-an-mlservice)esistente.

## Creare un servizio MLS {#create-an-mlservice}

Potete creare un servizio MLS eseguendo una richiesta POST e un payload che fornisce un nome per il servizio e un ID MLInvalido. L’istanza MLI utilizzata per creare un servizio MLS non è necessaria per disporre di sperimentazioni di formazione esistenti, ma potete scegliere di creare il servizio MLS con un modello già esistente fornendo l’ID di esperienza e l’ID di esecuzione della formazione corrispondenti.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Nome desiderato per MLService. Il servizio corrispondente a questo servizio MLService erediterà questo valore per essere visualizzato nell&#39;interfaccia utente della Galleria servizi come nome del servizio. |
| `description` | Una descrizione facoltativa per MLService. Il servizio corrispondente a questo servizio MLService erediterà questo valore per essere visualizzato nell&#39;interfaccia utente della Galleria servizi come descrizione del servizio. |
| `mlInstanceId` | Un ID istanza MLI valido. |
| `trainingDataSetId` | Un ID dataset di formazione che, se fornito, ignorerà l&#39;ID dataset predefinito dell&#39;istanza MLI. Se l’istanza MLI utilizzata per creare il servizio MLService non definisce un set di dati di formazione, dovete fornire un ID set di dati di formazione appropriato. |
| `trainingExperimentId` | Un ID esperimento che puoi facoltativamente fornire. Se questo valore non viene fornito, la creazione di MLService creerà anche un nuovo esperimento utilizzando le configurazioni predefinite di MLIn. |
| `trainingExperimentRunId` | Un ID di esecuzione della formazione che potete facoltativamente fornire. Se questo valore non viene fornito, la creazione di MLService creerà ed eseguirà anche un&#39;esecuzione di formazione utilizzando i parametri di formazione predefiniti di MLIn. |
| `trainingSchedule` | Viene eseguita una pianificazione per la formazione automatizzata. Se questa proprietà è definita, MLService eseguirà automaticamente la formazione in base a quanto previsto. |
| `trainingSchedule.startTime` | Una marca temporale per la quale verrà avviata la formazione pianificata. |
| `trainingSchedule.endTime` | Una marca temporale per la quale terminerà l&#39;esecuzione della formazione pianificata. |
| `trainingSchedule.cron` | Un&#39;espressione cron che definisce la frequenza delle esecuzioni di formazione automatizzate. |
| `scoringSchedule` | Programmazione per l&#39;esecuzione automatica del punteggio. Se questa proprietà è definita, MLService eseguirà automaticamente l&#39;esecuzione del punteggio su base programmata. |
| `scoringSchedule.startTime` | Marca temporale per la quale verrà avviata l&#39;esecuzione del punteggio pianificato. |
| `scoringSchedule.endTime` | Una marca temporale per la quale terminerà l&#39;esecuzione del punteggio pianificato. |
| `scoringSchedule.cron` | Espressione cron che definisce la frequenza delle esecuzioni di punteggio automatizzate. |

**Risposta**

Una risposta di successo restituisce un payload contenente i dettagli del servizio MLService appena creato, incluso il relativo identificatore univoco (`id`), ID esperimento per la formazione (`trainingExperimentId`), ID esperimento per il punteggio (`scoringExperimentId`) e ID set di dati per la formazione in input (`trainingDataSetId`).

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

## Recuperare un elenco di MLServices {#retrieve-a-list-of-mlservices}

È possibile recuperare un elenco di MLServices eseguendo una singola richiesta GET. Per facilitare il filtraggio dei risultati, potete specificare i parametri di query nel percorso di richiesta. Per un elenco delle query disponibili, consultate la sezione appendice sui parametri delle [query per il recupero](./appendix.md#query)delle risorse.

**Formato API**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parametro | Descrizione |
| --- | --- |
| `{QUERY_PARAMETER}` | Uno dei parametri [di query](./appendix.md#query) disponibili utilizzati per filtrare i risultati. |
| `{VALUE}` | Il valore del parametro di query precedente. |

**Richiesta**

La richiesta seguente contiene una query e recupera un elenco di MLServices che condividono lo stesso ID istanza (`{MLINSTANCE_ID}`).

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta di successo restituisce un elenco di MLServices con i relativi dettagli, inclusi MLService ID (`{MLSERVICE_ID}`), Experience ID for Training (`{TRAINING_ID}`), Experience ID for Scoring (`{SCORING_ID}`) e l&#39;ID del set di dati per la formazione in input (`{DATASET_ID}`).

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

## Recuperare un servizio MLService specifico {#retrieve-a-specific-mlservice}

Potete recuperare i dettagli di un esperimento specifico eseguendo una richiesta GET che include l&#39;ID del servizio MLS desiderato nel percorso della richiesta.

**Formato API**

```http
GET /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: Un ID MLService valido.

**Richiesta**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Potete aggiornare un servizio MLS esistente sovrascrivendone le proprietà tramite una richiesta PUT che include l&#39;ID del servizio MLService di destinazione nel percorso della richiesta e fornisce un payload JSON contenente le proprietà aggiornate.

>[!TIP]
>
>Per garantire il successo di questa richiesta PUT, si consiglia innanzitutto di eseguire una richiesta GET per [recuperare il servizio MLService per ID](#retrieve-a-specific-mlservice). Quindi, modificate e aggiornate l&#39;oggetto JSON restituito e applicate l&#39;intero oggetto JSON modificato come payload per la richiesta PUT.

**Formato API**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: Un ID MLService valido.

**Richiesta**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

## Eliminare un servizio MLS

È possibile eliminare un singolo servizio MLS eseguendo una richiesta DELETE che include l&#39;ID del servizio MLService di destinazione nel percorso della richiesta.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

## Eliminazione di MLServices per ID istanza

Potete eliminare tutti i servizi MLS appartenenti a una particolare istanza MLIneseguendo una richiesta DELETE che specifica un ID MLIncome parametro di query.

**Formato API**

```http
DELETE /mlServices?mlInstanceId={MLINSTANCE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MLINSTANCE_ID}` | Un ID istanza MLI valido. |

**Richiesta**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
