---
keywords: Experience Platform;pubblicare un modello;Data Science Workspace;argomenti popolari;sensei machine learning api
solution: Experience Platform
title: Publish a Model as a Service tramite l’API di apprendimento automatico di Sensei
type: Tutorial
description: Questo tutorial illustra il processo di pubblicazione di un modello come servizio utilizzando l’API di apprendimento automatico di Sensei.
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 2%

---

# Publish un modello come servizio utilizzando [!DNL Sensei Machine Learning API]

Questo tutorial descrive il processo di pubblicazione di un modello come servizio utilizzando [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## Introduzione

Questo tutorial richiede una buona conoscenza di Adobe Experience Platform Data Science Workspace. Prima di iniziare questo tutorial, controlla [Data Science Workspace overview](../home.md) per un&#39;introduzione di alto livello al servizio.

Per seguire questa esercitazione, è necessario disporre di un motore ML esistente, di un&#39;istanza ML e di un esperimento. Per i passaggi su come crearli nell&#39;API, consulta l&#39;esercitazione su [importazione di una ricetta in pacchetti](./import-packaged-recipe-api.md).

Infine, prima di iniziare questo tutorial, consulta la sezione [guida introduttiva](../api/getting-started.md) della guida per gli sviluppatori per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API [!DNL Sensei Machine Learning], incluse le intestazioni richieste utilizzate in questo tutorial:

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

Tutte le richieste di POST, PUT e PATCH richiedono un’intestazione aggiuntiva:

- Content-Type: application/json

### Termini chiave

La tabella seguente illustra alcuni termini comuni utilizzati in questa esercitazione:

| Termine | Definizione |
| --- | --- |
| **Istanza di Machine Learning (istanza ML)** | Istanza di un motore [!DNL Sensei] per un determinato tenant, contenente dati, parametri e codice [!DNL Sensei] specifici. |
| **Esperimento** | Entità ombrello per l’esecuzione di esperimenti di formazione, il punteggio delle esecuzioni di esperimenti o entrambi. |
| **Esperimento pianificato** | Termine che descrive l’automazione delle esecuzioni degli esperimenti di formazione o punteggio, gestito da una pianificazione definita dall’utente. |
| **Esecuzione esperimento** | Un esempio particolare di addestramento o valutazione degli esperimenti. Le esecuzioni di più esperimenti di un particolare esperimento possono differire nei valori dei set di dati utilizzati per l’addestramento o il punteggio. |
| **Modello addestrato** | Modello di apprendimento automatico creato dal processo di sperimentazione e ingegneria delle feature prima di arrivare a un modello convalidato, valutato e finalizzato. |
| **Modello pubblicato** | Un modello finalizzato e basato su versioni è stato elaborato dopo l’addestramento, la convalida e la valutazione. |
| **Servizio di apprendimento automatico (servizio ML)** | Istanza ML distribuita come servizio per supportare richieste on-demand per l’apprendimento e il punteggio utilizzando un endpoint API. È possibile creare un servizio ML anche utilizzando esecuzioni di esperimenti già addestrate. |

## Creare un servizio ML con un addestramento esistente Esecuzione esperimento e punteggio pianificato

Quando pubblichi un addestramento Esperimento eseguito come servizio ML, puoi pianificare il punteggio fornendo i dettagli per l’esperimento di punteggio Eseguito sul payload di una richiesta POST. Questo determina la creazione di un’entità esperimento pianificata per il punteggio.

**Formato API**

```http
POST /mlServices
```

**Richiesta**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'Content-Type: application/json'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "trainingExperimentId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingExperimentRunId": "5c5af39c73fcec153117eed1",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `mlInstanceId` | Identificazione dell’istanza ML esistente, l’esecuzione dell’esperimento di formazione utilizzato per creare il servizio ML deve corrispondere a questa particolare istanza ML. |
| `trainingExperimentId` | Identificazione dell’esperimento corrispondente all’identificazione dell’istanza ML. |
| `trainingExperimentRunId` | Una particolare esecuzione dell’esperimento di formazione da utilizzare per la pubblicazione del servizio ML. |
| `scoringDataSetId` | Identificazione che fa riferimento al set di dati specifico da utilizzare per le esecuzioni dell’esperimento con punteggio pianificato. |
| `scoringTimeframe` | Valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per il punteggio delle esecuzioni degli esperimenti. Ad esempio, un valore di `10080` indica che i dati degli ultimi 10080 minuti o 168 ore verranno utilizzati per ogni esecuzione di esperimento con punteggio pianificato. Tieni presente che un valore di `0` non filtrerà i dati, tutti i dati all&#39;interno del set di dati vengono utilizzati per il punteggio. |
| `scoringSchedule` | Contiene dettagli relativi alle esecuzioni pianificate degli esperimenti con punteggio. |
| `scoringSchedule.startTime` | Datetime che indica quando avviare il punteggio. |
| `scoringSchedule.endTime` | Datetime che indica quando avviare il punteggio. |
| `scoringSchedule.cron` | Valore di Cron che indica l’intervallo entro il quale assegnare un punteggio alle esecuzioni dell’esperimento. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del servizio ML appena creato, incluso il relativo `id` univoco e il `scoringExperimentId` per il corrispondente esperimento di punteggio.


```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  },
  "created": "2019-04-08T14:45:25.981Z",
  "updated": "2019-04-08T14:45:25.981Z"
}
```

## Creazione di un servizio ML da un’istanza ML esistente

A seconda del caso d’uso e dei requisiti specifici, la creazione di un servizio ML con un’istanza ML è flessibile in termini di pianificazione dell’addestramento e del punteggio delle esecuzioni degli esperimenti. Questo tutorial illustra i casi specifici in cui:

- [Non è necessario un apprendimento pianificato, ma è necessario un punteggio pianificato.](#ml-service-with-scheduled-experiment-for-scoring)
- [Sono necessarie esecuzioni pianificate degli esperimenti sia per l’apprendimento che per il punteggio.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

È possibile creare un servizio ML utilizzando un’istanza ML senza pianificare alcun addestramento o valutazione degli esperimenti. Tali servizi ML creeranno entità di esperimento ordinarie e una singola esecuzione di esperimento per l’addestramento e il punteggio.

### Servizio ML con esperimento pianificato per il punteggio {#ml-service-with-scheduled-experiment-for-scoring}

Puoi creare un servizio ML pubblicando un’istanza ML con esecuzioni di esperimenti pianificate per il punteggio, che creerà un’entità di esperimento ordinaria per l’apprendimento. Viene generata un’esecuzione dell’esperimento di formazione che verrà utilizzata per tutte le esecuzioni pianificate dell’esperimento con punteggio. Verifica che siano presenti `mlInstanceId`, `trainingDataSetId` e `scoringDataSetId` necessari per la creazione del servizio ML e che esistano e siano valori validi.

**Formato API**

```http
POST /mlServices
```

**Richiesta**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "mlInstanceId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingDataSetId": "5c5af39c73fcec153117eed1",
        "trainingTimeframe": "10000",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| Chiave JSON | Descrizione |
| --- | --- |
| `mlInstanceId` | Identificazione dell’istanza ML esistente, che rappresenta l’istanza ML utilizzata per creare il servizio ML. |
| `trainingDataSetId` | Identificazione che si riferisce al set di dati specifico da utilizzare per l’esperimento di formazione. |
| `trainingTimeframe` | Valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per l’addestramento di Experiment. Ad esempio, un valore di `"10080"` indica che i dati degli ultimi 10080 minuti o 168 ore verranno utilizzati per l’esecuzione dell’esperimento di formazione. Tieni presente che un valore di `"0"` non filtrerà i dati; tutti i dati all&#39;interno del set di dati vengono utilizzati per l&#39;apprendimento. |
| `scoringDataSetId` | Identificazione che fa riferimento al set di dati specifico da utilizzare per le esecuzioni dell’esperimento con punteggio pianificato. |
| `scoringTimeframe` | Valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per il punteggio delle esecuzioni degli esperimenti. Ad esempio, un valore di `"10080"` indica che i dati degli ultimi 10080 minuti o 168 ore verranno utilizzati per ogni esecuzione di esperimento con punteggio pianificato. Tieni presente che un valore di `"0"` non filtrerà i dati, tutti i dati all&#39;interno del set di dati vengono utilizzati per il punteggio. |
| `scoringSchedule` | Contiene dettagli relativi alle esecuzioni pianificate degli esperimenti con punteggio. |
| `scoringSchedule.startTime` | Datetime che indica quando avviare il punteggio. |
| `scoringSchedule.endTime` | Datetime che indica quando avviare il punteggio. |
| `scoringSchedule.cron` | Valore di Cron che indica l’intervallo entro il quale assegnare un punteggio alle esecuzioni dell’esperimento. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del servizio ML appena creato. Ciò include l&#39;univoco del servizio `id`, nonché `trainingExperimentId` e `scoringExperimentId` per i relativi esperimenti di formazione e punteggio, rispettivamente.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

### Servizio ML con esperimenti pianificati per formazione e punteggio {#ml-service-with-scheduled-experiments-for-training-and-scoring}

Per pubblicare un’istanza ML esistente come servizio ML con esecuzioni di esperimenti di apprendimento e punteggio pianificate, è necessario fornire pianificazioni sia di apprendimento che di punteggio. Quando viene creato un servizio ML con questa configurazione, vengono create anche entità esperimento pianificate sia per l’apprendimento che per il punteggio. Tieni presente che le pianificazioni di formazione e punteggio non devono essere necessariamente le stesse. Durante l’esecuzione di un processo di punteggio, verrà recuperato e utilizzato per l’esecuzione pianificata il modello addestrato più recente prodotto dalle esecuzioni pianificate degli esperimenti di apprendimento.

**Formato API**

```http
POST /mlServices
```

**Richiesta**

```SHELL
curl -X POST 'https://platform.adobe.io/data/sensei/mlServices' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "string",
        "description": "string",
        "mlInstanceId": "string",
        "trainingDataSetId": "string",
        "trainingTimeframe": "string",
        "scoringDataSetId": "string",
        "scoringTimeframe": "string",
        "trainingSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        },
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| Chiave JSON | Descrizione |
| --- | --- |
| `mlInstanceId` | Identificazione dell’istanza ML esistente, che rappresenta l’istanza ML utilizzata per creare il servizio ML. |
| `trainingDataSetId` | Identificazione che si riferisce al set di dati specifico da utilizzare per l’esperimento di formazione. |
| `trainingTimeframe` | Valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per l’addestramento di Experiment. Ad esempio, un valore di `"10080"` indica che i dati degli ultimi 10080 minuti o 168 ore verranno utilizzati per l’esecuzione dell’esperimento di formazione. Tieni presente che un valore di `"0"` non filtrerà i dati; tutti i dati all&#39;interno del set di dati vengono utilizzati per l&#39;apprendimento. |
| `scoringDataSetId` | Identificazione che fa riferimento al set di dati specifico da utilizzare per le esecuzioni dell’esperimento con punteggio pianificato. |
| `scoringTimeframe` | Valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per il punteggio delle esecuzioni degli esperimenti. Ad esempio, un valore di `"10080"` indica che i dati degli ultimi 10080 minuti o 168 ore verranno utilizzati per ogni esecuzione di esperimento con punteggio pianificato. Tieni presente che un valore di `"0"` non filtrerà i dati, tutti i dati all&#39;interno del set di dati vengono utilizzati per il punteggio. |
| `trainingSchedule` | Contiene dettagli relativi alle esecuzioni pianificate degli esperimenti di formazione. |
| `scoringSchedule` | Contiene dettagli relativi alle esecuzioni pianificate degli esperimenti con punteggio. |
| `scoringSchedule.startTime` | Datetime che indica quando avviare il punteggio. |
| `scoringSchedule.endTime` | Datetime che indica quando avviare il punteggio. |
| `scoringSchedule.cron` | Valore di Cron che indica l’intervallo entro il quale assegnare un punteggio alle esecuzioni dell’esperimento. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del servizio ML appena creato. Questo include l&#39;univoco `id` del servizio, nonché `trainingExperimentId` e `scoringExperimentId` dei relativi esperimenti di formazione e punteggio, rispettivamente. Nella risposta di esempio seguente, la presenza di `trainingSchedule` e `scoringSchedule` suggerisce che le entità esperimento per l&#39;apprendimento e il punteggio sono esperimenti pianificati.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",,
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

## Cercare un servizio ML {#retrieving-ml-services}

Per cercare un servizio ML esistente, effettuare una richiesta `GET` a `/mlServices` e fornire l&#39;elemento `id` univoco del servizio ML nel percorso.

**Formato API**

```http
GET /mlServices/{SERVICE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SERVICE_ID}` | `id` univoco del servizio ML che stai cercando. |

**Richiesta**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del servizio ML.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-05-13T23:46:03.478Z",
  "updated": "2019-05-13T23:46:03.478Z"
}
```

>[!NOTE]
>
>Il recupero di diversi servizi ML può restituire una risposta con più o meno coppie chiave-valore. La risposta precedente è una rappresentazione di un servizio [ML con esecuzioni pianificate dell&#39;addestramento e del punteggio dell&#39;esperimento](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## Pianificare l’apprendimento o il punteggio

Se si desidera pianificare il punteggio e l&#39;addestramento per un servizio ML già pubblicato, è possibile aggiornare il servizio ML esistente con una richiesta `PUT` in data `/mlServices`.

**Formato API**

```http
PUT /mlServices/{SERVICE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SERVICE_ID}` | `id` univoco del servizio ML che si sta aggiornando. |

**Richiesta**

La richiesta seguente pianifica l&#39;addestramento e il punteggio per un servizio ML esistente aggiungendo le chiavi `trainingSchedule` e `scoringSchedule` con le rispettive chiavi `startTime`, `endTime` e `cron`.

```SHELL
curl -X PUT 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "string",
        "description": "string",
        "mlInstanceId": "string",
        "trainingExperimentId": "string",
        "trainingDataSetId": "string",
        "trainingTimeframe": "integer",
        "scoringExperimentId": "string",
        "scoringDataSetId": "string",
        "scoringTimeframe": "integer",
        "trainingSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-11T00:00",
          "cron": "20 * * * *"
        },
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-11T00:00",
          "cron": "20 * * * *"
        }
      }'
```

>[!WARNING]
>
>Non tentare di modificare `startTime` sui processi di formazione e punteggio pianificati esistenti. Se `startTime` deve essere modificato, è consigliabile pubblicare lo stesso modello e ripianificare i processi di formazione e valutazione.

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del servizio ML aggiornato.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T09:43:55.563Z"
}
```
