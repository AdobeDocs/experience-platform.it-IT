---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Pubblicare un modello come servizio (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# Pubblicare un modello come servizio (API)

## Prerequisiti

- Segui questa [esercitazione](../../tutorials/authentication.md) per ottenere l&#39;autorizzazione per iniziare a effettuare chiamate API.
Dall&#39;esercitazione sono ora disponibili le seguenti informazioni:
   - `{ACCESS_TOKEN}`: Il valore del token del portatore specificato dopo l&#39;autenticazione.
   - `{IMS_ORG}`: Credenziali organizzazione IMS trovate nella vostra integrazione unica con Adobe Experience Platform.
   - `{API_KEY}`: Il valore chiave API specifico trovato nella vostra integrazione unica con Adobe Experience Platform.
- Questa esercitazione richiede le entità ML Engine, ML Instance e Experiment esistenti. Fare riferimento a questa [esercitazione](./import-packaged-recipe-api.md) sulla creazione di entità Motore ML, Istanza ML o Esperimento.
- Per informazioni sugli endpoint API e sulle richieste menzionate in questa esercitazione, consultate la [Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)completa.

## Termini chiave

In questa esercitazione viene utilizzata una terminologia comune:

| Termine | Definizione |
--- | ---
| **Istanza di apprendimento automatico (Istanza ML)** | L&#39;entità concettuale che è un&#39;istanza di Sensei Engine per un particolare tenant composta da dati, parametri e codice Sensei specifici. |
| **Sperimentazione** | Un&#39;entità ombrello per tenere in esecuzione gli esperti di formazione, eseguire gli esperimenti di valutazione o entrambi. |
| **Sperimentazione pianificata** | Termine per descrivere l’automazione della formazione o l’assegnazione di un punteggio alle esecuzioni di esperti, regolato da una pianificazione definita dall’utente. |
| **Esecuzione Di Un Esperimento** | Un particolare esempio di formazione o di valutazione di Esperimenti. Le esecuzioni di più esperimenti da un particolare esperimento possono variare nei valori del set di dati utilizzati per la formazione o il punteggio. |
| **Modello** | Un modello di apprendimento automatico creato dal processo di sperimentazione e di progettazione di feature prima di arrivare a un modello convalidato, valutato e finalizzato. |
| **Modello pubblicato** | Un modello finale e con versione raggiunto dopo formazione, convalida e valutazione. |
| **Servizio di apprendimento automatico (servizio ML)** | Istanza ML distribuita come servizio per supportare la richiesta su richiesta di formazione e il punteggio tramite un endpoint. È inoltre possibile creare un servizio ML utilizzando esperienze già acquisite. |


## Flusso di lavoro API

Questa esercitazione passerà alla creazione, al recupero e all&#39;aggiornamento di un servizio ML.

## Creazione di un servizio ML con un esperimento di formazione esistente eseguito e assegnazione di un punteggio pianificato

Quando pubblicate un esperimento di formazione eseguito come servizio ML, potete pianificare il punteggio fornendo i dettagli per l&#39;esperimento di punteggio eseguito nel `scoringSchedule` vostro {JSON_PAYLOAD}. Questo determina la creazione di un&#39;entità Sperimentale pianificata per il punteggio. Assicurarsi di disporre di `mlInstanceId`, `trainingExperimentId`, `trainingExperimentRunId`, `scoringDataSetId`e che siano presenti e siano valori validi.

Per iniziare, effettuate una `POST` richiesta a `/mlServices`. Di seguito è riportato un esempio del comando curl:

**Richiesta**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` : Il valore chiave API specifico trovato nella vostra integrazione unica con Adobe Experience Platform.
- `{IMS_ORG}` :  L’ID organizzazione IMS si trova nei dettagli dell’integrazione nella console I/O di Adobe.
- `{ACCESS_TOKEN}` : Il valore del token del portatore specificato dopo l&#39;autenticazione.
- `{JSON_PAYLOAD}` : Di seguito è riportato un esempio di formato di payload JSON:

```JSON
{
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  }
}
```

- `mlInstanceId` : Identificazione dell&#39;istanza ML esistente, l&#39;esperienza di formazione eseguita per creare il servizio ML deve corrispondere a questa particolare istanza ML.
- `trainingExperimentId` : Identificazione dell&#39;esperimento corrispondente all&#39;identificazione dell&#39;istanza ML.
- `trainingExperimentRunId` : Esecuzione di un particolare esperimento di formazione da utilizzare per la pubblicazione del servizio ML.
- `scoringDataSetId` : Identificazione relativa al set di dati specifico da utilizzare per le esecuzioni di prove di punteggio programmate.
- `scoringTimeframe` : Un valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per il punteggio Esecuzione di un esperimento. Ad esempio, un valore di `"10080"` indica che i dati degli ultimi 10080 minuti o 168 ore saranno utilizzati per ogni esecuzione programmata dell&#39;esperimento di punteggio. Si noti che un valore di non `"0"` filtra i dati, tutti i dati all&#39;interno del dataset vengono utilizzati per il punteggio.
- `scoringSchedule` : Contiene informazioni relative al punteggio pianificato Esecuzione di prove.
- `startTime` : definizione.
- `endTime` : definizione.
- `cron` : definizione.

**Risposta**

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

Dalla risposta JSON, la chiave `scoringExperimentId` con il relativo valore suggerisce che è stato creato un nuovo esperimento di punteggio, insieme al programma Sperimentazione fornito nella `POST` richiesta. La `id` chiave nella risposta identifica in modo univoco il servizio ML creato.

## Creazione di un servizio ML da un&#39;istanza ML esistente

A seconda del caso d’uso e dei requisiti specifici, la creazione di un servizio ML con un’istanza ML è flessibile in termini di programmazione di corsi di formazione e assegnazione dei punteggi alle esecuzioni degli esperti. Questa esercitazione passerà attraverso i casi specifici in cui:

- [Non è necessaria formazione pianificata, ma è necessario un punteggio pianificato.](#ml-service-with-scheduled-experiment-for-scoring)
- [È necessario pianificare le esecuzioni degli esperti sia per la formazione che per il punteggio.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

È possibile creare un servizio ML utilizzando un&#39;istanza ML senza pianificare alcuna formazione o valutazione. Tale servizio ML creerà entità di prova ordinarie e un singolo esperimento viene eseguito per la formazione e il punteggio.

### Servizio ML con l&#39;esperimento pianificato per il punteggio

La creazione di un servizio ML mediante la pubblicazione di un&#39;istanza ML con esecuzioni di esperti pianificate per il punteggio darà luogo alla creazione di un&#39;entità Sperimentale ordinaria per la formazione. L&#39;esecuzione dell&#39;esperimento di formazione generato verrà utilizzata per tutte le esecuzioni dell&#39;esperimento di punteggio pianificate. Verifica di disporre dei `mlInstanceId`, `trainingDataSetId`e `scoringDataSetId` necessari per la creazione del servizio ML, nonché della loro esistenza e della loro validità.

Per iniziare, effettuate una `POST` richiesta a `/mlServices`. Di seguito è riportato un esempio del comando curl:

**Richiesta**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` : Il valore chiave API specifico trovato nella vostra integrazione unica con Adobe Experience Platform.
- `{IMS_ORG}` :  L’ID organizzazione IMS si trova nei dettagli dell’integrazione nella console I/O di Adobe.
- `{ACCESS_TOKEN}` : Il valore del token del portatore specificato dopo l&#39;autenticazione.
- `{JSON_PAYLOAD}` : Di seguito è riportato un esempio di formato di payload JSON:

```JSON
{
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
}
```

| Chiave JSON | Descrizione |
| --- | --- |
| **`mlInstanceId`** | Identificazione dell&#39;istanza ML esistente, che rappresenta l&#39;istanza ML utilizzata per creare il servizio ML. |
| **`trainingDataSetId`** | Identificazione che fa riferimento al set di dati specifico da utilizzare per l’esperimento di formazione. |
| **`trainingTimeframe`** | Un valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per gli esperimenti di formazione. Ad esempio, un valore di `"10080"` indica che i dati degli ultimi 10080 minuti o 168 ore saranno utilizzati per l’esecuzione dell’esperimento di formazione. Un valore di non `"0"` filtra i dati, tutti i dati all’interno del set di dati vengono utilizzati per la formazione. |
| **`scoringDataSetId`** | Identificazione relativa al set di dati specifico da utilizzare per le esecuzioni di prove di punteggio programmate. |
| **`scoringTimeframe`** | Un valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per il punteggio Esecuzione di un esperimento. Ad esempio, un valore di `"10080"` indica che i dati degli ultimi 10080 minuti o 168 ore saranno utilizzati per ogni esecuzione programmata dell&#39;esperimento di punteggio. Si noti che un valore di non `"0"` filtra i dati, tutti i dati all&#39;interno del dataset vengono utilizzati per il punteggio. |
| **`scoringSchedule`** | Contiene informazioni relative al punteggio pianificato Esecuzione di prove. |

**Risposta**

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

Dalla `JSON` risposta, le chiavi `trainingExperimentId` e `scoringExperimentId` suggerisce che per questo servizio ML sia stata creata una nuova entità di formazione e valutazione di Sperimenti. La presenza dell&#39; `scoringSchedule` oggetto fa riferimento ai dettagli sulla pianificazione di esecuzione dell&#39;esperimento di punteggio. La `id` chiave nella risposta fa riferimento al servizio ML appena creato.

### Servizio ML con Sperimentazioni programmate per la formazione e il punteggio

Per pubblicare un&#39;istanza ML esistente come servizio ML con formazione programmata ed esecuzione di prove di punteggio, devi fornire sia programmi di formazione che programmi di punteggio. Quando viene creato un servizio ML di questa configurazione, vengono create anche entità Sperimento pianificate per la formazione e il punteggio. Tieni presente che i programmi di formazione e valutazione non devono necessariamente corrispondere. Durante l&#39;esecuzione di un processo di punteggio, verrà recuperato e utilizzato l&#39;ultimo modello addestrato prodotto da Test Runs di formazione programmata per l&#39;esecuzione del punteggio.

Per creare il servizio ML, effettuare una `POST` richiesta `/mlServices` con l&#39;oggetto `{JSON_PAYLOAD}` che rappresenta il servizio ML da aggiungere. Assicurarsi che i valori `mlInstanceId`, `trainingDataSetId`, e `scoringDataSetId` exists e siano validi.

**Richiesta**

```SHELL
curl -X POST "https://platform-int.adobe.io/data/sensei/mlServices" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{API_KEY}` : Il valore chiave API specifico trovato nella vostra integrazione unica con Adobe Experience Platform.
- `{IMS_ORG}` :  L’ID organizzazione IMS si trova nei dettagli dell’integrazione nella console I/O di Adobe.
- `{ACCESS_TOKEN}` : Il valore del token del portatore specificato dopo l&#39;autenticazione.
- `{JSON_PAYLOAD}` : Di seguito è riportato un esempio di formato di payload JSON:

```JSON
{
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
}
```

| Chiave JSON | Descrizione |
| --- | --- |
| **`mlInstanceId`** | Identificazione dell&#39;istanza ML esistente, che rappresenta l&#39;istanza ML utilizzata per creare il servizio ML. |
| **`trainingDataSetId`** | Identificazione che fa riferimento al set di dati specifico da utilizzare per l’esperimento di formazione. |
| **`trainingTimeframe`** | Un valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per gli esperimenti di formazione. Ad esempio, un valore di `"10080"` indica che i dati degli ultimi 10080 minuti o 168 ore saranno utilizzati per l’esecuzione dell’esperimento di formazione. Un valore di non `"0"` filtra i dati, tutti i dati all’interno del set di dati vengono utilizzati per la formazione. |
| **`scoringDataSetId`** | Identificazione relativa al set di dati specifico da utilizzare per le esecuzioni di prove di punteggio programmate. |
| **`scoringTimeframe`** | Un valore intero che rappresenta i minuti necessari per filtrare i dati da utilizzare per il punteggio Esecuzione di un esperimento. Ad esempio, un valore di `"10080"` indica che i dati degli ultimi 10080 minuti o 168 ore saranno utilizzati per ogni esecuzione programmata dell&#39;esperimento di punteggio. Si noti che un valore di non `"0"` filtra i dati, tutti i dati all&#39;interno del dataset vengono utilizzati per il punteggio. |
| **`trainingSchedule`** | Contiene informazioni relative alle esecuzioni programmate degli esperti di formazione. |
| **`scoringSchedule`** | Contiene informazioni relative al punteggio pianificato Esecuzione di prove. |

**Risposta**

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

L&#39;aggiunta di `trainingExperimentId` e `scoringExperimentId` nel corpo di risposta suggerisce la creazione di entità di esperti sia per la formazione che per il punteggio. La presenza di `trainingSchedule` e suggerisce `scoringSchedule` che i suddetti enti di esperti per la formazione e il punteggio sono previsti Esperimenti. La `id` chiave nella risposta fa riferimento al servizio ML appena creato.

## Recupero dei servizi ML

Per recuperare un servizio ML esistente è sufficiente effettuare una `GET` richiesta all&#39; `/mlServices` endpoint. Assicurarsi di avere l&#39;identificazione del servizio ML per il servizio ML specifico che si sta tentando di recuperare.

**Richiesta**

```SHELL
curl -X GET "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
```

- `{API_KEY}` : Il valore chiave API specifico trovato nella vostra integrazione unica con Adobe Experience Platform.
- `{IMS_ORG}` :  L’ID organizzazione IMS si trova nei dettagli dell’integrazione nella console I/O di Adobe.
- `{ACCESS_TOKEN}` : Il valore del token del portatore specificato dopo l&#39;autenticazione.

**Risposta**

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

La risposta JSON rappresenta l&#39;oggetto ML Service. Questo oggetto equivale alla risposta per la creazione del servizio ML. Si noti che il recupero di diversi Servizi ML potrebbe restituire una risposta con più o meno coppie chiave-valore. La risposta di cui sopra è una rappresentazione di un servizio [ML con formazione programmata ed esecuzione](#ml-service-with-scheduled-experiments-for-training-and-scoring)di prove di punteggio.


## Pianificazione formazione o punteggio

Supponiamo che desideri pianificare il punteggio e la formazione su un servizio ML già pubblicato, per farlo puoi aggiornare il servizio ML esistente con una `PUT` richiesta in `/mlServices`. Assicurarsi di avere l&#39;identificazione del servizio ML che si desidera aggiornare. Per riferimento, il [recupero del servizio](#retrieving-ml-services) ML che si desidera aggiornare potrebbe essere un primo passo utile.

**Richiesta**

```SHELL
curl -X PUT "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{SERVICE_ID}` : Identificazione univoca relativa al servizio ML che si desidera aggiornare.
- `{API_KEY}` : Il valore chiave API specifico trovato nella vostra integrazione unica con Adobe Experience Platform.
- `{IMS_ORG}` :  L’ID organizzazione IMS si trova nei dettagli dell’integrazione nella console I/O di Adobe.
- `{ACCESS_TOKEN}` : Il valore del token del portatore specificato dopo l&#39;autenticazione.
- `{JSON_PAYLOAD}` : Di seguito è riportato un esempio di formato di payload JSON:

```JSON
{
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
}
```

Programmare la formazione e il punteggio può essere fatto aggiungendo la `trainingSchedule` chiave e la `scoringSchedule` chiave con le rispettive `startTime`, `endTime`e `cron` chiavi.

>[!NOTE] che `PUT` le richieste su `mlServices` ti consentono di modificare i Servizi con le esecuzioni programmate esistenti. Non **tentare** di modificare i processi `startTime` di formazione e valutazione già pianificati. Se è `startTime` necessario modificare il modello, prendete in considerazione la pubblicazione dello stesso modello e la riprogrammazione dei processi di formazione e assegnazione dei punteggi.

**Risposta**

La risposta sarà il `{JSON_PAYLOAD}` ma con ulteriori `id`, `created`e `updated` tasti nell&#39;oggetto.

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
