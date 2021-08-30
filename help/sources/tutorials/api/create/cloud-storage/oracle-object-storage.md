---
keywords: Experience Platform;home;argomenti comuni;archiviazione oggetti Oracle;archiviazione oggetti oracle
solution: Experience Platform
title: Creare una connessione di base di archiviazione degli oggetti di Oracle utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform ad Oracle Object Storage utilizzando l’API del servizio di flusso.
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 1%

---

# Creare una connessione di base [!DNL Oracle Object Storage] utilizzando l&#39;API [!DNL Flow Service]

Una connessione di base rappresenta la connessione autenticata tra un&#39;origine e Adobe Experience Platform.

Questa esercitazione descrive i passaggi necessari per creare una connessione di base per [!DNL Oracle Object Storage] utilizzando l&#39; [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL Oracle Object Storage] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Oracle Object Storage], è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `serviceUrl` | Endpoint [!DNL Oracle Object Storage] necessario per l&#39;autenticazione. Il formato dell&#39;endpoint è: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | ID chiave di accesso [!DNL Oracle Object Storage] necessario per l&#39;autenticazione. |
| `secretKey` | Password [!DNL Oracle Object Storage] necessaria per l&#39;autenticazione. |
| `bucketName` | Il nome del bucket consentito richiesto se l’utente ha accesso limitato. Il nome del bucket deve essere lungo tra i tre e i 63 caratteri, deve iniziare e terminare con una lettera o un numero e può contenere solo lettere minuscole, numeri o trattini (`-`). Impossibile formattare il nome del bucket come indirizzo IP. |
| `folderPath` | Percorso della cartella consentito richiesto se l&#39;utente dispone di accesso limitato. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID della specifica di connessione per [!DNL Oracle Object Storage] è: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

Per ulteriori informazioni su come ottenere questi valori, consulta la [Guida all&#39;autenticazione di Oracle Object Storage](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md) .

## Creare una connessione di base

Una connessione di base conserva le informazioni tra l&#39;origine e la piattaforma, incluse le credenziali di autenticazione dell&#39;origine, lo stato corrente della connessione e l&#39;ID di connessione di base univoco. L’ID di connessione di base consente di esplorare e navigare tra i file di origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Oracle Object Storage] come parte dei parametri della richiesta.

**Formato API**

```http
POST /connections
```

**Richiesta**

La seguente richiesta crea una connessione di base per [!DNL Oracle Object Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.serviceUrl` | Endpoint [!DNL Oracle Object Storage] necessario per l&#39;autenticazione. |
| `auth.params.accessKey` | ID chiave di accesso [!DNL Oracle Object Storage] necessario per l&#39;autenticazione. |
| `auth.params.secretKey` | Password [!DNL Oracle Object Storage] necessaria per l&#39;autenticazione. |
| `auth.params.bucketName` | Il nome del bucket consentito richiesto se l’utente ha accesso limitato. |
| `auth.params.folderPath` | Percorso della cartella consentito richiesto se l&#39;utente dispone di accesso limitato. |
| `connectionSpec.id` | ID delle specifiche di connessione [!DNL Oracle Object Storage]: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

**Risposta**

Una risposta corretta restituisce l&#39;ID di connessione della nuova connessione creata. Questo ID è necessario per esplorare i dati di archiviazione cloud nell’esercitazione successiva.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL Oracle Object Storage] utilizzando l&#39;API [!DNL Flow Service] e hai ottenuto il relativo ID di connessione univoco. Puoi usare questo ID connessione per [esplorare gli archivi cloud utilizzando l&#39;API del servizio di flusso](../../explore/cloud-storage.md).
