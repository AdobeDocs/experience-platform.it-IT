---
keywords: Experience Platform;home;argomenti comuni;Oracle Object Storage;oracle object storage
solution: Experience Platform
title: Creare una connessione Oracle Object Storage Base utilizzando l’API del servizio Flow
type: Tutorial
description: Scopri come collegare Adobe Experience Platform ad Oracle Object Storage utilizzando l’API del servizio Flow.
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 4%

---

# Creare una connessione di base [!DNL Oracle Object Storage] utilizzando l&#39;API [!DNL Flow Service]

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questo tutorial illustra i passaggi necessari per creare una connessione di base per [!DNL Oracle Object Storage] utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL Oracle Object Storage] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Oracle Object Storage], è necessario fornire i valori per le proprietà di connessione seguenti:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `serviceUrl` | Endpoint [!DNL Oracle Object Storage] richiesto per l&#39;autenticazione. Formato endpoint: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | ID della chiave di accesso [!DNL Oracle Object Storage] richiesto per l&#39;autenticazione. |
| `secretKey` | La password [!DNL Oracle Object Storage] richiesta per l&#39;autenticazione. |
| `bucketName` | Il nome del bucket consentito è necessario se l’utente dispone di accesso limitato. Il nome del bucket deve contenere tra tre e 63 caratteri, deve iniziare e terminare con una lettera o un numero e può contenere solo lettere minuscole, numeri o trattini (`-`). Il nome del bucket non può essere formattato come un indirizzo IP. |
| `folderPath` | Il percorso della cartella consentito è necessario se l’utente ha limitato l’accesso. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Oracle Object Storage]: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

Per ulteriori informazioni su come ottenere questi valori, fare riferimento alla [Guida all&#39;autenticazione di Oracle Object Storage](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

### Utilizzo delle API di Experience Platform

Per informazioni su come effettuare correttamente chiamate alle API di Experience Platform, consulta la guida introduttiva [alle API di Experience Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Una connessione di base mantiene le informazioni tra l’origine e Experience Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID connessione di base, eseguire una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Oracle Object Storage] come parte dei parametri della richiesta.

**Formato API**

```http
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Oracle Object Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Oracle Object Storage connection",
        "description": "Oracle Object Storage connection",
        "auth": {
            "specName": "Access Key",
            "params": {
                "serviceUrl": "{SERVICE_URL}",
                "accessKey": "{ACCESS_KEY}",
                "secretKey": "{SECRET_KEY}",
                "bucketName": "{BUCKET_NAME}",
                "folderPath", "{FOLDER_PATH}"
            }
        },
        "connectionSpec": {
            "id": "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.serviceUrl` | Endpoint [!DNL Oracle Object Storage] richiesto per l&#39;autenticazione. |
| `auth.params.accessKey` | ID della chiave di accesso [!DNL Oracle Object Storage] richiesto per l&#39;autenticazione. |
| `auth.params.secretKey` | La password [!DNL Oracle Object Storage] richiesta per l&#39;autenticazione. |
| `auth.params.bucketName` | Il nome del bucket consentito è necessario se l’utente dispone di accesso limitato. |
| `auth.params.folderPath` | Il percorso della cartella consentito è necessario se l’utente ha limitato l’accesso. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Oracle Object Storage]: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID di connessione della connessione appena creata. Questo ID è necessario per esplorare i dati dell’archiviazione cloud nella prossima esercitazione.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL Oracle Object Storage] utilizzando l&#39;API [!DNL Flow Service] e ne hai ottenuto l&#39;ID di connessione univoco. Puoi usare questo ID connessione per [esplorare gli archivi cloud utilizzando l&#39;API del servizio Flusso](../../explore/cloud-storage.md).
