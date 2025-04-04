---
title: Creare una connessione di base Microsoft Dynamics utilizzando l’API del servizio Flow
description: Scopri come connettere Experience Platform a un account Microsoft Dynamics utilizzando l’API del servizio Flusso.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 5%

---

# Connetti [!DNL Microsoft Dynamics] ad Experience Platform utilizzando l&#39;API [!DNL Flow Service]

Leggi questa guida per scoprire come collegare l&#39;origine [!DNL Microsoft Dynamics] a Adobe Experience Platform utilizzando [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Experience Platform

Per informazioni su come effettuare correttamente chiamate alle API di Experience Platform, consulta la guida introduttiva [alle API di Experience Platform](../../../../../landing/api-guide.md).

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettere correttamente Experience Platform a un account Dynamics utilizzando l&#39;API [!DNL Flow Service].

### Raccogli le credenziali richieste

Affinché [!DNL Flow Service] possa connettersi a [!DNL Dynamics], è necessario fornire i valori per le proprietà di connessione seguenti:

>[!BEGINTABS]

>[!TAB Autenticazione di base]

| Credenziali | Descrizione |
| --- | --- |
| `serviceUri` | L&#39;URL del servizio dell&#39;istanza [!DNL Dynamics]. |
| `username` | Il nome utente per l&#39;account utente [!DNL Dynamics]. |
| `password` | Password per l&#39;account [!DNL Dynamics]. |

>[!TAB Autenticazione Service-principal e chiave]

| Credenziali | Descrizione |
| --- | --- |
| `servicePrincipalId` | ID client dell&#39;account [!DNL Dynamics]. Questo ID è necessario quando si utilizza l’entità servizio e l’autenticazione basata su chiave. |
| `servicePrincipalKey` | Chiave segreta dell&#39;entità servizio. Questa credenziale è necessaria quando si utilizza l&#39;entità servizio e l&#39;autenticazione basata su chiave. |

>[!ENDTABS]

Per ulteriori informazioni, consulta [questo [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Creare una connessione di base

>[!TIP]
>
>Una volta creata, non è possibile modificare il tipo di autenticazione di una connessione di base [!DNL Dynamics]. Per modificare il tipo di autenticazione, è necessario creare una nuova connessione di base.

Una connessione di base mantiene le informazioni tra l’origine e Experience Platform, incluse le credenziali di autenticazione dell’origine, lo stato corrente della connessione e l’ID univoco della connessione di base. L’ID della connessione di base consente di esplorare e navigare tra i file dall’interno dell’origine e identificare gli elementi specifici che desideri acquisire, comprese le informazioni relative ai tipi di dati e ai formati.

Per creare un ID connessione di base, eseguire una richiesta POST all&#39;endpoint `/connections` fornendo le credenziali di autenticazione [!DNL Dynamics] come parte dei parametri della richiesta.

**Formato API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticazione di base]

Per creare una connessione di base [!DNL Dynamics] utilizzando l&#39;autenticazione di base, eseguire una richiesta POST all&#39;API [!DNL Flow Service] fornendo i valori per `serviceUri`, `username` e `password` della connessione.

**Richiesta**

La richiesta seguente crea una connessione di base per un&#39;origine [!DNL Dynamics] utilizzando l&#39;autenticazione di base.

+++Seleziona per visualizzare l’esempio di richiesta

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics connection",
      "description": "Dynamics connection using basic auth",
      "auth": {
          "specName": "Basic Authentication for Dynamics-Online",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.serviceUri` | L&#39;URI del servizio associato all&#39;istanza [!DNL Dynamics]. |
| `auth.params.username` | Il nome utente associato al tuo account [!DNL Dynamics]. |
| `auth.params.password` | La password associata al tuo account [!DNL Dynamics]. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Dynamics]: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione di base appena creata, incluso il relativo identificatore univoco (`id`).

+++Seleziona per visualizzare l’esempio di risposta

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!TAB Autenticazione basata su chiave entità servizio]

Per creare una connessione di base [!DNL Dynamics] utilizzando l&#39;autenticazione basata sulla chiave dell&#39;entità servizio, eseguire una richiesta POST all&#39;API [!DNL Flow Service] fornendo i valori per `serviceUri`, `servicePrincipalId` e `servicePrincipalKey` della connessione.

**Richiesta**

La richiesta seguente crea una connessione di base per un&#39;origine [!DNL Dynamics] utilizzando l&#39;autenticazione basata su chiave dell&#39;entità servizio di base.

+++Seleziona per visualizzare l’esempio di richiesta

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics connection",
      "description": "Dynamics connection using key-based authentication",
      "auth": {
          "specName": "Service Principal Key Based Authentication",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
              "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `auth.params.serviceUri` | L&#39;URI del servizio associato all&#39;istanza [!DNL Dynamics]. |
| `auth.params.servicePrincipalId` | ID client dell&#39;account [!DNL Dynamics]. Questo ID è necessario quando si utilizza l’entità servizio e l’autenticazione basata su chiave. |
| `auth.params.servicePrincipalKey` | Chiave segreta dell&#39;entità servizio. Questa credenziale è necessaria quando si utilizza l&#39;entità servizio e l&#39;autenticazione basata su chiave. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Dynamics]: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce la connessione appena creata, incluso il relativo identificatore univoco (`id`).

+++Seleziona per visualizzare l’esempio di risposta

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!ENDTABS]

## Esplora le tabelle di dati

Per esplorare le tabelle dati [!DNL Dynamics], effettua una richiesta GET all&#39;endpoint `/connections/{BASE_CONNECTION_ID}/explore` e fornisci l&#39;ID connessione di base come parte dei parametri della query.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parametri della query | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID della connessione di base. Usa questo ID per esplorare il contenuto e la struttura dell’origine. |

**Richiesta**

La richiesta seguente recupera l&#39;elenco di tabelle e viste disponibili per un&#39;origine [!DNL Dynamics] con ID connessione di base: `dd668808-25da-493f-8782-f3433b976d1e`.

+++Seleziona per visualizzare l’esempio di richiesta

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce la directory delle tabelle e delle visualizzazioni [!DNL Dynamics] a livello principale.

+++Seleziona per visualizzare l’esempio di risposta

```json
[
    {
        "type": "table",
        "name": "systemuserlicenses",
        "path": "systemuserlicenses",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Process Dependency",
        "path": "workflowdependency",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "view",
        "name": "accountView1",
        "path": "accountView1",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "view",
        "name": "Inactive_ACC_custom",
        "path": "Inactive_ACC_custom",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

+++

### Utilizza la chiave primaria per ottimizzare l’esplorazione dei dati

>[!NOTE]
>
>È possibile utilizzare attributi non di ricerca solo quando si utilizza l’approccio di chiave primaria per l’ottimizzazione.

È possibile ottimizzare le query di esplorazione fornendo `primaryKey` come parte dei parametri di query. Specificare la chiave primaria della tabella [!DNL Dynamics] quando si include `primaryKey` come parametro di query.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?preview=true&object={OBJECT}&objectType={OBJECT_TYPE}&previewCount=10&primaryKey={PRIMARY_KEY}
```

| Parametri della query | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID della connessione di base. Usa questo ID per esplorare il contenuto e la struttura dell’origine. |
| `preview` | Valore booleano che abilita l’anteprima dei dati. |
| `{OBJECT}` | L&#39;oggetto [!DNL Dynamics] che si desidera esplorare. |
| `{OBJECT_TYPE}` | Tipo dell&#39;oggetto. |
| `previewCount` | Restrizione che limita l’anteprima restituita a un determinato numero di record. |
| `{PRIMARY_KEY}` | Chiave primaria della tabella che si sta recuperando per l&#39;anteprima. |

**Richiesta**

+++Seleziona per visualizzare l’esempio di richiesta

```shell
curl -X GET \
  'https://platform-stage.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?preview=true&object=lead&objectType=table&previewCount=10&primaryKey=leadid' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

## Controllare la struttura di una tabella

Per verificare la struttura di una tabella specifica, eseguire una richiesta GET a `/connections/{BASE_CONNECTION_ID}/explore` e specificare il percorso della tabella specifica come parametro di query.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={TABLE_PATH}&objectType=table
```

| Parametro query | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID della connessione di base. Usa questo ID per esplorare il contenuto e la struttura dell’origine. |
| `{TABLE_PATH}` | Percorso della tabella specifica che si desidera esplorare. |

**Richiesta**

La richiesta seguente recupera la struttura e il contenuto di una tabella [!DNL Dynamics] con percorso `workflowdependency`.

+++Seleziona per visualizzare l’esempio di richiesta

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=workflowdependency&objectType=table' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce il contenuto del percorso `workflowdependency`.

+++Seleziona per visualizzare l’esempio di risposta

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "first_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "last_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "email",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            }
        ]
    }
}
```

+++

## Controllare la struttura di una vista

In [!DNL Dynamics] una visualizzazione si riferisce alle colonne da visualizzare, alla larghezza di ogni colonna, al sistema predefinito in cui viene ordinato un elenco di record e ai filtri predefiniti applicati per limitare i record da visualizzare nell&#39;elenco.

Per verificare la struttura di una visualizzazione, effettuare una richiesta GET a `/connections/{BASE_CONNECTION_ID}/explore` e specificare il percorso di visualizzazione nei parametri di query. È inoltre necessario specificare `objectType` come `view`.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={VIEW_PATH}&objectType=view
```

| Parametro query | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID della connessione di base. Usa questo ID per esplorare il contenuto e la struttura dell’origine. |
| `{VIEW_PATH}` | Percorso della visualizzazione che si desidera controllare. |

**Richiesta**

La richiesta seguente recupera `accountView1`.

+++Seleziona per visualizzare l’esempio di richiesta

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=accountView1&objectType=view' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce la struttura di `accountView1`.

+++Seleziona per visualizzare l’esempio di risposta

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "name",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "fetchxml",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "querytype",
                "type": "integer",
                "meta": {
                    "originalType": "int"
                },
                "xdm": {
                    "type": "integer",
                    "minimum": -2147483648,
                    "maximum": 2147483647
                }
            },
            {
                "name": "userqueryid",
                "type": "string",
                "meta": {
                    "originalType": "guid"
                },
                "xdm": {
                    "type": "string"
                }
            }
        ]
    }
}
```

+++

## Anteprima vista tipo entità

Per visualizzare in anteprima il contenuto di una visualizzazione, effettuare una richiesta GET a `/connections/{BASE_CONNECTION_ID}/explore` e includere il percorso di visualizzazione e `preview=true` nei parametri di query.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={VIEW_PATH}&preview=true&objectType=view
```

| Parametro query | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID della connessione di base. Usa questo ID per esplorare il contenuto e la struttura dell’origine. |
| `{VIEW_PATH}` | Percorso della visualizzazione che si desidera controllare. |


**Richiesta**

La richiesta seguente visualizza l&#39;anteprima del contenuto di `accountView1`.

+++Seleziona per visualizzare l’esempio di richiesta

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=accountView1&preview=true&objectType=view' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Risposta**

Una risposta corretta restituisce il contenuto di `accountView1`.

+++Seleziona per visualizzare l’esempio di risposta

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "emailaddress1",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "contactid",
                "type": "string",
                "meta": {
                    "originalType": "guid"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "fullname",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "contactid": "396e19de-0852-ec11-8c62-00224808a1df",
            "fullname": "Tim Barr",
            "emailaddress1": "barrtim@googlemedia.com"
        }
    ]
}
```

+++

## Creare una connessione sorgente per acquisire la vista

Per creare una connessione di origine e acquisire una visualizzazione, effettuare una richiesta POST all&#39;endpoint `/sourceConnections`, fornire il nome della tabella e specificare `entityType` come `view` nel corpo della richiesta.

**Formato API**

```http
POST /sourceConnections
```

**Richiesta**

La richiesta seguente crea una connessione di origine [!DNL Dynamics] e acquisisce le visualizzazioni.

+++Seleziona per visualizzare l’esempio di richiesta

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics Source Connection",
      "description": "Dynamics Source Connection",
      "baseConnectionId": "dd668808-25da-493f-8782-f3433b976d1e",
      "data": {
          "format": "tabular",
          "schema": null,
          "properties": null
      },
      "params": {
          "tableName": "Contacts with name TIM",
          "entityType": "view"
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID della connessione sorgente appena generato e il tag corrispondente.

+++Seleziona per visualizzare l’esempio di risposta

```json
{
    "id": "e566bab3-1b58-428c-b751-86b8cc79a3b4",
    "etag": "\"82009592-0000-0200-0000-678121030000\""
}
```

+++

### Utilizza la chiave primaria per ottimizzare il flusso di dati

È inoltre possibile ottimizzare il flusso di dati [!DNL Dynamics] specificando la chiave primaria come parte dei parametri del corpo della richiesta.

**Formato API**

```http
POST /sourceConnections
```

**Richiesta**

La richiesta seguente crea una connessione di origine [!DNL Dynamics] specificando la chiave primaria come `contactid`.

+++Seleziona per visualizzare l’esempio di richiesta

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics Source Connection",
      "description": "Dynamics Source Connection",
      "baseConnectionId": "dd668808-25da-493f-8782-f3433b976d1e",
      "data": {
          "format": "tabular"
      },
      "params": {
          "tableName": "contact",
          "primaryKey": "contactid"
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `baseConnectionId` | ID della connessione di base. |
| `data.format` | Il formato dei dati. |
| `params.tableName` | Nome della tabella in [!DNL Dynamics]. |
| `params.primaryKey` | Chiave primaria della tabella che ottimizzerà le query. |
| `connectionSpec.id` | ID della specifica di connessione corrispondente all&#39;origine [!DNL Dynamics]. |

+++

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID della connessione sorgente appena generato e il tag corrispondente.

+++Seleziona per visualizzare l’esempio di risposta

```json
{
    "id": "e566bab3-1b58-428c-b751-86b8cc79a3b4",
    "etag": "\"82009592-0000-0200-0000-678121030000\""
}
```

+++


## Passaggi successivi

Seguendo questa esercitazione, è stata creata una connessione di base [!DNL Microsoft Dynamics] utilizzando l&#39;API [!DNL Flow Service]. Puoi utilizzare questo ID connessione di base nelle seguenti esercitazioni:

* [Esplora la struttura e il contenuto delle tabelle dati utilizzando l&#39;API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crea un flusso di dati per portare i dati CRM in Experience Platform utilizzando l&#39;API  [!DNL Flow Service] ](../../collect/crm.md)
