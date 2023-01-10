---
keywords: Experience Platform;home;argomenti popolari;hub eventi;hub eventi di Azure;hub eventi
solution: Experience Platform
title: Creare una connessione di origine degli hub eventi di Azure utilizzando l’API del servizio di flusso
type: Tutorial
description: Scopri come collegare Adobe Experience Platform a un account Hubs di Azure Event utilizzando l’API del servizio di flusso.
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 2%

---


# Crea un [!DNL Azure Event Hubs] connessione di origine tramite [!DNL Flow Service] API

Questa esercitazione descrive i passaggi per la connessione [!DNL Azure Event Hubs] (in appresso denominato &quot;[!DNL Event Hubs]&quot;) ad Experience Platform, utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [Origini](../../../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
- [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per connettersi correttamente [!DNL Event Hubs] su Platform utilizzando [!DNL Flow Service] API.

### Raccogli credenziali richieste

Per [!DNL Flow Service] per connettersi con [!DNL Event Hubs] account, è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `sasKeyName` | Nome della regola di autorizzazione, noto anche come nome della chiave SAS. |
| `sasKey` | La chiave primaria del [!DNL Event Hubs] spazio dei nomi. La `sasPolicy` che `sasKey` corrisponde a `manage` diritti configurati per [!DNL Event Hubs] elenco da compilare. |
| `namespace` | Lo spazio dei nomi del [!DNL Event Hubs] stai accedendo. Un [!DNL Event Hubs] Lo spazio dei nomi fornisce un contenitore di ambito univoco, in cui è possibile creare uno o più [!DNL Event Hubs]. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. La [!DNL Event Hubs] ID della specifica di connessione: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Per ulteriori informazioni su questi valori, consulta [questo documento Hubs evento](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Il primo passaggio nella creazione di una connessione sorgente è quello di autenticare il [!DNL Event Hubs] e genera un ID di connessione di base. Un ID di connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e di identificare gli elementi specifici da acquisire, comprese le informazioni relative ai tipi di dati e ai formati corrispondenti.

Per creare un ID di connessione di base, invia una richiesta POST al `/connections` l&#39;endpoint durante la fornitura del [!DNL Event Hubs] credenziali di autenticazione come parte dei parametri della richiesta.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.namespace` | Lo spazio dei nomi del [!DNL Event Hubs] stai accedendo. |
| `connectionSpec.id` | La [!DNL Event Hubs] ID della specifica di connessione: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

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

Per creare una connessione di origine, invia una richiesta POST al `/sourceConnections` punto finale [!DNL Flow Service] API.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `baseConnectionId` | L&#39;ID di connessione del [!DNL Event Hubs] origine generata nel passaggio precedente. |
| `connectionSpec.id` | ID della specifica di connessione fissa per [!DNL Event Hubs]. Questo ID è: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | Il formato del [!DNL Event Hubs] dati da acquisire. Attualmente, l’unico formato di dati supportato è `json`. |
| `params.eventHubName` | Nome del [!DNL Event Hubs] sorgente. |
| `params.dataType` | Questo parametro definisce il tipo di dati da acquisire. I tipi di dati supportati includono: `raw` e `xdm`. |
| `params.reset` | Questo parametro definisce come verranno letti i dati. Utilizzo `latest` per iniziare a leggere dai dati più recenti e utilizzare `earliest` per iniziare a leggere dai primi dati disponibili nel flusso. Questo parametro è facoltativo e viene impostato come impostazione predefinita su `earliest` se non fornito. |
| `params.consumerGroup` | Meccanismo di pubblicazione o sottoscrizione da utilizzare per [!DNL Event Hubs]. Questo parametro è facoltativo e viene impostato come impostazione predefinita su `$Default` se non fornito. Fai riferimento a questo [[!DNL Event Hubs] guida all&#39;evento per i consumatori](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) per ulteriori informazioni. |

## Passaggi successivi

Seguendo questa esercitazione, hai creato un [!DNL Event Hubs] connessione di origine tramite [!DNL Flow Service] API. Puoi usare questo ID di connessione sorgente nell’esercitazione successiva per [creare un flusso di dati in streaming utilizzando [!DNL Flow Service] API](../../collect/streaming.md).
