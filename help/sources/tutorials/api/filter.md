---
keywords: Experience Platform;home;argomenti popolari;servizio di flusso;API di servizio di flusso;origini;origini
title: Filtrare I Dati A Livello Di Riga Per Una Sorgente Utilizzando L’API Del Servizio Di Flusso
description: Questa esercitazione descrive i passaggi su come filtrare i dati a livello di origine utilizzando l’API del servizio di flusso
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: 963fc5e31e1728a8a1a7e94bc0cc47d010347325
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 3%

---

# Filtrare i dati a livello di riga per un’origine utilizzando [!DNL Flow Service] API

>[!IMPORTANT]
>
>Il supporto per il filtraggio dei dati a livello di riga è attualmente disponibile solo per le seguenti origini:
>
>* [BigQuery Google](../../connectors/databases/bigquery.md)
>* [Salesforce](../../connectors/crm/salesforce.md)
>* [Snowflake](../../connectors/databases/snowflake.md)


Questa esercitazione fornisce passaggi su come filtrare i dati a livello di riga per un’origine utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): [!DNL Experience Platform] consente l’acquisizione di dati da varie sorgenti, fornendo al contempo la possibilità di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi.
* [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../landing/api-guide.md).

## Filtrare i dati sorgente

Di seguito sono descritti i passaggi da eseguire per filtrare i dati a livello di riga per l’origine.

### Cercare le specifiche di connessione

Prima di poter utilizzare l’API per filtrare i dati a livello di riga per un’origine, è necessario recuperare i dettagli delle specifiche di connessione dell’origine al fine di determinare gli operatori e la lingua supportati da una specifica origine.

Per recuperare le specifiche di connessione di una determinata origine, invia una richiesta di GET al `/connectionSpecs` punto finale [!DNL Flow Service] mentre fornisci il nome della proprietà dell’origine come parte dei parametri di query.

**Formato API**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| `{QUERY_PARAMS}` | Parametri di query facoltativi per filtrare i risultati. È possibile recuperare [!DNL Google BigQuery] specifica di connessione applicando la `name` proprietà e specifica `"google-big-query"` nella tua ricerca. |

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

Una risposta corretta restituisce le specifiche di connessione per [!DNL Google BigQuery], incluse informazioni sul linguaggio di query e gli operatori logici supportati.

>[!NOTE]
>
>La risposta API seguente viene troncata per brevità.

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
| `attributes.filterAtSource.enabled` | Determina se l&#39;origine interrogata supporta il filtro per i dati a livello di riga. |
| `attributes.filterAtSource.queryLanguage` | Determina la lingua della query supportata dall&#39;origine interrogata. |
| `attributes.filterAtSource.logicalOperators` | Determina gli operatori logici che è possibile utilizzare per filtrare i dati a livello di riga per l’origine. |
| `attributes.filterAtSource.comparisonOperators` | Determina gli operatori di confronto utilizzabili per filtrare i dati a livello di riga per l’origine. Vedi la tabella seguente per ulteriori informazioni sugli operatori di confronto. |
| `attributes.filterAtSource.columnNameEscapeChar` | Determina il carattere da utilizzare per l&#39;escape delle colonne. |
| `attributes.filterAtSource.valueEscapeChar` | Determina il modo in cui i valori verranno circondati durante la scrittura di una query SQL. |

{style="table-layout:auto"}

#### Operatori di confronto

| Operatore | Descrizione |
| --- | --- |
| `==` | Filtra in base al fatto che la proprietà sia uguale al valore fornito. |
| `!=` | Filtra in base al fatto che la proprietà non sia uguale al valore fornito. |
| `<` | Filtra in base al fatto che la proprietà sia minore del valore specificato. |
| `>` | Filtra per determinare se la proprietà è maggiore del valore specificato. |
| `<=` | Filtra per specificare se la proprietà è minore o uguale al valore specificato. |
| `>=` | Filtra per specificare se la proprietà è maggiore o uguale al valore specificato. |
| `like` | Filtri utilizzati in una `WHERE` per cercare un pattern specificato. |
| `in` | Filtra per stabilire se la proprietà si trova in un intervallo specificato. |

{style="table-layout:auto"}

### Specificare le condizioni di filtro per l’acquisizione

Dopo aver identificato gli operatori logici e il linguaggio di query supportati dalla sorgente, puoi utilizzare il linguaggio PQL (Profile Query Language) per specificare le condizioni di filtro che desideri applicare ai dati di origine.

Nell’esempio seguente, le condizioni vengono applicate solo a selezionare dati che equivalgono ai valori forniti per i tipi di nodo elencati come parametri.

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

### Anteprima dei dati

Puoi visualizzare in anteprima i dati effettuando una richiesta di GET al `/explore` punto finale [!DNL Flow Service] API fornendo `filters` come parte dei parametri di query e specificando le condizioni di input PQL in [!DNL Base64].

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| Parametro | Descrizione |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID connessione di base della sorgente. |
| `{TABLE_PATH}` | Proprietà del percorso della tabella che si desidera esaminare. |
| `{FILTERS}` | Le tue condizioni di filtro PQL codificate in [!DNL Base64]. |

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

Una richiesta corretta restituisce la risposta seguente.

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

### Creazione di una connessione di origine per i dati filtrati

Per creare una connessione di origine e acquisire dati filtrati, effettuare una richiesta di POST al `/sourceConnections` l&#39;endpoint fornisce le condizioni di filtro come parte dei parametri del corpo.

**Formato API**

```http
POST /sourceConnections
```

**Richiesta**

La richiesta seguente crea una connessione di origine da cui acquisire i dati `test1.fasTestTable` dove `city` = `DDN`.

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

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della nuova connessione sorgente creata.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## Appendice

Questa sezione fornisce ulteriori esempi di payload diversi per il filtraggio.

### Condizioni particolari

È possibile omettere la `fnApply` per gli scenari che richiedono una sola condizione.

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

### Utilizzo della `in` operatore

Per un esempio dell’operatore , consulta il payload di esempio riportato di seguito `in`.

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

### Utilizzo della `isNull` operatore

Per un esempio dell’operatore , consulta il payload di esempio riportato di seguito `isNull`.

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

### Utilizzo della `NOT` operatore

Per un esempio dell’operatore , consulta il payload di esempio riportato di seguito `NOT`.

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
