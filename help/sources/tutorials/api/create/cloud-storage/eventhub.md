---
title: Creare una connessione di origine degli hub eventi di Azure tramite l’API del servizio Flusso
description: Scopri come connettere Adobe Experience Platform a un account Azure Event Hubs utilizzando l’API del servizio Flusso.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 2%

---

# Creare un [!DNL Azure Event Hubs] connessione sorgente tramite [!DNL Flow Service] API

>[!IMPORTANT]
>
>Il [!DNL Azure Event Hubs] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Questo tutorial illustra i passaggi necessari per la connessione [!DNL Azure Event Hubs] (in seguito denominati &quot;[!DNL Event Hubs]&quot;) per l&#39;Experience Platform, utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Sorgenti](../../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
- [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente [!DNL Event Hubs] alla piattaforma utilizzando [!DNL Flow Service] API.

### Raccogli le credenziali richieste

Per ottenere [!DNL Flow Service] per connettersi con [!DNL Event Hubs] account, è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `sasKeyName` | Il nome della regola di autorizzazione, noto anche come nome della chiave SAS. |
| `sasKey` | La chiave primaria della [!DNL Event Hubs] spazio dei nomi. Il `sasPolicy` che il `sasKey` corrisponde a deve avere `manage` diritti configurati per il [!DNL Event Hubs] elenco da compilare. |
| `namespace` | Lo spazio dei nomi del [!DNL Event Hubs] si sta effettuando l&#39;accesso. Un [!DNL Event Hubs] namespace fornisce un contenitore di ambito univoco, nel quale è possibile creare uno o più [!DNL Event Hubs]. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. Il [!DNL Event Hubs] ID specifica di connessione: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Per ulteriori informazioni su questi valori, consulta [questo documento Hub eventi](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

Il primo passaggio nella creazione di una connessione sorgente consiste nell’autenticare [!DNL Event Hubs] e generare un ID di connessione di base. Un ID di connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare elementi specifici da acquisire, incluse informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL Event Hubs] credenziali di autenticazione come parte dei parametri della richiesta.

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
| `auth.params.sasKeyName` | Il nome della regola di autorizzazione, noto anche come nome della chiave SAS. |
| `auth.params.sasKey` | Firma di accesso condiviso generata. |
| `auth.params.namespace` | Lo spazio dei nomi del [!DNL Event Hubs] si sta effettuando l&#39;accesso. |
| `connectionSpec.id` | Il [!DNL Event Hubs] ID specifica di connessione: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID connessione è richiesto nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Creare una connessione sorgente

Una connessione di origine crea e gestisce la connessione all’origine esterna da cui vengono acquisiti i dati. Una connessione di origine è costituita da informazioni quali origine dati, formato dati e un ID di connessione di origine necessari per creare un flusso di dati. Un&#39;istanza della connessione di origine è specifica di un tenant e di un&#39;organizzazione.

Per creare una connessione sorgente, effettua una richiesta POST al `/sourceConnections` endpoint del [!DNL Flow Service] API.

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
| `name` | Nome della connessione di origine. Assicurati che il nome della connessione sorgente sia descrittivo, in quanto può essere utilizzato per cercare informazioni sulla connessione sorgente. |
| `description` | Valore facoltativo che è possibile fornire per includere ulteriori informazioni sulla connessione di origine. |
| `baseConnectionId` | ID di connessione del tuo [!DNL Event Hubs] origine generata nel passaggio precedente. |
| `connectionSpec.id` | ID della specifica di connessione fissa per [!DNL Event Hubs]. Questo ID è: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | Il formato del [!DNL Event Hubs] i dati che desideri acquisire. Attualmente, l’unico formato di dati supportato è `json`. |
| `params.eventHubName` | Il nome per il [!DNL Event Hubs] sorgente. |
| `params.dataType` | Questo parametro definisce il tipo di dati che viene acquisito. I tipi di dati supportati includono: `raw` e `xdm`. |
| `params.reset` | Questo parametro definisce la modalità di lettura dei dati. Utilizzare `latest` per iniziare a leggere dai dati più recenti e utilizzare `earliest` per iniziare a leggere dai primi dati disponibili nel flusso. Questo parametro è facoltativo e viene impostato automaticamente su `earliest` se non specificato. |
| `params.consumerGroup` | Il meccanismo di pubblicazione o di abbonamento da utilizzare per [!DNL Event Hubs]. Questo parametro è facoltativo e viene impostato automaticamente su `$Default` se non specificato. Fai riferimento a questo [[!DNL Event Hubs] guida sui consumatori dell’evento](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) per ulteriori informazioni. |

## Passaggi successivi

Seguendo questa esercitazione, hai creato un’ [!DNL Event Hubs] connessione sorgente tramite [!DNL Flow Service] API. Puoi utilizzare questo ID connessione sorgente nell’esercitazione successiva per [creare un flusso di dati in streaming utilizzando [!DNL Flow Service] API](../../collect/streaming.md).
