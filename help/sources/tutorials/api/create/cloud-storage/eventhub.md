---
keywords: Experience Platform;home;argomenti popolari;hub eventi;hub eventi di Azure;hub eventi
solution: Experience Platform
title: Creare una connessione di origine degli hub eventi di Azure utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a un account Hubs di Azure Event utilizzando l’API del servizio di flusso.
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 2%

---


# Creare una connessione sorgente [!DNL Azure Event Hubs] utilizzando l&#39;API [!DNL Flow Service]

Questa esercitazione descrive i passaggi necessari per collegare [!DNL Azure Event Hubs] (in seguito denominato &quot;[!DNL Event Hubs]&quot;) all’Experience Platform, utilizzando l’ [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [Origini](../../../../home.md):  [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo tramite  [!DNL Platform] i servizi.
- [Sandbox](../../../../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente a [!DNL Event Hubs] Platform utilizzando l’ API [!DNL Flow Service].

### Raccogli credenziali richieste

Affinché [!DNL Flow Service] possa connettersi all&#39;account [!DNL Event Hubs], è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `sasKeyName` | Nome della regola di autorizzazione, noto anche come nome della chiave SAS. |
| `sasKey` | La firma di accesso condiviso generata. |
| `namespace` | Spazio dei nomi del [!DNL Event Hubs] a cui si accede. Uno spazio dei nomi [!DNL Event Hubs] fornisce un contenitore di ambito univoco in cui è possibile creare uno o più [!DNL Event Hubs]. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. L&#39;ID delle specifiche di connessione [!DNL Event Hubs] è: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Per ulteriori informazioni su questi valori, consulta [questo documento Host eventi](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md) .

## Creare una connessione di base

Il primo passaggio nella creazione di una connessione sorgente è quello di autenticare la [!DNL Event Hubs] sorgente e generare un ID di connessione di base. Un ID di connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Event Hubs] come parte dei parametri della richiesta.

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
            "specName": "Azure EventHub authentication credentials",
            "params": {
                "sasKeyName": "{SAS_KEY_NAME}",
                "sasKey": "{SAS_KEY}",
                "namespace": "{NAMESPACE}"
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
| `auth.params.namespace` | Spazio dei nomi del [!DNL Event Hubs] a cui si accede. |
| `connectionSpec.id` | L&#39;ID delle specifiche di connessione [!DNL Event Hubs] è: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova connessione di base creata, incluso il relativo identificatore univoco (`id`). Questo ID di connessione è necessario nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Creazione di una connessione sorgente

Una connessione di origine crea e gestisce la connessione all’origine esterna da cui vengono acquisiti i dati. Una connessione di origine è costituita da informazioni quali l’origine dati, il formato dati e un ID di connessione di origine necessari per creare un flusso di dati. Un’istanza di connessione di origine è specifica per un tenant e un’organizzazione IMS.

Per creare una connessione sorgente, effettua una richiesta POST all’ endpoint `/sourceConnections` dell’ API [!DNL Flow Service] .

**Formato API**

```http
POST /sourceConnections
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'authorization: Bearer {ACCESS_TOKEN}' \
    -H 'content-type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_Org}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -d '{
        "name": "Azure Event Hubs source connection",
        "description": "A source connection for Azure Event Hubs",
        "baseConnectionId": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
        "connectionSpec": {
            "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "eventHubName": "{EVENTHUB_NAME}",
            "dataType": "raw",
            "reset": "latest",
            "consumerGroup": "{CONSUMER_GROUP}"
        }
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della connessione di origine. Assicurati che il nome della connessione sorgente sia descrittivo, in quanto puoi utilizzarlo per cercare informazioni sulla connessione sorgente. |
| `description` | Valore facoltativo che è possibile fornire per includere ulteriori informazioni sulla connessione sorgente. |
| `baseConnectionId` | L&#39;ID di connessione dell&#39;origine [!DNL Event Hubs] generato nel passaggio precedente. |
| `connectionSpec.id` | ID della specifica di connessione fissa per [!DNL Event Hubs]. Questo ID è : `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | Il formato dei dati [!DNL Event Hubs] da acquisire. Attualmente, l’unico formato di dati supportato è `json`. |
| `params.eventHubName` | Il nome dell&#39;origine [!DNL Event Hubs]. |
| `params.dataType` | Questo parametro definisce il tipo di dati da acquisire. I tipi di dati supportati includono: `raw` e `xdm`. |
| `params.reset` | Questo parametro definisce come verranno letti i dati. Utilizza `latest` per iniziare a leggere i dati più recenti e utilizza `earliest` per iniziare a leggere i primi dati disponibili nel flusso. Questo parametro è facoltativo e viene impostato automaticamente su `earliest` se non viene fornito. |
| `params.consumerGroup` | Il meccanismo di pubblicazione o sottoscrizione da utilizzare per [!DNL Event Hubs]. Questo parametro è facoltativo e viene impostato automaticamente su `$Default` se non viene fornito. Per ulteriori informazioni, consulta questa [[!DNL Event Hubs] guida sui consumatori di eventi](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) . |

## Passaggi successivi

Seguendo questa esercitazione, hai creato una connessione sorgente [!DNL Event Hubs] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID di connessione sorgente nell’esercitazione successiva per [creare un flusso di dati utilizzando l’ [!DNL Flow Service] API](../../collect/streaming.md).
