---
keywords: Experience Platform;home;argomenti comuni;connessione origine dati
solution: Experience Platform
title: Inserire dati di parquet da un sistema di storage cloud di terze parti utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Questa esercitazione utilizza l’API del servizio Flusso per illustrarvi i passaggi necessari per acquisire i dati Apache Parquet da un sistema di archiviazione cloud di terze parti.
exl-id: fb1b19d6-16bb-4a5f-9e81-f537bac95041
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 3%

---

# Acquisire dati Parquet da un sistema di archiviazione cloud di terze parti utilizzando [!DNL Flow Service] API

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti all&#39;interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui è possibile connettere tutte le sorgenti supportate.

Questa esercitazione utilizza la funzione [!DNL Flow Service] API per illustrarvi i passaggi necessari per acquisire dati Parquet da un sistema di archiviazione cloud di terze parti.

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [Origini](../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
- [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per acquisire correttamente i dati di Parquet da un archivio cloud di terze parti utilizzando il [!DNL Flow Service] API.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], compresi quelli appartenenti [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

- `Content-Type: application/json`

## Creare una connessione

Per acquisire i dati del parquet utilizzando [!DNL Platform] API, è necessario disporre di una connessione valida per l&#39;origine di archiviazione cloud di terze parti a cui si accede. Se non si dispone già di una connessione per lo storage con cui si desidera lavorare, è possibile crearne una tramite le seguenti esercitazioni:

- [Amazon S3](./create/cloud-storage/s3.md)
- [BLOB di Azure](./create/cloud-storage/blob.md)
- [Azure Data Lake Storage Gen2](./create/cloud-storage/adls-gen2.md)
- [Google Cloud Store](./create/cloud-storage/google.md)
- [SFTP](./create/cloud-storage/sftp.md)

Ottieni e archivia l&#39;identificatore univoco (`$id`) della connessione, quindi passare al passaggio successivo di questa esercitazione.

## Creare uno schema di destinazione

Per utilizzare i dati di origine in [!DNL Platform], è inoltre necessario creare uno schema di destinazione per strutturare i dati di origine in base alle esigenze. Lo schema di destinazione viene quindi utilizzato per creare un [!DNL Platform] set di dati in cui sono contenuti i dati di origine.

Se preferisci utilizzare l’interfaccia utente in [!DNL Experience Platform], [Esercitazione sull’Editor di schema](../../../xdm/tutorials/create-schema-ui.md) fornisce istruzioni dettagliate per l’esecuzione di azioni simili nell’Editor di schema.

**Formato API**

```http
POST /schemaregistry/tenant/schemas
```

**Richiesta**

La seguente richiesta di esempio crea uno schema XDM che estende XDM [!DNL Individual Profile] classe.

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

Una risposta corretta restituisce i dettagli dello schema appena creato, incluso il relativo identificatore univoco (`$id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

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

## Creazione di una connessione sorgente {#source}

Con uno schema XDM di destinazione creato, è ora possibile creare una connessione di origine utilizzando una richiesta di POST per [!DNL Flow Service] API. Una connessione di origine è costituita da una connessione per l’API, un formato di dati di origine e un riferimento allo schema XDM di destinazione recuperato nel passaggio precedente.

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
| `baseConnectionId` | Connessione per l’API che rappresenta l’archiviazione cloud. |
| `data.schema.id` | (`$id`) se lo schema xdm di destinazione è stato recuperato nel passaggio precedente. |
| `params.path` | Percorso del file di origine. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della nuova connessione sorgente creata. Memorizza questo valore come richiesto nei passaggi successivi per la creazione di una connessione di destinazione.

```json
{
    "id": "73bc8911-505a-4e46-bc89-11505a6e466f",
    "etag": "\"c4004435-0000-0200-0000-5e7437d90000\""
}
```

## Creare una connessione di base di set di dati

Per acquisire dati esterni in [!DNL Platform], un [!DNL Experience Platform] prima è necessario acquisire la connessione alla base di dati.

Per creare una connessione a una base di dati, segui i passaggi descritti in [esercitazione sulla connessione base di set di dati](./create-dataset-base-connection.md).

Continua a seguire i passaggi descritti nella guida per gli sviluppatori fino a quando non avrai creato una connessione di base ai set di dati. Ottieni e archivia l&#39;identificatore univoco (`$id`) e procedi a utilizzarlo come ID di connessione di base nel passaggio successivo per creare una connessione di destinazione.

## Creare un set di dati di destinazione

È possibile creare un set di dati di destinazione eseguendo una richiesta di POST al [API del servizio catalogo](https://www.adobe.io/experience-platform-apis/references/catalog/), fornendo l’ID dello schema di destinazione all’interno del payload.

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

Una risposta corretta restituisce un array contenente l&#39;ID del set di dati appena creato nel formato `"@/datasets/{DATASET_ID}"`. L’ID del set di dati è una stringa di sola lettura generata dal sistema che viene utilizzata per fare riferimento al set di dati nelle chiamate API. Memorizza l’ID del set di dati di destinazione come richiesto nei passaggi successivi per creare una connessione di destinazione e un flusso di dati.

```json
[
    "@/dataSets/5e7439b1ad55a618ad4c5102"
]
```

## Creare una connessione di destinazione {#target}

Ora sono disponibili gli identificatori univoci per una connessione a base di set di dati, uno schema di destinazione e un set di dati di destinazione. Utilizzando questi identificatori, puoi creare una connessione di destinazione utilizzando [!DNL Flow Service] API per specificare il set di dati che conterrà i dati di origine in entrata.

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
| `baseConnectionId` | ID della connessione di base del set di dati. |
| `data.schema.id` | La `$id` dello schema XDM di destinazione. |
| `params.dataSetId` | ID del set di dati di destinazione. |
| `connectionSpec.id` | ID delle specifiche di connessione per l&#39;archiviazione cloud. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco della nuova connessione di destinazione (`id`). Memorizza questo valore come richiesto nei passaggi successivi.

```json
{
    "id": "9b3abc95-f2e9-47c1-babc-95f2e927c1ec",
    "etag": "\"7501936b-0000-0200-0000-5e743bcc0000\""
}
```

## Creare un flusso di dati

L’ultimo passo verso l’acquisizione di dati Parquet da un archivio cloud di terze parti è quello di creare un flusso di dati. A questo punto sono stati preparati i seguenti valori richiesti:

- [ID connessione di origine](#source)
- [ID connessione di destinazione](#target)

Un flusso di dati è responsabile della pianificazione e della raccolta dei dati da un’origine. È possibile creare un flusso di dati eseguendo una richiesta di POST fornendo al contempo i valori precedentemente menzionati all’interno del payload.

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
| `sourceConnectionIds` | L&#39;ID della connessione di origine recuperato in un passaggio precedente. |
| `targetConnectionIds` | L&#39;ID di connessione di destinazione recuperato in un passaggio precedente. |

**Risposta**

Una risposta corretta restituisce l&#39;ID (`id`) del flusso di dati appena creato.

```json
{
    "id": "89ff50ef-b082-426e-bf50-efb082d26e78",
    "etag": "\"890070b8-0000-0200-0000-5e743c040000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un connettore di origine per raccogliere i dati di Parquet dal sistema di archiviazione cloud di terze parti su base pianificata. I dati in arrivo possono ora essere utilizzati da downstream [!DNL Platform] servizi quali [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i seguenti documenti:

- [Panoramica del profilo cliente in tempo reale](../../../profile/home.md)
- [Panoramica di Data Science Workspace](../../../data-science-workspace/home.md)
