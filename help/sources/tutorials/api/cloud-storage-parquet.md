---
keywords: Experience Platform;home;argomenti popolari;connessione origine dati
solution: Experience Platform
title: Acquisire dati Parquet da un sistema di archiviazione cloud di terze parti utilizzando l’API del servizio Flow
type: Tutorial
description: Questa esercitazione utilizza l’API Flow Service per illustrarti i passaggi necessari per acquisire i dati di Apache Parquet da un sistema di archiviazione cloud di terze parti.
exl-id: fb1b19d6-16bb-4a5f-9e81-f537bac95041
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 3%

---

# Acquisire dati Parquet da un sistema di archiviazione cloud di terze parti utilizzando [!DNL Flow Service] API

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da diverse origini all’interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui tutte le sorgenti supportate sono collegabili.

Questa esercitazione utilizza [!DNL Flow Service] API per guidarti attraverso i passaggi per acquisire i dati Parquet da un sistema di archiviazione cloud di terze parti.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Sorgenti](../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
- [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per acquisire correttamente i dati Parquet da un’archiviazione cloud di terze parti utilizzando [!DNL Flow Service] API.

### Lettura delle chiamate API di esempio

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nel [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori per le intestazioni richieste

Per effettuare chiamate a [!DNL Platform] , devi prima completare le [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], compresi quelli appartenenti a [!DNL Flow Service], sono isolate in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

- `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

- `Content-Type: application/json`

## Creare una connessione

Per acquisire i dati di Parquet utilizzando [!DNL Platform] API, devi disporre di una connessione valida per l’origine dell’archiviazione cloud di terze parti a cui stai accedendo. Se non si dispone già di una connessione per l&#39;archiviazione che si desidera utilizzare, è possibile crearne una tramite le seguenti esercitazioni:

- [Amazon S3](./create/cloud-storage/s3.md)
- [BLOB di Azure](./create/cloud-storage/blob.md)
- [Archiviazione Azure Data Lake Gen2](./create/cloud-storage/adls-gen2.md)
- [Google Cloud Store](./create/cloud-storage/google.md)
- [SFTP](./create/cloud-storage/sftp.md)

Ottenere e memorizzare l’identificatore univoco (`$id`) della connessione, quindi procedere al passaggio successivo di questa esercitazione.

## Creare uno schema di destinazione

Per utilizzare i dati di origine in [!DNL Platform], è inoltre necessario creare uno schema di destinazione per strutturare i dati di origine in base alle tue esigenze. Lo schema di destinazione viene quindi utilizzato per creare un [!DNL Platform] set di dati in cui sono contenuti i dati di origine.

Se preferisci utilizzare l’interfaccia utente in [!DNL Experience Platform], il [Esercitazione sull’editor di schemi](../../../xdm/tutorials/create-schema-ui.md) In vengono fornite istruzioni dettagliate per l&#39;esecuzione di azioni simili nell&#39;Editor di schema.

**Formato API**

```http
POST /schemaregistry/tenant/schemas
```

**Richiesta**

L’esempio di richiesta seguente crea uno schema XDM che estende XDM [!DNL Individual Profile] classe.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
    "type": "object",
    "title": "Sample Demo Profile XDM {{$guid}}",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-subscriptions"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        }
    ],
    "meta:containerId": "tenant",
    "meta:resourceType": "schemas",
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile"
}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del nuovo schema creato, incluso il relativo identificatore univoco (`$id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
    "meta:altId": "_{TENANT_ID}.schemas.e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Sample Demo Profile XDM 8d96a964-aad8-43c5-a73a-c8b9b1ccbfb1",
    "type": "object",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-subscriptions",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-subscriptions",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-subscriptions",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1584673864341,
        "repo:lastModifiedDate": 1584673864341,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{MODIFIED_USER_ID}",
        "eTag": "fa704f80da907c8f0f66f453ffcac3e52958687edbf55d71231dc5e1522193c4"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Creare una connessione sorgente {#source}

Con uno schema XDM di destinazione creato, è ora possibile creare una connessione di origine utilizzando una richiesta POST al [!DNL Flow Service] API. Una connessione di origine è costituita da una connessione per l’API, da un formato dati di origine e da un riferimento allo schema XDM di destinazione recuperato nel passaggio precedente.

**Formato API**

```http
POST /sourceConnections
```

**Richiesta**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Source Connection S3 {{$guid}}",
        "baseConnectionId": "5831c52c-c261-4945-b1c5-2cc261d945b2",
        "connectionSpec": {
            "id": "ecadc60c-7455-4d87-84dc-2a0e293d997b",
            "version": 1
        },
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
                "id": "",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "path": "partners-demo/samples",
            "recursive": "true"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `baseConnectionId` | La connessione per l’API che rappresenta l’archiviazione cloud. |
| `data.schema.id` | Il (`$id`) se lo schema xdm di destinazione viene recuperato nel passaggio precedente. |
| `params.path` | Percorso del file di origine. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’identificatore univoco (`id`) della connessione sorgente appena creata. Memorizza questo valore come richiesto nei passaggi successivi per la creazione di una connessione di destinazione.

```json
{
    "id": "73bc8911-505a-4e46-bc89-11505a6e466f",
    "etag": "\"c4004435-0000-0200-0000-5e7437d90000\""
}
```

## Creare una connessione a un set di dati

Per acquisire dati esterni in [!DNL Platform], un [!DNL Experience Platform] è prima necessario acquisire la connessione a un set di dati.

Per creare una connessione a un set di dati, segui i passaggi descritti in [tutorial sulla connessione a dataset base](./create-dataset-base-connection.md).

Continua seguendo i passaggi descritti nella guida per sviluppatori fino a creare una connessione a un set di dati. Ottenere e memorizzare l’identificatore univoco (`$id`) e continuare a utilizzarlo come ID connessione di base nel passaggio successivo per creare una connessione di destinazione.

## Creare un set di dati di destinazione

È possibile creare un set di dati di destinazione eseguendo una richiesta POST al [API Catalog Service](https://www.adobe.io/experience-platform-apis/references/catalog/), che fornisce l’ID dello schema di destinazione all’interno del payload.

**Formato API**

```http
POST /catalog/dataSets
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Leads Dataset {{$guid}}",
        "schemaRef": {
            "id": ""https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80"",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `schemaRef.id` | ID dello schema XDM di destinazione. |

**Risposta**

In caso di esito positivo, la risposta restituisce un array contenente l’ID del set di dati appena creato nel formato `"@/datasets/{DATASET_ID}"`. L’ID del set di dati è una stringa di sola lettura generata dal sistema e utilizzata per fare riferimento al set di dati nelle chiamate API. Memorizza l’ID del set di dati di destinazione come richiesto nei passaggi successivi per creare una connessione di destinazione e un flusso di dati.

```json
[
    "@/dataSets/5e7439b1ad55a618ad4c5102"
]
```

## Creare una connessione di destinazione {#target}

Ora disponi degli identificatori univoci per una connessione a un set di dati, uno schema di destinazione e un set di dati di destinazione. Utilizzando questi identificatori, puoi creare una connessione di destinazione utilizzando [!DNL Flow Service] API per specificare il set di dati che conterrà i dati di origine in entrata.

**Formato API**

```http
POST /targetConnections
```

**Richiesta**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "baseConnectionId": "291257e3-c560-4e07-9257-e3c5606e07d1",
        "connectionSpec": {
            "id":"c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "name": "Target Connection {{$guid}}",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": ""https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80"",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5e7439b1ad55a618ad4c5102"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `baseConnectionId` | ID della connessione al set di dati. |
| `data.schema.id` | Il `$id` dello schema XDM di destinazione. |
| `params.dataSetId` | ID del set di dati di destinazione. |
| `connectionSpec.id` | ID della specifica di connessione per l’archiviazione cloud. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’identificatore univoco della nuova connessione di destinazione (`id`). Memorizza questo valore come richiesto nei passaggi successivi.

```json
{
    "id": "9b3abc95-f2e9-47c1-babc-95f2e927c1ec",
    "etag": "\"7501936b-0000-0200-0000-5e743bcc0000\""
}
```

## Creare un flusso di dati

L’ultimo passaggio per acquisire i dati di Parquet da un’archiviazione cloud di terze parti consiste nel creare un flusso di dati. A questo punto sono stati preparati i seguenti valori obbligatori:

- [ID connessione sorgente](#source)
- [ID connessione di destinazione](#target)

Un flusso di dati è responsabile della pianificazione e della raccolta di dati da un’origine. Puoi creare un flusso di dati eseguendo una richiesta POST e fornendo i valori precedentemente menzionati all’interno del payload.

**Formato API**

```http
POST /flows
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Demo Parquet Ingestion Flow {{$guid}}",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "73bc8911-505a-4e46-bc89-11505a6e466f"
        ],
        "targetConnectionIds": [
            "9b3abc95-f2e9-47c1-babc-95f2e927c1ec"
        ],
        "scheduleParams": {
            "startTime": {{$timestamp}},
            "frequency": "minute",
            "interval": 1000,
            "backfill": true
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `sourceConnectionIds` | ID della connessione di origine recuperato in un passaggio precedente. |
| `targetConnectionIds` | ID di connessione di destinazione recuperato in un passaggio precedente. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID (`id`) del flusso di dati appena creato.

```json
{
    "id": "89ff50ef-b082-426e-bf50-efb082d26e78",
    "etag": "\"890070b8-0000-0200-0000-5e743c040000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un connettore di origine per raccogliere i dati Parquet dal sistema di archiviazione cloud di terze parti su base pianificata. I dati in arrivo possono ora essere utilizzati da downstream [!DNL Platform] servizi quali [!DNL Real-Time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i seguenti documenti:

- [Panoramica del profilo cliente in tempo reale](../../../profile/home.md)
- [Panoramica di Data Science Workspace](../../../data-science-workspace/home.md)
