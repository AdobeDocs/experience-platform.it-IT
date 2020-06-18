---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore PayPal utilizzando l'API del servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: 7328226b8349ffcdddadbd27b74fc54328b78dc5
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 1%

---


# Creare un connettore PayPal utilizzando l&#39;API del servizio di flusso

>[!NOTE]
>Il connettore PayPal è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

Flow Service è utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti diverse all&#39;interno  Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39;API del servizio di flusso per guidarvi attraverso i passaggi necessari per collegare PayPal a  Experience Platform.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti del  Adobe Experience Platform:

* [Origini](../../../../home.md):  Experience Platform consente l&#39;acquisizione di dati da varie fonti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../../../sandboxes/home.md):  Experience Platform fornisce sandbox virtuali che dividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a PayPal tramite l&#39;API del servizio di flusso.

### Raccogli credenziali richieste

Affinché il servizio di flusso possa connettersi con PayPal, è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| Host | L&#39;URL dell&#39;istanza PayPal. (predefinito: api.sandbox.paypal.com). |
| ID client | L&#39;ID cliente associato all&#39;applicazione PayPal. |
| Segreto cliente | Il segreto cliente associato all&#39;applicazione PayPal. |
| ID specifica connessione | Identificatore univoco necessario per creare una connessione. L&#39;ID della specifica di connessione per PayPal è: `221c7626-58f6-4eec-8ee2-042b0226f03b` |

Per ulteriori informazioni su come iniziare, consulta [questo documento](https://developer.paypal.com/docs/api/overview/#get-credentials)PayPal.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere le chiamate](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi di  Experience Platform.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API Platform, è prima necessario completare l&#39;esercitazione [di](../../../../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API Experience Platform, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in  Experience Platform, incluse quelle appartenenti al servizio di flusso, sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API Platform richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* Content-Type: `application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione per conto PayPal, in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

**Formato API**

```http
POST /connections
```

**Richiesta**

Per creare una connessione PayPal, è necessario fornire l&#39;ID univoco della specifica di connessione come parte della richiesta POST. L&#39;ID della specifica di connessione per PayPal è `221c7626-58f6-4eec-8ee2-042b0226f03b`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Paypal connection",
        "description": "Paypal connection",
        "auth": {
        "specName": "Client-Id-Secret Based Authentication",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            }
        },
        "connectionSpec": {
            "id": "221c7626-58f6-4eec-8ee2-042b0226f03b",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `auth.params.host` | L&#39;URL dell&#39;istanza PayPal. |
| `auth.params.clientId` | L&#39;ID client associato all&#39;istanza PayPal. |
| `auth.params.clientSecret` | Il segreto cliente associato all&#39;istanza PayPal. |
| `connectionSpec.id` | ID specifica connessione PayPal: `221c7626-58f6-4eec-8ee2-042b0226f03b`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell&#39;esercitazione successiva.

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione PayPal utilizzando l&#39;API del servizio di flusso e hai ottenuto il valore ID univoco della connessione. Puoi usare questo ID nell’esercitazione successiva per imparare a [esplorare l’applicazione dei pagamenti utilizzando l’API](../../explore/payments.md)del servizio di flusso.
