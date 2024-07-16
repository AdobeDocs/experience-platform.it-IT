---
title: Creare una connessione di base BLOB di Azure utilizzando l’API del servizio di flusso
description: Scopri come connettere Adobe Experience Platform a Azure Blob utilizzando l’API del servizio Flusso.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 3%

---

# Creare una connessione di base [!DNL Azure Blob] utilizzando l&#39;API [!DNL Flow Service]

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Azure Blob] (di seguito &quot;[!DNL Blob]&quot;) utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per creare correttamente una connessione di origine [!DNL Blob] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Affinché [!DNL Flow Service] possa connettersi all&#39;archivio [!DNL Blob], è necessario fornire i valori per la seguente proprietà di connessione:

>[!BEGINTABS]

>[!TAB Autenticazione stringa di connessione]

| Credenziali | Descrizione |
| --- | --- |
| `connectionString` | Stringa contenente le informazioni di autorizzazione necessarie per autenticare [!DNL Blob] in Experience Platform. Schema della stringa di connessione [!DNL Blob]: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Per ulteriori informazioni sulle stringhe di connessione, vedere il documento [!DNL Blob] in [configurazione delle stringhe di connessione](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Blob]: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

>[!TAB Autenticazione URI SAS]

| Credenziali | Descrizione |
| --- | --- |
| `sasUri` | URI della firma di accesso condiviso che è possibile utilizzare come tipo di autenticazione alternativo per connettere l&#39;account [!DNL Blob]. Il modello URI SAS [!DNL Blob] è: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Per ulteriori informazioni, vedere questo documento [!DNL Blob] in [URI di firma di accesso condiviso](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `container` | Nome del contenitore a cui si desidera designare l&#39;accesso. Durante la creazione di un nuovo account con l&#39;origine [!DNL Blob], è possibile fornire un nome contenitore per specificare l&#39;accesso utente alla sottocartella desiderata. |
| `folderPath` | Percorso della cartella a cui desideri fornire l’accesso. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Blob]: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

>[!ENDTABS]

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

>[!TIP]
>
>Una volta creata, non è possibile modificare il tipo di autenticazione di una connessione di base [!DNL Blob]. Per modificare il tipo di autenticazione, è necessario creare una nuova connessione di base.

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

L&#39;origine [!DNL Blob] supporta sia la stringa di connessione che l&#39;autenticazione della firma di accesso condiviso (SAS). Un URI di firma di accesso condiviso (SAS) consente l&#39;autorizzazione delegata protetta per l&#39;account [!DNL Blob]. È possibile utilizzare SAS per creare credenziali di autenticazione con diversi gradi di accesso, in quanto un&#39;autenticazione basata su SAS consente di impostare autorizzazioni, date di inizio e di scadenza, nonché disposizioni a risorse specifiche.

Durante questo passaggio, puoi anche designare le sottocartelle a cui il tuo account avrà accesso definendo il nome del contenitore e il percorso della sottocartella.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Blob] come parte dei parametri della richiesta.

**Formato API**

```http
POST /connections
```

**Richiesta**

>[!BEGINTABS]

>[!TAB Stringa di connessione]

La richiesta seguente crea una connessione di base per [!DNL Blob] utilizzando l&#39;autenticazione basata su stringhe di connessione:

+++Richiesta

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Blob connection using connectionString",
      "description": "Azure Blob connection using connectionString",
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

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.connectionString` | Stringa di connessione necessaria per accedere ai dati nell’archiviazione BLOB. Schema della stringa di connessione BLOB: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | ID della specifica di connessione all&#39;archiviazione BLOB: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

+++

>[!TAB Autenticazione URI SAS]

Per creare una connessione [!DNL Blob] utilizzando l&#39;URI della firma di accesso condiviso, eseguire una richiesta POST all&#39;API [!DNL Flow Service] fornendo i valori per l&#39;elemento [!DNL Blob] `sasUri`.

+++Richiesta

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Blob source connection using SAS URI",
      "description": "Azure Blob source connection using SAS URI",
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

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.connectionString` | L&#39;URI SAS necessario per accedere ai dati nell&#39;archiviazione [!DNL Blob]. Schema URI SAS [!DNL Blob]: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`. |
| `connectionSpec.id` | L&#39;ID della specifica di connessione di archiviazione [!DNL Blob] è: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

+++

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL Blob] utilizzando le API ed è stato ottenuto un ID univoco come parte del corpo della risposta. Puoi usare questo ID connessione per [esplorare gli archivi cloud utilizzando l&#39;API del servizio Flusso](../../explore/cloud-storage.md).
