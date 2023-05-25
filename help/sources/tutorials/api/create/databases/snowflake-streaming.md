---
title: Collegare l'account di streaming di Snowflake a Adobe Experience Platform
description: Scopri come collegare Adobe Experience Platform a Streaming di Snowflake utilizzando l’API del servizio Flusso.
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
source-git-commit: 825da75c8f98863b408477a4895cd9146d121d3d
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 3%

---

# Flusso [!DNL Snowflake] dati di cui effettuare l&#39;Experience Platform utilizzando [!DNL Flow Service] API

>[!IMPORTANT]
>
>* Il [!DNL Snowflake] l&#39;origine di streaming è in versione beta. Leggi le [Panoramica sulle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.
>* Il [!DNL Snowflake] la sorgente di streaming è disponibile nel catalogo delle sorgenti per i clienti che hanno acquistato Real-Time CDP Ultimate.


Questo tutorial illustra i passaggi necessari per la connessione e lo streaming dei dati dal [!DNL Snowflake] account a Adobe Experience Platform utilizzando [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Sandbox](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

Per l’impostazione dei prerequisiti e per le informazioni su [!DNL Snowflake] origine di streaming. Leggi le [[!DNL Snowflake] panoramica origine streaming](../../../../connectors/databases/snowflake-streaming.md).

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../../../landing/api-guide.md).

## Creare una connessione di base {#create-a-base-connection}

Una connessione di base mantiene le informazioni tra l’origine e Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID di connessione di base, effettua una richiesta POST al `/connections` endpoint durante la fornitura del [!DNL Snowflake] credenziali di autenticazione come parte del corpo della richiesta.

**Formato API**

```https
POST /connections
```

**Richiesta**

La richiesta seguente crea una connessione di base per [!DNL Snowflake]:

>[!TIP]
>
>Il `auth.specName` il valore deve essere immesso esattamente come nell’esempio seguente, compresi gli spazi vuoti.

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
| `auth.params.account` | Il nome del tuo [!DNL Snowflake] account di streaming. |
| `auth.params.database` | Il nome del tuo [!DNL Snowflake] database da cui verranno estratti i dati. |
| `auth.params.warehouse` | Il nome del tuo [!DNL Snowflake] data warehouse. Il [!DNL Snowflake] warehouse gestisce il processo di esecuzione delle query per l&#39;applicazione. Ogni data warehouse è indipendente l’uno dall’altro e deve essere accessibile singolarmente quando si trasferiscono i dati su Platform. |
| `auth.params.username` | Il nome utente per il [!DNL Snowflake] account di streaming. |
| `auth.params.schema` | (Facoltativo) Lo schema di database associato al tuo [!DNL Snowflake] account di streaming. |
| `auth.params.password` | La password per [!DNL Snowflake] account di streaming. |
| `auth.params.role` | (Facoltativo) Il ruolo dell’utente per questo [!DNL Snowflake] connessione. Se non specificato, il valore predefinito è `public`. |
| `connectionSpec.id` | Il [!DNL Snowflake] ID specifica di connessione: `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione di base appena creata e il tag corrispondente.

```json
{
    "id": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Esplora le tabelle di dati {#explore-your-data-tables}

Utilizzare quindi l&#39;ID connessione di base per esplorare e spostarsi tra le tabelle dati dell&#39;origine effettuando una richiesta di GET al `/connections/{BASE_CONNECTION_ID}/explore?objectType=root` mentre fornisci l’ID connessione di base come parametro.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | L’ID della connessione di base [!DNL Snowflake] origine di streaming. |


**Richiesta**

La richiesta seguente recupera la struttura e il contenuto del [!DNL Snowflake] account di streaming.

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
          "backfill": "true"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `baseConnectionId` | ID della connessione di base autenticata per [!DNL Snowflake] origine di streaming. Questo ID è stato generato in un passaggio precedente. |
| `connectionSpec.id` | ID della specifica di connessione per [!DNL Snowflake] origine di streaming. |
| `params.tableName` | Nome della tabella nel [!DNL Snowflake] che desideri portare su Platform. |
| `params.timestampColumn` | Nome della colonna timestamp che verrà utilizzata per recuperare i valori incrementali. |
| `params.backfill` | Flag booleano che determina se i dati vengono recuperati dall’inizio (0 epoca) o dal momento in cui viene avviata l’origine. Per ulteriori informazioni su questo valore, leggere [[!DNL Snowflake] panoramica origine streaming](../../../../connectors/databases/snowflake-streaming.md). |

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID della connessione sorgente e l’eTag corrispondente. L’ID della connessione di origine verrà utilizzato in un passaggio successivo per creare un flusso di dati.

```json
{
    "id": "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## Creare un flusso di dati

Per creare un flusso di dati per inviare dati dalla presentazione [!DNL Snowflake] a Platform, è necessario effettuare una richiesta POST al `/flows` endpoint, fornendo i seguenti valori:

>[!TIP]
>
>Segui i collegamenti riportati di seguito per guide dettagliate su come recuperare i seguenti ID.

* [ID connessione sorgente](#create-a-source-connection)
* [ID connessione di destinazione](../../collect/database-nosql.md#create-a-target-connection)
* [ID specifica di flusso](../../collect/database-nosql.md#retrieve-dataflow-specifications)
* [ID di mappatura](../../collect/database-nosql.md#create-a-mapping)

**Formato API**

```http
POST /flows
```

**Richiesta**

La seguente richiesta crea un flusso di dati in streaming per il tuo [!DNL Snowflake] account.

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
| `sourceConnectionIds` | ID della connessione sorgente per [!DNL Snowflake] origine di streaming. |
| `targetConnectionIds` | ID della connessione di destinazione per [!DNL Snowflake] origine di streaming. |
| `flowSpec.id` | L’ID della specifica di flusso per creare un flusso di dati per un [!DNL Snowflake] origine di streaming. Questo ID della specifica di flusso consente di creare un flusso di dati in streaming con le trasformazioni di mappatura. Questo ID è fisso ed è: `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. |
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

Seguendo questa esercitazione, hai creato un flusso di dati in streaming per [!DNL Snowflake] dati utilizzando [!DNL Flow Service] API. Per ulteriori informazioni sulle origini di Adobe Experience Platform, consulta la seguente documentazione:

* [Panoramica sulle origini](../../../../home.md)
* [Monitorare il flusso di dati utilizzando le API](../../monitor.md)