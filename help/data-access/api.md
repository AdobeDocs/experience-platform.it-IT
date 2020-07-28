---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida per gli sviluppatori Data Access
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 4%

---


# Guida per gli sviluppatori Data Access

L&#39;API Data Access supporta  Adobe Experience Platform fornendo agli utenti un&#39;interfaccia RESTful incentrata sulla scoperta e l&#39;accessibilità dei set di dati acquisiti all&#39;interno [!DNL Experience Platform].

![Accesso ai dati  Experience Platform](images/Data_Access_Experience_Platform.png)

## Riferimento della specifica API

La documentazione di riferimento per le API Swagger è disponibile [qui](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml).

## Terminologia

Una descrizione di alcuni termini comunemente utilizzati in tutto il documento.

| Termine | Descrizione |
| ----- | ------------ |
| Set di dati | Raccolta di dati che include schema e campi. |
| Batch | Un insieme di dati raccolti in un determinato periodo di tempo ed elaborati insieme come un&#39;unica unità. |

## Recupera elenco di file all&#39;interno di un batch

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

L&#39; `"data"` array contiene un elenco di tutti i file all&#39;interno del batch specificato. Ogni file restituito ha un proprio ID univoco (`{FILE_ID}`) contenuto nel `"dataSetFileId"` campo. Questo ID univoco può quindi essere utilizzato per accedere o scaricare il file.

| Proprietà | Descrizione |
| -------- | ----------- |
| `data.dataSetFileId` | ID file per ciascun file del batch specificato. |
| `data._links.self.href` | URL per accedere al file. |

## Accedere e scaricare i file in un batch

Utilizzando un identificatore file (`{FILE_ID}`), l&#39;API di accesso ai dati può essere utilizzata per accedere ai dettagli specifici di un file, incluso il nome, la dimensione in byte e un collegamento da scaricare.

La risposta conterrà un array di dati. A seconda che il file a cui fa riferimento l’ID sia un singolo file o una directory, l’array di dati restituito può contenere una singola voce o un elenco di file appartenenti a tale directory. Ogni elemento file includerà i dettagli del file.

**Formato API**

```http
GET /files/{FILE_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{FILE_ID}` | Uguale all’ `"dataSetFileId"`, l’ID del file a cui accedere. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta a un singolo file**

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
| `data.name` | Nome del file (ad esempio, profile.csv). |
| `data.length` | Dimensione del file (in byte). |
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

Quando viene restituita una directory, essa contiene un array di tutti i file all’interno della directory.

| Proprietà | Descrizione |
| -------- | ----------- |
| `data.name` | Nome del file (ad esempio, profile.csv). |
| `data._links.self.href` | URL per scaricare il file. |

## Accesso al contenuto di un file

L&#39; [!DNL Data Access] API può essere utilizzata anche per accedere al contenuto di un file. Questo può essere utilizzato per scaricare il contenuto in un&#39;origine esterna.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{FILE_ID}` | L&#39;ID del file all&#39;interno di un set di dati. |
| `{FILE_NAME}` | Nome completo del file (ad esempio, profile.csv). |

**Risposta**

```
Contents of the file
```

## Esempi di codice aggiuntivi

Per ulteriori esempi, fare riferimento all&#39;esercitazione sull&#39;accesso ai [dati](tutorials/dataset-data.md).

## Iscrizione agli eventi di assimilazione dei dati

[!DNL Platform] rende disponibili per l&#39;iscrizione specifici eventi di alto valore tramite la [Developer Console](https://www.adobe.com/go/devs_console_ui). Ad esempio, puoi abbonarti agli eventi di inserimento dei dati per ricevere una notifica di potenziali ritardi e guasti. Per ulteriori informazioni, consulta l’esercitazione sulla [sottoscrizione alle notifiche](../ingestion/quality/subscribe-events.md) di assimilazione dei dati.