---
title: Creare una connessione di base per l’archiviazione cloud di Google utilizzando l’API del servizio Flow
description: Scopri come collegare Adobe Experience Platform a un account di Google Cloud Storage utilizzando l’API del servizio Flow.
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: 3636b785d82fa2e49f76825650e6159be119f8b4
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# Creare un [!DNL Google Cloud Storage] connessione di base tramite [!DNL Flow Service] API

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Google Cloud Storage] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a un account di Google Cloud Storage utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi con [!DNL Google Cloud Storage] account, è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `accessKeyId` | Una stringa alfanumerica di 61 caratteri utilizzata per autenticare il [!DNL Google Cloud Storage] da un account a Platform. |
| `secretAccessKey` | Una stringa con codifica base 64 di 40 caratteri utilizzata per autenticare il [!DNL Google Cloud Storage] da un account a Platform. |
| `bucketName` | Il nome del tuo [!DNL Google Cloud Storage] secchio. Se desideri fornire l’accesso a una sottocartella specifica nell’archiviazione cloud, devi specificare un nome di bucket. |
| `folderPath` | Percorso della cartella a cui desideri fornire l’accesso. |

Per ulteriori informazioni su questi valori, vedere [Chiavi HMAC di Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guida. Per i passaggi su come generare il proprio ID chiave di accesso e la propria chiave di accesso segreta, consulta [[!DNL Google Cloud Storage] panoramica](../../../../connectors/cloud-storage/google-cloud-storage.md).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL Google Cloud Storage] credenziali di autenticazione come parte dei parametri della richiesta.

>[!TIP]
>
>Durante questo passaggio, puoi anche designare le sottocartelle a cui il tuo account avrà accesso definendo il nome del bucket e il percorso della sottocartella.

**Formato API**

```http
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Google Cloud Storage]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google Cloud Storage connection",
      "description": "Connector for Google Cloud Storage",
      "auth": {
          "specName": "Basic Authentication for google-cloud",
          "params": {
              "accessKeyId": "accessKeyId",
              "secretAccessKey": "secretAccessKey",
              "bucketName": "acme-google-cloud-bucket",
              "folderPath": "/acme/customers/sales"
          }
      },
      "connectionSpec": {
          "id": "32e8f412-cdf7-464c-9885-78184cb113fd",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.accessKeyId` | ID della chiave di accesso associato al tuo [!DNL Google Cloud Storage] account. |
| `auth.params.secretAccessKey` | La chiave di accesso segreta associata al tuo [!DNL Google Cloud Storage] account. |
| `auth.params.bucketName` | Il nome del tuo [!DNL Google Cloud Storage] secchio. Se desideri fornire l’accesso a una sottocartella specifica nell’archiviazione cloud, devi specificare un nome di bucket. |
| `auth.params.folderPath` | Percorso della cartella a cui desideri fornire l’accesso. |
| `connectionSpec.id` | Il [!DNL Google Cloud Storage] ID specifica di connessione: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati dell’archiviazione cloud nella prossima esercitazione.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una [!DNL Google Cloud Storage] è stata ottenuta una connessione tramite API e un ID univoco come parte del corpo della risposta. Puoi usare questo ID connessione per [esplorare gli archivi cloud utilizzando l’API del servizio Flow](../../explore/cloud-storage.md).
