---
keywords: Experience Platform;home;argomenti popolari;sistema di automazione del marketing;Raccogliere dati di automazione del marketing
solution: Experience Platform
title: Creare un flusso di dati per le origini di automazione marketing utilizzando l’API del servizio di flusso
topic-legacy: overview
type: Tutorial
description: Questa esercitazione descrive i passaggi per recuperare i dati da un sistema di automazione del marketing e inserirli in Adobe Experience Platform utilizzando i connettori sorgente e le API.
exl-id: f3754bd0-ed31-4bf2-8f97-975bf6a9b076
source-git-commit: 85af48f773d36eb00149b9fdec71a9c566a1bde5
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 2%

---

# Crea un flusso di dati per le origini di automazione del marketing utilizzando [!DNL Flow Service] API

Questa esercitazione descrive i passaggi per recuperare i dati da un’origine di automazione del marketing e portarli a Platform utilizzando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Per creare un flusso di dati, devi già disporre di un ID di connessione di base valido con un’origine di automazione di marketing. Se non disponi di questo ID, consulta la sezione [panoramica di origini](../../../home.md#marketing-automation) per un elenco delle origini di automazione marketing con cui è possibile creare una connessione di base.

## Introduzione

Questa esercitazione richiede anche di avere una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Guida per gli sviluppatori del Registro di sistema dello schema](../../../../xdm/api/getting-started.md): Include informazioni importanti da conoscere per eseguire correttamente le chiamate all’API del Registro di sistema dello schema. Questo include `{TENANT_ID}`, il concetto di &quot;contenitori&quot; e le intestazioni richieste per effettuare richieste (con particolare attenzione all’intestazione Accept e ai suoi possibili valori).
* [[!DNL Catalog Service]](../../../../catalog/home.md): Catalogo è il sistema di registrazione per la posizione dei dati e la derivazione all&#39;interno di Experience Platform.
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md): L’API di acquisizione in batch consente di inserire dati in Experience Platform come file batch.
* [Sandbox](../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Utilizzo delle API di Platform

Per informazioni su come effettuare correttamente le chiamate alle API di Platform, consulta la guida su [guida introduttiva alle API di Platform](../../../../landing/api-guide.md).

## Creazione di una connessione sorgente {#source}

È possibile creare una connessione sorgente effettuando una richiesta di POST al [!DNL Flow Service] API. Una connessione di origine è costituita da un ID connessione, un percorso del file di dati di origine e un ID della specifica di connessione.

Per creare una connessione di origine, è inoltre necessario definire un valore enum per l&#39;attributo del formato dati.

Utilizza i seguenti valori enum per i connettori basati su file:

| Formato dati | Valore Enum |
| ----------- | ---------- |
| Delimitato | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

Per tutti i connettori basati su tabella, imposta il valore su `tabular`.

**Formato API**

```https
POST /sourceConnections
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "HubSpot source connection",
        "baseConnectionId": "c6d4ee17-6752-4e83-94ee-1767522e83fa",
        "description": "HubSpot source connection",
        "data": {
            "format": "tabular",
        },
        "params": {
            "path": "Hubspot.Contacts"
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `baseConnectionId` | ID di connessione univoco del sistema di automazione di marketing di terze parti a cui accedi. |
| `params.path` | Percorso del file di origine a cui si accede. |
| `connectionSpec.id` | ID della specifica di connessione del sistema di automazione di marketing. |

**Risposta**

Una risposta corretta restituisce l&#39;identificatore univoco (`id`) della nuova connessione sorgente creata. Memorizza questo valore come richiesto nei passaggi successivi per la creazione di una connessione di destinazione.

```json
{
    "id": "f44dbef2-a4f0-4978-8dbe-f2a4f0e978cf",
    "etag": "\"5f00fba7-0000-0200-0000-5ed560520000\""
}
```

## Creare uno schema XDM di destinazione {#target-schema}

Affinché i dati di origine possano essere utilizzati in Platform, è necessario creare uno schema di destinazione per strutturare i dati di origine in base alle tue esigenze. Lo schema di destinazione viene quindi utilizzato per creare un set di dati di Platform in cui sono contenuti i dati di origine.

È possibile creare uno schema XDM di destinazione effettuando una richiesta POST al [API del Registro di sistema dello schema](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Per i passaggi dettagliati su come creare uno schema XDM di destinazione, consulta l’esercitazione su [creazione di uno schema tramite API](../../../../xdm/api/schemas.md).

## Creare un set di dati di destinazione {#target-dataset}

È possibile creare un set di dati di destinazione eseguendo una richiesta di POST al [API del servizio catalogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), fornendo l’ID dello schema di destinazione all’interno del payload.

Per i passaggi dettagliati su come creare un set di dati di destinazione, consulta l’esercitazione su [creazione di un set di dati tramite API](../../../../catalog/api/create-dataset.md).

## Creare una connessione di destinazione {#target-connection}

Una connessione di destinazione rappresenta la connessione alla destinazione in cui i dati acquisiti arrivano. Per creare una connessione di destinazione, devi fornire l’ID di specifica di connessione fisso associato al Data Lake. Questo ID della specifica di connessione è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ora disponi degli identificatori univoci di uno schema di destinazione di un set di dati di destinazione e dell’ID delle specifiche di connessione di un data lake. Utilizzo della [!DNL Flow Service] API, puoi creare una connessione di destinazione specificando questi identificatori insieme al set di dati che conterrà i dati di origine in entrata.

**Formato API**

```https
POST /targetConnections
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "HubSpot target connection",
        "description": "HubSpot target connection",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/da411446eec78026c28d9fafd9e406e304b771d55b07b91b",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5ed5639d798a22191b6987b2"
        },
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `data.schema.id` | La `$id` dello schema XDM di destinazione. |
| `data.schema.version` | Versione dello schema. Questo valore deve essere impostato `application/vnd.adobe.xed-full+json;version=1`, che restituisce la versione secondaria più recente dello schema. |
| `params.dataSetId` | ID del set di dati di destinazione. |
| `connectionSpec.id` | ID delle specifiche di connessione utilizzato per connettersi al Data Lake. Questo ID è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

```json
{
    "id": "4b3d05d8-b7aa-40de-bd05-d8b7aa80de65",
    "etag": "\"dd00a1a2-0000-0200-0000-5ed564850000\""
}
```

## Creare una mappatura {#mapping}

Affinché i dati di origine possano essere acquisiti in un set di dati di destinazione, devono prima essere mappati sullo schema di destinazione a cui aderisce il set di dati di destinazione.

Per creare un set di mappatura, invia una richiesta POST al gruppo `mappingSets` punto finale [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) fornendo lo schema XDM di destinazione `$id` e i dettagli dei set di mappatura che desideri creare.

**Formato API**

```https
POST /conversion/mappingSets
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/da411446eec78026c28d9fafd9e406e304b771d55b07b91b",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Vid",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "Properties_Firstname_Value",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_repo.createDate",
                "sourceAttribute": "Added_At",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| Proprietà | Descrizione |
| --- | --- |
| `xdmSchema` | ID dello schema XDM di destinazione. |

**Risposta**

Una risposta corretta restituisce i dettagli della mappatura appena creata, incluso il relativo identificatore univoco (`id`). Memorizza questo valore come necessario in un passaggio successivo per la creazione di un flusso di dati.

```json
{
    "id": "500a9b747fcf4908a21917d49bd61780",
    "version": 0,
    "createdDate": 1591043336298,
    "modifiedDate": 1591043336298,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Specifiche del flusso di dati di ricerca {#specs}

Un flusso di dati è responsabile della raccolta dei dati da origini e del loro inserimento in Platform. Per creare un flusso di dati, devi prima ottenere le specifiche del flusso di dati responsabili della raccolta dei dati di automazione del marketing.

**Formato API**

```https
GET /flowSpecs?property=name=="CRMToAEP"
```

**Richiesta**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CRMToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce i dettagli della specifica del flusso di dati responsabile dell’inserimento dei dati dall’origine in Platform. La risposta include le specifiche di flusso univoche `id` necessario per creare un nuovo flusso di dati.

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
                "221c7626-58f6-4eec-8ee2-042b0226f03b",
                "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
                "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
                "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
                "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
                "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
                "102706fb-a5cd-42ee-afe0-bc42f017ff43",
                "09182899-b429-40c9-a15a-bf3ddbc8ced7",
                "0479cc14-7651-4354-b233-7480606c2ac3",
                "d6b52d86-f0f8-475f-89d4-ce54c8527328",
                "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
                "1fe283f6-9bec-11ea-bb37-0242ac130002"
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
            "attributes": {
                "notification": {
                    "category": "sources",
                    "flowRun": {
                        "enabled": true
                    }
                }
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        }
    ]
}
```

## Creare un flusso di dati

L’ultimo passo verso la raccolta dei dati di automazione del marketing è quello di creare un flusso di dati. A questo punto sono stati preparati i seguenti valori richiesti:

* [ID connessione di origine](#source)
* [ID connessione di destinazione](#target)
* [ID mappatura](#mapping)
* [ID specifica del flusso di dati](#specs)

Un flusso di dati è responsabile della pianificazione e della raccolta dei dati da un’origine. È possibile creare un flusso di dati eseguendo una richiesta di POST fornendo al contempo i valori precedentemente menzionati all’interno del payload.

Per pianificare un’acquisizione, è innanzitutto necessario impostare il valore dell’ora di inizio in modo che l’ora di inizio sia espressa in secondi. Quindi, è necessario impostare il valore della frequenza su una delle cinque opzioni: `once`, `minute`, `hour`, `day`oppure `week`. Il valore dell’intervallo indica il periodo tra due acquisizioni consecutive e la creazione di un’acquisizione una tantum non richiede l’impostazione di un intervallo. Per tutte le altre frequenze, il valore dell&#39;intervallo deve essere impostato su uguale o maggiore di `15`.

**Formato API**

```https
POST /flows
```

**Richiesta**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "HubSpot dataflow",
        "description": "collecting Hubspot.Contacts",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "f44dbef2-a4f0-4978-8dbe-f2a4f0e978cf"
        ],
        "targetConnectionIds": [
            "4b3d05d8-b7aa-40de-bd05-d8b7aa80de65"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "deltaColumn": {
                        "name": "updatedAt",
                        "dateFormat": "YYYY-MM-DD",
                        "timezone": "UTC"
                    }
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "500a9b747fcf4908a21917d49bd61780",
                    "mappingVersion": 0
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1591043454",
            "frequency":"once",
            "interval":"15"
        }
    }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `flowSpec.id` | La [ID delle specifiche di flusso](#specs) recuperato nel passaggio precedente. |
| `sourceConnectionIds` | La [ID connessione di origine](#source) recuperato in un passaggio precedente. |
| `targetConnectionIds` | La [ID connessione di destinazione](#target-connection) recuperato in un passaggio precedente. |
| `transformations.params.mappingId` | La [ID mappatura](#mapping) recuperato in un passaggio precedente. |
| `transformations.params.deltaColum` | Colonna designata utilizzata per distinguere tra dati nuovi ed esistenti. I dati incrementali verranno acquisiti in base al timestamp della colonna selezionata. Il formato della data supportato per `deltaColumn` è `yyyy-MM-dd HH:mm:ss`. |
| `transformations.params.mappingId` | ID di mappatura associato al database. |
| `scheduleParams.startTime` | Ora di inizio del flusso di dati in epoch time. |
| `scheduleParams.frequency` | Frequenza con cui il flusso di dati raccoglie i dati. I valori accettabili includono: `once`, `minute`, `hour`, `day`oppure `week`. |
| `scheduleParams.interval` | L&#39;intervallo indica il periodo tra due esecuzioni di flusso consecutive. Il valore dell&#39;intervallo deve essere un numero intero diverso da zero. L&#39;intervallo non è necessario quando la frequenza è impostata come `once` e deve essere maggiore o uguale a `15` per altri valori di frequenza. |

**Risposta**

Una risposta corretta restituisce l&#39;ID (`id`) del flusso di dati appena creato.

```json
{
    "id": "e0bd8463-0913-4ca1-bd84-6309134ca1f6",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni sulle esecuzioni del flusso, lo stato di completamento e gli errori. Per ulteriori informazioni su come monitorare i flussi di dati, consulta l’esercitazione su [monitoraggio dei flussi di dati nell’API ](../monitor.md)

## Passaggi successivi

Seguendo questa esercitazione, hai creato un connettore di origine per raccogliere i dati da un sistema di automazione di marketing su base pianificata. I dati in arrivo possono ora essere utilizzati dai servizi della piattaforma a valle, come [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica del profilo cliente in tempo reale](../../../../profile/home.md)
* [Panoramica di Data Science Workspace](../../../../data-science-workspace/home.md)
