---
keywords: Experience Platform;home;argomenti popolari;Google Cloud Storage;Google cloud storage;google;Google;Google
solution: Experience Platform
title: Creare una connessione sorgente di archiviazione Google Cloud utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a un account di archiviazione Google Cloud utilizzando l’API del servizio di flusso.
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 2%

---

# Creare una connessione sorgente [!DNL Google Cloud Storage] utilizzando l&#39;API [!DNL Flow Service]

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti all&#39;interno di Adobe Experience Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful da cui è possibile connettere tutte le sorgenti supportate.

Questa esercitazione utilizza l’ API [!DNL Flow Service] per seguire i passaggi necessari per la connessione di [!DNL Experience Platform] a un account [!DNL Google Cloud Storage].

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md):  [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a un account di archiviazione Google Cloud utilizzando l’ API [!DNL Flow Service] .

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi all&#39;account [!DNL Google Cloud Storage], è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| ID chiave di accesso | Una stringa alfanumerica di 61 caratteri utilizzata per autenticare l’account [!DNL Google Cloud Storage] in Platform. |
| Chiave di accesso segreta | Una stringa con codifica base a 64 caratteri utilizzata per autenticare l&#39;account [!DNL Google Cloud Storage] in Platform. |

Per ulteriori informazioni su questi valori, consulta la guida [Chiavi HMAC di Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) . Per i passaggi su come generare il proprio ID chiave di accesso e la chiave di accesso segreta, consulta la [[!DNL Google Cloud Storage] panoramica](../../../../connectors/cloud-storage/google-cloud-storage.md).

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* `Content-Type: application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione per ogni account [!DNL Google Cloud Storage] in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

**Formato API**

```http
POST /connections
```

**Richiesta**

Per creare una connessione [!DNL Google Cloud Storage], è necessario fornire l’ID univoco della specifica di connessione come parte della richiesta di POST. L&#39;ID della specifica di connessione per [!DNL Google Cloud Storage] è `32e8f412-cdf7-464c-9885-78184cb113fd`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google Cloud Storage connection",
        "description": "Connector for Google Cloud Storage",
        "auth": {
            "specName": "Basic Authentication for google-cloud",
            "params": {
                "accessKeyId": "accessKeyId",
                "secretAccessKey": "secretAccessKey"
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
| `auth.params.accessKeyId` | ID chiave di accesso associato al tuo account [!DNL Google Cloud Storage] . |
| `auth.params.secretAccessKey` | Chiave di accesso segreto associata al tuo account [!DNL Google Cloud Storage]. |
| `connectionSpec.id` | ID delle specifiche di connessione [!DNL Google Cloud Storage]: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso l’identificatore univoco (`id`). Questo ID è necessario per esplorare i dati di archiviazione cloud nell’esercitazione successiva.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione [!DNL Google Cloud Storage] utilizzando le API e come parte del corpo della risposta è stato ottenuto un ID univoco. Puoi utilizzare questo ID connessione per [esplorare gli archivi cloud utilizzando l&#39;API del servizio di flusso](../../explore/cloud-storage.md) o [acquisire i dati del parquet utilizzando l&#39;API del servizio di flusso](../../cloud-storage-parquet.md).
