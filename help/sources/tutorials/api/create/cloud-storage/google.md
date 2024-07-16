---
title: Creare una connessione di base per l’archiviazione cloud di Google utilizzando l’API del servizio Flow
description: Scopri come collegare Adobe Experience Platform a un account di Google Cloud Storage utilizzando l’API del servizio Flow.
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: 3636b785d82fa2e49f76825650e6159be119f8b4
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 4%

---

# Creare una connessione di base [!DNL Google Cloud Storage] utilizzando l&#39;API [!DNL Flow Service]

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Google Cloud Storage] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a un account di Google Cloud Storage tramite l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Affinché [!DNL Flow Service] possa connettersi al tuo account [!DNL Google Cloud Storage], devi fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `accessKeyId` | Una stringa alfanumerica di 61 caratteri utilizzata per autenticare l&#39;account [!DNL Google Cloud Storage] in Platform. |
| `secretAccessKey` | Stringa di 40 caratteri con codifica base 64 utilizzata per autenticare l&#39;account [!DNL Google Cloud Storage] in Platform. |
| `bucketName` | Nome del bucket [!DNL Google Cloud Storage]. Se desideri fornire l’accesso a una sottocartella specifica nell’archiviazione cloud, devi specificare un nome di bucket. |
| `folderPath` | Percorso della cartella a cui desideri fornire l’accesso. |

Per ulteriori informazioni su questi valori, consulta la guida delle [chiavi HMAC di Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Per i passaggi su come generare il proprio ID chiave di accesso e la propria chiave di accesso segreta, consulta la [[!DNL Google Cloud Storage] panoramica](../../../../connectors/cloud-storage/google-cloud-storage.md).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Google Cloud Storage] come parte dei parametri della richiesta.

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
| `auth.params.accessKeyId` | ID della chiave di accesso associato al tuo account [!DNL Google Cloud Storage]. |
| `auth.params.secretAccessKey` | La chiave di accesso segreta associata al tuo account [!DNL Google Cloud Storage]. |
| `auth.params.bucketName` | Nome del bucket [!DNL Google Cloud Storage]. Se desideri fornire l’accesso a una sottocartella specifica nell’archiviazione cloud, devi specificare un nome di bucket. |
| `auth.params.folderPath` | Percorso della cartella a cui desideri fornire l’accesso. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Google Cloud Storage]: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati dell’archiviazione cloud nella prossima esercitazione.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL Google Cloud Storage] utilizzando le API ed è stato ottenuto un ID univoco come parte del corpo della risposta. Puoi usare questo ID connessione per [esplorare gli archivi cloud utilizzando l&#39;API del servizio Flusso](../../explore/cloud-storage.md).
