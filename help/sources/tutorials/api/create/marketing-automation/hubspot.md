---
keywords: Experience Platform;home;popular topics;hubspot;Hubspot
solution: Experience Platform
title: Creare un connettore HubSpot utilizzando l'API del servizio di flusso
topic: overview
type: Tutorial
description: Questa esercitazione utilizza l’API del servizio di flusso per guidarvi attraverso i passaggi necessari per connettere  Experience Platform a HubSpot.
translation-type: tm+mt
source-git-commit: 9092c3d672967d3f6f7bf7116c40466a42e6e7b1
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 1%

---


# Creare un connettore [!DNL HubSpot] utilizzando l&#39;API [!DNL Flow Service]

>[!NOTE]
>
>Il connettore [!DNL HubSpot] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, vedere [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions).

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie origini all&#39;interno di Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39;API [!DNL Flow Service] per guidarvi attraverso i passaggi necessari per collegarvi [!DNL Experience Platform] a [!DNL HubSpot].

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md):  [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a [!DNL HubSpot] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL HubSpot], è necessario fornire le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `clientId` | L&#39;ID client associato all&#39;applicazione [!DNL HubSpot]. |
| `clientSecret` | Il segreto client associato all&#39;applicazione [!DNL HubSpot]. |
| `accessToken` | Token di accesso ottenuto durante l&#39;autenticazione iniziale dell&#39;integrazione OAuth. |
| `refreshToken` | Token di aggiornamento ottenuto durante l&#39;autenticazione iniziale dell&#39;integrazione OAuth. |
| `connectionSpec` | Identificatore univoco necessario per creare una connessione. L&#39;ID della specifica di connessione per [!DNL HubSpot] è: `cc6a4487-9e91-433e-a3a3-9cf6626c1806` |

Per ulteriori informazioni su come iniziare, fare riferimento a questo [documento HubSpot](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi del Experience Platform .

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a2/>. ](../../../../../tutorials/authentication.md) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* `Content-Type: application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione per ogni account [!DNL HubSpot], in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

**Formato API**

```https
POST /connections
```

**Richiesta**

Per creare una connessione [!DNL HubSpot], è necessario fornire l&#39;ID univoco della specifica di connessione come parte della richiesta di POST. L&#39;ID della specifica di connessione per [!DNL HubSpot] è `cc6a4487-9e91-433e-a3a3-9cf6626c1806`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for hubspot",
        "description": "connection for hubspot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.clientId` | L&#39;ID client associato all&#39;applicazione [!DNL HubSpot]. |
| `auth.params.clientSecret` | Il segreto client associato all&#39;applicazione [!DNL HubSpot]. |
| `auth.params.accessToken` | Token di accesso ottenuto durante l&#39;autenticazione iniziale dell&#39;integrazione OAuth. |
| `auth.params.refreshToken` | Token di aggiornamento ottenuto durante l&#39;autenticazione iniziale dell&#39;integrazione OAuth. |

**Risposta**

Una risposta corretta restituisce la nuova connessione creata, incluso il relativo identificatore di connessione univoco (`id`). Questo ID è necessario per esplorare i dati nell&#39;esercitazione successiva.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Seguendo questa esercitazione, hai creato una connessione [!DNL HubSpot] utilizzando l&#39;API [!DNL Flow Service] e hai ottenuto il valore ID univoco della connessione. Puoi usare questo ID connessione nell&#39;esercitazione successiva per scoprire come [esplorare i sistemi di automazione di marketing utilizzando l&#39;API del servizio di flusso](../../explore/marketing-automation.md).