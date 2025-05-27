---
title: Supporto di collegamenti privati nelle origini
description: Scopri come creare e utilizzare collegamenti privati per origini Adobe Experience Platform
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: 4c91ffc60a2537fcc76ce935bf3b163984fdc5e4
workflow-type: tm+mt
source-wordcount: '1326'
ht-degree: 6%

---

# Supporto di collegamenti privati nelle origini

>[!AVAILABILITY]
>
>Questa funzione è a disponibilità limitata ed è attualmente supportata solo dalle seguenti sorgenti:
>
>* [[!DNL Azure Blob]](../../connectors/cloud-storage/blob.md)
>* [[!DNL Azure Data Lake Gen2]](../../connectors/cloud-storage/adls-gen2.md)
>* [[!DNL Azure File Storage]](../../connectors/cloud-storage/azure-file-storage.md)
>* [[!DNL Snowflake]](../../connectors/databases/snowflake.md)

Leggi questa guida per scoprire come stabilire una connessione dell’endpoint privato alle origini basate su Azure tramite un collegamento privato e consentire un meccanismo di trasferimento più sicuro per i dati.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../landing/api-guide.md).

## Creare un endpoint privato {#create-private-endpoint}

Per creare un endpoint privato, effettuare una richiesta POST a `/privateEndpoints`.

**Formato API**

```http
POST /privateEndpoints
```

**Richiesta**

La richiesta seguente crea un endpoint privato:

+++Seleziona per visualizzare l’esempio di richiesta

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Private Endpoint",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [],
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
    }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome dell’endpoint privato. |
| `subscriptionId` | ID associato all&#39;abbonamento [!DNL Azure]. Per ulteriori informazioni, leggere la guida di [!DNL Azure] in [recupero degli ID sottoscrizione e tenant da  [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id). |
| `resourceGroupName` | Il nome del gruppo di risorse in [!DNL Azure]. Un gruppo di risorse contiene risorse correlate per una soluzione [!DNL Azure]. Per ulteriori informazioni, leggere la guida di [!DNL Azure] in [gestione dei gruppi di risorse](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal). |
| `resourceName` | Nome della risorsa. In [!DNL Azure] una risorsa fa riferimento a istanze quali macchine virtuali, applicazioni Web e database. Per ulteriori informazioni, leggere la guida di [!DNL Azure] in [informazioni sul gestore delle risorse [!DNL Azure] ](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview). |
| `fqdns` | I nomi di dominio completi per l’origine. Questa proprietà è necessaria solo quando si utilizza l&#39;origine [!DNL Snowflake]. |
| `connectionSpec.id` | ID della specifica di connessione dell&#39;origine in uso. |
| `connectionSpec.version` | Versione dell&#39;ID della specifica di connessione in uso. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce quanto segue:

+++Seleziona per visualizzare l’esempio di risposta

```json
{
  "id": "2c7f6574-299a-4832-aec5-886e875872e2",
  "name": "ACME Private Endpoint",
  "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
  "resourceGroupName": "acme-sources-experience-platform",
  "resourceName": "acmeexperienceplatform",
  "fqdns": [],
  "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
  },
  "state": "Pending"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | ID dell’endpoint privato appena creato. |
| `name` | Nome dell’endpoint privato. |
| `subscriptionId` | ID associato all&#39;abbonamento [!DNL Azure]. Per ulteriori informazioni, leggere la guida di [!DNL Azure] in [recupero degli ID sottoscrizione e tenant da  [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id). |
| `resourceGroupName` | Il nome del gruppo di risorse in [!DNL Azure]. Un gruppo di risorse contiene risorse correlate per una soluzione [!DNL Azure]. Per ulteriori informazioni, leggere la guida di [!DNL Azure] in [gestione dei gruppi di risorse](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal). |
| `resourceName` | Nome della risorsa. In [!DNL Azure] una risorsa fa riferimento a istanze quali macchine virtuali, applicazioni Web e database. Per ulteriori informazioni, leggere la guida di [!DNL Azure] in [informazioni sul gestore delle risorse [!DNL Azure] ](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview). |
| `fqdns` | I nomi di dominio completi per l’origine. Questa proprietà è necessaria solo quando si utilizza l&#39;origine [!DNL Snowflake]. |
| `connectionSpec.id` | ID della specifica di connessione dell&#39;origine in uso. |
| `connectionSpec.version` | Versione dell&#39;ID della specifica di connessione in uso. |
| `state` | Lo stato corrente dell’endpoint privato. Gli stati validi includono: <ul><li>`Pending`</li><li>`Failed`</li><li>`Approved`</li><li>`Rejected`</li></ul> |

+++

## Recuperare un elenco di endpoint privati {#retrieve-private-endpoints}

Per recuperare un elenco di endpoint privati da una data sandbox nell&#39;organizzazione, effettuare una richiesta GET a `/privateEndpoints`.

**Formato API**

```http
GET /privateEndpoints
```

**Richiesta**

La richiesta seguente recupera un elenco di tutti gli endpoint privati presenti nell’organizzazione.

+++Seleziona per visualizzare l’esempio di richiesta

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di endpoint privati dell’organizzazione.

+++Seleziona per visualizzare l’esempio di risposta

```json
{
  "items": [
       {
      "id": "ac9eb695-0d1a-42d4-bc45-0842aeaa1eff",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinking",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    },
          {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
        "version": "1.0"
      }
    } 
  ]
}
```

+++

## Recuperare un elenco di endpoint privati per una determinata origine {#retrieve-private-endpoints-by-source}

Per recuperare un elenco di endpoint privati corrispondenti a un&#39;origine specifica, effettuare una richiesta GET all&#39;endpoint `/privateEndpoints` e fornire `connectionSpec.id` dell&#39;origine.

**Formato API**

```http
GET /privateEndpoints?property=connectionSpec.id=={CONNECTION_SPEC_ID}
```

| Parametri query | Descrizione |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | ID della specifica di connessione dell’origine per la quale si desidera cercare endpoint privati. |

**Richiesta**

La richiesta seguente recupera un elenco di tutti gli endpoint privati corrispondenti all&#39;origine con ID specifica di connessione: `4c10e202-c428-4796-9208-5f1f5732b1cf`.

+++Seleziona per visualizzare l’esempio di richiesta

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints?property=connectionSpec.id==4c10e202-c428-4796-9208-5f1f5732b1cf' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di tutti gli endpoint privati corrispondenti all&#39;origine con ID della specifica di connessione: `4c10e202-c428-4796-9208-5f1f5732b1cf`.

+++Seleziona per visualizzare l’esempio di risposta

```json
{
  "items": [
       {
      "id": "ac9eb695-0d1a-42d4-bc45-0842aeaa1eff",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinkhg",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    },
    {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    } 
  ]
}
```

+++

## Recuperare un endpoint privato {#retrieve-specific-private-endpoint}

Per recuperare un endpoint privato specifico, effettuare una richiesta GET a `/privateEndpoints` e fornire l&#39;ID dell&#39;endpoint privato che si desidera recuperare.

**Formato API**

```http
GET /privateEndpoints/{PRIVATE_ENDPOINT_ID}
```

| Parametri query | Descrizione |
| --- | --- |
| `{PRIVATE_ENDPOINT_ID}` | ID dell’endpoint privato da recuperare. |

**Richiesta**

La richiesta seguente recupera l&#39;endpoint privato con ID:`2c5699b0-b9b6-486f-8877-ee5e21fe9a9d`.

+++Seleziona per visualizzare l’esempio di richiesta

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/2c5699b0-b9b6-486f-8877-ee5e21fe9a9d' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;endpoint privato con ID `2c5699b0-b9b6-486f-8877-ee5e21fe9a9d`

+++Seleziona per visualizzare l’esempio di risposta

```json
{
  "items": [
       {
      "id": "2c5699b0-b9b6-486f-8877-ee5e21fe9a9d",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinkhg",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    }
  ]
}
```

+++

## Risolvere un endpoint privato {#resolve-private-endpoint}

**Formato API**

```http
GET /privateEndpoints?op=autoResolve
```

**Richiesta**

+++Seleziona per visualizzare l’esempio di richiesta

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints?op=autoResolve' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "usePrivateLink": true,
              "connectionString": "{CONNECTION_STRING}"
          }
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

+++

**Risposta**

+++Seleziona per visualizzare l’esempio di risposta

```json
{
  "items": [
        {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      } 
    }
  ]
}
```

+++

## Abilita authoring interattivo {#enable-interactive-authoring}

L’authoring interattivo viene utilizzato per funzionalità quali l’esplorazione di una connessione o di un account e la visualizzazione in anteprima dei dati. Per abilitare l&#39;authoring interattivo, effettuare una richiesta POST a `/privateEndpoints/interactiveAuthoring` e specificare `enable` come operatore nei parametri di query.

**Formato API**

```http
POST /privateEndpoints/interactiveAuthoring?op=enable
```

| Parametri query | Descrizione |
| --- | --- |
| `op` | Operazione che si desidera eseguire. Per abilitare la creazione interattiva, impostare il valore `op` su `enable`. |

**Richiesta**

La richiesta seguente abilita l’authoring interattivo per l’endpoint privato e imposta il TTL su 60 minuti.

+++Seleziona per visualizzare l’esempio di richiesta

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/interactiveAuthoring?op=enable' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "autoTerminationMinutes": 60
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `autoTerminationMinutes` | Il TTL (time-to-live) di authoring interattivo in minuti. L’authoring interattivo viene utilizzato per funzionalità quali l’esplorazione di una connessione o di un account e la visualizzazione in anteprima dei dati. Puoi impostare un TTL massimo di 120 minuti. Il valore TTL predefinito è 60 minuti. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 (Accettato).

## Recuperare lo stato di authoring interattivo {#retrieve-interactive-authoring-status}

Per visualizzare lo stato corrente dell&#39;authoring interattivo per l&#39;endpoint privato, effettuare una richiesta GET a `/privateEndpoints/interactiveAuthoring`.

**Formato API**

```http
GET /privateEndpoints/interactiveAuthoring
```

**Richiesta**

La richiesta seguente recupera lo stato dell’authoring interattivo:

+++Seleziona per visualizzare l’esempio di richiesta

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/interactiveAuthoring' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Risposta**

+++Seleziona per visualizzare l’esempio di risposta

```json
{
    "status": "Disabled"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `status` | Lo stato dell’authoring interattivo. I valori validi includono: `disabled`, `enabling`, `enabled`. |

+++

## Elimina endpoint privato {#delete-private-endpoint}

Per eliminare l&#39;endpoint privato, effettuare una richiesta DELETE a `/privateEndpoints` e fornire l&#39;ID dell&#39;endpoint che si desidera eliminare.

**Formato API**

```http
DELETE /privateEndpoints/{PRIVATE_ENDPOINT_ID}
```

| Parametri query | Descrizione |
| --- | --- |
| `{PRIVATE_ENDPOINT_ID}` | ID dell’endpoint privato da eliminare. |

**Richiesta**

La richiesta seguente elimina l&#39;endpoint privato con ID: `02a74b31-a566-4a86-9cea-309b101a7f24`.

+++Seleziona per visualizzare l’esempio di richiesta

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/02a74b31-a566-4a86-9cea-309b101a7f24' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 (Completato). Puoi verificare l&#39;eliminazione effettuando una richiesta GET e a `/privateEndpoints` e fornendo l&#39;ID eliminato come parametro di query.

## Servizio di flusso {#flow-service}

Leggi le sezioni seguenti per informazioni su come utilizzare endpoint privati insieme all&#39;[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

### Creare una connessione con un endpoint privato {#create-base-connection}

Per creare una connessione con un endpoint privato in Experience Platform, effettuare una richiesta POST all&#39;endpoint `/connections` dell&#39;API [!DNL Flow Service].

**Formato API**

```http
POST /connections/
```

**Richiesta**

La richiesta seguente crea una connessione di base autenticata per [!DNL Snowflake], utilizzando anche un endpoint privato.

+++Seleziona per visualizzare l’esempio di richiesta

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "A base connection for a Snowflake source that uses a private link.",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "{CONNECTION_STRING}",
              "usePrivateLink" : true
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome della connessione di base. |
| `description` | (Facoltativo) Una descrizione che fornisce informazioni aggiuntive sulla connessione. |
| `auth.specName` | Autenticazione utilizzata per connettere l’origine ad Experience Platform. |
| `auth.params.connectionString` | Stringa di connessione [!DNL Snowflake]. Per ulteriori informazioni, leggere la [[!DNL Snowflake] guida all&#39;autenticazione API](../api/create/databases/snowflake.md). |
| `auth.params.usePrivateLink` | Valore booleano che determina se si utilizza o meno un endpoint privato. Impostare questo valore su `true` se si utilizza un endpoint privato. |
| `connectionSpec.id` | ID della specifica di connessione di [!DNL Snowflake]. |
| `connectionSpec.version` | Versione dell&#39;ID della specifica di connessione [!DNL Snowflake]. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID e l’eTag della connessione di base appena generati.

+++Seleziona per visualizzare l’esempio di risposta

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

+++

### Recuperare le connessioni associate a un determinato endpoint privato {#retrieve-connections-by-endpoint}

Per recuperare le connessioni associate a un particolare endpoint privato, effettuare una richiesta GET all&#39;endpoint `/connections` e fornire l&#39;ID dell&#39;endpoint privato come parametro di query.

**Formato API**

```http
GET /connections?property=auth.params.privateEndpointId=={PRIVATE_ENDPOINT_ID}
```

| Parametri query | Descrizione |
| --- | --- |
| {PRIVATE_ENDPOINT_ID} | ID dell’endpoint privato associato alle connessioni che desideri recuperare. |

**Richiesta**

La richiesta seguente recupera le connessioni esistenti associate all&#39;endpoint privato con ID: `02a74b31-a566-4a86-9cea-309b101a7f24`.

+++Seleziona per visualizzare l’esempio di richiesta

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections?property=auth.params.privateEndpointId==02a74b31-a566-4a86-9cea-309b101a7f24' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di connessioni associate all’endpoint privato sottoposto a query.

+++Seleziona per visualizzare l’esempio di risposta

```json
{
  "items": [
    {
      "id": "42a27b1f-8e3f-48ce-8c29-7e474b29a015",
      "createdAt": 1729154379292,
      "updatedAt": 1729154382031,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme-e2e",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "etag": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    },
    {
      "id": "6350311a-664c-4b08-aad4-4065781aac81",
      "createdAt": 1718199941102,
      "updatedAt": 1718199945147,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme demo",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "etag": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    }
  ],
  "_links": {
     
  }
}
```

+++

### Recuperare le connessioni associate a qualsiasi endpoint privato {#retrieve-connections}

Per recuperare le connessioni associate a qualsiasi endpoint privato, effettuare una richiesta GET all&#39;endpoint `/connections` e fornire `property=auth.params.usePrivateLink==true` come parametro di query.

**Formato API**

```http
GET /connections?property=auth.params.usePrivateLink==true
```

**Richiesta**

La richiesta seguente recupera tutte le connessioni dell’organizzazione che utilizzano endpoint privati.

+++Seleziona per visualizzare l’esempio di richiesta

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections?property=auth.params.usePrivateLink==true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce tutte le connessioni associate a endpoint privati.

+++Seleziona per visualizzare l’esempio di risposta

```json
{
  "items": [
    {
      "id": "42a27b1f-8e3f-48ce-8c29-7e474b29a015",
      "createdAt": 1729154379292,
      "updatedAt": 1729154382031,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme-e2e",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "etag": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    },
    {
      "id": "6350311a-664c-4b08-aad4-4065781aac81",
      "createdAt": 1718199941102,
      "updatedAt": 1718199945147,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme demo",
      "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true
        }
      },
      "version": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "etag": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    }
  ],
  "_links": {
     
  }
}
```

+++