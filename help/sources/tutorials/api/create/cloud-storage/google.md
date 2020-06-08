---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di archiviazione Google Cloud utilizzando l'API del servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: 0ed2ed3b08f262100746f255a78c248a1748eb5e
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 2%

---


# Creare un connettore di archiviazione Google Cloud utilizzando l&#39;API del servizio di flusso

Flow Service è utilizzato per raccogliere e centralizzare i dati dei clienti da varie origini diverse all&#39;interno di Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39;API del servizio di flusso per guidarti attraverso i passaggi necessari per connettere Experience Platform a un account di archiviazione Google Cloud.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie fonti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi della piattaforma.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a un account di archiviazione Google Cloud tramite l&#39;API del servizio di flusso.

### Raccogli credenziali richieste

Affinché il servizio di flusso possa connettersi al tuo account di archiviazione Google Cloud, devi fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `accessKeyId` | ID chiave di accesso per l&#39;account Google Cloud Storage. |
| `secretAccessKey` | La chiave di accesso segreta per l&#39;account Google Cloud Storage. |

Per informazioni su come iniziare, visita [questo documento](https://cloud.google.com/docs/authentication)Google Cloud.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione [come leggere le chiamate](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi della piattaforma Experience.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API della piattaforma, dovete prima completare l&#39;esercitazione [di](../../../../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in Experience Platform, incluse quelle appartenenti a Flow Service, sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API della piattaforma richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* Content-Type: `application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. Per l&#39;account di archiviazione Google Cloud è necessaria una sola connessione, in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

**Formato API**

```http
POST /connections
```

**Richiesta**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
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
| `auth.params.accessKeyId` | ID chiave di accesso associato al tuo account di archiviazione Google Cloud. |
| `auth.params.secretAccessKey` | La chiave di accesso segreta associata al tuo account di archiviazione Google Cloud. |
| `connectionSpec.id` | ID specifica di connessione di Google Cloud Storage: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati di archiviazione cloud nell&#39;esercitazione successiva.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione Google Cloud Storage utilizzando le API e un ID univoco è stato ottenuto come parte del corpo della risposta. Potete utilizzare questo ID connessione per [esplorare gli storage cloud utilizzando l&#39;API](../../explore/cloud-storage.md) del servizio di flusso o per [assimilare i dati del parquet tramite l&#39;API](../../cloud-storage-parquet.md)del servizio di flusso.