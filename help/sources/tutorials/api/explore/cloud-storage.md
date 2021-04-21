---
keywords: Experience Platform;home;argomenti comuni;archiviazione cloud;archiviazione cloud
solution: Experience Platform
title: Esplorare un sistema di storage ad alta voce utilizzando l’API del servizio di flusso
topic-legacy: overview
description: Questa esercitazione utilizza l’API del servizio Flusso per esplorare un sistema di archiviazione cloud di terze parti.
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 1%

---

# Esplorare un sistema di archiviazione cloud utilizzando l&#39;API [!DNL Flow Service]

Questa esercitazione utilizza l’ [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) per esplorare un sistema di archiviazione cloud di terze parti.

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../home.md):  [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
* [Sandbox](../../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a un sistema di archiviazione cloud utilizzando l’ [!DNL Flow Service] API .

### Ottenere un ID di connessione

Per esplorare un archivio cloud di terze parti utilizzando le API [!DNL Platform], è necessario disporre di un ID di connessione valido. Se non si dispone già di una connessione per lo storage con cui si desidera lavorare, è possibile crearne una tramite le seguenti esercitazioni:

* [[!DNL Amazon S3]](../create/cloud-storage/s3.md)
* [[!DNL Azure Blob]](../create/cloud-storage/blob.md)
* [[!DNL Azure Data Lake Storage Gen2]](../create/cloud-storage/adls-gen2.md)
* [[!DNL Azure File Storage]](../create/cloud-storage/azure-file-storage.md)
* [[!DNL FTP]](../create/cloud-storage/ftp.md)
* [[!DNL Google Cloud Storage]](../create/cloud-storage/google.md)
* [HDFS](../create/cloud-storage/hdfs.md)
* [[!DNL Oracle Object Storage]](../create/cloud-storage/oracle-object-storage.md)
* [[!DNL SFTP]](../create/cloud-storage/sftp.md)

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* `Content-Type: application/json`

## Esplora l&#39;archiviazione cloud

Utilizzando l’ID di connessione per l’archiviazione cloud, puoi esplorare file e directory eseguendo richieste GET. Quando esegui richieste di GET per esplorare l’archiviazione cloud, devi includere i parametri di query elencati nella tabella seguente:

| Parametro | Descrizione |
| --------- | ----------- |
| `objectType` | Tipo di oggetto da esplorare. Imposta questo valore come: <ul><li>`folder`: Esplorare una directory specifica</li><li>`root`: Esplora la directory principale.</li></ul> |
| `object` | Questo parametro è necessario solo quando si visualizza una directory specifica. Il suo valore rappresenta il percorso della directory che desideri esplorare. |

Utilizza la seguente chiamata per trovare il percorso del file da inserire in [!DNL Platform]:

**Formato API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
GET /connections/{CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONNECTION_ID}` | ID di connessione per il connettore di origine dell&#39;archiviazione cloud. |
| `{PATH}` | Percorso di una directory. |

**Richiesta**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=folder&object=/some/path/' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un array di file e cartelle presenti nella directory interrogata. Prendi nota della proprietà `path` del file che desideri caricare, in quanto devi fornirlo nel passaggio successivo per controllarne la struttura.

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

È possibile esaminare la struttura di un file di dati dall&#39;origine di archiviazione cloud eseguendo una richiesta di GET fornendo il percorso e il tipo del file. Puoi anche controllare diversi tipi di file come CSV, TSV o JSON compresso e delimitare i file specificando i relativi tipi di file come parte dei parametri di query.

**Formato API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | ID di connessione del connettore di origine dell&#39;archiviazione cloud. |
| `{FILE_PATH}` | Percorso del file da esaminare. |
| `{FILE_TYPE}` | Il tipo di file. I tipi di file supportati sono:<ul><li>DELIMITATO</code>: Valore separato da delimitatore. I file DSV devono essere separati da virgole.</li><li>JSON</code>: Notazione oggetto JavaScript. I file JSON devono essere conformi a XDM</li><li>PARQUET</code>: Parquet Apache. I file di parquet devono essere conformi a XDM.</li></ul> |
| `{QUERY_PARAMS}` | Parametri di query facoltativi che possono essere utilizzati per filtrare i risultati. Per ulteriori informazioni, consulta la sezione sui [parametri di query](#query) . |

**Richiesta**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

L&#39; [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) supporta l&#39;utilizzo di parametri di query per visualizzare in anteprima ed esaminare diversi tipi di file.

| Parametro | Descrizione |
| --------- | ----------- |
| `columnDelimiter` | Il valore a carattere singolo specificato come delimitatore di colonna per esaminare i file CSV o TSV. Se il parametro non viene fornito, il valore predefinito è una virgola `(,)`. |
| `compressionType` | Un parametro di query obbligatorio per l’anteprima di un file JSON o delimitato compresso. I file compressi supportati sono: <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |

## Passaggi successivi

Seguendo questa esercitazione, hai esplorato il tuo sistema di archiviazione cloud, trovato il percorso del file che desideri portare in [!DNL Platform] e ne hai visualizzato la struttura. Puoi utilizzare queste informazioni nell&#39;esercitazione successiva per [raccogliere dati dall&#39;archiviazione cloud e inserirli in Platform](../collect/cloud-storage.md).
