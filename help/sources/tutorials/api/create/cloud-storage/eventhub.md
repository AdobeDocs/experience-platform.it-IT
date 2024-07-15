---
title: Creare una connessione Source Azure Event Hubs utilizzando l’API del servizio Flusso
description: Scopri come connettere Adobe Experience Platform a un account Azure Event Hubs utilizzando l’API del servizio Flusso.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: 1256f0c76b29edad4808fc4be1d61399bfbae8fa
workflow-type: tm+mt
source-wordcount: '1492'
ht-degree: 2%

---

# Creare una connessione di origine [!DNL Azure Event Hubs] utilizzando l&#39;API [!DNL Flow Service]

>[!IMPORTANT]
>
>L&#39;origine [!DNL Azure Event Hubs] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Leggi questo tutorial per scoprire come connettere [!DNL Azure Event Hubs] (di seguito &quot;[!DNL Event Hubs]&quot;) all&#39;Experience Platform, utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
- [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettere correttamente [!DNL Event Hubs] a Platform utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Affinché [!DNL Flow Service] possa connettersi al tuo account [!DNL Event Hubs], devi fornire i valori per le seguenti proprietà di connessione:

>[!BEGINTABS]

>[!TAB Autenticazione standard]

| Credenziali | Descrizione |
| --- | --- |
| `sasKeyName` | Il nome della regola di autorizzazione, noto anche come nome della chiave SAS. |
| `sasKey` | Chiave primaria dello spazio dei nomi [!DNL Event Hubs]. I `sasPolicy` a cui corrisponde `sasKey` devono avere `manage` diritti configurati affinché l&#39;elenco [!DNL Event Hubs] possa essere popolato. |
| `namespace` | Spazio dei nomi di [!DNL Event Hub] a cui si sta effettuando l&#39;accesso. Uno spazio dei nomi [!DNL Event Hub] fornisce un contenitore di ambito univoco, in cui è possibile creare uno o più [!DNL Event Hubs]. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione [!DNL Event Hubs]: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

>[!TAB Autenticazione SAS]

| Credenziali | Descrizione |
| --- | --- |
| `sasKeyName` | Il nome della regola di autorizzazione, noto anche come nome della chiave SAS. |
| `sasKey` | Chiave primaria dello spazio dei nomi [!DNL Event Hubs]. I `sasPolicy` a cui corrisponde `sasKey` devono avere `manage` diritti configurati affinché l&#39;elenco [!DNL Event Hubs] possa essere popolato. |
| `namespace` | Spazio dei nomi di [!DNL Event Hub] a cui si sta effettuando l&#39;accesso. Uno spazio dei nomi [!DNL Event Hub] fornisce un contenitore di ambito univoco, in cui è possibile creare uno o più [!DNL Event Hubs]. |
| `eventHubName` | Inserisci il nome [!DNL Azure Event Hub]. Per ulteriori informazioni sui nomi di [!DNL Event Hub], leggere la [documentazione di Microsoft](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub). |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione [!DNL Event Hubs]: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Per ulteriori informazioni sull&#39;autenticazione delle firme di accesso condiviso per [!DNL Event Hubs], leggere la [[!DNL Azure] guida sull&#39;utilizzo di SAS](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

>[!TAB Hub eventi Azure Active Directory Auth]

| Credenziali | Descrizione |
| --- | --- |
| `tenantId` | ID tenant a cui desideri richiedere l’autorizzazione. L’ID tenant può essere formattato come GUID o come nome descrittivo. **Nota**: nell&#39;interfaccia [!DNL Microsoft Azure] l&#39;ID tenant viene indicato come &quot;ID directory&quot;. |
| `clientId` | L&#39;ID applicazione assegnato alla tua app. Puoi recuperare questo ID dal portale [!DNL Microsoft Entra ID] in cui hai registrato [!DNL Azure Active Directory]. |
| `clientSecretValue` | Segreto client utilizzato insieme all’ID client per autenticare l’app. Puoi recuperare il segreto client dal portale [!DNL Microsoft Entra ID] in cui hai registrato [!DNL Azure Active Directory]. |
| `namespace` | Spazio dei nomi di [!DNL Event Hub] a cui si sta effettuando l&#39;accesso. Uno spazio dei nomi [!DNL Event Hub] fornisce un contenitore di ambito univoco, in cui è possibile creare uno o più [!DNL Event Hubs]. |

Per ulteriori informazioni su [!DNL Azure Active Directory], leggere la [Guida di Azure sull&#39;utilizzo di Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!TAB Autenticazione Azure Active Directory con ambito hub eventi]

| Credenziali | Descrizione |
| --- | --- |
| `tenantId` | ID tenant a cui desideri richiedere l’autorizzazione. L’ID tenant può essere formattato come GUID o come nome descrittivo. **Nota**: nell&#39;interfaccia [!DNL Microsoft Azure] l&#39;ID tenant viene indicato come &quot;ID directory&quot;. |
| `clientId` | L&#39;ID applicazione assegnato alla tua app. Puoi recuperare questo ID dal portale [!DNL Microsoft Entra ID] in cui hai registrato [!DNL Azure Active Directory]. |
| `clientSecretValue` | Segreto client utilizzato insieme all’ID client per autenticare l’app. Puoi recuperare il segreto client dal portale [!DNL Microsoft Entra ID] in cui hai registrato [!DNL Azure Active Directory]. |
| `namespace` | Spazio dei nomi di [!DNL Event Hub] a cui si sta effettuando l&#39;accesso. Uno spazio dei nomi [!DNL Event Hub] fornisce un contenitore di ambito univoco, in cui è possibile creare uno o più [!DNL Event Hubs]. |
| `eventHubName` | Inserisci il nome [!DNL Azure Event Hub]. Per ulteriori informazioni sui nomi di [!DNL Event Hub], leggere la [documentazione di Microsoft](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub). |

>[!ENDTABS]

Per ulteriori informazioni su questi valori, fare riferimento al [documento Hub eventi](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base

>[!TIP]
>
>Una volta creata, non è possibile modificare il tipo di autenticazione di una connessione di base [!DNL Event Hubs]. Per modificare il tipo di autenticazione, è necessario creare una nuova connessione di base.

Il primo passaggio nella creazione di una connessione di origine consiste nell&#39;autenticare l&#39;origine [!DNL Event Hubs] e generare un ID connessione di base. Un ID di connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare elementi specifici da acquisire, incluse informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Event Hubs] come parte dei parametri della richiesta.

**Formato API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticazione standard]

Per creare un account utilizzando l&#39;autenticazione standard, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo i valori per `sasKeyName`, `sasKey` e `namespace`.

+++Richiesta

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
| `auth.params.namespace` | Spazio dei nomi di [!DNL Event Hubs] a cui si sta effettuando l&#39;accesso. |
| `connectionSpec.id` | L&#39;ID della specifica di connessione [!DNL Event Hubs] è: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID connessione è richiesto nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB Autenticazione SAS]

Per creare un account utilizzando l&#39;autenticazione SAS, eseguire una richiesta POST all&#39;endpoint `/connections` fornendo i valori per `sasKeyName`, `sasKey`,`namespace` e `eventHubName`.

+++Richiesta

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
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME} 
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
| `auth.params.namespace` | Spazio dei nomi di [!DNL Event Hubs] a cui si sta effettuando l&#39;accesso. |
| `params.eventHubName` | Nome dell&#39;origine [!DNL Event Hubs]. |
| `connectionSpec.id` | L&#39;ID della specifica di connessione [!DNL Event Hubs] è: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID connessione è richiesto nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB Hub eventi Azure Active Directory Auth]

Per creare un account utilizzando Azure Active Directory Auth, eseguire una richiesta POST all&#39;endpoint `/connections` fornendo i valori per `tenantId`, `clientId`,`clientSecretValue` e `namespace`.

+++Richiesta

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
          "specName": "Event Hub Azure Active Directory Auth",
          "params": {
              "tenantId": "{TENANT_ID}",
              "clientId": "{CLIENT_ID}",
              "clientSecretValue": "{CLIENT_SECRET_VALUE}",
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
| `auth.params.tenantId` | ID tenant dell’applicazione. **Nota**: nell&#39;interfaccia [!DNL Microsoft Azure] l&#39;ID tenant viene indicato come &quot;ID directory&quot;. |
| `auth.params.clientId` | L’ID cliente dell’organizzazione. |
| `auth.params.clientSecretValue` | Il valore segreto client dell’organizzazione. |
| `auth.params.namespace` | Spazio dei nomi di [!DNL Event Hubs] a cui si sta effettuando l&#39;accesso. |
| `connectionSpec.id` | L&#39;ID della specifica di connessione [!DNL Event Hubs] è: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID connessione è richiesto nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB Autenticazione Azure Active Directory con ambito hub eventi]

Per creare un account utilizzando Azure Active Directory Auth, eseguire una richiesta POST all&#39;endpoint `/connections` fornendo i valori per `tenantId`, `clientId`, `clientSecretValue`, `namespace` e `eventHubName`.

+++Richiesta

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
          "specName": "Event Hub Scoped Azure Active Directory Auth",
          "params": {
              "tenantId": "{TENANT_ID}",
              "clientId": "{CLIENT_ID}",
              "clientSecretValue": "{CLIENT_SECRET_VALUE}",
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME}" 
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
| `auth.params.tenantId` | ID tenant dell’applicazione. **Nota**: nell&#39;interfaccia [!DNL Microsoft Azure] l&#39;ID tenant viene indicato come &quot;ID directory&quot;. |
| `auth.params.clientId` | L’ID cliente dell’organizzazione. |
| `auth.params.clientSecretValue` | Il valore segreto client dell’organizzazione. |
| `auth.params.namespace` | Spazio dei nomi di [!DNL Event Hubs] a cui si sta effettuando l&#39;accesso. |
| `auth.params.eventHubName` | Nome dell&#39;origine [!DNL Event Hubs]. |
| `connectionSpec.id` | L&#39;ID della specifica di connessione [!DNL Event Hubs] è: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Risposta

In caso di esito positivo, la risposta restituisce i dettagli della connessione di base appena creata, incluso il relativo identificatore univoco (`id`). Questo ID connessione è richiesto nel passaggio successivo per creare una connessione sorgente.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!ENDTABS]

## Creare una connessione sorgente

>[!TIP]
>
>Un gruppo di consumer [!DNL Event Hubs] può essere utilizzato solo per un singolo flusso alla volta.

Una connessione di origine crea e gestisce la connessione all’origine esterna da cui vengono acquisiti i dati. Una connessione di origine è costituita da informazioni quali origine dati, formato dati e un ID di connessione di origine necessari per creare un flusso di dati. Un&#39;istanza della connessione di origine è specifica di un tenant e di un&#39;organizzazione.

Per creare una connessione di origine, effettuare una richiesta POST all&#39;endpoint `/sourceConnections` dell&#39;API [!DNL Flow Service].

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
          "eventHubName": "{EVENT_HUB_NAME}",
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
| `baseConnectionId` | ID di connessione dell&#39;origine [!DNL Event Hubs] generato nel passaggio precedente. |
| `connectionSpec.id` | ID della specifica di connessione fissa per [!DNL Event Hubs]. ID: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | Formato dei dati [!DNL Event Hubs] che si desidera acquisire. Attualmente, l&#39;unico formato di dati supportato è `json`. |
| `params.eventHubName` | Nome dell&#39;origine [!DNL Event Hubs]. |
| `params.dataType` | Questo parametro definisce il tipo di dati che viene acquisito. I tipi di dati supportati sono: `raw` e `xdm`. |
| `params.reset` | Questo parametro definisce la modalità di lettura dei dati. Utilizza `latest` per iniziare a leggere dai dati più recenti e `earliest` per iniziare a leggere dai primi dati disponibili nel flusso. Questo parametro è facoltativo e, se non specificato, viene impostato automaticamente su `earliest`. |
| `params.consumerGroup` | Meccanismo di pubblicazione o sottoscrizione da utilizzare per [!DNL Event Hubs]. Questo parametro è facoltativo e, se non specificato, viene impostato automaticamente su `$Default`. Per ulteriori informazioni, consulta questa [[!DNL Event Hubs] guida sugli eventi consumer](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers). **Nota**: un gruppo di consumer [!DNL Event Hubs] può essere utilizzato solo per un singolo flusso in un determinato momento. |

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione di origine [!DNL Event Hubs] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di origine nella prossima esercitazione per [creare un flusso di dati in streaming utilizzando l&#39; [!DNL Flow Service] API](../../collect/streaming.md).
