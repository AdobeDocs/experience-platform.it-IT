---
title: Collegare l’archiviazione BLOB di Azure ad Experience Platform utilizzando l’API del servizio Flusso
description: Scopri come connettere Adobe Experience Platform a Azure Blob utilizzando l’API del servizio Flusso.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 7acdc090c020de31ee1a010d71a2969ec9e5bbe1
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 3%

---

# Connetti [!DNL Azure Blob Storage] ad Experience Platform utilizzando l&#39;API

Leggi questa guida per scoprire come collegare il tuo account [!DNL Azure Blobg Storage] a Adobe Experience Platform utilizzando [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Experience Platform

Per informazioni su come effettuare correttamente chiamate alle API di Experience Platform, consulta la guida introduttiva [alle API di Experience Platform](../../../../../landing/api-guide.md).

### Raccogli le credenziali richieste

Per informazioni sull&#39;autenticazione, leggere la [[!DNL Azure Blob Storage] panoramica](../../../../connectors/cloud-storage/blob.md#authentication).

## Connetti il tuo account [!DNL Azure Blob Storage] ad Experience Platform {#connect}

Per informazioni su come collegare il tuo account [!DNL Azure Blob Storage] ad Experience Platform, leggi i passaggi seguenti.

### Creare una connessione di base

>[!NOTE]
>
>Una volta creata, non è possibile modificare il tipo di autenticazione di una connessione di base [!DNL Azure Blob Storage]. Per modificare il tipo di autenticazione, è necessario creare una nuova connessione di base.

Una connessione di base collega l’origine ad Experience Platform, memorizzando i dettagli di autenticazione, lo stato della connessione e un ID univoco. Utilizza questo ID per sfogliare i file sorgente e identificare elementi specifici da acquisire, compresi i relativi tipi di dati e formati.

È possibile connettere l&#39;account [!DNL Azure Blob Storage] ad Experience Platform utilizzando i seguenti tipi di autenticazione:

* **Autenticazione chiave account**: utilizza la chiave di accesso dell&#39;account di archiviazione per autenticare e connettersi all&#39;account [!DNL Azure Blob Storage].
* **Firma di accesso condiviso (SAS)**: utilizza un URI SAS per fornire accesso delegato e limitato nel tempo alle risorse nell&#39;account [!DNL Azure Blob Storage].
* **Autenticazione basata sull&#39;entità servizio**: utilizza un&#39;entità servizio Azure Active Directory (AAD) (ID client e segreto) per l&#39;autenticazione sicura nell&#39;account di archiviazione BLOB di Azure.

**Formato API**

```https
POST /connections
```

Per creare un ID connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` e fornire le credenziali di autenticazione come parte dei parametri della richiesta.

>[!BEGINTABS]

>[!TAB Autenticazione chiave account]

Per utilizzare l&#39;autenticazione della chiave dell&#39;account, fornire i valori per `connectionString`, `container` e `folderPath`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage connection using connectingString",
    "description": "Azure Blob Storage connection using connectionString",
    "auth": {
      "specName": "ConnectionString",
      "params": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| Parametro | Descrizione |
| --- | --- |
| `connectionString` | Stringa di connessione per l&#39;account [!DNL Azure Blob Storage]. Schema della stringa di connessione: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY};EndpointSuffix=core.windows.net`. |
| `container` | Nome del contenitore [!DNL Azure Blob Storage] in cui sono archiviati i file di dati. |
| `folderPath` | Percorso all’interno del contenitore specificato in cui si trovano i file. |
| `connectionSpec.id` | ID della specifica di connessione dell&#39;origine [!DNL Azure Blob Storage]. Questo ID è corretto come: `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!TAB Firma di accesso condiviso]

Per utilizzare la firma di accesso condiviso, fornire i valori per `sasUri`, `container` e `folderPath`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage source connection using SAS URI",
    "description": "Azure Blob Storage source connection using SAS URI",
    "auth": {
      "specName": "SAS URI Authentication",
      "params": {
        "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| Parametro | Descrizione |
| --- | --- |
| `sasUri` | URI della firma di accesso condiviso che è possibile utilizzare come tipo di autenticazione alternativo per connettere l&#39;account. Schema URI SAS: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}`. |
| `container` | Nome del contenitore [!DNL Azure Blob Storage] in cui sono archiviati i file di dati. |
| `folderPath` | Percorso all’interno del contenitore specificato in cui si trovano i file. |
| `connectionSpec.id` | ID della specifica di connessione dell&#39;origine [!DNL Azure Blob Storage]. Questo ID è corretto come: `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!TAB Autenticazione basata su entità servizio]

Per connettersi tramite autenticazione basata su entità servizio, fornire valori per: `serviceEndpoint`, `servicePrincipalId`, `servicePrincipalKey`, `accountKind`, `tenant`, `container` e `folderPath`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage source connection using service principal based authentication",
    "description": "Azure Blob Storage source connection using service principal based authentication",
    "auth": {
      "specName": "Service Principal Based Authentication",
      "params": {
        "serviceEndpoint": "{SERVICE_ENDPOINT}",
        "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
        "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
        "accountKind": "{ACCOUNT_KIND}",
        "tenant": "{TENANT}",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| Parametro | Descrizione |
| --- | --- |
| `serviceEndpoint` | L&#39;URL dell&#39;endpoint dell&#39;account [!DNL Azure Blob Storage]. In genere nel formato: `https://{ACCOUNT_NAME}.blob.core.windows.net`. |
| `servicePrincipalId` | ID client/applicazione dell&#39;entità servizio Azure Active Directory (AAD) utilizzata per l&#39;autenticazione. |
| `servicePrincipalKey` | Il segreto client o la password associata all&#39;entità servizio Azure. |
| `accountKind` | Il tipo del tuo account [!DNL Azure Blob Storage]. I valori comuni includono `StorageV2`, `BlobStorage` o `Storage`. |
| `tenant` | ID tenant di Azure Active Directory (AAD) in cui è registrata l&#39;entità servizio. |
| `container` | Nome del contenitore [!DNL Azure Blob Storage] in cui sono archiviati i file di dati. |
| `folderPath` | Percorso all’interno del contenitore specificato in cui si trovano i file. |
| `connectionSpec.id` | ID della specifica di connessione dell&#39;origine [!DNL Azure Blob Storage]. Questo ID è corretto come: `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!ENDTABS]

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```



## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL Blob] utilizzando le API ed è stato ottenuto un ID univoco come parte del corpo della risposta. Puoi usare questo ID connessione per [esplorare gli archivi cloud utilizzando l&#39;API del servizio Flusso](../../explore/cloud-storage.md).
