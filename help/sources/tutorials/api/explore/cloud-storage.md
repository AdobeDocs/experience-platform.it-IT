---
keywords: Experience Platform;home;argomenti popolari;archiviazione cloud;archiviazione cloud
title: Esplorare le cartelle di archiviazione cloud utilizzando l’API del servizio Flusso
description: Questa esercitazione utilizza l’API Flow Service per esplorare un sistema di archiviazione cloud di terze parti.
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: 88e6f084ce1b857f785c4c1721d514ac3b07e80b
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 2%

---

# Esplora le cartelle di archiviazione cloud utilizzando [!DNL Flow Service] API

Questo tutorial illustra come esplorare e visualizzare in anteprima la struttura e i contenuti dell’archiviazione cloud utilizzando [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API.

>[!NOTE]
>
>Per esplorare l’archiviazione cloud, è necessario disporre già di un ID connessione di base valido per un’origine di archiviazione cloud. Se non disponi di questo ID, consulta [panoramica sulle origini](../../../home.md#cloud-storage) per un elenco delle origini di archiviazione cloud con cui è possibile creare una connessione di base.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../landing/api-guide.md).

## Esplora le cartelle di archiviazione cloud

Per recuperare informazioni sulla struttura delle cartelle di archiviazione cloud, effettua una richiesta GET al [!DNL Flow Service] fornendo l’ID della connessione di base della sorgente.

Quando esegui richieste GET per esplorare l’archiviazione cloud, devi includere i parametri di query elencati nella tabella seguente:

| Parametro | Descrizione |
| --------- | ----------- |
| `objectType` | Tipo di oggetto che si desidera esplorare. Imposta questo valore come: <ul><li>`folder`: esplora una directory specifica</li><li>`root`: esplora la directory principale.</li></ul> |
| `object` | Questo parametro è necessario solo quando si visualizza una directory specifica. Il relativo valore rappresenta il percorso della directory che desideri esplorare. |


**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID della connessione di base dell’origine di archiviazione cloud. |
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

In caso di esito positivo, la risposta restituisce un array di file e cartelle presenti nella directory in cui è stata eseguita la query. Prendi nota della `path` del file che desideri caricare, in quanto è necessario fornirlo nel passaggio successivo per esaminarne la struttura.

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

## Inspect: struttura di un file

Per controllare la struttura del file di dati dall’archiviazione cloud, esegui una richiesta di GET fornendo il percorso del file e digita come parametro di query.

Puoi controllare la struttura di un file di dati dall’origine dell’archiviazione cloud eseguendo una richiesta di GET e fornendo il percorso e il tipo del file. Puoi anche esaminare diversi tipi di file, come CSV, TSV o JSON compresso e file delimitati specificandone i tipi come parte dei parametri di query.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=FILE&object={FILE_PATH}&preview=true&ileType=delimited&encoding=ISO-8859-1;
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | ID di connessione del connettore di origine dell’archiviazione cloud. |
| `{FILE_PATH}` | Percorso del file che si desidera controllare. |
| `{FILE_TYPE}` | Il tipo di file. I tipi di file supportati includono:<ul><li>DELIMITATO</code>: valore separato da delimitatore. I file DSV devono essere separati da virgole.</li><li>JSON</code>: notazione oggetto JavaScript. I file JSON devono essere conformi a XDM</li><li>PARQUET</code>: Apache Parquet I file Parquet devono essere conformi a XDM.</li></ul> |
| `{QUERY_PARAMS}` | Parametri di query facoltativi che possono essere utilizzati per filtrare i risultati. Consulta la sezione su [parametri di query](#query) per ulteriori informazioni. |

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

In caso di esito positivo, la risposta restituisce la struttura del file oggetto della query, inclusi i nomi delle tabelle e i tipi di dati.

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

Il [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) supporta l’utilizzo di parametri di query per l’anteprima e l’ispezione di diversi tipi di file.

| Parametro | Descrizione |
| --------- | ----------- |
| `columnDelimiter` | Il valore di un singolo carattere specificato come delimitatore di colonna per esaminare i file CSV o TSV. Se il parametro non viene fornito, il valore predefinito è una virgola `(,)`. |
| `compressionType` | Parametro query obbligatorio per l’anteprima di un file delimitato o JSON compresso. I file compressi supportati sono: <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `encoding` | Definisce il tipo di codifica da utilizzare per il rendering dell&#39;anteprima. I tipi di codifica supportati sono: `UTF-8` e `ISO-8859-1`. **Nota**: Il `encoding` Il parametro è disponibile solo durante l’acquisizione di file CSV delimitati. Altri tipi di file verranno acquisiti con la codifica predefinita, `UTF-8`. |

## Passaggi successivi

Seguendo questa esercitazione, hai esplorato il sistema di archiviazione cloud e trovato il percorso del file che desideri importare in [!DNL Platform]e ne ha visualizzato la struttura. Queste informazioni sono disponibili nell&#39;esercitazione successiva per [raccogliere dati dall’archiviazione cloud e inserirli in Platform](../collect/cloud-storage.md).
