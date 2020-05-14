---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore Azure Data Explorer utilizzando l'API del servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: 37a5f035023cee1fc2408846fb37d64b9a3fc4b6
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 1%

---


# Creare un connettore Azure Data Explorer utilizzando l&#39;API del servizio di flusso

>[!NOTE]
>Il connettore di Azure Data Explorer è in versione beta. Le funzioni e la documentazione sono soggette a modifiche.

Flow Service è utilizzato per raccogliere e centralizzare i dati dei clienti da varie origini diverse all&#39;interno di Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39;API del servizio di flusso per seguire i passaggi necessari per connettere Azure Data Explorer (in seguito denominato &quot;Esplora dati&quot;) alla piattaforma Experience.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie fonti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi della piattaforma.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a Esplora dati tramite l&#39;API del servizio di flusso.

### Raccogli credenziali richieste

Affinché il servizio di flusso possa connettersi con Esplora dati, è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `endpoint` | L&#39;endpoint del server di Esplora dati. |
| `database` | Nome del database di Esplora dati. |
| `tenant` | L&#39;ID tenant univoco utilizzato per connettersi al database di Esplora dati. |
| `servicePrincipalId` | L&#39;ID entità servizio univoco utilizzato per connettersi al database di Esplora dati. |
| `servicePrincipalKey` | Chiave entità servizio univoca utilizzata per connettersi al database di Esplora dati. |
| `connectionSpec.id` | Identificatore univoco necessario per creare una connessione. L&#39;ID della specifica di connessione per Esplora dati è `0479cc14-7651-4354-b233-7480606c2ac3`. |

Per ulteriori informazioni su come iniziare, consulta [questo documento](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad)di Esplora dati.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione [come leggere le chiamate](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi della piattaforma Experience.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API della piattaforma, dovete prima completare l&#39;esercitazione [di](../../../../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in Experience Platform, incluse quelle appartenenti al servizio di flusso, sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API della piattaforma richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* Content-Type: `application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessario un solo connettore per l&#39;account Data Explorer, in quanto può essere utilizzato per creare più connettori sorgente per inserire dati diversi.

**Formato API**

```http
POST /connections
```

**Richiesta**

Per creare una connessione di Esplora dati, è necessario fornire l&#39;ID univoco della specifica di connessione come parte della richiesta POST. L&#39;ID della specifica di connessione per Esplora dati è `0479cc14-7651-4354-b233-7480606c2ac3`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Data Explorer connection",
        "description": "A connection for Azure Data Explorer",
        "auth": {
            "specName": "Service Principal Based Authentication",
            "params": {
                    "endpoint": "{ENDPOINT}",
                    "database": "{DATABASE}",
                    "tenant": "{TENANT}",
                    "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                    "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
                }
        },
        "connectionSpec": {
            "id": "0479cc14-7651-4354-b233-7480606c2ac3",
            "version": "1.0"
        }
    }'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `auth.params.endpoint` | L&#39;endpoint del server di Esplora dati. |
| `auth.params.database` | Nome del database di Esplora dati. |
| `auth.params.tenant` | L&#39;ID tenant univoco utilizzato per connettersi al database di Esplora dati. |
| `auth.params.servicePrincipalId` | L&#39;ID entità servizio univoco utilizzato per connettersi al database di Esplora dati. |
| `auth.params.servicePrincipalKey` | Chiave entità servizio univoca utilizzata per connettersi al database di Esplora dati. |
| `connectionSpec.id` | ID specifica connessione di Esplora dati: `0479cc14-7651-4354-b233-7480606c2ac3`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell&#39;esercitazione successiva.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione di Esplora dati utilizzando l&#39;API del servizio di flusso e hai ottenuto il valore ID univoco della connessione. Puoi usare questo ID nell’esercitazione successiva per imparare a [esplorare i database utilizzando l’API](../../explore/database-nosql.md)del servizio di flusso.
