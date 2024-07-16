---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;API servizio di flusso;sorgenti;Sorgenti
title: Filtrare I Dati A Livello Di Riga Per Un Source Utilizzando L’API Del Servizio Di Flusso
description: Questo tutorial illustra i passaggi necessari per filtrare i dati a livello di origine utilizzando l’API del servizio Flow
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: b0e2fc4767fb6fbc90bcdd3350b3add965988f8f
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 2%

---

# Filtrare i dati a livello di riga per un&#39;origine utilizzando l&#39;API [!DNL Flow Service]

>[!IMPORTANT]
>
>Il supporto per il filtro dei dati a livello di riga è attualmente disponibile solo per le seguenti origini:
>
>* [BigQuery Google](../../connectors/databases/bigquery.md)
>* [Microsoft Dynamics](../../connectors/crm/ms-dynamics.md)
>* [Salesforce](../../connectors/crm/salesforce.md)
>* [Snowflake](../../connectors/databases/snowflake.md)

Questo tutorial descrive come filtrare i dati a livello di riga per un&#39;origine utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../landing/api-guide.md).

## Filtrare i dati di origine

Di seguito sono descritti i passaggi da eseguire per filtrare i dati a livello di riga per l’origine.

### Cerca specifiche di connessione

Prima di poter utilizzare l’API per filtrare i dati a livello di riga per un’origine, è necessario innanzitutto recuperare i dettagli della specifica di connessione dell’origine per determinare gli operatori e la lingua supportati da un’origine specifica.

Per recuperare la specifica di connessione di una determinata origine, effettuare una richiesta di GET all&#39;endpoint `/connectionSpecs` dell&#39;API [!DNL Flow Service] fornendo il nome della proprietà dell&#39;origine come parte dei parametri di query.

**Formato API**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| `{QUERY_PARAMS}` | Parametri di query facoltativi in base ai quali filtrare i risultati. È possibile recuperare la specifica di connessione [!DNL Google BigQuery] applicando la proprietà `name` e specificando `"google-big-query"` nella ricerca. |

**Richiesta**

La richiesta seguente recupera le specifiche di connessione per [!DNL Google BigQuery].

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce le specifiche di connessione per [!DNL Google BigQuery], incluse informazioni sul linguaggio di query e sugli operatori logici supportati.

>[!NOTE]
>
>Per brevità, la risposta API riportata di seguito è troncata.

```json
"attributes": {
  "filterAtSource": {
    "enabled": true,
    "queryLanguage": "SQL",
    "logicalOperators": [
      "and",
      "or",
      "not"
    ],
    "comparisonOperators": [
      "=",
      "!=",
      "<",
      "<=",
      ">",
      ">=",
      "like",
      "in"
    ],
    "columnNameEscapeChar": "`",
    "valueEscapeChar": "'"
  }
```

| Proprietà | Descrizione |
| --- | --- |
| `attributes.filterAtSource.enabled` | Determina se l&#39;origine della query supporta il filtro per i dati a livello di riga. |
| `attributes.filterAtSource.queryLanguage` | Determina il linguaggio di query supportato dall&#39;origine della query. |
| `attributes.filterAtSource.logicalOperators` | Determina gli operatori logici che è possibile utilizzare per filtrare i dati a livello di riga per l&#39;origine. |
| `attributes.filterAtSource.comparisonOperators` | Determina gli operatori di confronto utilizzabili per filtrare i dati a livello di riga per l&#39;origine. Per ulteriori informazioni sugli operatori di confronto, consulta la tabella seguente. |
| `attributes.filterAtSource.columnNameEscapeChar` | Determina il carattere da utilizzare per l&#39;escape delle colonne. |
| `attributes.filterAtSource.valueEscapeChar` | Determina il modo in cui i valori verranno racchiusi durante la scrittura di una query SQL. |

{style="table-layout:auto"}

#### Operatori di confronto

| Operatore | Descrizione |
| --- | --- |
| `==` | Filtra in base al fatto che la proprietà sia uguale al valore specificato. |
| `!=` | Filtra in base al fatto che la proprietà non sia uguale al valore specificato. |
| `<` | Filtra in base al fatto che la proprietà sia minore del valore specificato. |
| `>` | Filtra in base al fatto che la proprietà sia maggiore del valore specificato. |
| `<=` | Filtra in base al fatto che la proprietà sia minore o uguale al valore specificato. |
| `>=` | Filtra in base al fatto che la proprietà sia maggiore o uguale al valore specificato. |
| `like` | I filtri vengono utilizzati in una clausola `WHERE` per cercare un modello specificato. |
| `in` | Filtra in base all’intervallo specificato per la proprietà. |

{style="table-layout:auto"}

### Specificare le condizioni di filtro per l’acquisizione

Dopo aver identificato gli operatori logici e il linguaggio di query supportati dall&#39;origine, è possibile utilizzare Profile Query Language (PQL) per specificare le condizioni di filtro da applicare ai dati di origine.

Nell’esempio seguente, le condizioni vengono applicate solo ai dati selezionati che corrispondono ai valori forniti per i tipi di nodo elencati come parametri.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "=",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "city"
      },
      {
        "nodeType": "literal",
        "value": "DDN"
      }
    ]
  }
}
```

### Visualizzare l’anteprima dei dati

È possibile visualizzare l&#39;anteprima dei dati effettuando una richiesta di GET all&#39;endpoint `/explore` dell&#39;API [!DNL Flow Service] fornendo `filters` come parte dei parametri di query e specificando le condizioni di input di PQL in [!DNL Base64].

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID della connessione di base dell&#39;origine. |
| `{TABLE_PATH}` | La proprietà path della tabella che si desidera controllare. |
| `{FILTERS}` | Le condizioni di filtro di PQL sono codificate in [!DNL Base64]. |

**Richiesta**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la richiesta restituisce la seguente risposta.

```json
{
  "format": "flat",
  "schema": {
    "columns": [
      {
        "name": "FIRSTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "LASTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "CITY",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "AGE",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "HEIGHT",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "ISEMPLOYED",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "POSTG",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "LATITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "LONGITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "JOINEDDATE",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDAT",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDATTS",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  },
 "data": [
    {
        "CITY": "MZN",
        "LASTNAME": "Jain",
        "JOINEDDATE": "2022-06-22T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-06-22T17:19:33",
        "FIRSTNAME": "Shivam",
        "POSTG": true,
        "HEIGHT": "169",
        "CREATEDATTS": "2022-06-22T17:19:33",
        "ISEMPLOYED": true,
        "LATITUDE": 2000.89,
        "AGE": "25"
    },
    {
        "CITY": "MUM",
        "LASTNAME": "Kreet",
        "JOINEDDATE": "2022-09-07T00:00:00",
        "LONGITUDE": 10500.01,
        "CREATEDAT": "2022-09-07T17:19:33",
        "FIRSTNAME": "Rakul",
        "POSTG": true,
        "HEIGHT": "155",
        "CREATEDATTS": "2022-09-07T17:19:33",
        "ISEMPLOYED": false,
        "LATITUDE": 2500.89,
        "AGE": "42"
    },
    {
        "CITY": "MAN",
        "LASTNAME": "Lee",
        "JOINEDDATE": "2022-09-14T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-09-14T05:02:33",
        "FIRSTNAME": "Denzel",
        "POSTG": true,
        "HEIGHT": "185",
        "CREATEDATTS": "2022-09-14T05:02:33",
        "ISEMPLOYED": true,
        "LATITUDE": 123.89,
        "AGE": "16"
    }
  ]
}
```

### Creare una connessione di origine per i dati filtrati

Per creare una connessione di origine e acquisire i dati filtrati, effettuare una richiesta POST all&#39;endpoint `/sourceConnections` fornendo le condizioni di filtro come parte dei parametri del corpo.

**Formato API**

```http
POST /sourceConnections
```

**Richiesta**

La richiesta seguente crea una connessione di origine per acquisire i dati da `test1.fasTestTable` dove `city` = `DDN`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "BigQuery Source Connection",
      "description": "Source Connection for Filter test",
      "baseConnectionId": "89d1459e-3cd0-4069-acb3-68f240db4eeb",
      "data": {
        "format": "tabular"
      },
      "params": {
        "tableName": "test1.fasTestTable",
        "filters": {
          "type": "PQL",
          "format": "pql/json",
          "value": {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "DDN"
              }
            ]
          }
        }
      },
      "connectionSpec": {
        "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
        "version": "1.0"
      }
    }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;identificatore univoco (`id`) della connessione di origine appena creata.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## Appendice

Questa sezione fornisce ulteriori esempi di payload diversi da filtrare.

### Condizioni singole

È possibile omettere `fnApply` iniziale per gli scenari che richiedono una sola condizione.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "like",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "firstname"
      },
      {
        "nodeType": "literal",
        "value": "%s"
      }
    ]
  }
}
```

### Utilizzo dell&#39;operatore `in`

Per un esempio dell&#39;operatore `in`, vedere il payload di esempio seguente.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "in",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "firstname"
          },
          {
            "nodeType": "literal",
            "value": [
              "Ramen",
              "John"
            ]
          }
        ]
      }
    ]
  }
}
```

### Utilizzo dell&#39;operatore `isNull`

Per un esempio dell&#39;operatore `isNull`, vedere il payload di esempio seguente.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "isNull",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "complaint_type"
      }
    ]
  }
}
```

### Utilizzo dell&#39;operatore `NOT`

Per un esempio dell&#39;operatore `NOT`, vedere il payload di esempio seguente.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "NOT",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "isNull",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "complaint_type"
          }
        ]
      }
    ]
  }
}
```

### Esempio con condizioni nidificate

Per un esempio di condizioni nidificate complesse, consulta il payload di esempio riportato di seguito.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": ">=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 20
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "<=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 30
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "or",
        "params": [
          {
            "nodeType": "fnApply",
            "fnName": "!=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "PUD"
              }
            ]
          },
          {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "joinedDate"
              },
              {
                "nodeType": "literal",
                "value": "2020-04-22"
              }
            ]
          }
        ]
      }
    ]
  }
}
```
