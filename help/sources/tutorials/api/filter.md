---
title: Filtrare I Dati A Livello Di Riga Per Un Source Utilizzando L’API Del Servizio Di Flusso
description: Questo tutorial illustra i passaggi necessari per filtrare i dati a livello di origine utilizzando l’API del servizio Flow
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: 544bb7b5aff437fd49c30ac3d6261f103a609cac
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 5%

---

# Filtrare i dati a livello di riga per un&#39;origine utilizzando l&#39;API [!DNL Flow Service]

>[!AVAILABILITY]
>
>Il supporto per il filtro dei dati a livello di riga è attualmente disponibile solo per le seguenti origini:
>
>* [[!DNL Google BigQuery]](../../connectors/databases/bigquery.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>* [[!DNL Snowflake]](../../connectors/databases/snowflake.md)
>* [[!DNL Marketo Engage] attività standard](../../connectors/adobe-applications/marketo/marketo.md)

Leggi questa guida per i passaggi su come filtrare i dati a livello di riga per un&#39;origine utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): [!DNL Experience Platform] consente l&#39;acquisizione di dati da varie origini e consente di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform].
* [Sandbox](../../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola istanza di [!DNL Platform] in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida in [guida introduttiva alle API di Platform](../../../landing/api-guide.md).

## Filtrare i dati di origine {#filter-source-data}

Di seguito sono descritti i passaggi da eseguire per filtrare i dati a livello di riga per l’origine.

### Recuperare le specifiche di connessione {#retrieve-your-connection-specs}

Il primo passaggio per filtrare i dati a livello di riga per l&#39;origine consiste nel recuperare le specifiche di connessione dell&#39;origine e determinare gli operatori e la lingua supportati dall&#39;origine.

Per recuperare la specifica di connessione di un&#39;origine specifica, effettuare una richiesta di GET all&#39;endpoint `/connectionSpecs` dell&#39;API [!DNL Flow Service] e fornire il nome della proprietà dell&#39;origine come parte dei parametri di query.

**Formato API**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| `{QUERY_PARAMS}` | Parametri di query facoltativi in base ai quali filtrare i risultati. È possibile recuperare la specifica di connessione [!DNL Google BigQuery] applicando la proprietà `name` e specificando `"google-big-query"` nella ricerca. |

+++Richiesta

La richiesta seguente recupera le specifiche di connessione per [!DNL Google BigQuery].

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Risposta

In caso di esito positivo, la risposta restituisce il codice di stato 200 e le specifiche di connessione per [!DNL Google BigQuery], incluse informazioni sul linguaggio di query e sugli operatori logici supportati.

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

+++

#### Operatori di confronto {#comparison-operators}

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

### Specificare le condizioni di filtro per l’acquisizione {#specify-filtering-conditions-for-ingestion}

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

### Visualizzare l’anteprima dei dati {#preview-your-data}

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

+++Richiesta

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Risposta

In caso di esito positivo, la risposta restituisce il contenuto e la struttura dei dati.

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

+++

### Creare una connessione di origine per i dati filtrati

Per creare una connessione di origine e acquisire i dati filtrati, effettuare una richiesta POST all&#39;endpoint `/sourceConnections` e specificare le condizioni di filtro nei parametri del corpo della richiesta.

**Formato API**

```http
POST /sourceConnections
```

+++Richiesta

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

+++

+++Risposta

In caso di esito positivo, la risposta restituisce l&#39;identificatore univoco (`id`) della connessione di origine appena creata.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

+++

## Filtra entità attività per [!DNL Marketo Engage] {#filter-for-marketo}

È possibile utilizzare il filtro a livello di riga per filtrare le entità attività quando si utilizza il [[!DNL Marketo Engage] connettore di origine](../../connectors/adobe-applications/marketo/marketo.md). Al momento, è possibile filtrare solo per entità attività e tipi di attività standard. Le attività personalizzate rimangono disciplinate in [[!DNL Marketo] mappature campi](../../connectors/adobe-applications/mapping/marketo.md).

### [!DNL Marketo] tipi di attività standard {#marketo-standard-activity-types}

La tabella seguente illustra i tipi di attività standard per [!DNL Marketo]. Utilizzare questa tabella come riferimento per i criteri di filtro.

| ID tipo di attività | Nome tipo di attività |
| --- | --- |
| 1 | Visita pagina Web |
| 2 | Modulo da compilare |
| 3 | Fai clic sul collegamento |
| 6 | Invia e-mail |
| 7 | E-mail consegnata |
| 8 | E-mail non recapitata |
| 9 | Annulla iscrizione e-mail |
| 10 | Apri e-mail |
| 11 | Fai clic su E-mail |
| 12 | Nuovo lead |
| 21 | Conversione lead |
| 22 | Modifica punteggio |
| 24 | Aggiungi all&#39;elenco |
| 25 | Rimuovi dall’elenco |
| 27 | E-mail non recapitata temporaneamente |
| 32 | Unisci lead |
| 34 | Aggiungi all’opportunità |
| 35 | Rimuovi dall’opportunità |
| 36 | Aggiorna opportunità |
| 46 | Momento di interesse |
| 101 | Modifica fase ricavi |
| 104 | Modifica stato in progressione |
| 110 | Chiama webhook |
| 113 | Aggiungi allo sviluppo |
| 114 | Cambia traccia sviluppo |
| 115 | Cambia cadenza di sviluppo |

{style="table-layout:auto"}

Segui i passaggi seguenti per filtrare le entità attività standard quando utilizzi il connettore di origine [!DNL Marketo].

### Creare un flusso di dati 2D

Crea un [[!DNL Marketo] flusso di dati](../ui/create/adobe-applications/marketo.md) e salvalo come bozza. Consulta la seguente documentazione per i passaggi dettagliati su come creare un flusso di dati in formato bozza:

* [Salvare un flusso di dati come bozza utilizzando l’interfaccia utente](../ui/draft.md)
* [Salvare un flusso di dati come bozza utilizzando l’API](../api/draft.md)

### Recupera l’ID del flusso di dati

Dopo aver creato un flusso di dati, devi recuperarne l’ID corrispondente.

Nell&#39;interfaccia utente passare al catalogo delle origini e selezionare **[!UICONTROL Flussi dati]** dall&#39;intestazione superiore. Utilizza la colonna di stato per identificare tutti i flussi di dati salvati in modalità bozza, quindi seleziona il nome del flusso di dati. Quindi, utilizza il pannello **[!UICONTROL Proprietà]** a destra per individuare l&#39;ID del flusso di dati.

### Recuperare i dettagli del flusso di dati

Quindi, devi recuperare i dettagli del flusso di dati, in particolare l’ID della connessione di origine associato al flusso di dati. Per recuperare i dettagli del flusso di dati, effettua una richiesta GET all&#39;endpoint `/flows` e fornisci l&#39;ID del flusso di dati come parametro del percorso.

**Formato API**

```http
GET /flows/{FLOW_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{FLOW_ID}` | ID del flusso di dati che desideri recuperare. |

+++Richiesta

La richiesta seguente recupera informazioni sull&#39;ID flusso di dati: `a7e88a01-40f9-4ebf-80b2-0fc838ff82ef`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/a7e88a01-40f9-4ebf-80b2-0fc838ff82ef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Risposta

In caso di esito positivo, la risposta restituisce i dettagli del flusso di dati, incluse le informazioni sulle connessioni di origine e di destinazione corrispondenti. Per pubblicare il flusso di dati, è necessario prendere nota degli ID di connessione di origine e di destinazione, in quanto questi valori sono richiesti in un secondo momento.

```json {line-numbers="true" start-line="1" highlight="23, 26"}
{
    "items": [
        {
            "id": "a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
            "createdAt": 1728592929650,
            "updatedAt": 1728597187444,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "exc_app",
            "updatedClient": "acme",
            "sandboxId": "7f3419ce-53e2-476b-b419-ce53e2376b02",
            "sandboxName": "prod",
            "imsOrgId": "acme@AdobeOrg",
            "name": "Marketo Engage Standard Activities ACME",
            "description": "",
            "flowSpec": {
                "id": "15f8402c-ba66-4626-b54c-9f8e54244d61",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"600290fc-0000-0200-0000-67084cc30000\"",
            "etag": "\"600290fc-0000-0200-0000-67084cc30000\"",
            "sourceConnectionIds": [
                "56f7eb3a-b544-4eaa-b167-ef1711044c7a"
            ],
            "targetConnectionIds": [
                "7e53e6e8-b432-4134-bb29-21fc6e8532e5"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
                        "connectionSpec": {
                            "id": "bf1f4218-73ce-4ff0-b744-48d78ffae2e4",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "0137118b-373a-4c4e-847c-13a0abf73b33",
                            "connectionSpec": {
                                "id": "bf1f4218-73ce-4ff0-b744-48d78ffae2e4",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "7e53e6e8-b432-4134-bb29-21fc6e8532e5",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "isSampleDataflow": false,
                "errorDiagnosticsEnabled": true
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingVersion": 0,
                        "mappingId": "f6447514ef95482889fac1818972e285"
                    }
                }
            ],
            "runs": "/runs?property=flowId==a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
            "lastOperation": {
                "started": 1728592929650,
                "updated": 0,
                "operation": "create"
            },
            "lastRunDetails": {
                "id": "2d7863d5-ca4d-4313-ac52-2603eaf2cdbe",
                "state": "success",
                "startedAtUTC": 1728594713537,
                "completedAtUTC": 1728597183080
            },
            "labels": [],
            "recordTypes": [
                {
                    "type": "experienceevent",
                    "extensions": {}
                }
            ]
        }
    ]
}
```

+++

### Recuperare i dettagli della connessione sorgente

Quindi, utilizzare l&#39;ID connessione di origine e inviare una richiesta di GET all&#39;endpoint `/sourceConnections` per recuperare i dettagli della connessione di origine.

**Formato API**

```http
GET /sourceConnections/{SOURCE_CONNECTION_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | ID della connessione di origine che si desidera recuperare. |

+++Richiesta

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Risposta

In caso di esito positivo, la risposta restituisce i dettagli della connessione sorgente. Prendi nota della versione in quanto questo valore sarà necessario nel passaggio successivo per aggiornare la connessione sorgente.

```json {line-numbers="true" start-line="1" highlight="30"}
{
    "items": [
        {
            "id": "b85b895f-a289-42e9-8fe1-ae448ccc7e53",
            "createdAt": 1729634331185,
            "updatedAt": 1729634331185,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "exc_app",
            "updatedClient": "acme",
            "sandboxId": "7f3419ce-53e2-476b-b419-ce53e2376b02",
            "sandboxName": "prod",
            "imsOrgId": "acme@AdobeOrg",
            "name": "New Source Connection - 2024-10-23T03:28:50+05:30",
            "description": "Source connection created from the workflow",
            "baseConnectionId": "fd9f7455-1e23-4831-9283-7717e20bee40",
            "state": "draft",
            "data": {
                "format": "tabular",
                "schema": null,
                "properties": null
            },
            "connectionSpec": {
                "id": "2d31dfd1-df1a-456b-948f-226e040ba102",
                "version": "1.0"
            },
            "params": {
                "columns": [],
                "tableName": "Activity"
            },
            "version": "\"210068a6-0000-0200-0000-6718201b0000\"",
            "etag": "\"210068a6-0000-0200-0000-6718201b0000\"",
            "inheritedAttributes": {
                "baseConnection": {
                    "id": "fd9f7455-1e23-4831-9283-7717e20bee40",
                    "connectionSpec": {
                        "id": "2d31dfd1-df1a-456b-948f-226e040ba102",
                        "version": "1.0"
                    }
                }
            },
            "lastOperation": {
                "started": 1729634331185,
                "updated": 0,
                "operation": "draft_create"
            }
        }
    ]
}
```

+++

### Aggiornare la connessione di origine con le condizioni di filtro

Ora che disponi dell’ID connessione sorgente e della versione corrispondente, puoi effettuare una richiesta PATCH con le condizioni del filtro che specificano i tipi di attività standard.

Per aggiornare la connessione di origine, effettuare una richiesta PATCH all&#39;endpoint `/sourceConnections` e fornire l&#39;ID della connessione di origine come parametro di query. Inoltre, devi fornire un parametro di intestazione `If-Match`, con la versione corrispondente della connessione sorgente.

>[!TIP]
>
>L&#39;intestazione `If-Match` è obbligatoria quando si effettua una richiesta PATCH. Il valore di questa intestazione è la versione/etag univoca del flusso di dati che desideri aggiornare. Il valore version/etag viene aggiornato a ogni aggiornamento riuscito di un flusso di dati.

**Formato API**

```http
GET /sourceConnections/{SOURCE_CONNECTION_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | ID della connessione di origine che si desidera recuperare. |

+++Richiesta

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'If-Match: {VERSION_HERE}'
  -d '
      {
        "op": "add",
        "path": "/params/filters",
        "value": {
            "type": "PQL",
            "format": "pql/json",
            "value": {
                "nodeType": "fnApply",
                "fnName": "in",
                "params": [
                    {
                        "nodeType": "fieldLookup",
                        "fieldName": "activityType"
                    },
                    {
                        "nodeType": "literal",
                        "value": [
                            "Change Status in Progression",
                            "Fill Out Form"
                        ]
                    }
                ]
            }
        }
    }'
```

+++

+++Risposta

In caso di esito positivo, la risposta restituisce l’ID della connessione di origine e l’etag (versione).

```json
{
    "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
    "etag": "\"210068a6-0000-0200-0000-6718201b0000\""
}
```

+++

### Publish connessione sorgente

Con la connessione di origine aggiornata con le condizioni di filtro, ora puoi passare dallo stato di bozza e pubblicare la connessione di origine. A tale scopo, invia una richiesta POST all&#39;endpoint `/sourceConnections` e fornisci l&#39;ID della bozza della connessione di origine e un&#39;operazione di pubblicazione.

**Formato API**

```http
POST /sourceConnections/{SOURCE_CONNECTION_ID}/action?op=publish
```

| Parametro | Descrizione |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | ID della connessione sorgente che desideri pubblicare. |
| `op` | Operazione che aggiorna lo stato della connessione di origine interrogata. Per pubblicare una bozza di connessione di origine, impostare `op` su `publish`. |

+++Richiesta

La richiesta seguente pubblica una bozza di connessione sorgente.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Risposta

In caso di esito positivo, la risposta restituisce l’ID della connessione di origine e l’etag (versione).

```json
{
    "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
    "etag": "\"9f007f7b-0000-0200-0000-670ef1150000\""
}
```

+++

### Publish connessione di destinazione

Come nel passaggio precedente, per procedere e pubblicare il flusso di dati bozza devi pubblicare anche la connessione di destinazione. Effettuare una richiesta POST all&#39;endpoint `/targetConnections` e fornire l&#39;ID della bozza di connessione di destinazione che si desidera pubblicare, nonché un&#39;operazione di pubblicazione.

**Formato API**

```http
POST /targetConnections/{TARGET_CONNECTION_ID}/action?op=publish
```

| Parametro | Descrizione |
| --- | --- |
| `{TARGET_CONNECTION_ID}` | ID della connessione di destinazione da pubblicare. |
| `op` | Operazione di azione che aggiorna lo stato della connessione di destinazione interrogata. Per pubblicare una bozza di connessione di destinazione, impostare `op` su `publish`. |

+++Richiesta

La richiesta seguente pubblica la connessione di destinazione con ID: `7e53e6e8-b432-4134-bb29-21fc6e8532e5`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/7e53e6e8-b432-4134-bb29-21fc6e8532e5/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Risposta

In caso di esito positivo, la risposta restituisce l’ID e l’e-mail corrispondente per la connessione di destinazione pubblicata.

```json
{
    "id": "7e53e6e8-b432-4134-bb29-21fc6e8532e5",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++


### Publish il flusso di dati

Con le connessioni di origine e di destinazione pubblicate entrambe, ora puoi procedere al passaggio finale e pubblicare il flusso di dati. Per pubblicare il flusso di dati, effettua una richiesta POST all&#39;endpoint `/flows` e fornisci l&#39;ID del flusso di dati e un&#39;operazione di pubblicazione.

**Formato API**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Parametro | Descrizione |
| --- | --- |
| `{FLOW_ID}` | ID del flusso di dati che desideri pubblicare. |
| `op` | Operazione che aggiorna lo stato del flusso di dati sottoposto a query. Per pubblicare un flusso di dati bozza, impostare `op` su `publish`. |

+++Richiesta

La richiesta seguente pubblica il flusso di dati della bozza.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/a7e88a01-40f9-4ebf-80b2-0fc838ff82ef/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Risposta

In caso di esito positivo, la risposta restituisce l’ID e il corrispondente `etag` del flusso di dati.

```json
{
  "id": "a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
  "etag": "\"4b0354b7-0000-0200-0000-6716ce1f0000\""
}
```

+++

Puoi utilizzare l’interfaccia utente di Experience Platform per verificare che il flusso di dati della bozza sia stato pubblicato. Passa alla pagina dei flussi di dati nel catalogo delle origini e fai riferimento al **[!UICONTROL Stato]** del flusso di dati. In caso di esito positivo, ora lo stato deve essere impostato su **Abilitato**.

>[!TIP]
>
>* Un flusso di dati con il filtro abilitato verrà recuperato una sola volta. Qualsiasi modifica apportata nei criteri di filtro (sia essa un&#39;aggiunta o una rimozione) può avere effetto solo sui dati incrementali.
>* Se devi acquisire dati storici per qualsiasi nuovo tipo di attività, ti consigliamo di creare un nuovo flusso di dati e definire i criteri di filtro con i tipi di attività appropriati nella condizione di filtro.
>* Non puoi filtrare i tipi di attività personalizzati.
>* Non è possibile visualizzare in anteprima i dati filtrati.

## Appendice

Questa sezione fornisce ulteriori esempi di payload diversi da filtrare.

### Condizioni singole

È possibile omettere `fnApply` iniziale per gli scenari che richiedono una sola condizione.

+++Seleziona per visualizzare l’esempio

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

+++

### Utilizzo dell&#39;operatore `in`

Per un esempio dell&#39;operatore `in`, vedere il payload di esempio seguente.

+++Seleziona per visualizzare l’esempio

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

+++

### Utilizzo dell&#39;operatore `isNull`

+++Seleziona per visualizzare l’esempio

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

+++

### Utilizzo dell&#39;operatore `NOT`

Per un esempio dell&#39;operatore `NOT`, vedere il payload di esempio seguente.


+++Seleziona per visualizzare l’esempio

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

+++

### Esempio con condizioni nidificate

Per un esempio di condizioni nidificate complesse, consulta il payload di esempio riportato di seguito.

+++Seleziona per visualizzare l’esempio

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

+++