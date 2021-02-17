---
keywords: ' Experience Platform;home;argomenti più comuni;collegamento in streaming;creare una connessione in streaming;guida API;esercitazione;creare una connessione in streaming;assimilazione in streaming;assimilazione;'
solution: Experience Platform
title: Creare una connessione in streaming mediante l'API
topic: tutorial
type: Tutorial
description: Questa esercitazione ti aiuterà a iniziare a utilizzare le API di assimilazione in streaming, parte delle API del servizio Adobe Experience Platform Data Ingestion.
translation-type: tm+mt
source-git-commit: 5932d63820dd0e50acccd18573746061232e099e
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 2%

---


# Creazione di una connessione in streaming mediante l&#39;API

Flow Service è utilizzato per raccogliere e centralizzare i dati dei clienti da varie origini diverse all&#39;interno di Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39;API [!DNL Flow Service] per guidarvi nei passaggi necessari per creare una connessione in streaming utilizzando l&#39;API del servizio di flusso.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): Il framework standard con cui  [!DNL Platform] organizzare i dati relativi all&#39;esperienza.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato in tempo reale basato su dati aggregati provenienti da più origini.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente chiamate alle API di assimilazione in streaming.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a2/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione di [panoramica sulla sandbox](../../../../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

## Creare una connessione

Una connessione specifica l&#39;origine e contiene le informazioni necessarie per rendere il flusso compatibile con le API di assimilazione in streaming. Quando si crea una connessione, è possibile creare una connessione non autenticata e una autenticata.

### Connessione non autenticata

Le connessioni non autenticate sono la connessione di streaming standard che è possibile creare quando si desidera trasmettere dati in streaming alla piattaforma.

**Formato API**

```http
POST /flowservice/connections
```

**Richiesta**

Per creare una connessione in streaming, è necessario fornire l&#39;ID provider e l&#39;ID specifica di connessione come parte della richiesta di POST. L&#39;ID provider è `521eee4d-8cbe-4906-bb48-fb6bd4450033` e l&#39;ID della specifica di connessione è `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.sourceId` | ID della connessione di streaming che si desidera creare. |
| `auth.params.dataType` | Il tipo di dati per la connessione di streaming. Il valore deve essere `xdm`. |
| `auth.params.name` | Nome della connessione di streaming che si desidera creare. |
| `connectionSpec.id` | Specifica di connessione `id` per le connessioni in streaming. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 con i dettagli della nuova connessione creata, incluso il relativo identificatore univoco (`id`).

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | `id` della nuova connessione creata. Di seguito viene indicato come `{CONNECTION_ID}`. |
| `etag` | Identificatore assegnato alla connessione, che specifica la revisione della connessione. |

### Connessione autenticata

Le connessioni autenticate devono essere utilizzate quando è necessario distinguere tra record provenienti da fonti affidabili e non attendibili. Gli utenti che desiderano inviare informazioni con Informazioni personali (PII, Personally Identifiable Information) devono creare una connessione autenticata durante lo streaming delle informazioni sulla piattaforma.

**Formato API**

```http
POST /flowservice/connections
```

**Richiesta**

Per creare una connessione in streaming, è necessario fornire l&#39;ID provider e l&#39;ID specifica di connessione come parte della richiesta di POST. L&#39;ID provider è `521eee4d-8cbe-4906-bb48-fb6bd4450033` e l&#39;ID della specifica di connessione è `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```


| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.sourceId` | ID della connessione di streaming che si desidera creare. |
| `auth.params.dataType` | Il tipo di dati per la connessione di streaming. Il valore deve essere `xdm`. |
| `auth.params.name` | Nome della connessione di streaming che si desidera creare. |
| `auth.params.authenticationRequired` | Il parametro che specifica che la connessione di streaming creata |
| `connectionSpec.id` | Specifica di connessione `id` per le connessioni in streaming. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 con i dettagli della nuova connessione creata, incluso il relativo identificatore univoco (`id`).

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | `id` della nuova connessione creata. Di seguito viene indicato come `{CONNECTION_ID}`. |
| `etag` | Identificatore assegnato alla connessione, che specifica la revisione della connessione. |

## Ottieni URL endpoint di streaming

Con la connessione creata, ora potete recuperare l&#39;URL dell&#39;endpoint di streaming.

**Formato API**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{CONNECTION_ID}` | Il valore `id` della connessione creata in precedenza. |

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sulla connessione richiesta. L&#39;URL dell&#39;endpoint di streaming viene creato automaticamente con la connessione e può essere recuperato utilizzando il valore `inletUrl`.

```json
{
    "items": [
        {
            "createdAt": 1583971856947,
            "updatedAt": 1583971856947,
            "createdBy": "{API_KEY}",
            "updatedBy": "{API_KEY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "id": "77a05521-91d6-451c-a055-2191d6851c34",
            "name": "Another new sample connection (Experience Event)",
            "description": "Sample description",
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Streaming Connection",
                "params": {
                    "sourceId": "Sample connection (ExperienceEvent)",
                    "inletUrl": "https://dcs.adobedc.net/collection/a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "inletId": "a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "dataType": "xdm",
                    "name": "Sample connection (ExperienceEvent)"
                }
            },
            "version": "\"56008aee-0000-0200-0000-5e697e150000\"",
            "etag": "\"56008aee-0000-0200-0000-5e697e150000\""
        }
    ]
}
```

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione HTTP in streaming che consente di utilizzare l&#39;endpoint in streaming per trasferire i dati nella piattaforma. Per istruzioni su come creare una connessione in streaming nell&#39;interfaccia utente, leggete l&#39; [creazione di un&#39;esercitazione sulla connessione in streaming](../../../ui/create/streaming/http.md).

Per informazioni su come eseguire lo streaming dei dati sulla piattaforma, leggere l&#39;esercitazione su [streaming time series data](../../../../../ingestion/tutorials/streaming-time-series-data.md) o l&#39;esercitazione su [streaming record data](../../../../../ingestion/tutorials/streaming-record-data.md).

## Appendice

Questa sezione fornisce informazioni supplementari sulla creazione di connessioni in streaming mediante l&#39;API.

### Invio di messaggi a una connessione in streaming autenticata

Se l&#39;autenticazione di una connessione in streaming è abilitata, il client dovrà aggiungere l&#39;intestazione `Authorization` alla propria richiesta.

Se l&#39;intestazione `Authorization` non è presente o viene inviato un token di accesso non valido/scaduto, viene restituita una risposta non autorizzata HTTP 401, con una risposta simile come segue:

**Risposta**

```json
{
    "type": "https://ns.adobe.com/adobecloud/problem/data-collection-service-authorization",
    "status": "401",
    "title": "Authorization",
    "report": {
        "message": "[id] Ims service token is empty"
    }
}
```
