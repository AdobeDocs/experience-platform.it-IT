---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore Google BigQuery utilizzando l'API del servizio di flusso
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 1%

---


# Creare un [!DNL Google BigQuery] connettore utilizzando l&#39; [!DNL Flow Service] API

>[!NOTE]
>Il [!DNL Google BigQuery] connettore è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti diverse all&#39;interno  Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39; [!DNL Flow Service] API per guidarvi attraverso i passaggi necessari per la connessione [!DNL Experience Platform] a [!DNL Google BigQuery] (in seguito denominata &quot;BigQuery&quot;).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti del  Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] i servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a BigQuery utilizzando l&#39; [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] connettersi a BigQuery, è necessario specificare le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `project` | L&#39;ID progetto del [!DNL BigQuery] progetto predefinito su cui eseguire la query. |
| `clientID` | Il valore ID utilizzato per generare il token di aggiornamento. |
| `clientSecret` | Il valore segreto utilizzato per generare il token di aggiornamento. |
| `refreshToken` | Token di aggiornamento ottenuto da [!DNL Google] utilizzato per autorizzare l&#39;accesso a [!DNL BigQuery]. |

Per ulteriori informazioni su questi valori, consultare [questo documento](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing)BigQuery.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../../../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti al gruppo [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

* Content-Type: `application/json`

## Cercare le specifiche di connessione

Per creare una [!DNL BigQuery] connessione, è necessario che all&#39;interno di [!DNL BigQuery] sia presente una serie di specifiche di [!DNL Flow Service]connessione. Il primo passo per collegarsi [!DNL Platform] a [!DNL BigQuery] è recuperare queste specifiche.

**Formato API**

Ogni origine disponibile dispone di un proprio set di specifiche di connessione per descrivere le proprietà del connettore, ad esempio i requisiti di autenticazione. Potete cercare le specifiche di connessione [!DNL BigQuery] eseguendo una richiesta GET e utilizzando i parametri di query.

L&#39;invio di una richiesta GET senza parametri di query restituirà le specifiche di connessione per tutte le origini disponibili. È possibile includere la query `property=name=="google-big-query"` per ottenere informazioni specifiche per [!DNL BigQuery].

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="google-big-query"
```

**Richiesta**

La richiesta seguente recupera le specifiche di connessione per [!DNL BigQuery].

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce le specifiche di connessione per [!DNL BigQuery], incluso il relativo identificatore univoco (`id`). Questo ID è richiesto nel passaggio successivo per creare una connessione di base.

```json
{
    "items": [
        {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "name": "google-big-query",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "project": {
                                "type": "string",
                                "description": "The project ID of the default BigQuery project to query against"
                            },
                            "clientId": {
                                "type": "string",
                                "description": "ID of the application used to generate the refresh token."
                            },
                            "clientSecret": {
                                "type": "string",
                                "description": "Secret of the application used to generate the refresh token.",
                                "format": "password"
                            },
                            "refreshToken": {
                                "type": "string",
                                "description": "The refresh token obtained from Google used to authorize access to BigQuery.",
                                "format": "password"
                            }
                        },
                        "required": [
                            "project",
                            "clientId",
                            "clientSecret",
                            "refreshToken"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Creazione di una connessione di base

Una connessione di base specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione di base per [!DNL BigQuery] account, in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

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
        "name": "BigQuery base connection",
        "description": "Base connection for Google BigQuery",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "project": "{PROJECT}",
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
    }'
```

| Proprietà | Descrizione |
| --------- | ----------- |
| `auth.params.project` | L&#39;ID progetto del [!DNL BigQuery] progetto predefinito su cui eseguire la query. contro. |
| `auth.params.clientId` | Il valore ID utilizzato per generare il token di aggiornamento. |
| `auth.params.clientSecret` | Il valore client utilizzato per generare il token di aggiornamento. |
| `auth.params.refreshToken` | Token di aggiornamento ottenuto da [!DNL Google] utilizzato per autorizzare l&#39;accesso a [!DNL BigQuery]. |
| `connectionSpec.id` | Specifica di connessione `id` dell’ [!DNL BigQuery] account recuperato nel passaggio precedente. |

**Risposta**

Una risposta corretta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati nell&#39;esercitazione successiva.

```json
{
    "id": "26ced882-729b-470f-8ed8-82729b570f03",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione di [!DNL BigQuery] base utilizzando l&#39; [!DNL Flow Service] API e hai ottenuto il valore ID univoco della connessione. È possibile utilizzare questo ID connessione di base nell&#39;esercitazione successiva per apprendere come [esplorare i database o i sistemi NoSQL utilizzando l&#39;API](../../explore/database-nosql.md)del servizio di flusso.
