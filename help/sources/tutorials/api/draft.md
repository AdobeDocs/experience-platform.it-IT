---
title: Creare bozze dell’API delle entità del servizio Flow
description: Scopri come creare bozze della connessione di base, della connessione di origine, della connessione di destinazione e del flusso di dati utilizzando l’API del servizio Flusso
exl-id: aad6a302-1905-4a23-bc3d-39e76c9a22da
source-git-commit: ebd650355a5a4c2a949739384bfd5c8df9577075
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 5%

---

# Creare bozze del [!DNL Flow Service] entità che utilizzano l&#39;API

È possibile utilizzare `mode=draft` parametro di query in [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>) per impostare [!DNL Flow Service] entità quali le connessioni di base, le connessioni di origine, le connessioni di destinazione e i flussi di dati a uno stato di bozza.

Le bozze possono essere aggiornate in un secondo momento con nuove informazioni e quindi pubblicate quando sono pronte, utilizzando `op=publish` parametro di query.

Questo tutorial descrive come impostare [!DNL Flow Service] allo stato di bozza e consentono di mettere in pausa e salvare i flussi di lavoro per il completamento in un secondo momento.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../sandboxes/home.md): Experienci Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente chiamate alle API di Platform, consulta la guida su [introduzione alle API di Platform](../../../landing/api-guide.md).

### Verifica il supporto della modalità bozza

È inoltre necessario verificare se l&#39;ID della specifica di connessione e l&#39;ID della specifica di flusso corrispondente dell&#39;origine utilizzata sono abilitati per la modalità bozza.

>[!BEGINTABS]

>[!TAB Cerca dettagli sulle specifiche di connessione]

+++Richiesta La richiesta seguente recupera le informazioni sulle specifiche di connessione per [!DNL Azure File Storage]:

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/be5ec48c-5b78-49d5-b8fa-7c89ec4569b8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Risposta

In caso di esito positivo, la risposta restituisce le informazioni sulle specifiche di connessione per l’origine. Per verificare se la modalità bozza è supportata per l’origine, verifica che `items[0].attributes.isDraftModeSupported` ha un valore di `true`.

```json {line-numbers="true" start-line="1" highlight="252"}
{
    "items": [
        {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "name": "azure-file-storage",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "basicAuthentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "host": {
                                "type": "string",
                                "description": "Specifies the Azure File Storage endpoint."
                            },
                            "userid": {
                                "type": "string",
                                "description": "Specify the user to access the Azure File Storage."
                            },
                            "password": {
                                "type": "string",
                                "description": "Specify the storage access key",
                                "format": "password"
                            }
                        },
                        "required": [
                            "host",
                            "userid",
                            "password"
                        ]
                    }
                }
            ],
            "sourceSpec": {
                "name": "CloudStorage",
                "type": "CloudStorage",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "type": "string",
                            "description": "input path for copying files, can be a folder path, file path or a wildcard pattern"
                        },
                        "recursive": {
                            "type": "boolean",
                            "description": "indicates recursive copy in case of folder or wild card path, default is false"
                        }
                    },
                    "required": [
                        "path"
                    ]
                },
                "attributes": {
                    "uiAttributes": {
                        "documentationLink": "http://www.adobe.com/go/sources-azure-file-storage-en",
                        "isSource": true,
                        "category": {
                            "key": "cloudStorage"
                        },
                        "icon": {
                            "key": "azureFileStorage"
                        },
                        "description": {
                            "key": "azureFileStorageDescription"
                        },
                        "label": {
                            "key": "azureFileStorageLabel"
                        }
                    }
                }
            },
            "exploreSpec": {
                "name": "FileSystem",
                "type": "FileSystem",
                "requestSpec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "description": "defines explorable objects",
                    "properties": {
                        "objectType": {
                            "type": "string",
                            "enum": [
                                "file",
                                "folder",
                                "root"
                            ]
                        }
                    },
                    "allOf": [
                        {
                            "if": {
                                "properties": {
                                    "objectType": {
                                        "enum": [
                                            "file"
                                        ]
                                    }
                                }
                            },
                            "then": {
                                "properties": {
                                    "object": {
                                        "type": "string",
                                        "description": "defines file to get schema or preview of."
                                    },
                                    "fileType": {
                                        "type": "string",
                                        "enum": [
                                            "delimited"
                                        ]
                                    },
                                    "preview": {
                                        "type": "boolean"
                                    }
                                },
                                "required": [
                                    "object",
                                    "fileType"
                                ]
                            }
                        },
                        {
                            "if": {
                                "properties": {
                                    "objectType": {
                                        "enum": [
                                            "folder"
                                        ]
                                    }
                                }
                            },
                            "then": {
                                "properties": {
                                    "object": {
                                        "type": "string"
                                    }
                                },
                                "required": [
                                    "object"
                                ]
                            }
                        }
                    ]
                },
                "responseSpec": {
                    "root": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "array",
                        "description": "lists tables/items under the database/container requested.",
                        "items": {
                            "type": "object",
                            "properties": {
                                "type": {
                                    "type": "string",
                                    "description": "defines type of an item."
                                },
                                "name": {
                                    "type": "string",
                                    "description": "defines display name of an item."
                                },
                                "path": {
                                    "type": "string",
                                    "description": "defines path of an item."
                                },
                                "canPreview": {
                                    "type": "boolean",
                                    "default": false,
                                    "description": "defines whether an item is previewable or not."
                                },
                                "canFetchSchema": {
                                    "type": "boolean",
                                    "default": false,
                                    "description": "defines whether schema can be fetched for an item or not."
                                }
                            }
                        }
                    },
                    "folder": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {
                                "type": {
                                    "type": "string"
                                },
                                "name": {
                                    "type": "string"
                                },
                                "path": {
                                    "type": "string"
                                },
                                "canPreview": {
                                    "type": "boolean",
                                    "default": false
                                },
                                "canFetchSchema": {
                                    "type": "boolean",
                                    "default": false
                                }
                            }
                        }
                    },
                    "file": {
                        "delimited": {
                            "$schema": "http://json-schema.org/draft-07/schema#",
                            "type": "object",
                            "properties": {
                                "format": {
                                    "type": "string"
                                },
                                "schema": {
                                    "type": "object",
                                    "properties": {
                                        "columns": {
                                            "type": "array",
                                            "items": {
                                                "type": "object",
                                                "properties": {
                                                    "name": {
                                                        "type": "string"
                                                    },
                                                    "type": {
                                                        "type": "string"
                                                    }
                                                }
                                            }
                                        }
                                    }
                                },
                                "data": {
                                    "type": "array",
                                    "items": {
                                        "type": "object"
                                    }
                                }
                            }
                        }
                    }
                }
            },
            "attributes": {
                "category": "Cloud Storage",
                "connectorName": "Azure File Storage",
                "isSource": true,
                "isDraftModeSupported": true,
                "uiAttributes": {
                    "apiFeatures": {
                        "explorePaginationSupported": false
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

>[!TAB Cerca dettagli sulle specifiche di flusso]

+++Richiesta La richiesta seguente recupera i dettagli delle specifiche di flusso per un’origine di archiviazione cloud:

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Risposta

In caso di esito positivo, la risposta restituisce le informazioni sulle specifiche di flusso per l’origine. Per verificare se la modalità bozza è supportata per l’origine, verifica che `items[0].attributes.isDraftModeSupported` ha un valore di `true`.

```json {line-numbers="true" start-line="1" highlight="167"}
{
  "items": [
    {
      "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
      "name": "CloudStorageToAEP",
      "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
      "version": "1.0",
      "sourceConnectionSpecIds": [
        "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
        "ecadc60c-7455-4d87-84dc-2a0e293d997b",
        "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
        "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
        "32e8f412-cdf7-464c-9885-78184cb113fd",
        "b7bf2577-4520-42c9-bae9-cad01560f7bc",
        "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
        "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
        "54e221aa-d342-4707-bcff-7a4bceef0001",
        "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
        "26f526f2-58f4-4712-961d-e41bf1ccc0e8"
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
        },
        {
          "name": "Encryption",
          "spec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object",
            "description": "defines various params required for encrypted data ingestion",
            "properties": {
              "publicKeyId": {
                "type": "string",
                "description": "publicKeyId returned in encryptionKey creation API. One must use the publicKeyId corresponding to the same publicKey they used for encrypting the files"
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
      "attributes": {
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

>[!ENDTABS]



## Creare una bozza di connessione di base {#create-a-draft-base-connection}

Per creare una bozza di connessione di base, effettuare una richiesta POST al `/connections` endpoint del [!DNL Flow Service] API e fornire `mode=draft` come parametro di query.

**Formato API**

```http
POST /connections?mode=draft
```

| Parametro | Descrizione |
| --- | --- |
| `mode` | Parametro di query fornito dall&#39;utente che determina lo stato della connessione di base. Per impostare una connessione di base come bozza, impostate `mode` a `draft`. |

**Richiesta**

La richiesta seguente crea una bozza di connessione di base per [!DNL Azure File Storage] origine:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "ACME Azure File Storage Base Connection",
        "description": "Azure File Storage base connection for ACME data (DRAFT)",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
      }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID della connessione di base e l’etag corrispondente per la connessione di base bozza. Puoi usare questo ID in un secondo momento per aggiornare e pubblicare la connessione di base.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Pubblicare la bozza di connessione di base {#publish-your-draft-base-connection}

Quando la bozza è pronta per la pubblicazione, invia una richiesta POST al `/connections` e fornire l&#39;ID della bozza di connessione di base che si desidera pubblicare, nonché un&#39;operazione di pubblicazione.

**Formato API**

```http
POST /connections/{BASE_CONNECTION_ID}/action?op=publish
```

| Parametro | Descrizione |
| --- | --- |
| `op` | Operazione che aggiorna lo stato della connessione di base sottoposta a query. Per pubblicare una bozza di connessione di base, impostare `op` a `publish`. |

**Richiesta**

La richiesta seguente pubblica la bozza della connessione di base per [!DNL Azure File Storage] creato in un passaggio precedente.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f9377f50-607a-4818-b77f-50607a181860/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID e l’e-mail corrispondente per la connessione di base pubblicata.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Creare una bozza di connessione sorgente {#create-a-draft-source-connection}

Per creare una bozza di connessione sorgente, effettua una richiesta POST al `/sourceConnections` endpoint del [!DNL Flow Service] API e fornire `mode=draft` come parametro di query.

**Formato API**

```http
POST /sourceConnections?mode=draft
```

| Parametro | Descrizione |
| --- | --- |
| `mode` | Parametro di query fornito dall&#39;utente che determina lo stato della connessione di origine. Per impostare una connessione di origine come bozza, impostate `mode` a `draft`. |

**Richiesta**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Azure File Storage Source Connection",
      "description: "Azure File Storage source connection for ACME data (DRAFT)",
      "baseConnectionId": "f9377f50-607a-4818-b77f-50607a181860",
      "data": {
          "format": "delimited",
      },
      "params": {
          "path": "/acme/summerCampaign/account.csv",
          "type": "file"
      },
      "connectionSpec": {
          "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
          "version": "1.0"
      }
  }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID della connessione sorgente e l’eTag corrispondente per la connessione sorgente in stato di bozza. Puoi usare questo ID in un secondo momento per aggiornare e pubblicare la connessione sorgente.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## Pubblicare la bozza della connessione sorgente {#publish-your-draft-source-connection}

>[!NOTE]
>
>Non è possibile pubblicare una connessione di origine se la connessione di base associata è ancora in stato di bozza. Prima di pubblicare la connessione di base, assicurati che la tua connessione di base sia stata pubblicata.

Quando la bozza è pronta per la pubblicazione, invia una richiesta POST al `/sourceConnections` e fornire l&#39;ID della bozza della connessione di origine che si desidera pubblicare, nonché un&#39;operazione di pubblicazione.

**Formato API**

```http
POST /sourceConnections/{SOURCE_CONNECTION_ID}/action?op=publish
```

| Parametro | Descrizione |
| --- | --- |
| `op` | Operazione che aggiorna lo stato della connessione di origine interrogata. Per pubblicare una bozza di connessione di origine, impostare `op` a `publish`. |

**Richiesta**

La richiesta seguente pubblica la bozza della connessione sorgente per [!DNL Azure File Storage] creato in un passaggio precedente.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/26b53912-1005-49f0-b539-12100559f0e2/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID e l’e-mail corrispondente per la connessione sorgente pubblicata.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## Creare una bozza di connessione di destinazione {#create-a-draft-target-connection}

Per creare una bozza di connessione di destinazione, effettua una richiesta POST al `/targetConnections` endpoint del [!DNL Flow Service] API e fornire `mode=draft` come parametro di query.

**Formato API**

```http
POST /targetConnections?mode=draft
```

| Parametro | Descrizione |
| --- | --- |
| `mode` | Parametro di query fornito dall&#39;utente che determina lo stato della connessione di destinazione. Per impostare una connessione di destinazione come bozza, impostare `mode` a `draft`. |

**Richiesta**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Azure File Storage Target Connection",
      "description": "Azure File Storage target connection ACME data (DRAFT)",
      "data": {
          "schema": {
              "id": "{SCHEMA_ID}",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "{DATASET_ID}"
      },
          "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
  }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID della connessione di destinazione e l’etag corrispondente per la bozza della connessione di destinazione. Puoi usare questo ID in un secondo momento per aggiornare e pubblicare la connessione di destinazione.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Pubblicare la bozza di connessione di destinazione {#publish-your-draft-target-connection}

>[!NOTE]
>
>Non è possibile pubblicare una connessione di destinazione se la connessione di base associata è ancora in stato di bozza. Prima di pubblicare la connessione di destinazione, assicurati che la connessione di base sia pubblicata.

Quando la bozza è pronta per la pubblicazione, invia una richiesta POST al `/targetConnections` e fornire l’ID della bozza di connessione di destinazione da pubblicare, nonché un’operazione di pubblicazione.

**Formato API**

```http
POST /targetConnections/{TARGET_CONNECTION_ID}/action?op=publish
```

| Parametro | Descrizione |
| --- | --- |
| `op` | Operazione di azione che aggiorna lo stato della connessione di destinazione interrogata. Per pubblicare una bozza di connessione di destinazione, impostare `op` a `publish`. |

**Richiesta**

La richiesta seguente pubblica la bozza di connessione di destinazione per [!DNL Azure File Storage] creato in un passaggio precedente.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dbc5c132-bc2a-4625-85c1-32bc2a262558/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID e l’e-mail corrispondente per la connessione di destinazione pubblicata.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Creare un flusso di dati 2D {#create-a-draft-dataflow}

Per impostare un flusso di dati come bozza, effettua una richiesta POST al `/flows` endpoint durante l&#39;aggiunta di `mode=draft` come parametro di query. Questo consente di creare un flusso di dati e salvarlo come bozza.

**Formato API**

```http
POST /flows?mode=draft
```

| Parametro | Descrizione |
| --- | --- |
| `mode` | Parametro di query fornito dall’utente che determina lo stato del flusso di dati. Per impostare un flusso di dati come sformo, impostate `mode` a `draft`. |

**Richiesta**

La richiesta seguente crea un flusso di dati bozza.

```shell
  'https://platform.adobe.io/data/foundation/flowservice/flows?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "ACME Azure File Storage Dataflow",
    "description": "Azure File Storage dataflow for ACME data (DRAFT)",
    "sourceConnectionIds": [
        "26b53912-1005-49f0-b539-12100559f0e2"
    ],
    "targetConnectionIds": [
        "dbc5c132-bc2a-4625-85c1-32bc2a262558"
    ],
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    }
  }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID di flusso e l’eTag corrispondente per il flusso di dati della bozza. Puoi utilizzare questo ID in un secondo momento per aggiornare e pubblicare il flusso di dati.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

## Pubblicare il flusso di dati della bozza {#publish-your-draft-dataflow}

>[!NOTE]
>
>Non puoi pubblicare un flusso di dati se le connessioni di origine e di destinazione associate sono ancora in stato di bozza. Prima di pubblicare il flusso di dati, assicurati che le connessioni di origine e di destinazione siano pubblicate.

Quando la bozza è pronta per la pubblicazione, invia una richiesta POST al `/flows` endpoint, fornendo l’ID del flusso di dati bozza da pubblicare e un’operazione di pubblicazione.

**Formato API**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Parametro | Descrizione |
| --- | --- |
| `op` | Operazione che aggiorna lo stato del flusso di dati sottoposto a query. Per pubblicare un flusso di dati 2D, impostate `op` a `publish`. |

**Richiesta**

La richiesta seguente pubblica il flusso di dati della bozza.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce l’ID e i corrispondenti `etag` del flusso di dati.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

## Passaggi successivi

Seguendo questa esercitazione, hai imparato a creare bozze delle tue [!DNL Flow Service] e pubblicare queste bozze. Per ulteriori informazioni sulle origini, consulta la [panoramica sulle origini](../../home.md).