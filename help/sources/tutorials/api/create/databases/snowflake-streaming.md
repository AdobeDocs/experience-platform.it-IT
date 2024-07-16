---
title: Collegare l'account di streaming di Snowflake a Adobe Experience Platform
description: Scopri come collegare Adobe Experience Platform a Streaming di Snowflake utilizzando l’API del servizio Flusso.
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3fc225a4-746c-4a91-aa77-bbeb091ec364
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 5%

---

# Trasmetti i dati [!DNL Snowflake] all&#39;Experience Platform utilizzando l&#39;API [!DNL Flow Service]

>[!IMPORTANT]
>
>* L&#39;origine di streaming [!DNL Snowflake] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, leggere la [Panoramica origini](../../../../home.md#terms-and-conditions).
>* L&#39;origine di streaming [!DNL Snowflake] è disponibile nell&#39;API per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Questo tutorial illustra i passaggi necessari per collegare e inviare dati dall&#39;account [!DNL Snowflake] a Adobe Experience Platform utilizzando l&#39;[[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Per la configurazione dei prerequisiti e informazioni sull&#39;origine di streaming [!DNL Snowflake]. Leggere la [[!DNL Snowflake] panoramica origine streaming](../../../../connectors/databases/snowflake-streaming.md).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base {#create-a-base-connection}

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettuare una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Snowflake] come parte del corpo della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Snowflake]:

>[!TIP]
>
>Il valore `auth.specName` deve essere immesso esattamente come nell&#39;esempio seguente, inclusi gli spazi vuoti.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "Snowflake base connection",
      "auth": {
          "specName": "Basic Authentication for Snowflake",
          "params": {
              "account": "wixnnnd-ui60793.snowflakecomputing.com",
              "database": "ACME_DB",
              "warehouse": "ACME_WH",
              "username": "nikola15",
              "schema": "PUBLIC",
              "password": "xxxx",
              "role": "ACCOUNTADMIN"
          }
      },
      "connectionSpec": {
          "id": "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `auth.params.account` | Nome dell&#39;account di streaming [!DNL Snowflake]. |
| `auth.params.database` | Il nome del database [!DNL Snowflake] da cui verranno estratti i dati. |
| `auth.params.warehouse` | Nome del data warehouse [!DNL Snowflake]. Il data warehouse [!DNL Snowflake] gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni data warehouse è indipendente l’uno dall’altro e deve essere accessibile singolarmente quando si trasferiscono i dati su Platform. |
| `auth.params.username` | Nome utente per l&#39;account di streaming [!DNL Snowflake]. |
| `auth.params.schema` | (Facoltativo) Lo schema di database associato all&#39;account di streaming [!DNL Snowflake]. |
| `auth.params.password` | Password per l&#39;account di streaming [!DNL Snowflake]. |
| `auth.params.role` | (Facoltativo) Ruolo dell&#39;utente per questa connessione [!DNL Snowflake]. Se non specificato, il valore predefinito è `public`. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Snowflake]: `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione di base appena creata e il tag corrispondente.

```json
{
    "id": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Esplora le tabelle di dati {#explore-your-data-tables}

Utilizzare quindi l&#39;ID connessione di base per esplorare e spostarsi tra le tabelle dati dell&#39;origine effettuando una richiesta di GET all&#39;endpoint `/connections/{BASE_CONNECTION_ID}/explore?objectType=root` e fornendo l&#39;ID connessione di base come parametro.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID connessione di base dell&#39;origine di streaming [!DNL Snowflake]. |


**Richiesta**

La richiesta seguente recupera la struttura e il contenuto dell&#39;account di streaming [!DNL Snowflake].

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/1b614dc0-b76e-41e1-b25f-09f4a9d3f111/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce la struttura e il contenuto dei dati dell’origine a livello di radice.

```json
{
    "items": [
        {
            "type": "table",
            "name": "ACME"
        }
    ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `items.type` | Tipo della tabella. |
| `items.names` | Nome della tabella. |

## Creare una connessione sorgente {#create-a-source-connection}

Una connessione di origine crea e gestisce la connessione all’origine esterna da cui vengono acquisiti i dati.

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
      "name": "Snowflake Streaming Source Connection",
      "description": "A source connection for Snowflake Streaming data",
      "baseConnectionId": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
      "connectionSpec": {
          "id": "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
          "version": "1.0"
      },
      "params": {
          "tableName": "ACME",
          "timestampColumn": "dOb",
          "backfill": "true",
          "timezoneValue": "PST"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `baseConnectionId` | ID di connessione di base autenticato per l&#39;origine di streaming [!DNL Snowflake]. Questo ID è stato generato in un passaggio precedente. |
| `connectionSpec.id` | ID della specifica di connessione per l&#39;origine di streaming [!DNL Snowflake]. |
| `params.tableName` | Nome della tabella nel database [!DNL Snowflake] che si desidera portare in Platform. |
| `params.timestampColumn` | Nome della colonna timestamp che verrà utilizzata per recuperare i valori incrementali. |
| `params.backfill` | Flag booleano che determina se i dati vengono recuperati dall’inizio (0 epoca) o dal momento in cui viene avviata l’origine. Per ulteriori informazioni su questo valore, leggere la [[!DNL Snowflake] panoramica origine streaming](../../../../connectors/databases/snowflake-streaming.md). |
| `params.timezoneValue` | Il valore del fuso orario indica l&#39;ora corrente del fuso orario da recuperare durante la query sul database [!DNL Snowflake]. Questo parametro deve essere fornito se la colonna timestamp nella configurazione è impostata su `TIMESTAMP_NTZ`. Se non specificato, per impostazione predefinita `timezoneValue` viene utilizzato il valore UTC. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID della connessione sorgente e l’eTag corrispondente. L’ID della connessione di origine verrà utilizzato in un passaggio successivo per creare un flusso di dati.

```json
{
    "id": "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Creare un flusso di dati

Per creare un flusso di dati per inviare dati dall&#39;account tour [!DNL Snowflake] a Platform, è necessario effettuare una richiesta POST all&#39;endpoint `/flows` fornendo i seguenti valori:

>[!TIP]
>
>Segui i collegamenti riportati di seguito per guide dettagliate su come recuperare i seguenti ID.

* [ID connessione Source](#create-a-source-connection)
* [ID connessione di destinazione](../../collect/database-nosql.md#create-a-target-connection)
* [ID specifica di flusso](../../collect/database-nosql.md#retrieve-dataflow-specifications)
* [ID di mappatura](../../collect/database-nosql.md#create-a-mapping)

**Formato API**

```http
POST /flows
```

**Richiesta**

La richiesta seguente crea un flusso di dati in streaming per il tuo account [!DNL Snowflake].

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake Streaming Dataflow",
      "description": "A dataflow for Snowflake streaming data",
      "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
      ],
      "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
      ],
      "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
      },
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
            "mappingVersion": 0
          }
        }
      ]
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `sourceConnectionIds` | ID della connessione di origine per l&#39;origine di streaming [!DNL Snowflake]. |
| `targetConnectionIds` | ID della connessione di destinazione per l&#39;origine di streaming [!DNL Snowflake]. |
| `flowSpec.id` | ID della specifica di flusso per creare un flusso di dati per un&#39;origine di flusso [!DNL Snowflake]. Questo ID della specifica di flusso consente di creare un flusso di dati in streaming con le trasformazioni di mappatura. L&#39;ID è corretto ed è: `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. |
| `transformations.params.mappingId` | ID di mappatura per il flusso di dati. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID di flusso e l’eTag corrispondente.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai creato un flusso di dati in streaming per i tuoi dati [!DNL Snowflake] utilizzando l&#39;API [!DNL Flow Service]. Per ulteriori informazioni sulle origini di Adobe Experience Platform, consulta la seguente documentazione:

* [Panoramica sulle origini](../../../../home.md)
* [Monitorare il flusso di dati utilizzando le API](../../monitor.md)
