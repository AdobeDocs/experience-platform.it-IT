---
keywords: ' Experience Platform;home;argomenti popolari;hub eventi;hub eventi di Azure;hub eventi'
solution: Experience Platform
title: Creare un connettore Azure Event Hubs utilizzando l'API del servizio di flusso
topic: overview
type: Tutorial
description: Questa esercitazione utilizza l'API del servizio di flusso per seguire i passaggi necessari per connettere  Experience Platform a un account Hubs evento di Azure.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 2%

---


# Creare un connettore [!DNL Azure Event Hubs] utilizzando l&#39;API [!DNL Flow Service]

>[!NOTE]
>
> Il connettore [!DNL Azure Event Hubs] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, vedere [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions).

[!DNL Flow Service] viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie origini all&#39;interno di Adobe Experience Platform. Il servizio fornisce un&#39;interfaccia utente e RESTful API da cui sono collegate tutte le origini supportate.

Questa esercitazione utilizza l&#39;API [!DNL Flow Service] per guidarti attraverso i passaggi necessari per connettersi [!DNL Experience Platform] a un account [!DNL Azure Event Hubs].

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Origini](../../../../home.md):  [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
- [Sandbox](../../../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a un account [!DNL Azure Event Hubs] utilizzando l&#39;API [!DNL Flow Service].

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi con l&#39;account [!DNL Azure Event Hubs], è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `sasKeyName` | Nome della regola di autorizzazione, noto anche come nome della chiave SAS. |
| `sasKey` | La firma di accesso condiviso generata. |
| `namespace` | Lo spazio dei nomi degli hub eventi a cui si accede. |
| `connectionSpec.id` | ID specifica di connessione [!DNL Azure Event Hubs]: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

Per ulteriori informazioni su questi valori, fare riferimento a [questo documento Hubs evento](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a2/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come illustrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

- `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva per il tipo di supporto:

- `Content-Type: application/json`

## Creare una connessione

Una connessione specifica un&#39;origine e contiene le credenziali per tale origine. È necessaria una sola connessione per ogni account [!DNL Azure Event Hubs], in quanto può essere utilizzata per creare più connettori sorgente per inserire dati diversi.

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
        "name": "Azure Event Hubs connection",
        "description": "Connector for Azure Event Hubs",
        "auth": {
            "specName": "Basic Authentication for Event Hubs",
            "params": {
                "sasKeyName": "sasKeyName",
                "sasKey": "sasKey",
                "namespace": "namespace"
            }
        },
        "connectionSpec": {
            "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.sasKeyName` | Nome della regola di autorizzazione, noto anche come nome della chiave SAS. |
| `auth.params.sasKey` | La firma di accesso condiviso generata. |
| `namespace` | Lo spazio dei nomi della [!DNL Event Hubs] a cui si accede. |
| `connectionSpec.id` | ID specifica di connessione [!DNL Azure Event Hubs]: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario per esplorare i dati di archiviazione cloud nell&#39;esercitazione successiva.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, avete creato una connessione [!DNL Azure Event Hubs] mediante le API e un ID univoco è stato ottenuto come parte del corpo della risposta. Puoi utilizzare questo ID connessione per [raccogliere i dati di streaming utilizzando l&#39;API del servizio di flusso](../../collect/streaming.md).