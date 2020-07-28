---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Esplora un sistema di archiviazione cloud utilizzando l'API del servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---


# Esplora un sistema di archiviazione cloud utilizzando l&#39; [!DNL Flow Service] API

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti diverse all&#39;interno  Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39; [!DNL Flow Service] API per esplorare un sistema di archiviazione cloud di terze parti.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti del  Adobe Experience Platform:

* [Origini](../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] i servizi.
* [Sandbox](../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a un sistema di archiviazione cloud utilizzando l&#39; [!DNL Flow Service] API.

### Ottenere una connessione di base

Per esplorare un archivio cloud di terze parti tramite [!DNL Platform] le API, è necessario possedere un ID di connessione di base valido. Se non si dispone già di una connessione di base per l&#39;archivio con cui si desidera lavorare, è possibile crearne una tramite le seguenti esercitazioni:

* [Amazon S3](../create/cloud-storage/s3.md)
* [BLOB di Azure](../create/cloud-storage/blob.md)
* [Azure Data Lake Storage Gen2](../create/cloud-storage/adls-gen2.md)
* [Google Cloud Store](../create/cloud-storage/google.md)
* [SFTP](../create/cloud-storage/sftp.md)

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* Content-Type: `application/json`

## Esplora l&#39;archiviazione cloud

Utilizzando la connessione di base per l&#39;archiviazione cloud, potete esplorare file e directory eseguendo richieste di GET. Quando si eseguono richieste di GET per esplorare l&#39;archiviazione cloud, è necessario includere i parametri di query elencati nella tabella seguente:

| Parametro | Descrizione |
| --------- | ----------- |
| `objectType` | Il tipo di oggetto che si desidera esplorare. Imposta questo valore come: <ul><li>`folder`: Esplora una directory specifica</li><li>`root`: Esplora la directory principale.</li></ul> |
| `object` | Questo parametro è richiesto solo quando si visualizza una directory specifica. Il suo valore rappresenta il percorso della directory che desiderate esplorare. |

Utilizzate la seguente chiamata per trovare il percorso del file in cui desiderate inserire [!DNL Platform]:

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID di una connessione di base per l&#39;archiviazione cloud. |
| `{PATH}` | Percorso di una directory. |

**Richiesta**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object=/some/path/' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un array di file e cartelle presenti nella directory interrogata. Prendete nota della `path` proprietà del file che desiderate caricare, in quanto dovete fornire al passaggio successivo per ispezionarne la struttura.

```json
[
    {
        "type": "File",
        "name": "data.csv",
        "path": "/some/path/data.csv"
    },
    {
        "type": "Folder",
        "name": "foobar",
        "path": "/some/path/foobar"
    }
]
```

##  Inspect la struttura di un file

Per esaminare la struttura del file di dati dall&#39;archivio cloud, esegui una richiesta di GET fornendo il percorso del file come parametro di query.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID di una connessione di base per l&#39;archiviazione cloud. |
| `{FILE_PATH}` | Percorso di un file. |
| `{FILE_TYPE}` | Il tipo di file. I tipi di file supportati includono:<ul><li>DELIMITATO</code>: Valore separato da delimitatore. I file DSV devono essere separati da virgole.</li><li>JSON</code>: Notazione oggetto JavaScript. I file JSON devono essere conformi a XDM</li><li>PARQUET</code>: Parquet Apache. I file parquet devono essere conformi a XDM.</li></ul> |

**Richiesta**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=file&object=/some/path/data.csv&fileType=DELIMITED' \
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

## Passaggi successivi

Seguendo questa esercitazione, hai esplorato il sistema di archiviazione cloud, trovato il percorso del file a cui desideri accedere [!DNL Platform]e ne hai visualizzato la struttura. Potete utilizzare queste informazioni nell&#39;esercitazione successiva per [raccogliere i dati dall&#39;archivio cloud e portarli in Platform](../collect/cloud-storage.md).