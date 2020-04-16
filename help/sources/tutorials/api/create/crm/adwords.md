---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore Google AdWords utilizzando l'API del servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: a456dce58c32348c9e680cd672b71dd7bbdc1a04

---


# Creare un connettore Google AdWords utilizzando l&#39;API del servizio di flusso

Flow Service è utilizzato per raccogliere e centralizzare i dati dei clienti da varie origini diverse all&#39;interno di Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l’API del servizio di flusso per seguire i passaggi necessari per connettere Experience Platform a Google AdWords (di seguito &quot;AdWords&quot;).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie fonti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi della piattaforma.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente ad AdWords tramite l&#39;API del servizio di flusso.

### Raccogli credenziali richieste

Affinché il servizio di flusso possa connettersi con AdWords, è necessario fornire i valori per le seguenti proprietà di connessione:

| **Credenziali** | **Descrizione** |
| -------------- | --------------- |
| `clientCustomerID` | ID cliente associato a Google AdWords di destinazione | account. |
| `developerToken` | Stringa utilizzata per identificare uno sviluppatore API AdWords. |
| `refreshToken` | Il token di aggiornamento ottenuto da Google utilizzato per autorizzare l&#39;accesso ad AdWords. |
| `clientID` | ID dell’applicazione utilizzata per generare il token di aggiornamento. |
| `clientSecret` | Il segreto client per l&#39;applicazione utilizzata per generare il token di aggiornamento. |

Per ulteriori informazioni su questi valori, consulta questo documento [](https://developers.google.com/adwords/api/docs/guides/authentication)Google AdWords.

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

## Cercare le specifiche di connessione

Per creare una connessione AdWords, all&#39;interno del servizio di flusso deve essere presente un set di specifiche di connessione AdWords. Il primo passo per collegare Platform ad AdWords è recuperare queste specifiche.

**Formato API**

Ogni origine disponibile dispone di un proprio set di specifiche di connessione per descrivere le proprietà del connettore, ad esempio i requisiti di autenticazione. È possibile ricercare le specifiche di connessione per AdWords eseguendo una richiesta GET e utilizzando i parametri di query.

L&#39;invio di una richiesta GET senza parametri di query restituirà le specifiche di connessione per tutte le origini disponibili. È possibile includere la query `property=name=="google-adwords"` per ottenere informazioni specifiche per AdWords.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="google-adwords"
```

**Richiesta**

La richiesta seguente recupera la specifica di connessione per AdWords.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?{QUERY_PARAMS}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce la specifica di connessione per AdWords, incluso il relativo identificatore univoco (`id`). Questo ID è richiesto nel passaggio successivo per creare una connessione di base.

```json
{
    "items": [
        {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "name": "google-adwords",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for google-adwords",
                    "type": "Basic_Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "clientCustomerID": {
                                "type": "string",
                                "description": "The Client customer ID of the AdWords account"
                            },
                            "developerToken": {
                                "type": "string",
                                "description": "The developer token associated with the manager account",
                                "format": "password"
                            },
                            "refreshToken": {
                                "type": "string",
                                "description": "The refresh token obtained from Google for authorizing access to AdWords",
                                "format": "password"
                            },
                            "clientId": {
                                "type": "string",
                                "description": "The client ID of the Google application used to acquire the refresh token"
                            },
                            "clientSecret": {
                                "type": "string",
                                "description": "The client secret of the google application used to acquire the refresh token",
                                "format": "password"
                            }
                        },
                        "required": [
                            "clientCustomerID",
                            "developerToken",
                            "refreshToken",
                            "clientId",
                            "clientSecret"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## Creazione di una connessione di base

Una connessione di base specifica un&#39;origine e contiene le credenziali per tale origine. Per l&#39;account AdWords è necessaria una sola connessione di base, in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

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
        "name": "google-adwords base connection",
        "description": "Base connection for google-adwords",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
                "developerToken": "{DEVELOPER_TOKEN}",
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "version": "1.0"
        }
    }
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.clientCustomerID` | L&#39;ID cliente cliente del tuo account AdWords. |
| `auth.params.developerToken` | Token sviluppatore del tuo account AdWords. |
| `auth.params.refreshToken` | Il token di aggiornamento dell&#39;account AdWords. |
| `auth.params.clientID` | L&#39;ID cliente del tuo account AdWords. |
| `auth.params.clientSecret` | Segreto cliente dell&#39;account AdWords. |
| `connectionSpec.id` | Specifica di connessione `id` dell&#39;account AdWords recuperato nel passaggio precedente. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della connessione di base appena creata. Questo ID è necessario per esplorare i dati AdWords nell&#39;esercitazione successiva.

```json
{
    "id": "e6ce1eab-416b-4a20-8e1e-ab416b1a206f",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione di base AdWords utilizzando l&#39;API del servizio di flusso e hai ottenuto il valore ID univoco della connessione. Puoi utilizzare questo ID di connessione di base nell&#39;esercitazione successiva per imparare a [esplorare i sistemi CRM utilizzando l&#39;API](../../explore/crm.md)del servizio di flusso.
