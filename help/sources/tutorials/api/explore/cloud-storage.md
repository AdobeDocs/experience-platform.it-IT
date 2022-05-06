---
keywords: Experience Platform;home;argomenti comuni;archiviazione cloud;archiviazione cloud
title: Esplorare cartelle di archiviazione cloud utilizzando l’API del servizio di flusso
description: Questa esercitazione utilizza l’API del servizio Flusso per esplorare un sistema di archiviazione cloud di terze parti.
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: 88e6f084ce1b857f785c4c1721d514ac3b07e80b
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 2%

---

# Esplora le cartelle di archiviazione cloud utilizzando [!DNL Flow Service] API

Questa esercitazione fornisce passaggi su come esplorare e visualizzare in anteprima la struttura e il contenuto dell&#39;archiviazione cloud utilizzando [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API.

>[!NOTE]
>
>Per esplorare l&#39;archiviazione cloud, è necessario disporre già di un ID di connessione di base valido per un&#39;origine di archiviazione cloud. Se non disponi di questo ID, consulta la sezione [panoramica di origini](../../../home.md#cloud-storage) per un elenco delle origini di archiviazione cloud con cui è possibile creare una connessione di base.

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../landing/api-guide.md).

## Esplora le cartelle di archiviazione cloud

È possibile recuperare informazioni sulla struttura delle cartelle di archiviazione cloud effettuando una richiesta di GET al [!DNL Flow Service] API fornendo l&#39;ID di connessione di base della sorgente.

Quando esegui richieste di GET per esplorare l’archiviazione cloud, devi includere i parametri di query elencati nella tabella seguente:

| Parametro | Descrizione |
| --------- | ----------- |
| `objectType` | Tipo di oggetto da esplorare. Imposta questo valore come: <ul><li>`folder`: Esplorare una directory specifica</li><li>`root`: Esplora la directory principale.</li></ul> |
| `object` | Questo parametro è necessario solo quando si visualizza una directory specifica. Il suo valore rappresenta il percorso della directory che desideri esplorare. |


**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID di connessione di base dell&#39;origine di archiviazione cloud. |
| `{PATH}` | Percorso di una directory. |

**Richiesta**

```shell
curl -X GET \
  'http://platform.adobe.io/data/foundation/flowservice/connections/dc3c0646-5e30-47be-a1ce-d162cb8f1f07/explore?objectType=folder&object=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un array di file e cartelle presenti nella directory interrogata. Prendi nota della `path` proprietà del file che desideri caricare, in quanto devi fornirlo nel passaggio successivo per esaminarne la struttura.

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "/test-connectors/testFolder-fileIngestion/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "profileData.json",
        "path": "/test-connectors/testFolder-fileIngestion/profileData.json",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "sampleprofile--3.parquet",
        "path": "/test-connectors/testFolder-fileIngestion/sampleprofile--3.parquet",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect la struttura di un file

Per esaminare la struttura del file di dati dall’archiviazione cloud, esegui una richiesta di GET fornendo il percorso del file e digita come parametro di query.

È possibile esaminare la struttura di un file di dati dall&#39;origine di archiviazione cloud eseguendo una richiesta di GET fornendo il percorso e il tipo del file. Puoi anche controllare diversi tipi di file come CSV, TSV o JSON compresso e delimitare i file specificando i rispettivi tipi di file come parte dei parametri di query.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=FILE&object={FILE_PATH}&preview=true&ileType=delimited&encoding=ISO-8859-1;
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | ID di connessione del connettore di origine dell&#39;archiviazione cloud. |
| `{FILE_PATH}` | Percorso del file da esaminare. |
| `{FILE_TYPE}` | Il tipo di file. I tipi di file supportati sono:<ul><li>DELIMITATO</code>: Valore separato da delimitatore. I file DSV devono essere separati da virgole.</li><li>JSON</code>: Notazione oggetto JavaScript. I file JSON devono essere conformi a XDM</li><li>PARQUET</code>: Parquet Apache. I file di parquet devono essere conformi a XDM.</li></ul> |
| `{QUERY_PARAMS}` | Parametri di query facoltativi che possono essere utilizzati per filtrare i risultati. Vedi la sezione su [parametri di query](#query) per ulteriori informazioni. |

**Richiesta**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce la struttura del file interrogato, inclusi i nomi di tabella e i tipi di dati.

```json
[
    {
        "name": "Id",
        "type": "String"
    },
    {
        "name": "FirstName",
        "type": "String"
    },
    {
        "name": "LastName",
        "type": "String"
    },
    {
        "name": "Email",
        "type": "String"
    },
    {
        "name": "Phone",
        "type": "String"
    }
]
```

## Utilizzo dei parametri di query {#query}

La [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) supporta l’utilizzo di parametri di query per visualizzare in anteprima ed esaminare diversi tipi di file.

| Parametro | Descrizione |
| --------- | ----------- |
| `columnDelimiter` | Il valore a carattere singolo specificato come delimitatore di colonna per esaminare i file CSV o TSV. Se il parametro non viene fornito, il valore predefinito è una virgola `(,)`. |
| `compressionType` | Un parametro di query obbligatorio per l’anteprima di un file JSON o delimitato compresso. I file compressi supportati sono: <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `encoding` | Definisce il tipo di codifica da utilizzare per il rendering dell’anteprima. I tipi di codifica supportati sono: `UTF-8` e `ISO-8859-1`. **Nota**: La `encoding` è disponibile solo durante l’acquisizione di file CSV delimitati. Altri tipi di file verranno acquisiti con la codifica predefinita, `UTF-8`. |

## Passaggi successivi

Seguendo questa esercitazione, hai esplorato il tuo sistema di archiviazione cloud, trovato il percorso del file a cui desideri accedere [!DNL Platform]e ne ha visualizzato la struttura. Puoi utilizzare queste informazioni nell’esercitazione successiva per [raccogliere dati dall’archivio cloud e inserirli in Platform](../collect/cloud-storage.md).
