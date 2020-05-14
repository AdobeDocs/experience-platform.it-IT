---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore MySQL utilizzando l'API del servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: 37a5f035023cee1fc2408846fb37d64b9a3fc4b6
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 1%

---


# Creare un connettore MySQL utilizzando l&#39;API del servizio di flusso

>[!NOTE]
>Il connettore MySQL è in versione beta. Le funzioni e la documentazione sono soggette a modifiche.

Flow Service è utilizzato per raccogliere e centralizzare i dati dei clienti da varie origini diverse all&#39;interno di Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l’API del servizio di flusso per seguire i passaggi necessari per connettere Experience Platform a MySQL.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie fonti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi della piattaforma.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a MySQL tramite l&#39;API del servizio di flusso.

### Raccogli credenziali richieste

Affinché il servizio di flusso possa connettersi all&#39;archivio MySQL, è necessario fornire il valore per la seguente proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Stringa di connessione MySQL associata all&#39;account. |

Per ulteriori informazioni sulle stringhe di connessione e su come ottenerle, leggere il documento [](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html)MySQL.

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

Per creare una connessione MySQL, è necessario che nel servizio di flusso esista un set di specifiche di connessione MySQL. Il primo passaggio per la connessione di Platform a MySQL consiste nel recuperare queste specifiche.

**Formato API**

Ogni origine disponibile dispone di un proprio set di specifiche di connessione per descrivere le proprietà del connettore, ad esempio i requisiti di autenticazione. L&#39;invio di una richiesta GET all&#39; `/connectionSpecs` endpoint restituirà le specifiche di connessione per tutte le origini disponibili. È inoltre possibile includere la query `property=name=="mysql"` per ottenere informazioni specifiche per MySQL.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="mysql"
```

**Richiesta**

La richiesta seguente recupera la specifica di connessione per MySQL.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="mysql"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce le specifiche di connessione per MySQL, incluso il relativo identificatore univoco (`id`). Questo ID è richiesto nel passaggio successivo per la creazione di una connessione di base.

```json
{
    "items": [
        {
            "id": "26d738e0-8963-47ea-aadf-c60de735468a",
            "name": "mysql",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Connection String Based Authentication",
                    "type": "connectionStringAuth",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to MySql",
                        "properties": {
                            "connectionString": {
                                "type": "string",
                                "description": "connection string to connect to any MySql instance.",
                                "format": "password",
                                "pattern": "^([sS]erver=)(.*)( ?;[pP]ort=)(.*)(; ?[dD]atabase=)(.*)(; ?[uU]id=)(.*)(; ?[pP]wd=)(.*)(;)",
                                "examples": [
                                    "Server=myserver.mysql.database.azure.com; Port=3306; Database=my_sql_db; Uid=username; Pwd=password; SslMode=Preferred;"
                                ]
                            }
                        },
                        "required": [
                            "connectionString"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Creazione di una connessione di base

Una connessione di base specifica un&#39;origine e contiene le credenziali per tale origine. Per l&#39;account MySQL è necessaria una sola connessione di base, in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

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
        "name": "MySQL Test Connection",
        "description": "MySQL Test Connection",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "{CONNECTION_STRING}"
            }
        },
        "connectionSpec": {
            "id": "26d738e0-8963-47ea-aadf-c60de735468a",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `auth.params.connectionString` | Stringa di connessione associata all&#39;account MySQL. |
| `connectionSpec.id` | L&#39;ID della specifica di connessione associata al tuo account MySQL. |

**Risposta**

Una risposta corretta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell&#39;esercitazione successiva.

```json
{
    "id": "1a444165-3439-4c16-8441-653439dc166a",
    "etag": "\"5b04c219-0000-0200-0000-5e179c8f0000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione di base MySQL tramite l&#39;API del servizio di flusso e si è ottenuto il valore ID univoco della connessione. È possibile utilizzare questo ID connessione di base nell&#39;esercitazione successiva per apprendere come [esplorare i database o i sistemi NoSQL utilizzando l&#39;API](../../explore/database-nosql.md)del servizio di flusso.