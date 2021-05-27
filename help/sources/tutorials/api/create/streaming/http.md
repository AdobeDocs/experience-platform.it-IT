---
keywords: Experience Platform;home;argomenti popolari;connessione streaming;creare una connessione streaming;guida api;tutorial;creare una connessione streaming;acquisizione streaming;acquisizione;
solution: Experience Platform
title: Creare una connessione in streaming utilizzando l’API
topic-legacy: tutorial
type: Tutorial
description: Questa esercitazione ti aiuterà a iniziare a utilizzare le API Streaming Ingestion, parte delle API del servizio Adobe Experience Platform Data Ingestion.
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: b672eab481a8286f92741a971991c7f83102acf7
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 2%

---


# Creazione di una connessione in streaming tramite API

Flow Service viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti diverse all’interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui è possibile connettere tutte le sorgenti supportate.

Questa esercitazione utilizza l’ API [!DNL Flow Service] per seguire i passaggi necessari per creare una connessione in streaming utilizzando l’API del servizio di flusso.

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): Il framework standardizzato tramite il quale  [!DNL Platform] organizza i dati relativi alle esperienze.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo consumatore unificato in tempo reale basato su dati aggregati provenienti da più origini.

Inoltre, per creare una connessione in streaming è necessario disporre di uno schema XDM di destinazione e di un set di dati. Per informazioni su come crearli, leggi l&#39;esercitazione su [streaming record data](../../../../../ingestion/tutorials/streaming-record-data.md) o l&#39;esercitazione su [streaming time-series data](../../../../../ingestion/tutorials/streaming-time-series-data.md).

Le sezioni seguenti forniscono informazioni aggiuntive che dovrai conoscere per effettuare correttamente le chiamate alle API di acquisizione in streaming.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- nome x-sandbox: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la documentazione di panoramica [sandbox](../../../../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Tipo di contenuto: application/json

## Creare una connessione di base

Una connessione di base specifica l’origine e contiene le informazioni necessarie per rendere il flusso compatibile con le API di acquisizione in streaming. Durante la creazione di una connessione di base, è possibile creare una connessione non autenticata e una connessione autenticata.

### Connessione non autenticata

Le connessioni non autenticate sono la connessione streaming standard che puoi creare quando desideri inviare dati in streaming a Platform.

**Formato API**

```http
POST /flowservice/connections
```

**Richiesta**

Per creare una connessione in streaming, è necessario fornire l’ID del provider e l’ID della specifica di connessione come parte della richiesta di POST. L&#39;ID provider è `521eee4d-8cbe-4906-bb48-fb6bd4450033` e l&#39;ID della specifica di connessione è `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.sourceId` | ID della connessione streaming che desideri creare. |
| `auth.params.dataType` | Tipo di dati per la connessione in streaming. Questo valore deve essere `xdm`. |
| `auth.params.name` | Nome della connessione streaming che si desidera creare. |
| `connectionSpec.id` | Specifica di connessione `id` per le connessioni in streaming. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 con i dettagli della nuova connessione creata, incluso l&#39;identificatore univoco (`id`).

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | La `id` della nuova connessione creata. Questo viene qui indicato come `{CONNECTION_ID}`. |
| `etag` | Identificatore assegnato alla connessione, che specifica la revisione della connessione. |

### Connessione autenticata

Le connessioni autenticate devono essere utilizzate quando è necessario distinguere tra record provenienti da fonti attendibili e non attendibili. Gli utenti che desiderano inviare informazioni con informazioni personali (PII, Personally Identifiable Information) devono creare una connessione autenticata durante lo streaming delle informazioni su Platform.

**Formato API**

```http
POST /flowservice/connections
```

**Richiesta**

Per creare una connessione in streaming, è necessario fornire l’ID del provider e l’ID della specifica di connessione come parte della richiesta di POST. L&#39;ID provider è `521eee4d-8cbe-4906-bb48-fb6bd4450033` e l&#39;ID della specifica di connessione è `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```


| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.sourceId` | ID della connessione streaming che desideri creare. |
| `auth.params.dataType` | Tipo di dati per la connessione in streaming. Questo valore deve essere `xdm`. |
| `auth.params.name` | Nome della connessione streaming che si desidera creare. |
| `auth.params.authenticationRequired` | Il parametro che specifica la connessione streaming creata |
| `connectionSpec.id` | Specifica di connessione `id` per le connessioni in streaming. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 con i dettagli della nuova connessione creata, incluso l&#39;identificatore univoco (`id`).

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | La `id` della nuova connessione creata. Questo viene qui indicato come `{CONNECTION_ID}`. |
| `etag` | Identificatore assegnato alla connessione, che specifica la revisione della connessione. |

## Ottieni URL endpoint di streaming

Con la connessione di base creata, ora puoi recuperare l’URL dell’endpoint di streaming.

**Formato API**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | Il valore `id` della connessione creata in precedenza. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sulla connessione richiesta. L’URL dell’endpoint di streaming viene creato automaticamente con la connessione e può essere recuperato utilizzando il valore `inletUrl` .

```json
{
    "items": [
        {
            "createdAt": 1583971856947,
            "updatedAt": 1583971856947,
            "createdBy": "{API_KEY}",
            "updatedBy": "{API_KEY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "id": "77a05521-91d6-451c-a055-2191d6851c34",
            "name": "Another new sample connection (Experience Event)",
            "description": "Sample description",
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Streaming Connection",
                "params": {
                    "sourceId": "Sample connection (ExperienceEvent)",
                    "inletUrl": "https://dcs.adobedc.net/collection/a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "inletId": "a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "dataType": "xdm",
                    "name": "Sample connection (ExperienceEvent)"
                }
            },
            "version": "\"56008aee-0000-0200-0000-5e697e150000\"",
            "etag": "\"56008aee-0000-0200-0000-5e697e150000\""
        }
    ]
}
```

## Creazione di una connessione sorgente

Dopo aver creato la connessione di base, sarà necessario creare una connessione di origine. Quando crei una connessione sorgente, è necessario il valore `id` dalla connessione di base creata.

**Formato API**

```http
POST /flowservice/sourceConnections
```

**Richiesta**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample source connection",
    "description": "Sample source connection description",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    }
}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 con informazioni dettagliate sulla nuova connessione sorgente creata, incluso l’identificatore univoco (`id`).

```json
{
    "id": "63070871-ec3f-4cb5-af47-cf7abb25e8bb",
    "etag": "\"28000b90-0000-0200-0000-6091b0150000\""
}
```

## Creare una connessione di destinazione

Dopo aver creato la connessione sorgente, è possibile creare una connessione di destinazione. Quando crei la connessione di destinazione, è necessario il valore `id` del set di dati creato in precedenza.

**Formato API**

```http
POST /flowservice/targetConnections
```

**Richiesta**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample target connection",
    "description": "Sample target connection description",
    "connectionSpec": {
        "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
        "version": "1.0"
    },
    "data": {
        "format": "parquet_xdm"
    },
    "params": {
        "dataSetId": "{DATASET_ID}"
    }
}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 con i dettagli della nuova connessione di destinazione creata, incluso il relativo identificatore univoco (`id`).

```json
{
    "id": "98a2a72e-a80f-49ae-aaa3-4783cc9404c2",
    "etag": "\"0500b73f-0000-0200-0000-6091b0b90000\""
}
```

## Creare un flusso di dati

Con le connessioni di origine e destinazione create, ora puoi creare un flusso di dati. Il flusso di dati è responsabile della pianificazione e della raccolta dei dati da un’origine. È possibile creare un flusso di dati eseguendo una richiesta POST all&#39;endpoint `/flows`.

**Formato API**

```http
POST /flows
```

**Richiesta**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample flow",
    "description": "Sample flow description",
    "flowSpec": {
        "id": "d8a6f005-7eaf-4153-983e-e8574508b877",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "{SOURCE_CONNECTION_ID}"
    ],
    "targetConnectionIds": [
        "{TARGET_CONNECTION_ID}"
    ]
}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 con i dettagli del flusso di dati appena creato, incluso il relativo identificatore univoco (`id`).

```json
{
    "id": "ab03bde0-86f2-45c7-b6a5-ad8374f7db1f",
    "etag": "\"1200c123-0000-0200-0000-6091b1730000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione HTTP in streaming che ti consente di utilizzare l’endpoint di streaming per acquisire dati in Platform. Per istruzioni su come creare una connessione in streaming nell&#39;interfaccia utente, leggi l&#39; [esercitazione sulla creazione di una connessione in streaming](../../../ui/create/streaming/http.md).

Per informazioni su come eseguire lo streaming dei dati su Platform, leggi l’esercitazione su [dati in streaming della serie temporale](../../../../../ingestion/tutorials/streaming-time-series-data.md) o l’esercitazione su [dati in streaming record](../../../../../ingestion/tutorials/streaming-record-data.md).

## Appendice

Questa sezione fornisce informazioni supplementari sulla creazione di connessioni in streaming utilizzando l’API.

### Invio di messaggi a una connessione in streaming autenticata

Se l’autenticazione di una connessione in streaming è abilitata, al client verrà richiesto di aggiungere l’intestazione `Authorization` alla richiesta.

Se l’intestazione `Authorization` non è presente o viene inviato un token di accesso non valido/scaduto, viene restituita una risposta HTTP 401 Non autorizzata con una risposta simile a quella riportata di seguito:

**Risposta**

```json
{
    "type": "https://ns.adobe.com/adobecloud/problem/data-collection-service-authorization",
    "status": "401",
    "title": "Authorization",
    "report": {
        "message": "[id] Ims service token is empty"
    }
}
```

### Pubblica i dati non elaborati da acquisire su Platform {#ingest-data}

Dopo aver creato il flusso, puoi inviare il messaggio JSON all’endpoint di streaming creato in precedenza.

**Formato API**

```http
POST /collection/{CONNECTION_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | Il valore `id` della nuova connessione streaming creata. |

**Richiesta**

La richiesta di esempio trasferisce dati non elaborati all’endpoint di streaming creato in precedenza.

```shell
curl -X POST https://dcs.adobedc.net/collection/2301a1f761f6d7bf62c5312c535e1076bbc7f14d728e63cdfd37ecbb4344425b \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: 1f086c23-2ea8-4d06-886c-232ea8bd061d' \
  -d '{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male"
      "birthday": {
          "year": 1984
          "month": 6
          "day": 9
      }
  }'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con i dettagli delle informazioni appena acquisite.

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{CONNECTION_ID}` | ID della connessione in streaming creata in precedenza. |
| `xactionId` | Un identificatore univoco generato lato server per il record appena inviato. Questo ID consente ad Adobe di tracciare il ciclo di vita di questo record attraverso vari sistemi e con il debug. |
| `receivedTimeMs` | Una marca temporale (epoch in millisecondi) che mostra a che ora è stata ricevuta la richiesta. |
