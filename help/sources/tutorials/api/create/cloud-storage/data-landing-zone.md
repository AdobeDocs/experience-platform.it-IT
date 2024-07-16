---
keywords: Experience Platform;home;argomenti popolari;
solution: Experience Platform
title: Connettere Data Landing Zone a Adobe Experience Platform utilizzando l’API del servizio Flow
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a Data Landing Zone utilizzando l’API del servizio Flusso.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: 0089aa0d6b765645840e6954c3957282c2ad972b
workflow-type: tm+mt
source-wordcount: '1300'
ht-degree: 5%

---

# Connetti [!DNL Data Landing Zone] a Adobe Experience Platform utilizzando l&#39;API del servizio Flusso

>[!IMPORTANT]
>
>Questa pagina è specifica per il connettore [!DNL Data Landing Zone] *source* in Experience Platform. Per informazioni sulla connessione al connettore [!DNL Data Landing Zone] *destination*, consulta la [[!DNL Data Landing Zone] pagina della documentazione di destinazione](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] è una struttura di archiviazione dei file sicura e basata su cloud per l&#39;inserimento di file in Adobe Experience Platform. I dati vengono eliminati automaticamente da [!DNL Data Landing Zone] dopo sette giorni.

Questo tutorial illustra i passaggi necessari per creare una connessione di origine [!DNL Data Landing Zone] utilizzando l&#39;[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Questo tutorial fornisce anche istruzioni su come recuperare [!DNL Data Landing Zone], nonché visualizzare e aggiornare le credenziali.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per creare correttamente una connessione di origine [!DNL Data Landing Zone] utilizzando l&#39;API [!DNL Flow Service].

Questo tutorial richiede anche di leggere la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md) per scoprire come eseguire l&#39;autenticazione nelle API di Platform e interpretare le chiamate di esempio fornite nella documentazione.

## Recuperare una zona di destinazione utilizzabile

Il primo passaggio nell&#39;utilizzo delle API per accedere a [!DNL Data Landing Zone] consiste nell&#39;effettuare una richiesta GET all&#39;endpoint `/landingzone` dell&#39;API [!DNL Connectors] fornendo `type=user_drop_zone` come parte dell&#39;intestazione della richiesta.

**Formato API**

```http
GET /data/foundation/connectors/landingzone?type=user_drop_zone
```

| Intestazioni | Descrizione |
| --- | --- |
| `user_drop_zone` | Il tipo `user_drop_zone` consente all&#39;API di distinguere un contenitore di zona di destinazione dagli altri tipi di contenitori disponibili. |

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

La risposta seguente restituisce informazioni su una zona di destinazione, inclusi i corrispondenti `containerName` e `containerTTL`.

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

## Recupera credenziali [!DNL Data Landing Zone]

Per recuperare le credenziali per un [!DNL Data Landing Zone], effettuare una richiesta GET all&#39;endpoint `/credentials` dell&#39;API [!DNL Connectors].

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

La risposta seguente restituisce le informazioni sulle credenziali per la zona di destinazione dati, inclusi `SASToken`, `SASUri`, `storageAccountName` e la data di scadenza correnti.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "expiryDate": "2024-01-06"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `containerName` | Il nome della zona di destinazione. |
| `SASToken` | Il token di firma di accesso condiviso per la tua zona di destinazione. Questa stringa contiene tutte le informazioni necessarie per autorizzare una richiesta. |
| `SASUri` | URI della firma di accesso condiviso per la zona di destinazione. Questa stringa è una combinazione dell&#39;URI della zona di destinazione per la quale si sta effettuando l&#39;autenticazione e del token SAS corrispondente, |
| `expiryDate` | Data di scadenza del token SAS. Devi aggiornare il token prima della data di scadenza per continuare a utilizzarlo nell’applicazione per caricare dati nella Data Landing Zone. Se non aggiorni manualmente il token prima della data di scadenza indicata, questo verrà aggiornato automaticamente e fornirà un nuovo token quando viene eseguita la chiamata delle credenziali GET. |


## Aggiorna credenziali [!DNL Data Landing Zone]

È possibile aggiornare `SASToken` effettuando una richiesta POST all&#39;endpoint `/credentials` dell&#39;API [!DNL Connectors].

**Formato API**

```http
POST /data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| Intestazioni | Descrizione |
| --- | --- |
| `user_drop_zone` | Il tipo `user_drop_zone` consente all&#39;API di distinguere un contenitore di zona di destinazione dagli altri tipi di contenitori disponibili. |
| `refresh` | L&#39;azione `refresh` consente di reimpostare le credenziali della zona di destinazione e generare automaticamente un nuovo `SASToken`. |

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

La seguente risposta restituisce valori aggiornati per `SASToken` e `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "expiryDate": "2024-01-06"
}
```

## Esplora la struttura e il contenuto del file della zona di destinazione

È possibile esplorare la struttura e il contenuto del file della zona di destinazione effettuando una richiesta GET all&#39;endpoint `connectionSpecs` dell&#39;API [!DNL Flow Service].

**Formato API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| Parametro | Descrizione |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | ID della specifica di connessione corrispondente a [!DNL Data Landing Zone]. ID corretto: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

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

In caso di esito positivo, la risposta restituisce un array di file e cartelle presenti nella directory in cui è stata eseguita la query. Prendere nota della proprietà `path` del file che si desidera caricare, in quanto è necessario fornirla nel passaggio successivo per esaminarne la struttura.

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
| `{CONNECTION_SPEC_ID}` | ID della specifica di connessione corrispondente a [!DNL Data Landing Zone]. ID corretto: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |
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

### Utilizza `determineProperties` per rilevare automaticamente le informazioni sulle proprietà di un file [!DNL Data Landing Zone]

È possibile utilizzare il parametro `determineProperties` per rilevare automaticamente le informazioni sulle proprietà del contenuto del file di [!DNL Data Landing Zone] durante una chiamata di GET per esplorare il contenuto e la struttura dell&#39;origine.

#### `determineProperties` casi d&#39;uso

Nella tabella seguente vengono descritti i diversi scenari che è possibile incontrare quando si utilizza il parametro di query `determineProperties` o si forniscono manualmente informazioni sul file.

| `determineProperties` | `queryParams` | Risposta |
| --- | --- | --- |
| True | N/D | Se `determineProperties` viene fornito come parametro di query, viene rilevato il rilevamento delle proprietà del file e la risposta restituisce una nuova chiave `properties` che include informazioni sul tipo di file, sul tipo di compressione e sul delimitatore di colonna. |
| N/D | True | Se i valori per tipo di file, tipo di compressione e delimitatore di colonna vengono forniti manualmente come parte di `queryParams`, vengono utilizzati per generare lo schema e le stesse proprietà vengono restituite come parte della risposta. |
| True | True | Se entrambe le opzioni vengono eseguite contemporaneamente, viene restituito un errore. |
| N/D | N/D | Se non viene fornita nessuna delle due opzioni, viene restituito un errore perché non è possibile ottenere le proprietà per la risposta. |

**Formato API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| Parametro | Descrizione | Esempio |
| --- | --- | --- |
| `determineProperties` | Questo parametro di query consente all&#39;API [!DNL Flow Service] di rilevare informazioni relative alle proprietà del file, incluse informazioni sul tipo di file, sul tipo di compressione e sul delimitatore di colonna. | `true` |

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

In caso di esito positivo, la risposta restituisce la struttura del file su cui è stata eseguita la query, inclusi i nomi e i tipi di dati dei file, nonché una chiave `properties` contenente informazioni su `fileType`, `compressionType` e `columnDelimiter`.

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
| `properties.fileType` | Il tipo di file corrispondente del file sottoposto a query. I tipi di file supportati sono: `delimited`, `json` e `parquet`. |
| `properties.compressionType` | Tipo di compressione corrispondente utilizzato per il file sottoposto a query. I tipi di compressione supportati sono: <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | Il delimitatore di colonna corrispondente utilizzato per il file sottoposto a query. Qualsiasi valore di carattere singolo è un delimitatore di colonna consentito. Il valore predefinito è una virgola `(,)`. |


## Creare una connessione sorgente

Una connessione di origine crea e gestisce la connessione all’origine esterna da cui vengono acquisiti i dati. Una connessione di origine è costituita da informazioni quali origine dati, formato dati e ID della connessione di origine necessari per creare un flusso di dati. Un&#39;istanza della connessione di origine è specifica di un tenant e di un&#39;organizzazione.

Per creare una connessione di origine, effettuare una richiesta POST all&#39;endpoint `/sourceConnections` dell&#39;API [!DNL Flow Service].


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
| `name` | Nome della connessione di origine [!DNL Data Landing Zone]. |
| `data.format` | Il formato dei dati che desideri inserire in Platform. |
| `params.path` | Percorso del file da portare su Platform. |
| `connectionSpec.id` | ID della specifica di connessione corrispondente a [!DNL Data Landing Zone]. ID corretto: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;identificatore univoco (`id`) della connessione di origine appena creata. Questo ID è richiesto nell’esercitazione successiva per creare un flusso di dati.

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai recuperato le credenziali di [!DNL Data Landing Zone], ne hai esplorato la struttura per trovare il file da portare in Platform e hai creato una connessione di origine per iniziare a portare i dati in Platform. Ora puoi passare alla prossima esercitazione, dove scoprirai come [creare un flusso di dati per portare i dati dell&#39;archiviazione cloud in Platform utilizzando l&#39;API [!DNL Flow Service] 2}.](../../collect/cloud-storage.md)
