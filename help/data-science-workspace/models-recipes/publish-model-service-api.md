---
keywords: Experience Platform;pubblicare un modello;Data Science Workspace;argomenti popolari;api di apprendimento automatico sensei
solution: Experience Platform
title: Pubblicare un modello come servizio utilizzando l’API di apprendimento automatico di Sensei
type: Tutorial
description: Questa esercitazione descrive il processo di pubblicazione di un modello come un servizio utilizzando l'API di apprendimento automatico di Sensei.
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 2%

---

# Pubblica un modello come servizio utilizzando [!DNL Sensei Machine Learning API]

Questa esercitazione descrive il processo di pubblicazione di un modello come servizio utilizzando [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## Introduzione

Questa esercitazione richiede una buona comprensione di Adobe Experience Platform Data Science Workspace. Prima di iniziare questa esercitazione, consulta la sezione [Panoramica di Data Science Workspace](../home.md) per un’introduzione di alto livello al servizio.

Per seguire questa esercitazione, devi disporre di un motore ML, un&#39;istanza ML e un esperimento esistenti. Per i passaggi su come crearli nell’API, consulta l’esercitazione su [importazione di una ricetta imballata](./import-packaged-recipe-api.md).

Infine, prima di avviare questa esercitazione, controlla il [guida introduttiva](../api/getting-started.md) sezione della guida per gli sviluppatori per informazioni importanti che è necessario conoscere per effettuare correttamente le chiamate al [!DNL Sensei Machine Learning] API, comprese le intestazioni richieste utilizzate durante questa esercitazione:

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

Tutte le richieste di POST, PUT e PATCH richiedono un’intestazione aggiuntiva:

- Tipo di contenuto: application/json

### Termini chiave

La tabella seguente illustra alcuni termini comuni utilizzati in questa esercitazione:

| Termine | Definizione |
| --- | --- |
| **Istanza di apprendimento automatico (Istanza ML)** | Un&#39;istanza di [!DNL Sensei] Motore per un tenant specifico, contenente dati, parametri e [!DNL Sensei] codice. |
| **Esperimento** | Un&#39;entità ombrello per tenere in esecuzione un esperimento di formazione, eseguire un esperimento di punteggio o entrambi. |
| **Esperimento pianificato** | Termine per descrivere l&#39;automazione della formazione o del punteggio Eseguiti da un esperimento, governato da un programma definito dall&#39;utente. |
| **Esecuzione esperimento** | Un particolare esempio di formazione o valutazione di Esperimenti. Le esecuzioni multiple di un esperimento da un particolare esperimento possono differire nei valori del set di dati utilizzati per la formazione o il punteggio. |
| **Modello addestrato** | Un modello di apprendimento automatico creato dal processo di sperimentazione e ingegneria delle funzioni prima di arrivare a un modello convalidato, valutato e finalizzato. |
| **Modello pubblicato** | Un modello finalizzato e basato su versioni è arrivato dopo l’addestramento, la convalida e la valutazione. |
| **Servizio di apprendimento automatico (servizio ML)** | Istanza ML distribuita come servizio per supportare richieste on-demand di formazione e valutazione utilizzando un endpoint API. È inoltre possibile creare un servizio ML utilizzando le esecuzioni di esperti esistenti. |

## Crea un servizio ML con un Experience Run di formazione esistente e un punteggio pianificato

Quando pubblichi un Experience Run as a ML Service di formazione, puoi pianificare il punteggio fornendo i dettagli per l’Esperimento di punteggio Esegui il payload di una richiesta POST. Questo comporta la creazione di un’entità Sperimento pianificata per il punteggio.

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
| `mlInstanceId` | L&#39;identificazione dell&#39;istanza ML esistente, l&#39;esecuzione dell&#39;esperimento di formazione utilizzato per creare il servizio ML deve corrispondere a questa particolare istanza ML. |
| `trainingExperimentId` | Identificazione dell&#39;esperimento corrispondente all&#39;identificazione dell&#39;istanza ML. |
| `trainingExperimentRunId` | Una particolare esercitazione Experience Run da utilizzare per la pubblicazione del servizio ML. |
| `scoringDataSetId` | Identificazione relativa al set di dati specifici da utilizzare per le esecuzioni di esperimenti di punteggio pianificati. |
| `scoringTimeframe` | Un valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per il punteggio delle esecuzioni di esperimenti. Ad esempio, un valore di `10080` significa che i dati degli ultimi 10080 minuti o 168 ore verranno utilizzati per ogni esecuzione di un esperimento di punteggio pianificato. Tieni presente che un valore di `0` non filtrano i dati, tutti i dati all’interno del set di dati vengono utilizzati per il punteggio. |
| `scoringSchedule` | Contiene dettagli relativi al punteggio pianificato esecuzioni di esperimenti. |
| `scoringSchedule.startTime` | Datetime che indica quando iniziare il punteggio. |
| `scoringSchedule.endTime` | Datetime che indica quando iniziare il punteggio. |
| `scoringSchedule.cron` | Valore Cron che indica l&#39;intervallo con cui eseguire il punteggio dell&#39;esperimento. |

**Risposta**

Una risposta corretta restituisce i dettagli del servizio ML appena creato, incluso il relativo univoco `id` e `scoringExperimentId` per il punteggio corrispondente Esperimento.


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

A seconda del caso d’uso specifico e dei requisiti, la creazione di un servizio ML con un’istanza ML è flessibile in termini di pianificazione della formazione e del punteggio delle esecuzioni dell’esperimento. Questa esercitazione passerà attraverso i casi specifici in cui:

- [Non è necessaria una formazione pianificata, ma è necessario un punteggio pianificato.](#ml-service-with-scheduled-experiment-for-scoring)
- [È necessario eseguire gli esperimenti pianificati sia per la formazione che per il punteggio.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Si noti che un servizio ML può essere creato utilizzando un&#39;istanza ML senza pianificare alcun addestramento o punteggio Esperimenti. Tali servizi ML creeranno entità di esperimento ordinarie e un unico Experience Run per la formazione e il punteggio.

### Servizio ML con Sperimentazione pianificata per il punteggio {#ml-service-with-scheduled-experiment-for-scoring}

È possibile creare un servizio ML pubblicando un&#39;istanza ML con esecuzioni di esperimenti pianificate per il punteggio, che creerà un&#39;entità di esperimento ordinaria per la formazione. Viene generato un Experience Run di formazione che verrà utilizzato per tutte le esecuzioni di Esperimenti di punteggio pianificati. Assicurati che la `mlInstanceId`, `trainingDataSetId`e `scoringDataSetId` necessari per la creazione del servizio ML e che esistono e sono valori validi.

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
| `trainingDataSetId` | Identificazione relativa al set di dati specifici da utilizzare per la formazione di esperti. |
| `trainingTimeframe` | Un valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per la formazione di Experience. Ad esempio, un valore di `"10080"` significa che i dati degli ultimi 10080 minuti o 168 ore saranno utilizzati per il training Experience Run. Tieni presente che un valore di `"0"` non filtrerà i dati, tutti i dati all’interno del set di dati vengono utilizzati per la formazione. |
| `scoringDataSetId` | Identificazione relativa al set di dati specifici da utilizzare per le esecuzioni di esperimenti di punteggio pianificati. |
| `scoringTimeframe` | Un valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per il punteggio delle esecuzioni di esperimenti. Ad esempio, un valore di `"10080"` significa che i dati degli ultimi 10080 minuti o 168 ore verranno utilizzati per ogni esecuzione di un esperimento di punteggio pianificato. Tieni presente che un valore di `"0"` non filtrano i dati, tutti i dati all’interno del set di dati vengono utilizzati per il punteggio. |
| `scoringSchedule` | Contiene dettagli relativi al punteggio pianificato esecuzioni di esperimenti. |
| `scoringSchedule.startTime` | Datetime che indica quando iniziare il punteggio. |
| `scoringSchedule.endTime` | Datetime che indica quando iniziare il punteggio. |
| `scoringSchedule.cron` | Valore Cron che indica l&#39;intervallo con cui eseguire il punteggio dell&#39;esperimento. |

**Risposta**

Una risposta corretta restituisce i dettagli del servizio ML appena creato. Questo include l&#39;esclusiva del servizio `id`, nonché `trainingExperimentId` e `scoringExperimentId` per i relativi esperimenti di formazione e valutazione, rispettivamente.

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

### Servizio ML con esperimenti pianificati per la formazione e il punteggio {#ml-service-with-scheduled-experiments-for-training-and-scoring}

Per pubblicare un&#39;istanza ML esistente come servizio ML con formazione programmata ed esecuzione di un esperimento di punteggio, devi fornire sia programmi di formazione che di valutazione. Quando viene creato un servizio ML di questa configurazione, vengono create anche entità Sperimento pianificate per l&#39;addestramento e il punteggio. Tieni presente che i programmi di formazione e valutazione non devono necessariamente essere gli stessi. Durante l’esecuzione di un processo di punteggio, verrà recuperato e utilizzato l’ultimo modello addestrato prodotto da esecuzioni di esperti di formazione pianificata per l’esecuzione del punteggio.

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
| `trainingDataSetId` | Identificazione relativa al set di dati specifici da utilizzare per la formazione di esperti. |
| `trainingTimeframe` | Un valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per la formazione di Experience. Ad esempio, un valore di `"10080"` significa che i dati degli ultimi 10080 minuti o 168 ore saranno utilizzati per il training Experience Run. Tieni presente che un valore di `"0"` non filtrerà i dati, tutti i dati all’interno del set di dati vengono utilizzati per la formazione. |
| `scoringDataSetId` | Identificazione relativa al set di dati specifici da utilizzare per le esecuzioni di esperimenti di punteggio pianificati. |
| `scoringTimeframe` | Un valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per il punteggio delle esecuzioni di esperimenti. Ad esempio, un valore di `"10080"` significa che i dati degli ultimi 10080 minuti o 168 ore verranno utilizzati per ogni esecuzione di un esperimento di punteggio pianificato. Tieni presente che un valore di `"0"` non filtrano i dati, tutti i dati all’interno del set di dati vengono utilizzati per il punteggio. |
| `trainingSchedule` | Contiene i dettagli relativi alla formazione programmata Esecuzione di un esperimento. |
| `scoringSchedule` | Contiene dettagli relativi al punteggio pianificato esecuzioni di esperimenti. |
| `scoringSchedule.startTime` | Datetime che indica quando iniziare il punteggio. |
| `scoringSchedule.endTime` | Datetime che indica quando iniziare il punteggio. |
| `scoringSchedule.cron` | Valore Cron che indica l&#39;intervallo con cui eseguire il punteggio dell&#39;esperimento. |

**Risposta**

Una risposta corretta restituisce i dettagli del servizio ML appena creato. Questo include l&#39;esclusiva del servizio `id`, nonché `trainingExperimentId` e `scoringExperimentId` dei relativi esperimenti di formazione e valutazione, rispettivamente. Nella risposta di esempio riportata di seguito, la presenza di `trainingSchedule` e `scoringSchedule` suggerisce che gli enti di esperienza per la formazione e il punteggio siano degli esperimenti pianificati.

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

Puoi cercare un servizio ML esistente creando un `GET` richiesta a `/mlServices` e fornire `id` del servizio ML nel percorso.

**Formato API**

```http
GET /mlServices/{SERVICE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SERVICE_ID}` | L&#39;unico `id` del servizio ML che stai cercando. |

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
>Il recupero di diversi servizi ML può restituire una risposta con più o meno coppie chiave-valore. La risposta di cui sopra è una rappresentazione di un [Servizio ML con formazione programmata e punteggio Esperimento in esecuzione](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## Pianificazione formazione o valutazione

Se desideri pianificare il punteggio e la formazione su un servizio ML già pubblicato, puoi farlo aggiornando il servizio ML esistente con un `PUT` richiesta di `/mlServices`.

**Formato API**

```http
PUT /mlServices/{SERVICE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SERVICE_ID}` | L&#39;unico `id` del servizio ML che si sta aggiornando. |

**Richiesta**

La seguente richiesta pianifica la formazione e il punteggio per un servizio ML esistente aggiungendo il `trainingSchedule` e `scoringSchedule` chiavi con le rispettive `startTime`, `endTime`e `cron` chiavi.

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
>Non tentare di modificare il `startTime` sui lavori di formazione e valutazione programmati esistenti. Se la `startTime` deve essere modificato, considera la pubblicazione dello stesso modello e la riprogrammazione dei processi di formazione e valutazione.

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
