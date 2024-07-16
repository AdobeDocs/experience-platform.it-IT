---
keywords: Experience Platform;guida per sviluppatori;endpoint;Data Science Workspace;argomenti popolari;mlservices;sensei machine learning api
solution: Experience Platform
title: Endpoint API MLServices
description: Un MLService è un modello pubblicato e addestrato che offre all’organizzazione la possibilità di accedere e riutilizzare i modelli sviluppati in precedenza. Una caratteristica chiave di MLServices è la capacità di automatizzare la formazione e il punteggio su base pianificata. Le esecuzioni pianificate dei corsi di formazione possono contribuire a mantenere l’efficienza e l’accuratezza di un modello, mentre le esecuzioni pianificate dei punteggi possono garantire la generazione coerente di nuove informazioni.
role: Developer
exl-id: cd236e0b-3bfc-4d37-83eb-432f6ad5c5b6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 2%

---

# Endpoint MLServices

Un MLService è un modello pubblicato e addestrato che offre all’organizzazione la possibilità di accedere e riutilizzare i modelli sviluppati in precedenza. Una caratteristica chiave di MLServices è la capacità di automatizzare la formazione e il punteggio su base pianificata. Le esecuzioni pianificate dei corsi di formazione possono contribuire a mantenere l’efficienza e l’accuratezza di un modello, mentre le esecuzioni pianificate dei punteggi possono garantire la generazione coerente di nuove informazioni.

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
| `name` | Il nome desiderato per MLService. Il servizio corrispondente a questo MLService erediterà questo valore per essere visualizzato nell’interfaccia utente di Service Gallery come nome del servizio. |
| `description` | Descrizione facoltativa per MLService. Il servizio corrispondente a questo MLService erediterà questo valore per essere visualizzato nell’interfaccia utente di Service Gallery come descrizione del servizio. |
| `mlInstanceId` | Un ID istanza MLI valido. |
| `trainingDataSetId` | Un ID del set di dati di apprendimento che, se fornito, sostituirà l’ID del set di dati predefinito dell’istanza MLI. Se l’istanza MLS utilizzata per creare MLService non definisce un set di dati di addestramento, devi fornire un ID appropriato per il set di dati di addestramento. |
| `trainingExperimentId` | Un ID esperimento che puoi facoltativamente fornire. Se questo valore non viene fornito, la creazione di MLService creerà anche un nuovo esperimento utilizzando le configurazioni predefinite dell’istanza MLS. |
| `trainingExperimentRunId` | ID dell’esecuzione dell’apprendimento che puoi facoltativamente fornire. Se questo valore non viene fornito, la creazione di MLService creerà ed eseguirà anche un’esecuzione di addestramento utilizzando i parametri di addestramento predefiniti dell’istanza MLS. |
| `trainingSchedule` | Una pianificazione per l’esecuzione automatica dell’addestramento. Se questa proprietà è definita, MLService eseguirà automaticamente le esecuzioni di addestramento su base pianificata. |
| `trainingSchedule.startTime` | Un timestamp per il quale inizieranno le esecuzioni di addestramento pianificate. |
| `trainingSchedule.endTime` | Un timestamp per il quale termineranno le esecuzioni di addestramento pianificate. |
| `trainingSchedule.cron` | Espressione cron che definisce la frequenza delle esecuzioni di addestramento automatizzate. |
| `scoringSchedule` | Viene eseguita una pianificazione per il punteggio automatico. Se questa proprietà è definita, MLService eseguirà automaticamente le esecuzioni di punteggio su base pianificata. |
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

## Recuperare un elenco di servizi MLS {#retrieve-a-list-of-mlservices}

È possibile recuperare un elenco di MLServices eseguendo una singola richiesta GET. Per filtrare i risultati, puoi specificare i parametri di query nel percorso della richiesta. Per un elenco delle query disponibili, consulta la sezione dell&#39;appendice sui [parametri di query per il recupero delle risorse](./appendix.md#query).

**Formato API**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parametro | Descrizione |
| --- | --- |
| `{QUERY_PARAMETER}` | Uno dei [parametri di query disponibili](./appendix.md#query) utilizzati per filtrare i risultati. |
| `{VALUE}` | Valore per il parametro di query precedente. |

**Richiesta**

La richiesta seguente contiene una query e recupera un elenco di MLServices che condividono lo stesso ID MLInstance (`{MLINSTANCE_ID}`).

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di MLServices e dei relativi dettagli, inclusi l&#39;ID MLService (`{MLSERVICE_ID}`), l&#39;ID esperimento per l&#39;addestramento (`{TRAINING_ID}`), l&#39;ID esperimento per il punteggio (`{SCORING_ID}`) e l&#39;ID del set di dati di addestramento di input (`{DATASET_ID}`).

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

In caso di esito positivo, la risposta restituisce un payload contenente i dettagli del servizio MLS richiesto.

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

Puoi aggiornare un MLService esistente sovrascrivendo le relative proprietà tramite una richiesta PUT che include l’ID MLService di destinazione nel percorso della richiesta e fornendo un payload JSON contenente le proprietà aggiornate.

>[!TIP]
>
>Per garantire il completamento di questa richiesta PUT, si consiglia di eseguire prima una richiesta GET per [recuperare MLService per ID](#retrieve-a-specific-mlservice). Quindi, modifica e aggiorna l’oggetto JSON restituito e applica l’intero oggetto JSON modificato come payload per la richiesta PUT.

**Formato API**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: ID MLService valido.

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

In caso di esito positivo, la risposta restituisce un payload contenente i dettagli aggiornati del servizio MLS.

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

È possibile eliminare un singolo MLService eseguendo una richiesta DELETE che includa l’ID MLService di destinazione nel percorso della richiesta.

**Formato API**

```http
DELETE /mlServices/{MLSERVICE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MLSERVICE_ID}` | ID MLService valido. |

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
| `{MLINSTANCE_ID}` | Un ID istanza MLI valido. |

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
