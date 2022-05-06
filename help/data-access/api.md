---
keywords: Experience Platform;home;argomenti popolari;accesso ai dati;sdk python;scintilla sdk;api di accesso ai dati;esportazione;esportazione
solution: Experience Platform
title: Guida all’API di accesso ai dati
topic-legacy: developer guide
description: L’API di accesso ai dati supporta Adobe Experience Platform fornendo agli sviluppatori un’interfaccia RESTful incentrata sulla scoperta e l’accessibilità dei set di dati acquisiti all’interno di Experience Platform.
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 6%

---

# Guida all’API di accesso ai dati

L’API di accesso ai dati supporta Adobe Experience Platform fornendo agli utenti un’interfaccia RESTful incentrata sulla scoperta e l’accessibilità dei set di dati acquisiti all’interno di [!DNL Experience Platform].

![Accesso ai dati su Experience Platform](images/Data_Access_Experience_Platform.png)

## Riferimento alle specifiche API

La documentazione di riferimento dell’API Swagger è disponibile [qui](https://www.adobe.io/experience-platform-apis/references/data-access/).

## Terminologia

Una descrizione di alcuni termini comunemente utilizzati in questo documento.

| Termine | Descrizione |
| ----- | ------------ |
| Set di dati | Raccolta di dati che include schema e campi. |
| Batch | Un insieme di dati raccolti in un periodo di tempo ed elaborati insieme come un’unica unità. |

## Recupera elenco di file all’interno di un batch

Utilizzando un identificatore batch (batchID), l&#39;API di accesso ai dati può recuperare un elenco di file appartenenti a quel particolare batch.

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

La `"data"` contiene un elenco di tutti i file all&#39;interno del batch specificato. Ogni file restituito ha un proprio ID univoco (`{FILE_ID}`) all&#39;interno del `"dataSetFileId"` campo . Questo ID univoco può quindi essere utilizzato per accedere o scaricare il file.

| Proprietà | Descrizione |
| -------- | ----------- |
| `data.dataSetFileId` | ID file per ogni file nel batch specificato. |
| `data._links.self.href` | URL per accedere al file. |

## Accedere e scaricare file in un batch

Utilizzando un identificatore di file (`{FILE_ID}`), l’API di accesso ai dati può essere utilizzata per accedere a dettagli specifici di un file, tra cui nome, dimensione in byte e un collegamento da scaricare.

La risposta conterrà un array di dati. A seconda che il file a cui fa riferimento l’ID sia un singolo file o una directory, l’array di dati restituito può contenere una singola voce o un elenco di file appartenenti a tale directory. Ogni elemento file includerà i dettagli del file.

**Formato API**

```http
GET /files/{FILE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{FILE_ID}` | Uguale a `"dataSetFileId"`, l’ID del file a cui accedere. |

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
| `data.name` | Nome del file (ad esempio profiles.csv). |
| `data.length` | Dimensioni del file (in byte). |
| `data._links.self.href` | URL per scaricare il file. |

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

Quando viene restituita una directory, contiene una matrice di tutti i file all’interno della directory.

| Proprietà | Descrizione |
| -------- | ----------- |
| `data.name` | Nome del file (ad esempio profiles.csv). |
| `data._links.self.href` | URL per scaricare il file. |

## Accedere al contenuto di un file

La [!DNL Data Access] L’API può essere utilizzata anche per accedere al contenuto di un file . Può quindi essere utilizzato per scaricare il contenuto in un’origine esterna.

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
| `{FILE_NAME}` | Nome completo del file (ad esempio profiles.csv). |

**Risposta**

`Contents of the file`

## Esempi di codice aggiuntivi

Per ulteriori campioni, consulta la sezione [esercitazione sull&#39;accesso ai dati](tutorials/dataset-data.md).

## Iscriviti agli eventi di inserimento dati

[!DNL Platform] rende disponibili per l’abbonamento eventi specifici di alto valore tramite [Console per sviluppatori di Adobe](https://www.adobe.com/go/devs_console_ui). Ad esempio, puoi abbonarti a eventi di inserimento dati per ricevere notifiche su potenziali ritardi e errori. Guarda l’esercitazione su [sottoscrizione alle notifiche di inserimento dati](../ingestion/quality/subscribe-events.md) per ulteriori informazioni.
