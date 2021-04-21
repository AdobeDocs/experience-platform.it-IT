---
keywords: Experience Platform;home;argomenti comuni;archiviazione oggetti Oracle;archiviazione oggetti oracle
solution: Experience Platform
title: Creare una connessione ad Oracle dell’origine di archiviazione degli oggetti mediante l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform ad Oracle Object Storage utilizzando l’API del servizio di flusso.
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---

# Creare una connessione sorgente [!DNL Oracle Object Storage] utilizzando l&#39;API [!DNL Flow Service]

Questa esercitazione utilizza l’ [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) per seguire i passaggi necessari per collegare Adobe Experience Platform a [!DNL Oracle Object Storage].

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

Per ulteriori informazioni su come ottenere questi valori, consulta la [Guida all&#39;autenticazione di Oracle Object Storage](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API di Platform, devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* `Content-Type: application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione per ogni account [!DNL Oracle Object Storage] in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

**Formato API**

```http
POST /connections
```

**Richiesta**

Per creare una connessione [!DNL Oracle Object Storage], è necessario fornire l’ID univoco della specifica di connessione come parte della richiesta di POST. L&#39;ID delle specifiche di connessione per [!DNL Oracle Object Storage] è `c85f9425-fb21-426c-ad0b-405e9bd8a46c`.

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
