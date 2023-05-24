---
keywords: Experience Platform;home;argomenti popolari;
solution: Experience Platform
title: Connettere Data Landing Zone a Adobe Experience Platform utilizzando l’API del servizio Flow
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a Data Landing Zone utilizzando l’API del servizio Flusso.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 5%

---

# Connetti [!DNL Data Landing Zone] a Adobe Experience Platform utilizzando l’API del servizio Flusso

>[!IMPORTANT]
>
>Questa pagina è specifica per [!DNL Data Landing Zone] *sorgente* connettore in Experience Platform. Per informazioni sulla connessione al [!DNL Data Landing Zone] *destinazione* connettore, fare riferimento al [[!DNL Data Landing Zone] pagina della documentazione di destinazione](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] è una struttura di archiviazione dei file sicura e basata su cloud per importare i file in Adobe Experience Platform. I dati vengono eliminati automaticamente dal [!DNL Data Landing Zone] dopo sette giorni.

Questo tutorial illustra i passaggi necessari per creare un [!DNL Data Landing Zone] connessione sorgente tramite [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Questo tutorial fornisce anche istruzioni su come recuperare [!DNL Data Landing Zone], nonché visualizzare e aggiornare le credenziali.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Sorgenti](../../../../home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per creare correttamente un [!DNL Data Landing Zone] connessione sorgente tramite [!DNL Flow Service] API.

Questo tutorial richiede anche di leggere la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md) per scoprire come eseguire l’autenticazione nelle API di Platform e interpretare le chiamate di esempio fornite nella documentazione.

## Recuperare una zona di destinazione utilizzabile

Il primo passaggio nell’utilizzo delle API per accedere a [!DNL Data Landing Zone] è effettuare una richiesta GET al `/landingzone` endpoint del [!DNL Connectors] API durante la fornitura di `type=user_drop_zone` come parte dell’intestazione della richiesta.

**Formato API**

```http
GET /data/foundation/connectors/landingzone?type=user_drop_zone
```

| Intestazioni | Descrizione |
| --- | --- |
| `user_drop_zone` | Il `user_drop_zone` Il tipo consente all’API di distinguere un contenitore per zona di destinazione dagli altri tipi di contenitori disponibili. |

**Richiesta**

La richiesta seguente recupera una zona di destinazione esistente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**Risposta**

La risposta che segue restituisce informazioni su una zona di atterraggio, compresi i dati corrispondenti `containerName` e `containerTTL`.

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `containerName` | Nome della zona di destinazione recuperata. |
| `containerTTL` | Il tempo di scadenza (in giorni) applicato ai dati all’interno della zona di destinazione. Qualsiasi valore all’interno di una determinata zona di sbarco viene cancellato dopo sette giorni. |

## Recupera [!DNL Data Landing Zone] credenziali

Per recuperare le credenziali per un [!DNL Data Landing Zone], invia una richiesta GET al `/credentials` endpoint del [!DNL Connectors] API.

**Formato API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=user_drop_zone
```

**Richiesta**

L’esempio di richiesta seguente recupera le credenziali per una zona di destinazione esistente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Risposta**

La risposta seguente restituisce le informazioni sulle credenziali per la zona di destinazione, incluso l’attuale `SASToken` e `SASUri`, nonché `storageAccountName` che corrisponde al contenitore della zona di destinazione.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `containerName` | Il nome della zona di destinazione. |
| `SASToken` | Il token di firma di accesso condiviso per la tua zona di destinazione. Questa stringa contiene tutte le informazioni necessarie per autorizzare una richiesta. |
| `SASUri` | URI della firma di accesso condiviso per la zona di destinazione. Questa stringa è una combinazione dell&#39;URI della zona di destinazione per la quale si sta effettuando l&#39;autenticazione e del token SAS corrispondente, |


## Aggiorna [!DNL Data Landing Zone] credenziali

È possibile aggiornare `SASToken` facendo una richiesta POST al `/credentials` endpoint del [!DNL Connectors] API.

**Formato API**

```http
POST /data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| Intestazioni | Descrizione |
| --- | --- |
| `user_drop_zone` | Il `user_drop_zone` Il tipo consente all’API di distinguere un contenitore per zona di destinazione dagli altri tipi di contenitori disponibili. |
| `refresh` | Il `refresh` consente di reimpostare le credenziali della zona di destinazione e generare automaticamente un nuovo `SASToken`. |

**Richiesta**

La richiesta seguente aggiorna le credenziali della zona di destinazione.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Risposta**

La seguente risposta restituisce valori aggiornati per il `SASToken` e `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## Esplora la struttura e il contenuto del file della zona di destinazione

Puoi esplorare la struttura del file e il contenuto della zona di destinazione effettuando una richiesta GET al `connectionSpecs` endpoint del [!DNL Flow Service] API.

**Formato API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| Parametro | Descrizione |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | ID della specifica di connessione che corrisponde a [!DNL Data Landing Zone]. Questo ID fisso è: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Richiesta**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
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
        "path": "dlz-user-container/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "data8.csv",
        "path": "dlz-user-container/data8.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "folder",
        "name": "userdata1",
        "path": "dlz-user-container/userdata1/",
        "canPreview": false,
        "canFetchSchema": false
    }
]
```

## Anteprima della struttura e del contenuto del file della zona di destinazione

Per controllare la struttura di un file nella zona di destinazione, esegui una richiesta di GET fornendo il percorso del file e digita come parametro di query.

**Formato API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| Parametro | Descrizione | Esempio |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | ID della specifica di connessione che corrisponde a [!DNL Data Landing Zone]. Questo ID fisso è: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |
| `{OBJECT_TYPE}` | Tipo di oggetto a cui si desidera accedere. | `file` |
| `{OBJECT}` | Percorso e nome dell&#39;oggetto a cui si desidera accedere. | `dlz-user-container/data8.csv` |
| `{FILE_TYPE}` | Il tipo di file. | <ul><li>`delimited`</li><li>`json`</li><li>`parquet`</li></ul> |
| `{PREVIEW}` | Valore booleano che definisce se l’anteprima del file è supportata. | </ul><li>`true`</li><li>`false`</li></ul> |

**Richiesta**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/data8.csv&fileType=delimited&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce la struttura del file oggetto della query, inclusi i nomi e i tipi di dati dei file.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "FirstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "LastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Phone",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Email": "rsmith@abc.com",
            "FirstName": "Richard",
            "Phone": "111111111",
            "Id": "12345",
            "LastName": "Smith"
        },
        {
            "Email": "morgan@bac.com",
            "FirstName": "Morgan",
            "Phone": "22222222222",
            "Id": "67890",
            "LastName": "Hart"
        }
    ]
}
```

### Utilizzare `determineProperties` per rilevare automaticamente le informazioni sulle proprietà di un file [!DNL Data Landing Zone]

È possibile utilizzare `determineProperties` parametro per rilevare automaticamente le informazioni sulle proprietà del contenuto del file [!DNL Data Landing Zone] quando effettui una chiamata di GET per esplorare il contenuto e la struttura dell’origine.

#### `determineProperties` casi di utilizzo

La tabella seguente illustra i diversi scenari che possono verificarsi quando si utilizza `determineProperties` parametro di query o fornire manualmente informazioni sul file.

| `determineProperties` | `queryParams` | Risposta |
| --- | --- | --- |
| True | N/D | Se `determineProperties` viene fornito come parametro di query, viene rilevato il rilevamento delle proprietà del file e la risposta restituisce un nuovo `properties` chiave che include informazioni sul tipo di file, sul tipo di compressione e sul delimitatore di colonna. |
| N/D | True | Se i valori per tipo di file, tipo di compressione e delimitatore di colonna vengono forniti manualmente come parte di `queryParams`, quindi vengono utilizzati per generare lo schema e le stesse proprietà vengono restituite come parte della risposta. |
| True | True | Se entrambe le opzioni vengono eseguite contemporaneamente, viene restituito un errore. |
| N/D | N/D | Se non viene fornita nessuna delle due opzioni, viene restituito un errore perché non è possibile ottenere le proprietà per la risposta. |

**Formato API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| Parametro | Descrizione | Esempio |
| --- | --- | --- |
| `determineProperties` | Questo parametro di query consente [!DNL Flow Service] API per rilevare informazioni relative alle proprietà del file, tra cui informazioni sul tipo di file, il tipo di compressione e il delimitatore di colonna. | `true` |

**Richiesta**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/garageWeek/file1&preview=true&determineProperties=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce la struttura del file oggetto della query, inclusi i nomi e i tipi di dati, nonché una `properties` chiave, contenente informazioni su `fileType`, `compressionType`, e `columnDelimiter`.

+++Fai clic qui

```json
{
    "properties": {
        "fileType": "delimited",
        "compressionType": "tarGzip",
        "columnDelimiter": "~"
    },
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "firstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "lastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "birthday",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "birthday": "1313-0505-19731973",
            "firstName": "Yvonne",
            "lastName": "Thilda",
            "id": "100",
            "email": "Yvonne.Thilda@yopmail.com"
        },
        {
            "birthday": "1515-1212-19731973",
            "firstName": "Mary",
            "lastName": "Pillsbury",
            "id": "101",
            "email": "Mary.Pillsbury@yopmail.com"
        },
        {
            "birthday": "0505-1010-19751975",
            "firstName": "Corene",
            "lastName": "Joeann",
            "id": "102",
            "email": "Corene.Joeann@yopmail.com"
        },
        {
            "birthday": "2727-0303-19901990",
            "firstName": "Dari",
            "lastName": "Greenwald",
            "id": "103",
            "email": "Dari.Greenwald@yopmail.com"
        },
        {
            "birthday": "1717-0404-19651965",
            "firstName": "Lucy",
            "lastName": "Magdalen",
            "id": "199",
            "email": "Lucy.Magdalen@yopmail.com"
        }
    ]
}
```

+++

| Proprietà | Descrizione |
| --- | --- |
| `properties.fileType` | Il tipo di file corrispondente del file sottoposto a query. I tipi di file supportati sono: `delimited`, `json`, e `parquet`. |
| `properties.compressionType` | Tipo di compressione corrispondente utilizzato per il file sottoposto a query. I tipi di compressione supportati sono: <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | Il delimitatore di colonna corrispondente utilizzato per il file sottoposto a query. Qualsiasi valore di carattere singolo è un delimitatore di colonna consentito. Il valore predefinito è una virgola `(,)`. |


## Creare una connessione sorgente

Una connessione di origine crea e gestisce la connessione all’origine esterna da cui vengono acquisiti i dati. Una connessione di origine è costituita da informazioni quali origine dati, formato dati e ID della connessione di origine necessari per creare un flusso di dati. Un&#39;istanza della connessione di origine è specifica di un tenant e di un&#39;organizzazione.

Per creare una connessione sorgente, effettua una richiesta POST al `/sourceConnections` endpoint del [!DNL Flow Service] API.


**Formato API**

```http
POST /sourceConnections
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Data Landing Zone source connection",
        "data": {
            "format": "delimited"
        },
        "params": {
            "path": "dlz-user-container/data8.csv"
        },
        "connectionSpec": {
            "id": "26f526f2-58f4-4712-961d-e41bf1ccc0e8",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Il nome del tuo [!DNL Data Landing Zone] connessione sorgente. |
| `data.format` | Il formato dei dati che desideri inserire in Platform. |
| `params.path` | Percorso del file da portare su Platform. |
| `connectionSpec.id` | ID della specifica di connessione che corrisponde a [!DNL Data Landing Zone]. Questo ID fisso è: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’identificatore univoco (`id`) della connessione sorgente appena creata. Questo ID è richiesto nell’esercitazione successiva per creare un flusso di dati.

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai recuperato [!DNL Data Landing Zone] , ne ha esplorato la struttura per trovare il file da portare in Platform e ha creato una connessione di origine per iniziare a portare i dati in Platform. Ora puoi passare alla prossima esercitazione, dove scoprirai come [crea un flusso di dati per portare i dati di archiviazione cloud su Platform utilizzando [!DNL Flow Service] API](../../collect/cloud-storage.md).
