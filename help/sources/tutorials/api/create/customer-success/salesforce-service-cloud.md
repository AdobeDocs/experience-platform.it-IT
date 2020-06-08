---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore Salesforce Service Cloud utilizzando l'API del servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: 0ed2ed3b08f262100746f255a78c248a1748eb5e
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 1%

---


# Creare un connettore Salesforce Service Cloud utilizzando l&#39;API del servizio di flusso

>[!NOTE]
>Il connettore Salesforce Service Cloud è in versione beta. Le funzioni e la documentazione sono soggette a modifiche.

Flow Service è utilizzato per raccogliere e centralizzare i dati dei clienti da varie origini diverse all&#39;interno di Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l’API del servizio di flusso per guidarti attraverso i passaggi necessari per connettere Experience Platform a Salesforce Service Cloud (in seguito denominata &quot;SSC&quot;).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie fonti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi della piattaforma.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a SSC tramite l&#39;API del servizio di flusso.

### Raccogli credenziali richieste

Affinché Flow Service possa connettersi con SSC, è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `username` | Nome utente per l’account utente. |
| `password` | La password dell&#39;account utente. |
| `securityToken` | Token di sicurezza per l&#39;account utente. |

Per ulteriori informazioni su come iniziare, consulta [questo documento](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm)Salesforce Service Cloud.

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

## Cercare le specifiche di connessione

Per creare una connessione SSC, è necessario che in Flow Service esista una serie di specifiche di connessione SSC. Il primo passo per collegare la piattaforma a SSC è recuperare queste specifiche.

**Formato API**

Ogni origine disponibile dispone di un proprio set di specifiche di connessione per descrivere le proprietà del connettore, ad esempio i requisiti di autenticazione. L&#39;invio di una richiesta GET all&#39; `/connectionSpecs` endpoint restituirà le specifiche di connessione per tutte le origini disponibili. È inoltre possibile includere la query `property=name=="salesforce-service-cloud"` per ottenere informazioni specifiche per SSC.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="salesforce-service-cloud"
```

**Richiesta**

La richiesta seguente recupera le specifiche di connessione per SSC.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="mysql"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce le specifiche di connessione per la SSC, incluso il suo unico identificatore (`id`). Questo ID è richiesto nel passaggio successivo per la creazione di una connessione di base.

```json
{
    "items": [
        {
            "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
            "name": "salesforce-service-cloud",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "BasicAuthentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "environmentUrl": {
                                "type": "string",
                                "description": "URL of the source instance"
                            },
                            "username": {
                                "type": "string",
                                "description": "User name for the user account"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            },
                            "securityToken": {
                                "type": "string",
                                "description": "Security token for the user account",
                                "format": "password"
                            }
                        },
                        "required": [
                            "username",
                            "password",
                            "securityToken"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## Creazione di una connessione di base

Una connessione di base specifica un&#39;origine e contiene le credenziali per tale origine. Per ciascun account SSC è necessaria una sola connessione di base, in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

**Formato API**

```http
POST /connections
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Base connection for salesforce service cloud",
        "description": "Base connection for salesforce service cloud",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "b66ab34-8619-49cb-96d1-39b37ede86ea",
            "version": "1.0"
        }
    }'
```

| Parametro | Descrizione |
| --------- | ----------- |
| `auth.params.username` | Il nome utente associato al tuo account SSC. |
| `auth.params.password` | La password associata al tuo account SSC. |
| `auth.params.securityToken` | Token di sicurezza associato al tuo account SSC. |
| `connectionSpec.id` | Specifica di connessione `id` del tuo account SSC recuperato nel passaggio precedente. |

**Risposta**

Una risposta corretta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell&#39;esercitazione successiva.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione di base SSC utilizzando l&#39;API Flow Service e hai ottenuto il valore ID univoco della connessione. Puoi usare questo ID connessione di base nell&#39;esercitazione successiva per scoprire come [esplorare i sistemi di successo dei clienti tramite l&#39;API](../../explore/customer-success.md)del servizio di flusso.
