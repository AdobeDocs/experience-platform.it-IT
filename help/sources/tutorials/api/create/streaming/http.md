---
keywords: Experience Platform;home;argomenti popolari;connessione streaming;creare una connessione streaming;guida api;tutorial;creare una connessione streaming;acquisizione streaming;acquisizione;
title: Creare una connessione in streaming API HTTP utilizzando l’API del servizio Flusso
description: Questo tutorial illustra come creare una connessione in streaming utilizzando l’origine API HTTP per i dati grezzi e XDM mediante l’API del servizio Flusso
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: fe2e93b9595d9df9a088d627d696b559f259e80d
workflow-type: tm+mt
source-wordcount: '1568'
ht-degree: 4%

---


# Creare una connessione streaming API HTTP utilizzando [!DNL Flow Service] API

Il servizio Flow viene utilizzato per raccogliere e centralizzare i dati dei clienti da diverse origini all’interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui tutte le sorgenti supportate sono collegabili.

Questa esercitazione utilizza [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) per guidarti attraverso i passaggi per creare una connessione in streaming utilizzando [!DNL Flow Service] API.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Platform] organizza i dati dell’esperienza.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato in tempo reale basato su dati aggregati provenienti da più origini.

Inoltre, la creazione di una connessione in streaming richiede uno schema XDM di destinazione e un set di dati. Per scoprire come crearli, leggi il tutorial su [dati di registrazione streaming](../../../../../ingestion/tutorials/streaming-record-data.md) o il tutorial su [streaming di dati di serie temporali](../../../../../ingestion/tutorials/streaming-time-series-data.md).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base specifica l’origine e contiene le informazioni necessarie per rendere il flusso compatibile con le API Streaming Ingestion. Quando si crea una connessione di base, è possibile creare una connessione non autenticata e autenticata.

### Connessione non autenticata

Le connessioni non autenticate sono la connessione streaming standard che puoi creare quando desideri inviare dati a Platform.

Per creare una connessione di base non autenticata, effettuare una richiesta POST al `/connections` mentre fornisci un nome per la connessione, il tipo di dati e l’ID di specifica della connessione API HTTP. Questo ID è `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

**Formato API**

```http
POST /flowservice/connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per l’API HTTP.

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "name": "ACME Streaming Connection XDM Data",
    "description": "ACME streaming connection for customer data",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    },
    "auth": {
      "specName": "Streaming Connection",
      "params": {
        "dataType": "xdm"
      }
    }
  }'
```

>[!TAB Dati non elaborati]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "name": "ACME Streaming Connection Raw Data",
    "description": "ACME streaming connection for customer data",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    },
    "auth": {
      "specName": "Streaming Connection",
      "params": {
        "dataType": "raw"
      }
    }
  }'
```

>[!ENDTABS]

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della connessione di base. Verificare che il nome sia descrittivo, in quanto è possibile utilizzarlo per cercare informazioni sulla connessione di base. |
| `description` | (Facoltativo) Proprietà che è possibile includere per fornire ulteriori informazioni sulla connessione di base. |
| `connectionSpec.id` | ID della specifica di connessione che corrisponde all’API HTTP. Questo ID è `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`. |
| `auth.params.dataType` | Il tipo di dati per la connessione in streaming. I valori supportati includono: `xdm` e `raw`. |
| `auth.params.name` | Nome della connessione in streaming che si desidera creare. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 con i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`).

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | Il `id` della connessione di base appena creata. |
| `etag` | Identificatore assegnato alla connessione, che specifica la versione della connessione di base. |

### Connessione autenticata

Le connessioni autenticate devono essere utilizzate quando è necessario distinguere tra record provenienti da fonti attendibili e non attendibili. Gli utenti che desiderano inviare informazioni con dati personali (PII, Personally Identifiable Information) devono creare una connessione autenticata durante lo streaming di informazioni su Platform.

Per creare una connessione di base autenticata, è necessario includere `authenticationRequired` nella richiesta e specificarne il valore come `true`. Durante questo passaggio, puoi anche fornire un ID sorgente per la connessione di base autenticata. Questo parametro è facoltativo e utilizzerà lo stesso valore del parametro `name` , se non viene fornito.


**Formato API**

```http
POST /flowservice/connections
```

**Richiesta**

La richiesta seguente crea una connessione di base autenticata per l’API HTTP.

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "ACME Streaming Connection XDM Data Authenticated",
     "description": "ACME streaming connection for customer data",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Authenticated XDM streaming connection",
             "dataType": "xdm",
             "name": "Authenticated XDM streaming connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!TAB Dati non elaborati]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "ACME Streaming Connection Raw Data Authenticated",
     "description": "ACME streaming connection for customer data",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Authenticated raw streaming connection",
             "dataType": "raw",
             "name": "Authenticated raw streaming connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!ENDTABS]

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.sourceId` | Identificatore aggiuntivo che può essere utilizzato durante la creazione di una connessione di base autenticata. Questo parametro è facoltativo e utilizzerà lo stesso valore del parametro `name` , se non viene fornito. |
| `auth.params.authenticationRequired` | Questo parametro specifica se la connessione streaming richiede l&#39;autenticazione o meno. Se `authenticationRequired` è impostato su `true` quindi è necessario fornire l’autenticazione per la connessione in streaming. Se `authenticationRequired` è impostato su `false` quindi l’autenticazione non è richiesta. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 con i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`).

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

## Ottieni URL endpoint di streaming

Una volta creata la connessione di base, ora puoi recuperare l’URL dell’endpoint di streaming.

**Formato API**

```http
GET /flowservice/connections/{BASE_CONNECTION_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Il `id` valore della connessione creata in precedenza. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con informazioni dettagliate sulla connessione richiesta. L’URL dell’endpoint di streaming viene creato automaticamente con la connessione e può essere recuperato utilizzando `inletUrl` valore.

```json
{
  "items": [
    {
      "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
      "createdAt": 1669238699119,
      "updatedAt": 1669238699119,
      "createdBy": "acme@AdobeID",
      "updatedBy": "acme@AdobeID",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "ACME Streaming Connection XDM Data",
      "description": "ACME streaming connection for customer data",
      "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "Streaming Connection",
        "params": {
          "sourceId": "ACME Streaming Connection XDM Data",
          "inletUrl": "https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec",
          "authenticationRequired": false,
          "inletId": "667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec",
          "dataType": "xdm",
          "name": "ACME Streaming Connection XDM Data"
        }
      },
      "version": "\"f50185ed-0000-0200-0000-637e8fad0000\"",
      "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
    }
  ]
}
```

## Creare una connessione sorgente {#source}

Per creare una connessione sorgente, effettua una richiesta POST al `/sourceConnections` mentre fornisci l’ID connessione di base.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Source Connection for Customer Data",
      "description": "A streaming source connection for ACME XDM Customer Data",
      "baseConnectionId": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
      "connectionSpec": {
          "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
          "version": "1.0"
      }
    }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 con informazioni dettagliate sulla nuova connessione sorgente creata, compreso il relativo identificatore univoco (`id`).

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

## Creare uno schema XDM di destinazione {#target-schema}

Per utilizzare i dati sorgente in Platform, è necessario creare uno schema di destinazione che strutturi i dati sorgente in base alle tue esigenze. Lo schema di destinazione viene quindi utilizzato per creare un set di dati di Platform in cui sono contenuti i dati di origine.

È possibile creare uno schema XDM di destinazione eseguendo una richiesta POST al [API del registro dello schema](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Per i passaggi dettagliati su come creare uno schema XDM di destinazione, consulta l’esercitazione su [creazione di uno schema tramite l’API](../../../../../xdm/api/schemas.md).

### Creare un set di dati di destinazione {#target-dataset}

È possibile creare un set di dati di destinazione eseguendo una richiesta POST al [API Catalog Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), che fornisce l’ID dello schema di destinazione all’interno del payload.

Per i passaggi dettagliati su come creare un set di dati di destinazione, consulta l’esercitazione su [creazione di un set di dati tramite l’API](../../../../../catalog/api/create-dataset.md).

## Creare una connessione di destinazione {#target}

Una connessione di destinazione rappresenta la connessione alla destinazione in cui arrivano i dati acquisiti. Per creare una connessione di destinazione, invia una richiesta POST a `/targetConnections` mentre fornisci gli ID per il set di dati di destinazione e lo schema XDM di destinazione. Durante questo passaggio, devi anche fornire l’ID di specifica della connessione al data lake. Questo ID è `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Target Connection",
      "description": "ACME Streaming Target Connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
              "version": "application/vnd.adobe.xed-full+json;version=1.0"
          }
      },
      "params": {
          "dataSetId": "637eb7fadc8a211b6312b65b"
      },
          "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
  }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 con i dettagli della nuova connessione di destinazione creata, incluso il relativo identificatore univoco (`id`).

```json
{
  "id": "07f2f6ff-1da5-4704-916a-c615b873cba9",
  "etag": "\"340680f7-0000-0200-0000-637eb8730000\""
}
```

## Creare una mappatura {#mapping}

Per poter acquisire i dati di origine in un set di dati di destinazione, è necessario prima mapparli sullo schema di destinazione a cui il set di dati di destinazione aderisce.

Per creare un set di mappatura, effettua una richiesta POST al `mappingSets` endpoint del [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) mentre fornisci lo schema XDM di destinazione `$id` e i dettagli dei set di mappatura da creare.

**Formato API**

```http
POST /mappingSets
```

**Richiesta**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
      "xdmVersion": "1.0",
      "mappings": [
          {
              "destinationXdmPath": "person.name.firstName",
              "sourceAttribute": "firstName",
              "identity": false,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.lastName",
              "sourceAttribute": "lastName",
              "identity": false,
              "version": 0
          }
      ]
  }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `xdmSchema` | Il `$id` dello schema XDM di destinazione. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della mappatura appena creata, compreso l’identificatore univoco (`id`). Questo ID è necessario in un passaggio successivo per creare un flusso di dati.

```json
{
  "id": "79a623960d3f4969835c9e00dc90c8df",
  "version": 0,
  "createdDate": 1669249214031,
  "modifiedDate": 1669249214031,
  "createdBy": "acme@AdobeID",
  "modifiedBy": "acme@AdobeID"
}
```

| Proprietà | Descrizione |
| --- | --- |

## Creare un flusso di dati

Una volta create le connessioni di origine e di destinazione, ora puoi creare un flusso di dati. Il flusso di dati è responsabile della pianificazione e della raccolta dei dati da un’origine. Puoi creare un flusso di dati eseguendo una richiesta POST al `/flows` endpoint.

**Formato API**

```http
POST /flows
```

**Richiesta**

>[!BEGINTABS]

>[!TAB Senza trasformazioni]

La seguente richiesta crea un flusso di dati in streaming per l’API HTTP senza trasformazioni di dati.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Dataflow",
      "description": "ACME streaming dataflow for customer data",
      "flowSpec": {
        "id": "d8a6f005-7eaf-4153-983e-e8574508b877",
        "version": "1.0"
      },
      "sourceConnectionIds": [
        "34ece231-294d-416c-ad2a-5a5dfb2bc69f"
      ],
      "targetConnectionIds": [
        "07f2f6ff-1da5-4704-916a-c615b873cba9"
      ]
    }'
```

>[!TAB Con trasformazioni]

Le seguenti richieste creano un flusso di dati in streaming per l’API HTTP con le trasformazioni di mappatura applicate ai dati.

Durante la creazione di un flusso di dati con trasformazioni, il `name` parametro non può essere modificato. Questo valore deve essere sempre impostato su `Mapping`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "<name>",
      "description": "<description>",
      "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
      },
      "sourceConnectionIds": [
        "34ece231-294d-416c-ad2a-5a5dfb2bc69f"
      ],
      "targetConnectionIds": [
        "07f2f6ff-1da5-4704-916a-c615b873cba9"
      ],
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingId": "79a623960d3f4969835c9e00dc90c8df",
            "mappingVersion": 0
          }
        }
      ]
    }'
```

>[!ENDTABS]

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome del flusso di dati. Assicurati che il nome del flusso di dati sia descrittivo, in quanto può essere utilizzato per cercare informazioni sul flusso di dati. |
| `description` | (Facoltativo) Una proprietà che puoi includere per fornire ulteriori informazioni sul flusso di dati. |
| `flowSpec.id` | ID della specifica di flusso per [!DNL HTTP API]. Per creare un flusso di dati con trasformazioni, devi utilizzare  `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. Per creare un flusso di dati senza trasformazioni, utilizza `d8a6f005-7eaf-4153-983e-e8574508b877`. |
| `sourceConnectionIds` | Il [ID connessione sorgente](#source) recuperato in un passaggio precedente. |
| `targetConnectionIds` | Il [ID connessione di destinazione](#target) recuperato in un passaggio precedente. |
| `transformations.params.mappingId` | Il [ID mappatura](#mapping) recuperato in un passaggio precedente. |

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 con i dettagli del flusso di dati appena creato, incluso il relativo identificatore univoco (`id`).

```json
{
  "id": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
  "etag": "\"dc0459ae-0000-0200-0000-637ebaec0000\""
}
```

## Pubblica i dati da acquisire in Platform {#ingest-data}

>[!NOTE]
>
>È necessario aggiungere un ritardo di almeno ~5 minuti tra la creazione del flusso di dati e l’acquisizione di eventuali dati in streaming. Questo consente di abilitare completamente il flusso di dati prima dell’acquisizione di qualsiasi dato.

Dopo aver creato il flusso, puoi inviare il messaggio JSON all’endpoint di streaming creato in precedenza.

**Formato API**

```http
POST /collection/{INLET_URL}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{INLET_URL}` | URL dell&#39;endpoint di streaming. Per recuperare l’URL, effettua una richiesta GET al `/connections` mentre fornisci l’ID connessione di base. |
| `{FLOW_ID}` | ID del flusso di dati in streaming API HTTP. |

**Richiesta**

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec?x-adobe-flow-id=e5895dc9-b0c8-4431-bab7-bb0d2b4be5db \
  -H 'Content-Type: application/json' \
  -d '{
        "header": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
          },
          "flowId": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
          "datasetId": "604a18a3bae67d18db6d258c"
        },
        "body": {
          "xdmMeta": {
            "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
              "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
            }
          },
          "xdmEntity": {
            "_id": "http-source-connector-acme-01",
            "person": {
              "name": {
                "firstName": "suman",
                "lastName": "nolan"
              }
            },
            "workEmail": {
              "primary": true,
              "address": "suman@acme.com",
              "type": "work",
              "status": "active"
            }
          }
        }
      }'
```

>[!TAB Dati non elaborati]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec?x-adobe-flow-id=e5895dc9-b0c8-4431-bab7-bb0d2b4be5db \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

>[!ENDTABS]

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli delle informazioni appena acquisite.

```json
{
    "inletId": "{BASE_CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BASE_CONNECTION_ID}` | ID della connessione in streaming creata in precedenza. |
| `xactionId` | Un identificatore univoco generato lato server per il record appena inviato. Questo ID aiuta gli Adobi a tracciare il ciclo di vita di questo record attraverso vari sistemi e con il debug. |
| `receivedTimeMs` | Un timestamp (epoca in millisecondi) che mostra l’ora in cui è stata ricevuta la richiesta. |


## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione HTTP in streaming, che consente di utilizzare l’endpoint di streaming per acquisire i dati in Platform. Per istruzioni su come creare una connessione in streaming nell’interfaccia utente, leggi [tutorial sulla creazione di una connessione in streaming](../../../ui/create/streaming/http.md).

Per informazioni su come inviare dati a Platform in streaming, leggi l’esercitazione su [streaming di dati di serie temporali](../../../../../ingestion/tutorials/streaming-time-series-data.md) o il tutorial su [dati di registrazione streaming](../../../../../ingestion/tutorials/streaming-record-data.md).

## Appendice

Questa sezione fornisce informazioni supplementari sulla creazione di connessioni in streaming tramite l’API.

### Invio di messaggi a una connessione streaming autenticata

Se per una connessione in streaming è abilitata l’autenticazione, al client verrà richiesto di aggiungere `Authorization` alla loro richiesta.

Se il `Authorization` l’intestazione non è presente o viene inviato un token di accesso non valido/scaduto, verrà restituita una risposta HTTP 401 Non autorizzato, con una risposta simile a quella riportata di seguito:

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
