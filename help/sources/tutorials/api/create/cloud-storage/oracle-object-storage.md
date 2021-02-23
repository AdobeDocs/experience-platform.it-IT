---
keywords: ' Experience Platform;home;argomenti più comuni; Archiviazione oggetti Oracli; archiviazione oggetti oracle'
solution: Experience Platform
title: Creazione di una connessione di origine dell'archivio oggetti  Oracle tramite l'API del servizio di flusso
topic: ' - Panoramica'
type: Tutorial
description: Scoprite come collegare Adobe Experience Platform a  Archiviazione oggetti di Oracle mediante l'API del servizio di flusso.
translation-type: tm+mt
source-git-commit: c1453a9f0be42f834d35af871051324df8dadf80
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 2%

---


# Creare una connessione di origine [!DNL Oracle Object Storage] utilizzando l&#39;API [!DNL Flow Service]

Questa esercitazione utilizza l&#39; [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) per seguire i passaggi necessari per connettere Adobe Experience Platform a [!DNL Oracle Object Storage].

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md):  Experience Platform consente l&#39;acquisizione di dati da varie fonti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Piattaforma.
* [Sandbox](../../../../../sandboxes/home.md):  Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a [!DNL Oracle Object Storage] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Oracle Object Storage], è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `serviceUrl` | L&#39;endpoint [!DNL Oracle Object Storage] richiesto per l&#39;autenticazione. Il formato dell&#39;endpoint è: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | ID chiave di accesso [!DNL Oracle Object Storage] richiesto per l&#39;autenticazione. |
| `secretKey` | La [!DNL Oracle Object Storage] password necessaria per l&#39;autenticazione. |
| `bucketName` | Il nome del bucket consentito richiesto se l&#39;utente dispone di un accesso limitato. Il nome del bucket deve essere compreso tra tre e 63 caratteri, deve iniziare e terminare con una lettera o un numero e può contenere solo lettere minuscole, numeri o trattini (`-`). Impossibile formattare il nome del bucket come indirizzo IP. |
| `folderPath` | Percorso della cartella consentito richiesto se l&#39;utente ha limitato l&#39;accesso. |

Per ulteriori informazioni su come ottenere questi valori, fare riferimento alla [ Guida all&#39;autenticazione dell&#39;archiviazione oggetti di Oracle](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi del Experience Platform .

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API della piattaforma, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a1/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API di Experience Platform, come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* `Content-Type: application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione per ogni account [!DNL Oracle Object Storage], in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

**Formato API**

```http
POST /connections
```

**Richiesta**

Per creare una connessione [!DNL Oracle Object Storage], è necessario fornire l&#39;ID univoco della specifica di connessione come parte della richiesta di POST. L&#39;ID della specifica di connessione per [!DNL Oracle Object Storage] è `c85f9425-fb21-426c-ad0b-405e9bd8a46c`.

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
| `auth.params.serviceUrl` | L&#39;endpoint [!DNL Oracle Object Storage] richiesto per l&#39;autenticazione. |
| `auth.params.accessKey` | ID chiave di accesso [!DNL Oracle Object Storage] richiesto per l&#39;autenticazione. |
| `auth.params.secretKey` | La [!DNL Oracle Object Storage] password necessaria per l&#39;autenticazione. |
| `auth.params.bucketName` | Il nome del bucket consentito richiesto se l&#39;utente dispone di un accesso limitato. |
| `auth.params.folderPath` | Percorso della cartella consentito richiesto se l&#39;utente ha limitato l&#39;accesso. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Oracle Object Storage]: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

**Risposta**

Una risposta corretta restituisce l&#39;ID di connessione della nuova connessione creata. Questo ID è necessario per esplorare i dati di archiviazione cloud nell&#39;esercitazione successiva.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL Oracle Object Storage] utilizzando l&#39;API [!DNL Flow Service] e ne hai ottenuto l&#39;ID di connessione univoco. Puoi utilizzare questo ID connessione per [esplorare gli archivi cloud utilizzando l&#39;API del servizio di flusso](../../explore/cloud-storage.md).