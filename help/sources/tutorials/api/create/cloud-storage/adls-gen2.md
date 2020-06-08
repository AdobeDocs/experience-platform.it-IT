---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore Azure Data Lake Storage Gen2 utilizzando l'API del servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: 0ed2ed3b08f262100746f255a78c248a1748eb5e
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 2%

---


# Creare un connettore Azure Data Lake Storage Gen2 utilizzando l&#39;API del servizio di flusso

Flow Service è utilizzato per raccogliere e centralizzare i dati dei clienti da varie origini diverse all&#39;interno di Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39;API del servizio di flusso per seguire i passaggi necessari per connettere Experience Platform ad Azure Data Lake Storage Gen2 (di seguito &quot;ADLS Gen2&quot;).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie fonti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi della piattaforma.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per creare correttamente un connettore di origine ADLS Gen2 utilizzando l&#39;API del servizio di flusso.

### Raccogli credenziali richieste

Affinché il servizio di flusso possa connettersi ad ADLS Gen2, è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `url` | L’URL dell’indirizzo. |
| `servicePrincipalId` | L&#39;ID client dell&#39;applicazione. |
| `servicePrincipalKey` | La chiave dell&#39;applicazione. |
| `tenant` | Le informazioni sul tenant che contengono l&#39;applicazione. |

Per ulteriori informazioni su questi valori, consultare [questo documento](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)ADLS Gen2.

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

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione per l&#39;account ADLS Gen2, in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

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
        "name": "adls-gen2",
        "description": "Connection for adls-gen2",
        "auth": {
            "specName": "Basic Authentication for adls-gen2",
            "params": {
                "url": "{URL}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
                "tenant": "{TENANT}"
            }
        },
        "connectionSpec": {
            "id": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.url` | L&#39;endpoint URL per l&#39;account ADLS Gen2. |
| `auth.params.servicePrincipalId` | L&#39;ID entità servizio del tuo account ADLS Gen2. |
| `auth.params.servicePrincipalKey` | Chiave entità servizio del tuo account ADLS Gen2. |
| `auth.params.tenant` | Informazioni sul tenant del tuo account ADLS Gen2. |
| `connectionSpec.id` | ID specifica di connessione ADLS Gen2: `0ed90a81-07f4-4586-8190-b40eccef1c5a1`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare lo spazio di archiviazione cloud nel passaggio successivo.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione ADLS Gen2 utilizzando le API e un ID univoco è stato ottenuto come parte del corpo della risposta. Potete utilizzare questo ID connessione per [esplorare gli storage cloud utilizzando l&#39;API](../../explore/cloud-storage.md) del servizio di flusso o per [assimilare i dati del parquet tramite l&#39;API](../../cloud-storage-parquet.md)del servizio di flusso.
