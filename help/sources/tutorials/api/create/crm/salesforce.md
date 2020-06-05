---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore Salesforce utilizzando l'API del servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: 72c1d53295d5c4204c02959c857edc06f246534c
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 1%

---


# Creare un connettore Salesforce utilizzando l&#39;API del servizio di flusso

Flow Service è utilizzato per raccogliere e centralizzare i dati dei clienti da varie origini diverse all&#39;interno di Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39;API del servizio di flusso per guidarti nei passaggi necessari per connettere la piattaforma a un account Salesforce per la raccolta dei dati CRM.

Se preferisci utilizzare l’interfaccia utente in Experience Platform, l’esercitazione [dell’interfaccia utente del connettore sorgente di](../../../ui/create/crm/salesforce.md) Salesforce fornisce istruzioni dettagliate per eseguire azioni simili.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie fonti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi della piattaforma.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettere correttamente la piattaforma a un account Salesforce tramite l&#39;API del servizio di flusso.

### Raccogli credenziali richieste

Affinché il servizio di flusso possa connettersi a Salesforce, è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `environmentUrl` | URL dell’istanza di origine Salesforce. |
| `username` | Nome utente per l’account utente Salesforce. |
| `password` | La password dell’account utente Salesforce. |
| `securityToken` | Token di sicurezza per l’account utente Salesforce. |

Per ulteriori informazioni su come iniziare, consulta [questo documento](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm)Salesforce.

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

Prima di collegare la piattaforma a un account Salesforce, devi verificare che siano presenti specifiche di connessione per Salesforce. Se le specifiche di connessione non esistono, non è possibile stabilire una connessione.

Ogni origine disponibile dispone di un proprio set di specifiche di connessione per descrivere le proprietà del connettore, ad esempio i requisiti di autenticazione. Puoi cercare le specifiche di connessione per Salesforce eseguendo una richiesta GET e utilizzando i parametri della query.

**Formato API**

L&#39;invio di una richiesta GET senza parametri di query restituirà le specifiche di connessione per tutte le origini disponibili. Puoi includere la query `property=name=="salesforce"` per ottenere informazioni specifiche per Salesforce.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="salesforce"
```

**Richiesta**

La richiesta seguente recupera le specifiche di connessione per Salesforce.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name==%22salesforce%22' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce le specifiche di connessione per Salesforce, incluso il relativo identificatore univoco (`id`). Questo ID è richiesto nel passaggio successivo per creare una connessione di base.

```json
{
    "items": [
        {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "name": "salesforce",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "Basic_Authentication",
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
            ]
        }
    ]
}
```

## Creazione di una connessione di base

Una connessione di base specifica un&#39;origine e contiene le credenziali per tale origine. Per l&#39;account Salesforce è necessaria una sola connessione di base, in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

Eseguite la seguente richiesta POST per creare una connessione di base.

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
        "name": "Salesforce Base Connection",
        "description": "Base connection for Salesforce account",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.username` | Il nome utente associato al tuo account Salesforce. |
| `auth.params.password` | La password associata al tuo account Salesforce. |
| `auth.params.securityToken` | Token di sicurezza associato al tuo account Salesforce. |
| `connectionSpec.id` | Specifica di connessione `id` dell’account Salesforce recuperato nel passaggio precedente. |

**Risposta**

Una risposta corretta contiene l&#39;identificatore univoco (`id`) della connessione di base. Questo ID è necessario per esplorare i dati nell&#39;esercitazione successiva.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione hai creato una connessione di base per l’account Salesforce che utilizza le API e un ID univoco è stato ottenuto come parte del corpo della risposta. Puoi utilizzare questo ID di connessione di base nell&#39;esercitazione successiva per imparare a [esplorare i sistemi CRM utilizzando l&#39;API](../../explore/crm.md)del servizio di flusso.