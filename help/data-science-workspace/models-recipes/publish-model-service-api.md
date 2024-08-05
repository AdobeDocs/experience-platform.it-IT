---
keywords: Experience Platform; pubblicare un modello; Data Science Area di lavoro; argomenti popolari; API di Machine Learning di Sensei
solution: Experience Platform
title: Publish un modello come servizio utilizzando l'API Machine Learning di Sensei
type: Tutorial
description: Questo esercitazione riguarda il processo di pubblicazione di un modello come servizio utilizzando l'API Sensei Machine Learning.
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1541'
ht-degree: 2%

---

# Publish un modello come servizio utilizzando [!DNL Sensei Machine Learning API]

>[!NOTE]
>
>Data Science Area di lavoro non è più disponibile per l&#39;acquisto.
>
>Questa documentazione è destinata ai clienti esistenti con precedenti diritti a Data Science Area di lavoro.

Questo esercitazione riguarda il processo di pubblicazione di un modello come servizio utilizzando .[[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)

## Introduzione

Questo esercitazione richiede una comprensione pratica di Adobe Experience Platform Data Science Area di lavoro. Prima di iniziare questo esercitazione, consulta la panoramica](../home.md) di [Data Science Area di lavoro per un&#39;introduzione di alto livello al servizio.

Per seguire con questo esercitazione, è necessario disporre di un motore ML, di un&#39;istanza ML e di un esperimento esistenti. Per i passaggi su come crearli nell&#39;API, consulta l&#39;esercitazione su [importazione di una ricetta in pacchetti](./import-packaged-recipe-api.md).

Infine, prima di iniziare questo tutorial, consulta la sezione [guida introduttiva](../api/getting-started.md) della guida per gli sviluppatori per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API [!DNL Sensei Machine Learning], incluse le intestazioni richieste utilizzate in questo tutorial:

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

Tutte le richieste di POST, PUT e PATCH richiedono un’intestazione aggiuntiva:

- Content-Type: application/json

### Termini chiave

Nella tabella seguente vengono illustrati alcuni termini comuni utilizzati in questo esercitazione:

| Termine | Definizione |
| --- | --- |
| **Istanza di Machine Learning (istanza ML)** | Un istanza di un [!DNL Sensei] motore per un tenant specifico, contenente dati, parametri e [!DNL Sensei] codice specifici. |
| **Esperimento** | Entità ombrello per l’esecuzione di esperimenti di formazione, il punteggio delle esecuzioni di esperimenti o entrambi. |
| **Esperimento pianificato** | Termine che descrive l’automazione delle esecuzioni degli esperimenti di formazione o punteggio, gestito da una pianificazione definita dall’utente. |
| **Esecuzione esperimento** | Un particolare istanza di training o di punteggio Esperimenti. Le esecuzioni di più esperimenti di un particolare esperimento possono differire nei valori dei set di dati utilizzati per l’addestramento o il punteggio. |
| **Modello addestrato** | Modello di apprendimento automatico creato dal processo di sperimentazione e ingegneria delle feature prima di arrivare a un modello convalidato, valutato e finalizzato. |
| **Modello pubblicato** | Un modello finalizzato e basato su versioni è stato elaborato dopo l’addestramento, la convalida e la valutazione. |
| **Servizio di apprendimento automatico (servizio ML)** | Un&#39;istanza ML distribuita come servizio per supportare le richieste on-demand di training e punteggio utilizzando un endpoint API. È inoltre possibile creare un servizio ML utilizzando le esecuzioni di esperimenti addestrate esistenti. |

## Crea un servizio ML con una training Experiment Run esistente e un punteggio pianificato

Quando pubblicare un esperimento training Esegui come servizio ML, puoi programmare punteggio fornendo dettagli per l&#39;esperimento di punteggio Esegui il payload di un richiesta POST. Ciò comporta la creazione di un&#39;entità Esperimento pianificato per il punteggio.

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
| `mlInstanceId` | L&#39;identificazione dell&#39;istanza ML esistente, l&#39;esecuzione dell&#39;esperimento training utilizzata per creare il servizio ML deve corrispondere a questa particolare istanza ML. |
| `trainingExperimentId` | Identificazione dell&#39;esperimento corrispondente all&#39;identificazione dell&#39;istanza ML. |
| `trainingExperimentRunId` | Un particolare training Experiment Run da utilizzare per la pubblicazione del servizio ML. |
| `scoringDataSetId` | Identificazione riferita al set di dati specifico da utilizzare per le esecuzioni degli esperimenti con punteggio pianificate. |
| `scoringTimeframe` | Un valore intero che rappresenta i minuti per filtrare i dati da utilizzare per assegnare un punteggio alle esecuzioni degli esperimenti. Ad esempio, per ogni esecuzione dell&#39;esperimento con punteggio pianificato verrà utilizzato un valore di dati relativi `10080` alle medie degli ultimi 10080 minuti o 168 ore. Si noti che un valore di non filtrerà i dati, tutti i dati all&#39;interno del set di `0` dati vengono utilizzati per il punteggio. |
| `scoringSchedule` | Contiene dettagli relativi al punteggio pianificato Esecuzioni degli esperimenti. |
| `scoringSchedule.startTime` | Datetime che indica quando iniziare a segnare. |
| `scoringSchedule.endTime` | Datetime che indica quando iniziare a segnare. |
| `scoringSchedule.cron` | Valore cron che indica l&#39;intervallo in base al quale assegnare un punteggio alle esecuzioni degli esperimenti. |

**Risposta**

Una risposta corretta restituisce i dettagli del servizio ML appena creato, incluso il suo esperimento univoco `id` e quello per il `scoringExperimentId` punteggio corrispondente.


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

## Creazione di un servizio ML da un&#39;istanza ML esistente

A seconda del caso d&#39;uso e dei requisiti specifici, la creazione di un servizio ML con un&#39;istanza ML è flessibile in termini di pianificazione delle training e assegnazione di punteggi alle esecuzioni degli esperimenti. Questo esercitazione esaminerà i casi specifici in cui:

- [Non è necessario training pianificato, ma un punteggio pianificato.](#ml-service-with-scheduled-experiment-for-scoring)
- [Sono necessarie esecuzioni pianificate degli esperimenti sia per la training che per il punteggio.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Si noti che un servizio ML può essere creato utilizzando un&#39;istanza ML senza pianificare alcun training o valutare gli esperimenti. Tali Servizi ML creeranno entità Esperimento ordinarie e un&#39;unica Esecuzione dell&#39;esperimento per training e punteggio.

### Servizio ML con esperimento pianificato per il punteggio {#ml-service-with-scheduled-experiment-for-scoring}

Puoi creare un servizio ML pubblicando un&#39;istanza ML con esecuzioni di esperimenti pianificate per il punteggio, che creerà un&#39;entità Esperimento ordinaria per training. Viene generata una training esecuzione dell&#39;esperimento, che verrà utilizzata per tutte le esecuzioni degli esperimenti con punteggio pianificate. Assicurati di disporre di , `mlInstanceId``trainingDataSetId`e `scoringDataSetId` necessari per la creazione del servizio ML, che esistano e siano valori validi.

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
| `mlInstanceId` | Identificazione dell&#39;istanza ML esistente, che rappresenta l&#39;istanza ML utilizzata per creare il servizio ML. |
| `trainingDataSetId` | Identificazione riferita al set di dati specifico da utilizzare per training esperimento. |
| `trainingTimeframe` | Un valore intero che rappresenta minuti per filtrare i dati da utilizzare per training esperimento. Ad esempio, per l&#39;esecuzione dell&#39;esperimento training verrà utilizzato un valore di `"10080"` medie dei dati degli ultimi 10080 minuti o 168 ore. Si noti che un valore di non filtrerà i dati, tutti i dati all&#39;interno del set di `"0"` dati vengono utilizzati per training. |
| `scoringDataSetId` | Identificazione riferita al set di dati specifico da utilizzare per le esecuzioni degli esperimenti con punteggio pianificate. |
| `scoringTimeframe` | Un valore intero che rappresenta i minuti per filtrare i dati da utilizzare per assegnare un punteggio alle esecuzioni degli esperimenti. Ad esempio, per ogni esecuzione dell&#39;esperimento con punteggio pianificato verrà utilizzato un valore di dati relativi `"10080"` alle medie degli ultimi 10080 minuti o 168 ore. Tieni presente che un valore di `"0"` non filtrerà i dati, tutti i dati all&#39;interno del set di dati vengono utilizzati per il punteggio. |
| `scoringSchedule` | Contiene dettagli relativi alle esecuzioni pianificate degli esperimenti con punteggio. |
| `scoringSchedule.startTime` | Datetime che indica quando avviare il punteggio. |
| `scoringSchedule.endTime` | Datetime che indica quando avviare il punteggio. |
| `scoringSchedule.cron` | Valore di Cron che indica l’intervallo entro il quale assegnare un punteggio alle esecuzioni dell’esperimento. |

**Risposta**

Una risposta corretta restituisce i dettagli del servizio ML appena creato. Ciò include gli esperimenti unici `id`del servizio, nonché la e `scoringExperimentId` per gli `trainingExperimentId` esperimenti di training e punteggio corrispondenti, rispettivamente.

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

### Servizio ML con esperimenti pianificati per training e punteggio {#ml-service-with-scheduled-experiments-for-training-and-scoring}

Per pubblicare un&#39;istanza ML esistente come servizio ML con training pianificate e esecuzioni di esperimenti con punteggio, è necessario fornire pianificazioni sia training che di punteggio. Quando viene creato un servizio ML di questa configurazione, vengono create anche entità Esperimento pianificate sia per training che per il punteggio. Tieni presente che le pianificazioni di training e punteggio non devono essere necessariamente uguali. Durante l’esecuzione di un processo di punteggio, verrà recuperato e utilizzato per l’esecuzione pianificata il modello addestrato più recente prodotto dalle esecuzioni pianificate degli esperimenti di apprendimento.

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
| `mlInstanceId` | Identificazione dell&#39;istanza ML esistente, che rappresenta l&#39;istanza ML utilizzata per creare il servizio ML. |
| `trainingDataSetId` | Identificazione che si riferisce al set di dati specifico da utilizzare per l’esperimento di formazione. |
| `trainingTimeframe` | Valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per l’addestramento di Experiment. Ad esempio, un valore di `"10080"` indica che i dati degli ultimi 10080 minuti o 168 ore verranno utilizzati per l’esecuzione dell’esperimento di formazione. Tieni presente che un valore di `"0"` non filtrerà i dati; tutti i dati all&#39;interno del set di dati vengono utilizzati per l&#39;apprendimento. |
| `scoringDataSetId` | Identificazione che fa riferimento al set di dati specifico da utilizzare per le esecuzioni dell’esperimento con punteggio pianificato. |
| `scoringTimeframe` | Valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per il punteggio delle esecuzioni degli esperimenti. Ad esempio, un valore di `"10080"` indica che i dati degli ultimi 10080 minuti o 168 ore verranno utilizzati per ogni esecuzione di esperimento con punteggio pianificato. Si noti che un valore di non filtrerà i dati, tutti i dati all&#39;interno del set di `"0"` dati vengono utilizzati per il punteggio. |
| `trainingSchedule` | Contiene dettagli riguardanti le training esecuzioni di esperimenti pianificate. |
| `scoringSchedule` | Contiene dettagli relativi al punteggio pianificato Esecuzioni degli esperimenti. |
| `scoringSchedule.startTime` | Datetime che indica quando iniziare a segnare. |
| `scoringSchedule.endTime` | Datetime che indica quando iniziare a segnare. |
| `scoringSchedule.cron` | Valore cron che indica l&#39;intervallo in base al quale assegnare un punteggio alle esecuzioni degli esperimenti. |

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

Una risposta corretta restituisce i dettagli del servizio ML.

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
>Il recupero di diversi servizi ML può restituire una risposta con più o meno coppie chiave-valore. La risposta precedente è una rappresentazione di un [servizio ML con training pianificate e esecuzioni](#ml-service-with-scheduled-experiments-for-training-and-scoring) di esperimenti con punteggio.


## Pianificare training o assegnare punteggi

Se si desidera programmare punteggio e training su un servizio ML già pubblicato, è possibile farlo aggiornando il servizio ML esistente con un `PUT` richiesta su `/mlServices`.

**Formato API**

```http
PUT /mlServices/{SERVICE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SERVICE_ID}` | L&#39;unicità `id` del servizio ML che stai aggiornando. |

**Richiesta**

Di seguito richiesta pianifica la training e il punteggio per un servizio ML esistente aggiungendo le chiavi e con le `trainingSchedule` rispettive `startTime`chiavi , `endTime`e `cron` .`scoringSchedule`

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
>Non tentare di modificare i `startTime` processi di training e punteggio pianificati esistenti. Se è necessario modificarlo `startTime` , è consigliabile pubblicare lo stesso modello e riprogrammare i processi di training e di assegnazione dei punteggi.

**Risposta**

Una risposta corretta restituisce i dettagli del servizio ML aggiornato.

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
