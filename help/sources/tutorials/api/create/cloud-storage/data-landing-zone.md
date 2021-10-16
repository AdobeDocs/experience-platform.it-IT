---
keywords: Experience Platform;home;argomenti popolari;
solution: Experience Platform
title: Collegare l’area di destinazione dei dati a Adobe Experience Platform utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform all’area di destinazione dei dati utilizzando l’API del servizio di flusso.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: 57089cc9aa9c586f5fae70e2a7154d48ebd62447
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 4%

---

# Connetti [!DNL Data Landing Zone] a Adobe Experience Platform utilizzando l’API del servizio di flusso

[!DNL Data Landing Zone] è una struttura di archiviazione dati basata su cloud per l’archiviazione temporanea dei file con provisioning di Adobe Experience Platform. I dati vengono eliminati automaticamente dal [!DNL Data Landing Zone] dopo sette giorni.

Questa esercitazione illustra i passaggi necessari per creare una connessione sorgente [!DNL Data Landing Zone] utilizzando l&#39; [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Questa esercitazione fornisce anche istruzioni su come recuperare le [!DNL Data Landing Zone], nonché visualizzare e aggiornare le credenziali.

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti dell’Experience Platform:

* [Origini](../../../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per creare correttamente una connessione sorgente [!DNL Data Landing Zone] utilizzando l&#39;API [!DNL Flow Service].

Questa esercitazione richiede anche di leggere la guida [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md) per scoprire come eseguire l’autenticazione nelle API di Platform e interpretare le chiamate di esempio fornite nella documentazione.

## Recuperare una zona di destinazione utilizzabile

Il primo passaggio nell’utilizzo delle API per accedere a [!DNL Data Landing Zone] consiste nell’effettuare una richiesta di GET all’ `/landingzone` endpoint dell’ [!DNL Connectors] API fornendo `type=user_drop_zone` come parte dell’intestazione della richiesta.

**Formato API**

```http
GET /connectors/landingzone?type=user_drop_zone
```

| Intestazioni | Descrizione |
| --- | --- |
| `user_drop_zone` | Il tipo `user_drop_zone` consente all’API di distinguere un contenitore di zona di destinazione dagli altri tipi di contenitori disponibili. |

**Richiesta**

La richiesta seguente recupera una zona di destinazione esistente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**Risposta**

La risposta seguente restituisce informazioni su una zona di destinazione, compresi i corrispondenti `containerName` e `containerTTL`.

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `containerName` | Nome della zona di destinazione recuperata. |
| `containerTTL` | L’impostazione &quot;time-to-live&quot; applicata ai dati all’interno della zona di destinazione. Tutte le operazioni all’interno di una determinata zona di sbarco vengono eliminate dopo sette giorni. |

## Recupera le credenziali [!DNL Data Landing Zone]

Per recuperare le credenziali per un [!DNL Data Landing Zone], invia una richiesta di GET all’ endpoint `/credentials` dell’ API [!DNL Connectors].

**Formato API**

```http
GET /connectors/landingzone/credentials?type=user_drop_zone
```

**Richiesta**

Nell’esempio di richiesta seguente vengono recuperate le credenziali per una zona di destinazione esistente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Risposta**

La risposta seguente restituisce le informazioni sulle credenziali per la zona di destinazione, compresi i `SASToken` e `SASUri` correnti, nonché il `storageAccountName` corrispondente al contenitore della zona di destinazione.

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


## Aggiorna le credenziali [!DNL Data Landing Zone]

Puoi aggiornare il tuo `SASToken` effettuando una richiesta POST all&#39;endpoint `/credentials` dell&#39;API [!DNL Connectors].

**Formato API**

```http
POST /connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| Intestazioni | Descrizione |
| --- | --- |
| `user_drop_zone` | Il tipo `user_drop_zone` consente all’API di distinguere un contenitore di zona di destinazione dagli altri tipi di contenitori disponibili. |
| `refresh` | L’azione `refresh` ti consente di reimpostare le credenziali della zona di destinazione e di generare automaticamente un nuovo elemento `SASToken`. |

**Richiesta**

La seguente richiesta aggiorna le credenziali della zona di destinazione.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Risposta**

La risposta seguente restituisce valori aggiornati per i valori `SASToken` e `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## Esplorare la struttura e il contenuto dei file della zona di destinazione

Puoi esplorare la struttura dei file e il contenuto della zona di destinazione effettuando una richiesta di GET all’ `connectionSpecs` endpoint dell’ API [!DNL Flow Service] .

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un array di file e cartelle presenti nella directory interrogata. Prendi nota della proprietà `path` del file da caricare, in quanto devi fornirlo nel passaggio successivo per controllarne la struttura.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce la struttura del file interrogato, inclusi i nomi di tabella e i tipi di dati.

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

## Creazione di una connessione sorgente

Una connessione di origine crea e gestisce la connessione all’origine esterna da cui vengono acquisiti i dati. Una connessione di origine è costituita da informazioni quali l’origine dati, il formato dati e l’ID di connessione di origine necessari per creare un flusso di dati. Un’istanza di connessione di origine è specifica per un tenant e un’organizzazione IMS.

Per creare una connessione sorgente, effettua una richiesta POST all’ endpoint `/sourceConnections` dell’ API [!DNL Flow Service] .


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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Nome della connessione [!DNL Data Landing Zone] di origine. |
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

Seguendo questa esercitazione, hai recuperato le credenziali [!DNL Data Landing Zone], esplorato la struttura del file per trovare il file che desideri portare a Platform e creato una connessione di origine per iniziare a inserire i dati in Platform. È ora possibile passare all’esercitazione successiva, in cui verrà illustrato come [creare un flusso di dati per portare i dati di archiviazione cloud a Platform utilizzando l’ [!DNL Flow Service] API](../../collect/cloud-storage.md).
