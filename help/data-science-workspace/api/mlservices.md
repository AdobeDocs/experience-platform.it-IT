---
keywords: Experience Platform;guida per sviluppatori;endpoint;Data Science Workspace;argomenti popolari;mlservices;api di apprendimento automatico sensei
solution: Experience Platform
title: Endpoint API MLServices
description: Un servizio MLService è un modello di formazione pubblicato che consente alla tua organizzazione di accedere e riutilizzare modelli sviluppati in precedenza. Una caratteristica chiave di MLServices è la capacità di automatizzare la formazione e il punteggio su base programmata. Le esecuzioni programmate dei corsi di formazione possono contribuire a mantenere l'efficienza e l'accuratezza del modello, mentre le esecuzioni programmate dei punteggi possono garantire la generazione coerente di nuove informazioni.
exl-id: cd236e0b-3bfc-4d37-83eb-432f6ad5c5b6
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 2%

---

# Endpoint MLServices

Un servizio MLService è un modello di formazione pubblicato che consente alla tua organizzazione di accedere e riutilizzare modelli sviluppati in precedenza. Una caratteristica chiave di MLServices è la capacità di automatizzare la formazione e il punteggio su base programmata. Le esecuzioni programmate dei corsi di formazione possono contribuire a mantenere l&#39;efficienza e l&#39;accuratezza del modello, mentre le esecuzioni programmate dei punteggi possono garantire la generazione coerente di nuove informazioni.

I programmi di formazione e valutazione automatizzati sono definiti con una marca temporale iniziale, una marca temporale finale e una frequenza rappresentata come [espressione cron](https://en.wikipedia.org/wiki/Cron). Le pianificazioni possono essere definite quando [creazione di un servizio MLS](#create-an-mlservice) o applicati da [aggiornamento di un servizio MLService esistente](#update-an-mlservice).

## Creare un servizio MLS {#create-an-mlservice}

Puoi creare un servizio MLS eseguendo una richiesta POST e un payload che fornisce un nome per il servizio e un ID istanza MLI valido. L’istanza MLI utilizzata per creare un servizio MLS non è necessaria per disporre di esperimenti di formazione esistenti, ma puoi scegliere di creare il servizio MLService con un modello addestrato esistente fornendo il corrispondente ID di esperimento e l’ID di esecuzione della formazione.

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
| `name` | Nome desiderato per il servizio MLS. Il servizio corrispondente a questo servizio MLService erediterà questo valore da visualizzare nell&#39;interfaccia utente di Service Gallery come nome del servizio. |
| `description` | Una descrizione facoltativa per il servizio MLS. Il servizio corrispondente a questo servizio MLService erediterà questo valore da visualizzare nell&#39;interfaccia utente di Service Gallery come descrizione del servizio. |
| `mlInstanceId` | Un ID istanza valido. |
| `trainingDataSetId` | Un ID set di dati di formazione che, se fornito, sovrascrive l’ID predefinito del set di dati di MLInance. Se l’istanza MLI utilizzata per creare il servizio MLService non definisce un set di dati di formazione, devi fornire un ID set di dati di formazione appropriato. |
| `trainingExperimentId` | Un ID esperimento che puoi facoltativamente fornire. Se questo valore non viene fornito, la creazione di MLService creerà anche un nuovo esperimento utilizzando le configurazioni predefinite di MLInance. |
| `trainingExperimentRunId` | Un ID di esecuzione della formazione che puoi facoltativamente fornire. Se questo valore non viene fornito, la creazione di MLService creerà ed eseguirà anche un&#39;esecuzione di formazione utilizzando i parametri di formazione predefiniti di MLInance. |
| `trainingSchedule` | Viene eseguito un programma per l&#39;addestramento automatico. Se questa proprietà è definita, MLService eseguirà automaticamente l&#39;addestramento su base pianificata. |
| `trainingSchedule.startTime` | Una marca temporale per la quale inizierà l’esecuzione dell’addestramento pianificato. |
| `trainingSchedule.endTime` | Una marca temporale per la quale viene eseguito l’addestramento pianificato verrà terminata. |
| `trainingSchedule.cron` | Espressione cron che definisce la frequenza delle esecuzioni di formazione automatizzate. |
| `scoringSchedule` | Viene eseguita una pianificazione per il punteggio automatico. Se questa proprietà è definita, MLService eseguirà automaticamente le esecuzioni del punteggio su base pianificata. |
| `scoringSchedule.startTime` | Una marca temporale per la quale inizierà l’esecuzione del punteggio pianificato. |
| `scoringSchedule.endTime` | Una marca temporale per la quale viene eseguito il punteggio pianificato termina. |
| `scoringSchedule.cron` | Espressione cron che definisce la frequenza delle esecuzioni di punteggio automatizzate. |

**Risposta**

Una risposta corretta restituisce un payload contenente i dettagli del servizio MLService appena creato, incluso l’identificatore univoco (`id`), ID esperimento per la formazione (`trainingExperimentId`), ID esperimento per il punteggio (`scoringExperimentId`) e l&#39;ID del set di dati per la formazione in input (`trainingDataSetId`).

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

È possibile recuperare un elenco di MLServices eseguendo una singola richiesta di GET. Per facilitare il filtro dei risultati, puoi specificare i parametri di query nel percorso della richiesta. Per un elenco delle query disponibili, fare riferimento alla sezione dell&#39;appendice su [parametri di query per il recupero delle risorse](./appendix.md#query).

**Formato API**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parametro | Descrizione |
| --- | --- |
| `{QUERY_PARAMETER}` | Uno dei [parametri di query disponibili](./appendix.md#query) utilizzato per filtrare i risultati. |
| `{VALUE}` | Il valore del parametro di query precedente. |

**Richiesta**

La richiesta seguente contiene una query e recupera un elenco di MLServices che condividono lo stesso ID istanza (`{MLINSTANCE_ID}`).

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di MLServices e dei relativi dettagli, compreso l&#39;ID del servizio MLS (`{MLSERVICE_ID}`), ID esperimento per la formazione (`{TRAINING_ID}`), ID esperimento per il punteggio (`{SCORING_ID}`) e l&#39;ID del set di dati per la formazione in input (`{DATASET_ID}`).

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

## Recupera un servizio MLService specifico {#retrieve-a-specific-mlservice}

Puoi recuperare i dettagli di un esperimento specifico eseguendo una richiesta GET che include l’ID del servizio MLService desiderato nel percorso della richiesta.

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

## Aggiornare un servizio MLS {#update-an-mlservice}

È possibile aggiornare un servizio MLS esistente sovrascrivendo le sue proprietà tramite una richiesta PUT che include l’ID del servizio MLS di destinazione nel percorso della richiesta e fornendo un payload JSON contenente le proprietà aggiornate.

>[!TIP]
>
>Per garantire il successo di questa richiesta PUT, si consiglia innanzitutto di eseguire una richiesta GET a [recuperare il servizio MLService per ID](#retrieve-a-specific-mlservice). Quindi, modifica e aggiorna l’oggetto JSON restituito e applica l’intero oggetto JSON modificato come payload per la richiesta PUT.

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

Una risposta corretta restituisce un payload contenente i dettagli aggiornati del servizio MLService.

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

È possibile eliminare tutti i servizi MLS appartenenti a una particolare istanza MLI eseguendo una richiesta DELETE che specifica un ID istanza MLI come parametro di query.

**Formato API**

```http
DELETE /mlServices?mlInstanceId={MLINSTANCE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MLINSTANCE_ID}` | Un ID istanza valido. |

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
