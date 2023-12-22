---
keywords: Experience Platform;home;argomenti popolari;accesso ai dati;python sdk;spark sdk;API di accesso ai dati;esportare;Export;Home;popular topic;data access;python sdk;spark sdk;data access api;export;Export
solution: Experience Platform
title: Guida dell’API di accesso ai dati
description: L’API di accesso ai dati supporta Adobe Experience Platform fornendo agli sviluppatori un’interfaccia RESTful incentrata sulla reperibilità e l’accessibilità dei set di dati acquisiti in Experienci Platform.
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
source-git-commit: d8694c094ae4a7284e4a3ed0ae5bc3dc198e501a
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 5%

---

# Guida dell’API di accesso ai dati

L’API di accesso ai dati supporta Adobe Experience Platform fornendo agli utenti un’interfaccia RESTful incentrata sulla reperibilità e l’accessibilità dei set di dati acquisiti in [!DNL Experience Platform].

![Un diagramma che illustra come l’accesso ai dati faciliti l’individuazione e l’accessibilità dei set di dati acquisiti in Experienci Platform.](images/Data_Access_Experience_Platform.png)

## Riferimento alle specifiche API

Puoi trovare la documentazione di riferimento dell’API Swagger [qui](https://developer.adobe.com/experience-platform-apis/references/data-access/).

## Terminologia {#terminology}

La tabella fornisce una descrizione di alcuni termini comunemente utilizzati in questo documento.

| Termine | Descrizione |
| ----- | ------------ |
| Set di dati | Una raccolta di dati che include uno schema e dei campi. |
| Batch | Un insieme di dati raccolti in un periodo di tempo ed elaborati insieme come una singola unità. |

## Recuperare l&#39;elenco dei file all&#39;interno di un batch {#retrieve-list-of-files-in-a-batch}

Per recuperare un elenco di file appartenenti a un batch specifico, utilizzare l&#39;identificatore batch (batchID) con l&#39;API di accesso ai dati.

**Formato API**

```http
GET /batches/{BATCH_ID}/files
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{BATCH_ID}` | ID del batch specificato. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```json
{
  "data": [
    {
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
        }
      }
    },
  ],
  "_page": {
    "limit": 100,
    "count": 1
  }
}
```

Il `"data"` array contiene un elenco di tutti i file all&#39;interno del batch specificato. Ogni file restituito ha il proprio ID univoco (`{FILE_ID}`) contenuto all&#39;interno del `"dataSetFileId"` campo. Puoi usare questo ID univoco per accedere o scaricare il file.

| Proprietà | Descrizione |
| -------- | ----------- |
| `data.dataSetFileId` | ID file per ogni file del batch specificato. |
| `data._links.self.href` | URL di accesso al file. |

## Accesso e download di file all&#39;interno di un batch

Per accedere a dettagli specifici di un file, utilizza un identificatore di file (`{FILE_ID}`) con l&#39;API di accesso ai dati, compreso il nome, la dimensione in byte e un collegamento per il download.

La risposta contiene un array di dati. A seconda che il file a cui fa riferimento l’ID sia un singolo file o una directory, l’array di dati restituito può contenere una singola voce o un elenco di file appartenenti a tale directory. Ogni elemento del file include i dettagli del file.

**Formato API**

```http
GET /files/{FILE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{FILE_ID}` | Uguale a `"dataSetFileId"`, ID del file a cui accedere. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta a file singolo**

```JSON
{
  "data": [
    {
      "name": "{FILE_NAME}",
      "length": "{LENGTH}",
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME}"
        }
      }
    }
  ],
  "_page": {
    "limit": 100,
    "count": 1
  }
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `data.name` | Il nome del file (ad esempio, `profiles.csv`). |
| `data.length` | Dimensione del file (in byte). |
| `data._links.self.href` | URL per il download del file. |

**Risposta directory**

```JSON
{
  "data": [
    {
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
        }
      }
    }
  ],
  "_page": {
    "limit": 100,
    "count": 2
  }
}
```

Quando viene restituita una directory, questa contiene una matrice di tutti i file all&#39;interno della directory.

| Proprietà | Descrizione |
| -------- | ----------- |
| `data.name` | Il nome del file (ad esempio, `profiles.csv`). |
| `data._links.self.href` | URL per il download del file. |

## Accedere al contenuto di un file {#access-file-contents}

È inoltre possibile utilizzare [!DNL Data Access] API per accedere al contenuto di un file. Puoi quindi scaricare il contenuto in un’origine esterna.

**Formato API**

```http
GET /files/{dataSetFileId}?path={FILE_NAME}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{FILE_NAME}` | Nome del file a cui si sta tentando di accedere. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{FILE_ID}` | ID del file all’interno di un set di dati. |
| `{FILE_NAME}` | Il nome completo del file (ad esempio, `profiles.csv`). |

**Risposta**

`Contents of the file`

## Esempi di codice aggiuntivi

Per ulteriori esempi, fare riferimento al [tutorial sull’accesso ai dati](tutorials/dataset-data.md).

## Iscriviti agli eventi di acquisizione dati {#subscribe-to-data-ingestion-events}

È possibile abbonarsi a eventi di valore elevato specifici tramite [Console Adobe Developer](https://developer.adobe.com/console/). Ad esempio, puoi abbonarti agli eventi di acquisizione dati per ricevere notifiche su potenziali ritardi e errori. Guarda il tutorial su [abbonamento a notifiche di acquisizione dati](../ingestion/quality/subscribe-events.md) per ulteriori informazioni.
