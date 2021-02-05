---
keywords: Experience Platform di ;pubblicare un modello;Data Science Workspace;argomenti più comuni;sensei machine learning api
solution: Experience Platform
title: Pubblicare un modello come servizio utilizzando l'API di apprendimento di Sensei Machine
topic: tutorial
type: Tutorial
description: Questa esercitazione illustra il processo di pubblicazione di un modello come servizio mediante l'API di apprendimento di Sensei Machine.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 1%

---


# Pubblicare un modello come servizio utilizzando [!DNL Sensei Machine Learning API]

Questa esercitazione descrive il processo di pubblicazione di un modello come servizio mediante l&#39; [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## Introduzione

Questa esercitazione richiede una buona conoscenza di Adobe Experience Platform Data Science Workspace. Prima di iniziare questa esercitazione, consultare la [panoramica di Data Science Workspace](../home.md) per un&#39;introduzione di alto livello al servizio.

Per seguire questa esercitazione, è necessario disporre di un motore ML, di un’istanza ML e di un’esperienza già esistenti. Per i passaggi su come crearli nell&#39;API, consultate l&#39;esercitazione su [importazione di una ricetta inclusa nel pacchetto](./import-packaged-recipe-api.md).

Infine, prima di iniziare questa esercitazione, consulta la sezione [getting started](../api/getting-started.md) della guida per gli sviluppatori per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all&#39;API [!DNL Sensei Machine Learning], comprese le intestazioni necessarie utilizzate durante questa esercitazione:

- `{ACCESS_TOKEN}`
- `{IMS_ORG}`
- `{API_KEY}`

Tutte le richieste di POST, PUT e PATCH richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

### Termini chiave

La tabella seguente riassume alcuni termini comuni utilizzati in questa esercitazione:

| Termine | Definizione |
--- | ---
| **Istanza di apprendimento automatico (Istanza ML)** | Un&#39;istanza di un motore [!DNL Sensei] per un tenant specifico, contenente dati, parametri e codice [!DNL Sensei] specifici. |
| **Sperimentazione** | Un&#39;entità ombrello per tenere in esecuzione gli esperti di formazione, eseguire gli esperimenti di valutazione o entrambi. |
| **Sperimentazione pianificata** | Termine per descrivere l’automazione della formazione o l’assegnazione di un punteggio alle esecuzioni di esperti, regolato da una pianificazione definita dall’utente. |
| **Esecuzione Di Un Esperimento** | Un particolare esempio di formazione o di valutazione di Esperimenti. Le esecuzioni di più esperimenti da un particolare esperimento possono variare nei valori del set di dati utilizzati per la formazione o il punteggio. |
| **Modello** | Un modello di machine learning creato dal processo di sperimentazione e di feature engineering prima di arrivare a un modello convalidato, valutato e finalizzato. |
| **Modello pubblicato** | Un modello finale e con versione raggiunto dopo formazione, convalida e valutazione. |
| **Servizio di apprendimento automatico (servizio ML)** | Un&#39;istanza ML distribuita come servizio per supportare le richieste on-demand di formazione e punteggio tramite un endpoint API. È inoltre possibile creare un servizio ML utilizzando le esecuzioni sperimentali già formate. |

## Creazione di un servizio ML con un&#39;esperienza di formazione esistente e assegnazione di un punteggio pianificato

Quando pubblicate un esperimento di formazione eseguito come servizio ML, potete pianificare il punteggio fornendo i dettagli per l&#39;esperimento di punteggio Eseguire il payload di una richiesta di POST. Questo determina la creazione di un&#39;entità Sperimentale pianificata per il punteggio.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}'
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
--- | ---
| `mlInstanceId` | Identificazione dell&#39;istanza ML esistente, l&#39;esperienza di formazione eseguita per creare il servizio ML deve corrispondere a questa particolare istanza ML. |
| `trainingExperimentId` | Identificazione dell&#39;esperimento corrispondente all&#39;identificazione dell&#39;istanza ML. |
| `trainingExperimentRunId` | Esecuzione di un particolare esperimento di formazione da utilizzare per la pubblicazione del servizio ML. |
| `scoringDataSetId` | Identificazione relativa al set di dati specifico da utilizzare per le esecuzioni di prove di punteggio programmate. |
| `scoringTimeframe` | Un valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per il punteggio Esecuzione di un esperimento. Ad esempio, un valore di `10080` indica che i dati degli ultimi 10080 minuti o 168 ore saranno utilizzati per ogni esecuzione programmata di un esperimento di punteggio. Tenere presente che il valore `0` non filtra i dati, tutti i dati all&#39;interno del dataset vengono utilizzati per il punteggio. |
| `scoringSchedule` | Contiene informazioni relative al punteggio pianificato Esecuzione di prove. |
| `scoringSchedule.startTime` | Datetime che indica quando iniziare il punteggio. |
| `scoringSchedule.endTime` | Datetime che indica quando iniziare il punteggio. |
| `scoringSchedule.cron` | Valore Cron che indica l&#39;intervallo con cui eseguire il punteggio dell&#39;esperimento. |

**Risposta**

Una risposta corretta restituisce i dettagli del servizio ML appena creato, inclusi `id` univoco e `scoringExperimentId` per il corrispondente esperimento di punteggio.


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

A seconda del caso d’uso e dei requisiti specifici, la creazione di un servizio ML con un’istanza ML è flessibile in termini di programmazione di corsi di formazione e assegnazione dei punteggi alle esecuzioni degli esperti. Questa esercitazione passerà attraverso i casi specifici in cui:

- [Non è necessaria formazione pianificata, ma è necessario un punteggio pianificato.](#ml-service-with-scheduled-experiment-for-scoring)
- [È necessario pianificare le esecuzioni degli esperti sia per la formazione che per il punteggio.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

È possibile creare un servizio ML utilizzando un&#39;istanza ML senza pianificare alcuna formazione o valutazione. Tali servizi ML creeranno entità comuni di prova e un solo esperimento eseguito per formazione e punteggio.

### Servizio ML con l&#39;esperimento pianificato per il punteggio {#ml-service-with-scheduled-experiment-for-scoring}

Puoi creare un servizio ML pubblicando un&#39;istanza ML con esecuzioni di esperimenti programmate per il punteggio, che creerà un&#39;entità Sperimento ordinaria per la formazione. Viene generata una prova di formazione che verrà utilizzata per tutte le esecuzioni programmate degli esperti. Assicurarsi di disporre dei valori `mlInstanceId`, `trainingDataSetId` e `scoringDataSetId` necessari per la creazione del servizio ML, nonché che siano presenti e siano valori validi.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
| `trainingDataSetId` | Identificazione che fa riferimento al set di dati specifico da utilizzare per l’esperimento di formazione. |
| `trainingTimeframe` | Un valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per gli esperimenti di formazione. Ad esempio, un valore di `"10080"` indica che i dati degli ultimi 10080 minuti o 168 ore saranno utilizzati per l&#39;esecuzione dell&#39;esperimento di formazione. Tenere presente che il valore `"0"` non filtra i dati, tutti i dati all&#39;interno del dataset vengono utilizzati per la formazione. |
| `scoringDataSetId` | Identificazione relativa al set di dati specifico da utilizzare per le esecuzioni di prove di punteggio programmate. |
| `scoringTimeframe` | Un valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per il punteggio Esecuzione di un esperimento. Ad esempio, un valore di `"10080"` indica che i dati degli ultimi 10080 minuti o 168 ore saranno utilizzati per ogni esecuzione programmata di un esperimento di punteggio. Tenere presente che il valore `"0"` non filtra i dati, tutti i dati all&#39;interno del dataset vengono utilizzati per il punteggio. |
| `scoringSchedule` | Contiene informazioni relative al punteggio pianificato Esecuzione di prove. |
| `scoringSchedule.startTime` | Datetime che indica quando iniziare il punteggio. |
| `scoringSchedule.endTime` | Datetime che indica quando iniziare il punteggio. |
| `scoringSchedule.cron` | Valore Cron che indica l&#39;intervallo con cui eseguire il punteggio dell&#39;esperimento. |

**Risposta**

Una risposta corretta restituisce i dettagli del servizio ML appena creato. Ciò include l&#39;esclusiva `id` del servizio, nonché `trainingExperimentId` e `scoringExperimentId` rispettivamente per i corrispondenti esperimenti di formazione e valutazione.

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

### Servizio ML con Sperimentazioni programmate per formazione e punteggio {#ml-service-with-scheduled-experiments-for-training-and-scoring}

Per pubblicare un&#39;istanza ML esistente come servizio ML con formazione programmata ed esecuzione di prove di punteggio, devi fornire sia programmi di formazione che programmi di punteggio. Quando viene creato un servizio ML di questa configurazione, vengono create anche entità Sperimento pianificate per la formazione e il punteggio. Tieni presente che i programmi di formazione e valutazione non devono necessariamente corrispondere. Durante l&#39;esecuzione di un processo di punteggio, verrà recuperato e utilizzato l&#39;ultimo modello addestrato prodotto da Test Runs di formazione programmata per l&#39;esecuzione del punteggio.

**Formato API**

```http
POST /mlServices
```

**Richiesta**

```SHELL
curl -X POST 'https://platform-int.adobe.io/data/sensei/mlServices' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
| `trainingDataSetId` | Identificazione che fa riferimento al set di dati specifico da utilizzare per l’esperimento di formazione. |
| `trainingTimeframe` | Un valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per gli esperimenti di formazione. Ad esempio, un valore di `"10080"` indica che i dati degli ultimi 10080 minuti o 168 ore saranno utilizzati per l&#39;esecuzione dell&#39;esperimento di formazione. Tenere presente che il valore `"0"` non filtra i dati, tutti i dati all&#39;interno del dataset vengono utilizzati per la formazione. |
| `scoringDataSetId` | Identificazione relativa al set di dati specifico da utilizzare per le esecuzioni di prove di punteggio programmate. |
| `scoringTimeframe` | Un valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per il punteggio Esecuzione di un esperimento. Ad esempio, un valore di `"10080"` indica che i dati degli ultimi 10080 minuti o 168 ore saranno utilizzati per ogni esecuzione programmata di un esperimento di punteggio. Tenere presente che il valore `"0"` non filtra i dati, tutti i dati all&#39;interno del dataset vengono utilizzati per il punteggio. |
| `trainingSchedule` | Contiene informazioni relative alle esecuzioni programmate degli esperti di formazione. |
| `scoringSchedule` | Contiene informazioni relative al punteggio pianificato Esecuzione di prove. |
| `scoringSchedule.startTime` | Datetime che indica quando iniziare il punteggio. |
| `scoringSchedule.endTime` | Datetime che indica quando iniziare il punteggio. |
| `scoringSchedule.cron` | Valore Cron che indica l&#39;intervallo con cui eseguire il punteggio dell&#39;esperimento. |

**Risposta**

Una risposta corretta restituisce i dettagli del servizio ML appena creato. Ciò include l&#39;esclusiva `id` del servizio, nonché `trainingExperimentId` e `scoringExperimentId` dei relativi esperimenti di formazione e valutazione. Nella risposta di esempio riportata di seguito, la presenza di `trainingSchedule` e `scoringSchedule` suggerisce che le entità Sperimentale per la formazione e il punteggio sono Sperimentazioni programmate.

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

È possibile cercare un servizio ML esistente eseguendo una richiesta `GET` a `/mlServices` e fornendo l&#39;unica `id` del servizio ML nel percorso.

**Formato API**

```http
GET /mlServices/{SERVICE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SERVICE_ID}` | L&#39;unica `id` del servizio ML che si sta cercando. |

**Richiesta**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
>Il recupero di diversi servizi ML potrebbe restituire una risposta con più o meno coppie chiave-valore. La risposta di cui sopra è una rappresentazione di un [Servizio ML con formazione programmata e punteggi esecuzione di prove ](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## Pianificazione formazione o punteggio

Se si desidera pianificare il punteggio e la formazione su un servizio ML già pubblicato, è possibile farlo aggiornando il servizio ML esistente con una richiesta `PUT` su `/mlServices`.

**Formato API**

```http
PUT /mlServices/{SERVICE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SERVICE_ID}` | L&#39;unica `id` del servizio ML che si sta aggiornando. |

**Richiesta**

La seguente richiesta pianifica la formazione e il punteggio per un servizio ML esistente aggiungendo le chiavi `trainingSchedule` e `scoringSchedule` con le rispettive chiavi `startTime`, `endTime` e `cron`.

```SHELL
curl -X PUT 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
>Non tentare di modificare i `startTime` processi di formazione e valutazione già pianificati. Se è necessario modificare `startTime`, prendete in considerazione la pubblicazione dello stesso modello e la riprogrammazione dei processi di formazione e assegnazione dei punteggi.

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
