---
title: Creare un flusso di dati per acquisire dati da un sistema CRM in Experience Platform
description: Scopri come utilizzare l’API del servizio Flusso per creare un flusso di dati e acquisire i dati di origine in Experience Platform.
exl-id: b07dd640-bce6-4699-9d2b-b7096746934a
source-git-commit: b4f8d44c3ce9507ff158cf051b7a4b524b293c64
workflow-type: tm+mt
source-wordcount: '2112'
ht-degree: 2%

---

# Creare un flusso di dati per acquisire dati da un sistema CRM in Experience Platform

Leggi questa guida per scoprire come creare un flusso di dati e acquisire dati in Adobe Experience Platform utilizzando [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Acquisizione batch](../../../../ingestion/batch-ingestion/overview.md): scopri come caricare in modo rapido ed efficiente grandi volumi di dati in batch.
* [Catalog Service](../../../../catalog/datasets/overview.md): organizza e tieni traccia dei set di dati in Experience Platform.
* [Preparazione dati](../../../../data-prep/home.md): trasforma e mappa i dati in arrivo in modo che corrispondano ai requisiti dello schema.
* [Flussi dati](../../../../dataflows/home.md): imposta e gestisci le pipeline che spostano i dati dalle origini alle destinazioni.
* [Schemi Experience Data Model (XDM)](../../../../xdm/home.md): struttura i dati utilizzando schemi XDM in modo che siano pronti per l&#39;utilizzo in Experience Platform.
* [Sandbox](../../../../sandboxes/home.md): verifica e sviluppo sicuri in ambienti isolati senza influire sui dati di produzione.
* [Origini](../../../home.md): scopri come collegare le tue origini dati esterne ad Experience Platform.

### Utilizzare le API di Experience Platform

Per informazioni su come effettuare correttamente chiamate alle API di Experience Platform, consulta la guida [guida introduttiva alle API di Experience Platform](../../../../landing/api-guide.md).

### Crea connessione di base {#base}

Per creare un flusso di dati per l’origine, è necessario un account di origine completamente autenticato e il relativo ID di connessione di base corrispondente. Se non disponi di questo ID, visita il [catalogo origini](../../../home.md) per trovare un elenco di origini per le quali puoi creare una connessione di base.

### Creare uno schema XDM di destinazione {#target-schema}

Uno schema Experience Data Model (XDM) fornisce un modo standardizzato per organizzare e descrivere i dati sull’esperienza del cliente in Experience Platform. Per acquisire i dati di origine in Experience Platform, devi innanzitutto creare uno schema XDM di destinazione che definisca la struttura e i tipi di dati da acquisire. Questo schema funge da blueprint per il set di dati di Experience Platform in cui risiederanno i dati acquisiti.

È possibile creare uno schema XDM di destinazione eseguendo una richiesta POST all&#39;API [Schema Registry](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Per i passaggi dettagliati su come creare uno schema XDM di destinazione, leggi le seguenti guide:

* [Crea uno schema utilizzando l&#39;API](../../../../xdm/api/schemas.md).
* [Creare uno schema utilizzando l&#39;interfaccia utente](../../../../xdm/tutorials/create-schema-ui.md).

Una volta creato, lo schema XDM di destinazione `$id` sarà necessario in seguito per il set di dati di destinazione e la mappatura.

### Creare un set di dati di destinazione {#target-dataset}

Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere strutturato come una tabella con colonne (schema) e righe (campi). I dati acquisiti correttamente in Experience Platform vengono memorizzati nel data lake come set di dati. Durante questo passaggio, puoi creare un nuovo set di dati o utilizzarne uno esistente.

È possibile creare un set di dati di destinazione effettuando una richiesta POST all&#39;API [Catalog Service](https://developer.adobe.com/experience-platform-apis/references/catalog/), fornendo al tempo stesso l&#39;ID dello schema di destinazione all&#39;interno del payload. Per i passaggi dettagliati su come creare un set di dati di destinazione, consulta la guida su [creazione di un set di dati utilizzando l&#39;API](../../../../catalog/api/create-dataset.md).

>[!TIP]
>
>Se desideri acquisire i dati in Real-Time Customer Profile, devi assicurarti che sia gli schemi XDM di destinazione che il set di dati di destinazione siano abilitati per il profilo.

+++Seleziona per visualizzare l’esempio

**Formato API**

```HTTP
POST /dataSets
```

**Richiesta**

L’esempio seguente mostra come creare un set di dati di destinazione abilitato per l’acquisizione di Real-Time Customer Profile. In questa richiesta, la proprietà `unifiedProfile` è impostata su `true` (nell&#39;oggetto `tags`), che indica ad Experience Platform di includere il set di dati nel profilo cliente in tempo reale.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Target Dataset",
    "schemaRef": {
      "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
      "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "tags": {
      "unifiedProfile": [
        "enabled: true"
      ]
    }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Un nome descrittivo per il set di dati di destinazione. Utilizza un nome chiaro e univoco per semplificare l’identificazione e la gestione del set di dati nelle operazioni future. |
| `schemaRef.id` | ID dello schema XDM di destinazione. |
| `tags.unifiedProfile` | Valore booleano che informa Experience Platform se i dati devono essere acquisiti in Real-Time Customer Profile. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID del set di dati target. Questo ID è necessario in un secondo momento per creare una connessione di destinazione.

```json
[
    "@/dataSets/6889f4f89b982b2b90bc1207"
]
```

+++

## Creare una connessione sorgente {#source}

Una connessione di origine definisce il modo in cui i dati vengono introdotti in Experience Platform da un’origine esterna. Specifica sia il sistema di origine che il formato dei dati in arrivo e fa riferimento a una connessione di base che contiene i dettagli di autenticazione. Ogni connessione sorgente è univoca per la tua organizzazione.

* Per le origini basate su file (ad esempio le archiviazioni cloud), una connessione di origine può includere impostazioni come delimitatore di colonna, tipo di codifica, tipo di compressione, espressioni regolari per la selezione dei file e se acquisire i file in modo ricorsivo.
* Per le origini basate su tabelle (ad esempio database, CRM e provider di automazione marketing), una connessione di origine può specificare dettagli quali il nome della tabella e le mappature delle colonne.

Per creare una connessione di origine, eseguire una richiesta POST all&#39;endpoint `/sourceConnections` dell&#39;API [!DNL Flow Service] e fornire l&#39;ID connessione di base, l&#39;ID specifica connessione e il percorso al file di dati di origine.

**Formato API**

```http
POST /sourceConnections
```

**Richiesta**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME source connection",
    "description": "A source connection for ACME contact data",
    "baseConnectionId": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "data": {
      "format": "tabular"
    },
    "params": {
      "tableName": "Contact",
      "columns": [
        {
          "name": "TestID",
          "type": "string",
          "xdm": {
            "type": "string"
          }
        },
        {
          "name": "Name",
          "type": "string",
          "xdm": {
            "type": "string"
          }
        },
        {
          "name": "Datefield",
          "type": "string",
          "meta:xdmType": "date-time",
          "xdm": {
            "type": "string",
            "format": "date-time"
          }
        }
      ]
    },
    "connectionSpec": {
      "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
      "version": "1.0"
    }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Un nome descrittivo per la connessione sorgente. Utilizza un nome chiaro e univoco per identificare e gestire più facilmente la connessione nelle operazioni future. |
| `description` | Descrizione facoltativa che è possibile aggiungere per fornire ulteriori informazioni sulla connessione di origine. |
| `baseConnectionId` | `id` della connessione di base. È possibile recuperare questo ID autenticando l&#39;origine in Experience Platform utilizzando l&#39;API [!DNL Flow Service]. |
| `data.format` | Il formato dei dati. Impostare questo valore su `tabular` per le origini basate su tabelle, ad esempio database, CRM e provider di automazione marketing. |
| `params.tableName` | Nome della tabella nell’account di origine che desideri acquisire in Experience Platform. |
| `params.columns` | Le colonne di tabella specifiche dei dati che desideri acquisire in Experience Platform. |
| `connectionSpec.id` | ID della specifica di connessione dell&#39;origine in uso. |

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID della connessione sorgente. Questo ID è necessario per creare un flusso di dati e acquisire i dati.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## Creare una connessione di destinazione {#target}

Una connessione di destinazione rappresenta la connessione alla destinazione in cui arrivano i dati acquisiti. Per creare una connessione di destinazione, devi fornire l’ID di specifica della connessione fissa associato al data lake. ID della specifica di connessione: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

**Formato API**

```http
POST /targetConnections
```

**Richiesta**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME target connection",
      "description": "ACME target connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6889f4f89b982b2b90bc1207"
      },
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Un nome descrittivo per la connessione di destinazione. Utilizza un nome chiaro e univoco per identificare e gestire più facilmente la connessione nelle operazioni future. |
| `description` | Descrizione facoltativa che è possibile aggiungere per fornire informazioni aggiuntive sulla connessione di destinazione. |
| `data.schema.id` | ID dello schema XDM di destinazione. |
| `params.dataSetId` | ID del set di dati di destinazione. |
| `connectionSpec.id` | ID della specifica di connessione del data lake. Questo ID è corretto: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

## Mappatura {#mapping}

Quindi, mappa i dati di origine con lo schema di destinazione a cui aderisce il set di dati di destinazione. Per creare una mappatura, effettuare una richiesta POST all&#39;endpoint `mappingSets` dell&#39;[[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/). Includi l’ID dello schema XDM di destinazione e i dettagli dei set di mappatura che desideri creare.

**Formato API**

```http
POST /mappingSets
```

**Richiesta**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
      "xdmVersion": "1.0",
      "id": null,
      "mappings": [
          {
              "destinationXdmPath": "_id",
              "sourceAttribute": "TestID",
              "identity": false,
              "identityGroup": null,
              "namespaceCode": null,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.fullName",
              "sourceAttribute": "Name",
              "identity": false,
              "identityGroup": null,
              "namespaceCode": null,
              "version": 0
          },
          {
              "destinationXdmPath": "person.birthDate",
              "sourceAttribute": "Datefield",
              "identity": false,
              "identityGroup": null,
              "namespaceCode": null,
              "version": 0
          }
      ]
  }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `xdmSchema` | `$id` dello schema XDM di destinazione. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della mappatura appena creata, incluso il relativo identificatore univoco (`id`). Questo ID è necessario in un passaggio successivo per creare un flusso di dati.

```json
{
    "id": "93ddfa69c4864d978832b1e5ef6ec3b9",
    "version": 0,
    "createdDate": 1612309018666,
    "modifiedDate": 1612309018666,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Recuperare le specifiche del flusso di dati {#flow-specs}

Prima di poter creare un flusso di dati, è necessario recuperare le specifiche corrispondenti alla sorgente. Per recuperare queste informazioni, effettuare una richiesta GET all&#39;endpoint `/flowSpecs` dell&#39;API [!DNL Flow Service].

**Formato API**

```http
GET /flowSpecs?property=name=="{NAME}"
```

| Parametro query | Descrizione |
| --- | --- |
| `property=name=="{NAME}"` | Nome della specifica del flusso di dati. <ul><li>Per le origini basate su file (ad esempio l&#39;archiviazione cloud), impostare questo valore su `CloudStorageToAEP`.</li><li>Per le origini basate su tabelle (ad esempio database, CRM e provider di automazione marketing), impostare questo valore su `CRMToAEP`.</li></ul> |

**Richiesta**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della specifica del flusso di dati responsabili dell’importazione di dati dall’origine in Experience Platform. La risposta include la specifica di flusso univoca `id` necessaria per creare un nuovo flusso di dati.

Per assicurarsi di utilizzare la specifica di flusso di dati corretta, controllare l&#39;array `items.sourceConnectionSpecIds` nella risposta. Verificare che l&#39;ID della specifica di connessione per l&#39;origine sia incluso nell&#39;elenco.

+++Seleziona per visualizzare

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "3416976c-a9ca-4bba-901a-1f08f66978ff",
                "38ad80fe-8b06-4938-94f4-d4ee80266b07",
                "d771e9c1-4f26-40dc-8617-ce58c4b53702",
                "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
                "3000eb99-cd47-43f3-827c-43caf170f015",
                "26d738e0-8963-47ea-aadf-c60de735468a",
                "74a1c565-4e59-48d7-9d67-7c03b8a13137",
                "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
                "cb66ab34-8619-49cb-96d1-39b37ede86ea",
                "eb13cb25-47ab-407f-ba89-c0125281c563",
                "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
                "37b6bf40-d318-4655-90be-5cd6f65d334b",
                "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
                "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
                "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
                "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
                "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
                "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
                "09182899-b429-40c9-a15a-bf3ddbc8ced7",
                "0479cc14-7651-4354-b233-7480606c2ac3",
                "d6b52d86-f0f8-475f-89d4-ce54c8527328",
                "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
                "fcad62f3-09b0-41d3-be11-449d5a621b69",
                "ea1c2a08-b722-11eb-8529-0242ac130003",
                "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
                "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
                "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
                "2fa8af9c-2d1a-43ea-a253-f00a00c74412",
                "e9d7ec6b-0873-4e57-ad21-b3a7c65e310b"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
            ],
            "optionSpec": {
                "name": "OptionSpec",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "errorDiagnosticsEnabled": {
                            "title": "Error diagnostics.",
                            "description": "Flag to enable detailed and sample error diagnostics summary.",
                            "type": "boolean",
                            "default": false
                        },
                        "partialIngestionPercent": {
                            "title": "Partial ingestion threshold.",
                            "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
                            "type": "number",
                            "exclusiveMinimum": 0
                        }
                    }
                }
            },
            "transformationSpecs": [
                {
                    "name": "Copy",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "properties": {
                            "deltaColumn": {
                                "type": "object",
                                "properties": {
                                    "name": {
                                        "type": "string"
                                    },
                                    "dateFormat": {
                                        "type": "string"
                                    },
                                    "timezone": {
                                        "type": "string"
                                    }
                                },
                                "required": [
                                    "name"
                                ]
                            }
                        },
                        "required": [
                            "deltaColumn"
                        ]
                    }
                },
                {
                    "name": "Mapping",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines various params required for different mapping from source to target",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            },
                            "mappingVersion": {
                                "type": "string"
                            }
                        }
                    }
                }
            ],
            "scheduleSpec": {
                "name": "PeriodicSchedule",
                "type": "Periodic",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "startTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "frequency": {
                            "type": "string",
                            "enum": [
                                "once",
                                "minute",
                                "hour",
                                "day",
                                "week"
                            ]
                        },
                        "interval": {
                            "type": "integer"
                        },
                        "backfill": {
                            "type": "boolean",
                            "default": true
                        }
                    },
                    "required": [
                        "startTime",
                        "frequency"
                    ],
                    "if": {
                        "properties": {
                            "frequency": {
                                "const": "once"
                            }
                        }
                    },
                    "then": {
                        "allOf": [
                            {
                                "not": {
                                    "required": [
                                        "interval"
                                    ]
                                }
                            },
                            {
                                "not": {
                                    "required": [
                                        "backfill"
                                    ]
                                }
                            }
                        ]
                    },
                    "else": {
                        "required": [
                            "interval"
                        ],
                        "if": {
                            "properties": {
                                "frequency": {
                                    "const": "minute"
                                }
                            }
                        },
                        "then": {
                            "properties": {
                                "interval": {
                                    "minimum": 15
                                }
                            }
                        },
                        "else": {
                            "properties": {
                                "interval": {
                                    "minimum": 1
                                }
                            }
                        }
                    }
                }
            },
            "runSpec": {
                "name": "ProviderParams",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "description": "defines various params required for creating flow run.",
                    "properties": {
                        "startTime": {
                            "type": "integer",
                            "description": "An integer that defines the start time of the run. The value is represented in Unix epoch time."
                        },
                        "windowStartTime": {
                            "type": "integer",
                            "description": "An integer that defines the start time of the window against which data is to be pulled. The value is represented in Unix epoch time."
                        },
                        "windowEndTime": {
                            "type": "integer",
                            "description": "An integer that defines the end time of the window against which data is to be pulled. The value is represented in Unix epoch time."
                        },
                        "deltaColumn": {
                            "type": "object",
                            "description": "The delta column is required to partition the data and separate newly ingested data from historic data.",
                            "properties": {
                                "name": {
                                    "type": "string"
                                },
                                "dateFormat": {
                                    "type": "string"
                                },
                                "timezone": {
                                    "type": "string"
                                }
                            },
                            "required": [
                                "name"
                            ]
                        }
                    },
                    "required": [
                        "startTime",
                        "windowStartTime",
                        "windowEndTime",
                        "deltaColumn"
                    ]
                }
            },
            "attributes": {
                "recordTypeEnabled": true,
                "defaultRecordType": "profile",
                "isSourceFlow": true,
                "flacValidationSupported": true,
                "isDraftModeSupported": true,
                "frequency": "batch",
                "notification": {
                    "category": "sources",
                    "flowRun": {
                        "enabled": true
                    }
                }
            },
            "permissionsInfo": {
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ],
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ]
            }
        }
    ]
}
```

+++

## Creare un flusso di dati {#dataflow}

Un flusso di dati è una pipeline configurata che trasferisce dati tra i servizi di Experience Platform. Definisce il modo in cui i dati vengono acquisiti da origini esterne (come database, archiviazione cloud o API), elaborati e instradati ai set di dati target. Questi set di dati vengono quindi utilizzati da servizi come Identity Service, Real-Time Customer Profile e Destinations per l’attivazione e l’analisi.

Per creare un flusso di dati, devi fornire i valori per i seguenti elementi:

* [ID connessione Source](#source)
* [ID connessione di destinazione](#target)
* [ID di mappatura](#mapping)
* [ID specifica flusso di dati](#flow-specs)

Durante questo passaggio, puoi utilizzare i seguenti parametri in `scheduleParams` per configurare una pianificazione di acquisizione per il flusso di dati:

| Parametro di pianificazione | Descrizione |
| --- | --- |
| `startTime` | Tempo di epoca (in secondi) in cui deve iniziare il flusso di dati. |
| `frequency` | La frequenza di acquisizione. Configura la frequenza per indicare la frequenza con cui deve essere eseguito il flusso di dati. Puoi impostare la frequenza su: <ul><li>`once`: imposta la frequenza su `once` per creare un&#39;acquisizione unica. Le impostazioni di intervallo e retrocompilazione non sono disponibili per i processi di acquisizione una tantum. Per impostazione predefinita, la frequenza di pianificazione è impostata su una volta.</li><li>`minute`: imposta la frequenza su `minute` per pianificare il flusso di dati per acquisire i dati al minuto.</li><li>`hour`: imposta la frequenza su `hour` per pianificare il flusso di dati per acquisire i dati su base oraria.</li><li>`day`: imposta la frequenza su `day` per pianificare il flusso di dati per acquisire i dati su base giornaliera.</li><li>`week`: imposta la frequenza su `week` per pianificare il flusso di dati per acquisire i dati settimanalmente.</li></ul> |
| `interval` | Intervallo tra acquisizioni consecutive (richiesto per tutte le frequenze eccetto `once`). Configura l’impostazione dell’intervallo per stabilire l’intervallo di tempo tra ogni acquisizione. Ad esempio, se la frequenza è impostata su giorno e l’intervallo è 15, il flusso di dati verrà eseguito ogni 15 giorni. Impossibile impostare l&#39;intervallo su zero. Il valore dell&#39;intervallo minimo accettato per ciascuna frequenza è il seguente:<ul><li>`once`: n/d</li><li>`minute`: 15</li><li>`hour`: 1</li><li>`day`: 1</li><li>`week`: 1</li></ul> |
| `backfill` | Indica se acquisire i dati storici prima di `startTime`. |

{style="table-layout:auto"}


**Formato API**

```http
POST /flows
```

**Richiesta**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Contact Dataflow",
      "description": "A dataflow for ACME contact data",
      "flowSpec": {
          "id": "14518937-270c-4525-bdec-c2ba7cce3860",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "b7581b59-c603-4df1-a689-d23d7ac440f3"
      ],
      "targetConnectionIds": [
          "320f119a-5ac1-4ab1-88ea-eb19e674ea2e"
      ],
      "transformations": [
          {
              "name": "Copy",
              "params": {
                  "deltaColumn": {
                      "name": "Datefield",
                      "dateFormat": "YYYY-MM-DD",
                      "timezone": "UTC"
                  }
              }
          },
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "93ddfa69c4864d978832b1e5ef6ec3b9",
                  "mappingVersion": 0
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1612310466",
          "frequency":"minute",
          "interval":"15",
          "backfill": "true"
      }
  }'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome descrittivo del flusso di dati. Utilizza un nome chiaro e univoco per semplificare l’identificazione e la gestione del flusso di dati nelle operazioni future. |
| `description` | Una descrizione opzionale che puoi aggiungere per fornire informazioni aggiuntive sul flusso di dati. |
| `flowSpec.id` | ID della specifica di flusso corrispondente alla sorgente. |
| `sourceConnectionIds` | ID della connessione di origine generato in un passaggio precedente. |
| `targetConnectionIds` | ID della connessione di destinazione generato in un passaggio precedente. |
| `transformations.params.deltaColum` | La colonna designata utilizzata per distinguere tra dati nuovi ed esistenti. I dati incrementali verranno acquisiti in base alla marca temporale della colonna selezionata. Il formato supportato per `deltaColumn` è `yyyy-MM-dd HH:mm:ss`. Per [!DNL Microsoft Dynamics], il formato supportato per `deltaColumn` è `yyyy-MM-ddTHH:mm:ssZ`. |
| `transformations.params.deltaColumn.dateFormat` | Formato data da seguire per la colonna delta. |
| `transformations.params.deltaColumn.timeZone` | Fuso orario da utilizzare per l’interpretazione dei valori nella colonna delta. |
| `transformations.params.mappingId` | ID di mappatura generato in un passaggio precedente. |
| `scheduleParams.startTime` | Il tempo di inizio del flusso di dati in tempo epoca (secondi dall’epoca Unix). Determina quando inizierà la prima esecuzione del flusso di dati. |
| `scheduleParams.frequency` | La frequenza con cui verrà eseguito il flusso di dati. I valori accettabili includono: `once`, `minute`, `hour`, `day` o `week`. |
| `scheduleParams.interval` | L’intervallo tra esecuzioni consecutive del flusso di dati, in base alla frequenza selezionata. Deve essere un numero intero diverso da zero. Ad esempio, se la frequenza è impostata su minuti e l’intervallo è 15, il flusso di dati verrà eseguito ogni 15 minuti. |
| `scheduleParams.backfill` | Valore booleano (`true` o `false`) che determina se acquisire i dati storici (backfill) quando il flusso di dati viene creato per la prima volta. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce l&#39;ID (`id`) del flusso di dati appena creato.

```json
{
    "id": "ae0a9777-b322-4ac1-b0ed-48ae9e497c7e",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

### Utilizza l’interfaccia utente per convalidare il flusso di lavoro API {#validate-in-ui}

Puoi utilizzare l’interfaccia utente di Experience Platform per convalidare la creazione del flusso di dati. Passa al catalogo *[!UICONTROL Origini]* nell&#39;interfaccia utente di Experience Platform, quindi seleziona **[!UICONTROL Flussi dati]** dalle schede intestazione. Utilizzare quindi la colonna [!UICONTROL Nome flusso di dati] e individuare il flusso di dati creato utilizzando l&#39;API [!DNL Flow Service].

![Interfaccia dei flussi di dati dell&#39;area di lavoro origini nell&#39;interfaccia utente di Experience Platform](../../../images/tutorials/validations/dataflows-interface.png)

Puoi convalidare ulteriormente il flusso di dati tramite l&#39;interfaccia [!UICONTROL Attività flusso di dati]. Utilizza la barra a destra per visualizzare le informazioni sull&#39;[!UICONTROL utilizzo API] del flusso di dati. In questa sezione vengono visualizzati lo stesso ID del flusso di dati, lo stesso ID del set di dati e lo stesso ID di mappatura generati durante il processo di creazione del flusso di dati in [!DNL Flow Service].

![Pagina di visualizzazione del flusso di dati dell&#39;area di lavoro di origine.](../../../images/tutorials/validations/api-usage.png)

## Passaggi successivi

Questa esercitazione ti ha guidato nel processo di creazione di un flusso di dati in Experience Platform utilizzando l&#39;API [!DNL Flow Service]. Hai imparato a creare e configurare i componenti necessari, inclusi lo schema XDM di destinazione, il set di dati, la connessione di origine, la connessione di destinazione e il flusso di dati stesso. Seguendo questi passaggi, puoi automatizzare l’acquisizione di dati da origini esterne in Experience Platform, consentendo ai servizi a valle come Real-Time Customer Profile e Destinations di sfruttare i dati acquisiti per casi d’uso avanzati.

### Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorarne le prestazioni direttamente nell’interfaccia utente di Experience Platform. Ciò include il tracciamento dei tassi di acquisizione, delle metriche di successo e di eventuali errori che si verificano. Per ulteriori informazioni su come monitorare il flusso di dati, consulta l&#39;esercitazione su [account di monitoraggio e flussi di dati](../../../../dataflows/ui/monitor-sources.md).

### Aggiornare il flusso di dati

Per aggiornare le configurazioni per la pianificazione, la mappatura o le informazioni generali dei flussi di dati, visita il tutorial su [aggiornamento dei flussi di dati di origine](../../api/update-dataflows.md).

## Eliminare il flusso di dati

È possibile eliminare i flussi di dati non più necessari o creati in modo errato utilizzando la funzione **[!UICONTROL Elimina]** disponibile nell&#39;area di lavoro **[!UICONTROL Flussi di dati]**. Per ulteriori informazioni su come eliminare i flussi di dati, consulta l&#39;esercitazione su [eliminazione dei flussi di dati](../../api/delete.md).
