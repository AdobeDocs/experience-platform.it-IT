---
keywords: Experience Platform;home;argomenti popolari;
solution: Experience Platform
title: Collegare l’area di destinazione dei dati a Adobe Experience Platform utilizzando l’API del servizio di flusso
type: Tutorial
description: Scopri come collegare Adobe Experience Platform all’area di destinazione dei dati utilizzando l’API del servizio di flusso.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: d57060ddeed64d3863f71ac1ea34ccc5c97265ea
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 5%

---

# Connetti [!DNL Data Landing Zone] a Adobe Experience Platform tramite l’API del servizio di flusso

>[!IMPORTANT]
>
>Questa pagina è specifica per [!DNL Data Landing Zone] *source* connettore in Experience Platform. Per informazioni sulla connessione al [!DNL Data Landing Zone] *destinazione* connettore, fare riferimento alla [[!DNL Data Landing Zone] pagina della documentazione di destinazione](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] è una struttura di archiviazione file sicura basata su cloud per l’importazione di file in Adobe Experience Platform. I dati vengono eliminati automaticamente dal [!DNL Data Landing Zone] dopo sette giorni.

Questa esercitazione illustra i passaggi necessari per creare un [!DNL Data Landing Zone] connessione di origine tramite [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Questa esercitazione fornisce anche istruzioni su come recuperare il [!DNL Data Landing Zone], nonché visualizzare e aggiornare le credenziali.

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti dell’Experience Platform:

* [Origini](../../../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per creare correttamente un [!DNL Data Landing Zone] connessione di origine tramite [!DNL Flow Service] API.

Questa esercitazione richiede anche di leggere la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md) per scoprire come autenticare le API di Platform e interpretare le chiamate di esempio fornite nella documentazione.

## Recuperare una zona di destinazione utilizzabile

Il primo passaggio nell’utilizzo delle API per accedere a [!DNL Data Landing Zone] deve effettuare una richiesta di GET al `/landingzone` punto finale [!DNL Connectors] API fornendo `type=user_drop_zone` come parte dell’intestazione della richiesta.

**Formato API**

```http
GET /data/foundation/connectors/landingzone?type=user_drop_zone
```

| Intestazioni | Descrizione |
| --- | --- |
| `user_drop_zone` | La `user_drop_zone` type consente all’API di distinguere un contenitore di zona di destinazione dagli altri tipi di contenitori disponibili. |

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

La risposta seguente restituisce informazioni su una zona di destinazione, inclusa la corrispondente `containerName` e `containerTTL`.

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `containerName` | Nome della zona di destinazione recuperata. |
| `containerTTL` | Il tempo di scadenza (in giorni) applicato ai dati all’interno della zona di destinazione. Tutte le operazioni all’interno di una determinata zona di sbarco vengono eliminate dopo sette giorni. |

## Recupera [!DNL Data Landing Zone] credenziali

Per recuperare le credenziali di un [!DNL Data Landing Zone], invia una richiesta di GET al `/credentials` punto finale [!DNL Connectors] API.

**Formato API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=user_drop_zone
```

**Richiesta**

Nell’esempio di richiesta seguente vengono recuperate le credenziali per una zona di destinazione esistente.

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

La risposta seguente restituisce le informazioni delle credenziali per la zona di destinazione, incluso l’attuale `SASToken` e `SASUri`, nonché `storageAccountName` corrisponde al contenitore della zona di destinazione.

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
| `containerName` | Nome della zona di destinazione. |
| `SASToken` | Token della firma di accesso condiviso per la zona di destinazione. Questa stringa contiene tutte le informazioni necessarie per autorizzare una richiesta. |
| `SASUri` | URI della firma di accesso condiviso per la zona di destinazione. Questa stringa è una combinazione dell’URI con la zona di destinazione per la quale si sta effettuando l’autenticazione e il relativo token SAS, |


## Aggiorna [!DNL Data Landing Zone] credenziali

È possibile aggiornare `SASToken` effettuando una richiesta di POST al `/credentials` punto finale [!DNL Connectors] API.

**Formato API**

```http
POST /data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| Intestazioni | Descrizione |
| --- | --- |
| `user_drop_zone` | La `user_drop_zone` type consente all’API di distinguere un contenitore di zona di destinazione dagli altri tipi di contenitori disponibili. |
| `refresh` | La `refresh` consente di ripristinare le credenziali della zona di destinazione e generare automaticamente un nuovo `SASToken`. |

**Richiesta**

La seguente richiesta aggiorna le credenziali della zona di destinazione.

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

La risposta seguente restituisce i valori aggiornati per la `SASToken` e `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## Esplorare la struttura e il contenuto dei file della zona di destinazione

Puoi esplorare la struttura dei file e il contenuto della zona di destinazione effettuando una richiesta di GET al `connectionSpecs` punto finale [!DNL Flow Service] API.

**Formato API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| Parametro | Descrizione |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | ID della specifica di connessione corrispondente a [!DNL Data Landing Zone]. Questo ID fisso è: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

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

Una risposta corretta restituisce un array di file e cartelle presenti nella directory interrogata. Prendi nota della `path` proprietà del file che desideri caricare, in quanto devi fornirlo nel passaggio successivo per esaminarne la struttura.

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

Per esaminare la struttura di un file nella zona di destinazione, esegui una richiesta di GET fornendo il percorso del file e digita come parametro di query.

**Formato API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| Parametro | Descrizione | Esempio |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | ID della specifica di connessione corrispondente a [!DNL Data Landing Zone]. Questo ID fisso è: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |
| `{OBJECT_TYPE}` | Il tipo di oggetto a cui si desidera accedere. | `file` |
| `{OBJECT}` | Percorso e nome dell&#39;oggetto a cui si desidera accedere. | `dlz-user-container/data8.csv` |
| `{FILE_TYPE}` | Il tipo di file. | <ul><li>`delimited`</li><li>`json`</li><li>`parquet`</li></ul> |
| `{PREVIEW}` | Un valore booleano che definisce se l’anteprima del file è supportata. | </ul><li>`true`</li><li>`false`</li></ul> |

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

Una risposta corretta restituisce la struttura del file interrogato, inclusi i nomi dei file e i tipi di dati.

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

### Utilizzo `determineProperties` per rilevare automaticamente le informazioni sulle proprietà dei file di un [!DNL Data Landing Zone]

È possibile utilizzare `determineProperties` per rilevare automaticamente le informazioni sulla proprietà del contenuto del file [!DNL Data Landing Zone] quando effettui una chiamata GET per esplorare i contenuti e la struttura della tua sorgente.

#### `determineProperties` casi di utilizzo

La tabella seguente illustra diversi scenari che è possibile incontrare quando si utilizza il `determineProperties` eseguire una query del parametro o fornire manualmente informazioni sul file.

| `determineProperties` | `queryParams` | Risposta |
| --- | --- | --- |
| True | N/D | Se `determineProperties` viene fornito come parametro di query, quindi si verifica il rilevamento delle proprietà del file e la risposta restituisce un nuovo `properties` che include informazioni sul tipo di file, il tipo di compressione e il delimitatore di colonna. |
| N/D | True | Se i valori per tipo di file, tipo di compressione e delimitatore di colonna sono forniti manualmente come parte di `queryParams`, vengono quindi utilizzati per generare lo schema e le stesse proprietà vengono restituite come parte della risposta. |
| True | True | Se entrambe le opzioni vengono eseguite contemporaneamente, viene restituito un errore. |
| N/D | N/D | Se non viene fornita nessuna delle due opzioni, viene restituito un errore perché non è possibile ottenere le proprietà per la risposta. |

**Formato API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| Parametro | Descrizione | Esempio |
| --- | --- | --- |
| `determineProperties` | Questo parametro di query consente il [!DNL Flow Service] API per rilevare informazioni sulle proprietà del file, tra cui informazioni sul tipo di file, il tipo di compressione e il delimitatore di colonna. | `true` |

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

Una risposta corretta restituisce la struttura del file interrogato, inclusi i nomi dei file e i tipi di dati, nonché un `properties` chiave, contenente informazioni su `fileType`, `compressionType`e `columnDelimiter`.

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
| `properties.fileType` | Il tipo di file corrispondente del file interrogato. I tipi di file supportati sono: `delimited`, `json`e `parquet`. |
| `properties.compressionType` | Il tipo di compressione corrispondente utilizzato per il file interrogato. I tipi di compressione supportati sono: <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | Il delimitatore di colonna corrispondente utilizzato per il file interrogato. Qualsiasi valore di carattere singolo è un delimitatore di colonna consentito. Il valore predefinito è una virgola `(,)`. |


## Creazione di una connessione sorgente

Una connessione di origine crea e gestisce la connessione all’origine esterna da cui vengono acquisiti i dati. Una connessione di origine è costituita da informazioni quali l’origine dati, il formato dati e l’ID di connessione di origine necessari per creare un flusso di dati. Un’istanza di connessione di origine è specifica per un tenant e un’organizzazione IMS.

Per creare una connessione di origine, invia una richiesta POST al `/sourceConnections` punto finale [!DNL Flow Service] API.


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
| `name` | Il nome del tuo [!DNL Data Landing Zone] connessione di origine. |
| `data.format` | Il formato dei dati che desideri inserire in Platform. |
| `params.path` | Il percorso del file che desideri portare in Platform. |
| `connectionSpec.id` | ID della specifica di connessione corrispondente a [!DNL Data Landing Zone]. Questo ID fisso è: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della nuova connessione sorgente creata. Questo ID è necessario nell’esercitazione successiva per creare un flusso di dati.

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai recuperato il tuo [!DNL Data Landing Zone] , ne è stata esplorata la struttura del file per trovare il file che si desidera portare in Platform e è stata creata una connessione di origine per iniziare a inserire i dati in Platform. È ora possibile passare all’esercitazione successiva, in cui verrà illustrato come [creare un flusso di dati per portare i dati di archiviazione cloud a Platform utilizzando [!DNL Flow Service] API](../../collect/cloud-storage.md).
