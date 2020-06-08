---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore Google AdWords utilizzando l'API del servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: 0ed2ed3b08f262100746f255a78c248a1748eb5e
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 1%

---


# Creare un connettore Google AdWords utilizzando l&#39;API del servizio di flusso

Flow Service è utilizzato per raccogliere e centralizzare i dati dei clienti da varie origini diverse all&#39;interno di Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l’API del servizio di flusso per guidarvi attraverso i passaggi necessari per collegare Experience Platform a Google AdWords.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie fonti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi della piattaforma.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che dovrete conoscere per collegarvi correttamente ad Ad utilizzando l&#39;API del servizio di flusso.

### Raccogli credenziali richieste

Affinché il servizio di flusso possa connettersi con AdWords, è necessario fornire i valori per le seguenti proprietà di connessione:

| **Credenziali** | **Descrizione** |
| -------------- | --------------- |
| ID cliente client | L&#39;ID cliente client dell&#39;account AdWords. |
| Token sviluppatore | Token sviluppatore associato all&#39;account manager. |
| Aggiorna token | Token di aggiornamento ottenuto da Google per autorizzare l&#39;accesso ad AdWords. |
| ID client | L&#39;ID client dell&#39;applicazione Google utilizzata per acquisire il token di aggiornamento. |
| Segreto cliente | Il segreto client dell’applicazione Google utilizzata per acquisire il token di aggiornamento. |
| ID specifica connessione | Identificatore univoco necessario per creare una connessione. L&#39;ID della specifica di connessione per Google AdWords è: `d771e9c1-4f26-40dc-8617-ce58c4b53702` |

Per ulteriori informazioni su questi valori, consulta questo documento [](https://developers.google.com/adwords/api/docs/guides/authentication)Google AdWords.

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

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. Per l&#39;account Google AdWords è necessaria una sola connessione, in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una nuova connessione AdWords, configurata dalle proprietà fornite nel payload:


```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "google-AdWords connection",
        "description": "Connection for google-AdWords",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
                "developerToken": "{DEVELOPER_TOKEN}",
                "authenticationType": "{AUTHENTICATION_TYPE}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `auth.params.clientCustomerID` | L&#39;ID cliente cliente del tuo account AdWords. |
| `auth.params.developerToken` | Token sviluppatore del tuo account AdWords. |
| `auth.params.refreshToken` | Il token di aggiornamento dell&#39;account AdWords. |
| `auth.params.clientID` | L&#39;ID cliente del tuo account AdWords. |
| `auth.params.clientSecret` | Segreto cliente dell&#39;account AdWords. |
| `connectionSpec.id` | ID specifica di connessione Google AdWords: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell&#39;esercitazione successiva.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione Google AdWords utilizzando l&#39;API del servizio di flusso e hai ottenuto il valore ID univoco della connessione. Potete utilizzare questo ID nell&#39;esercitazione successiva per apprendere come [esplorare i sistemi pubblicitari mediante l&#39;API](../../explore/advertising.md)di servizio di flusso.
