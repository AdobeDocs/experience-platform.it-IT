---
keywords: Experience Platform;home;argomenti popolari;preparazione dati;guida api;set di mappatura;
solution: Experience Platform
title: Endpoint API per set di mappature
topic-legacy: mapping sets
description: Puoi utilizzare l'endpoint `/mappingSets` nell'API Adobe Experience Platform per recuperare, creare, aggiornare e convalidare a livello di programmazione i set di mappatura.
exl-id: a4e4ddcd-164e-42aa-b7d1-ba59d70da142
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 5%

---

# Endpoint di mapping

I set di mapping possono essere utilizzati per definire il modo in cui i dati di uno schema di origine vengono mappati su quello di uno schema di destinazione. È possibile utilizzare `/mappingSets` nell’API di preparazione dati per recuperare, creare, aggiornare e convalidare in modo programmatico i set di mappatura.

## Set di mappature elenco

Puoi recuperare un elenco di tutti i set di mappatura per la tua organizzazione IMS effettuando una richiesta di GET al `/mappingSets` punto finale.

**Formato API**

La `/mappingSets` l’endpoint supporta diversi parametri di query per facilitare il filtraggio dei risultati. Anche se la maggior parte di questi parametri sono opzionali, si consiglia vivamente di utilizzarli per ridurre i costi di overhead. Tuttavia, è necessario includere entrambi i `start` e `limit` come parte della richiesta. È possibile includere più parametri, separati da e commerciale (`&`).

```http
GET /mappingSets?limit={LIMIT}&start={START}
GET /mappingSets?limit={LIMIT}&start={START}&name={NAME}
GET /mappingSets?limit={LIMIT}&start={START}&orderBy={ORDER_BY}
GET /mappingSets?limit={LIMIT}&start={START}&expandSchema={EXPAND_SCHEMA}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{LIMIT}` | (**Obbligatorio**) Specifica il numero di set di mapping restituiti. |
| `{START}` | (**Obbligatorio**) Specifica l&#39;offset delle pagine dei risultati. Per ottenere la prima pagina di risultati, imposta il valore su `start=0`. |
| `{NAME}` | Filtra i set di mappatura per nome. |
| `{ORDER_BY}` | Ordina l’ordine dei risultati. Gli unici campi supportati sono `createdDate` e `updatedDate`. Puoi anteporre la proprietà a `+` o `-` per ordinarlo rispettivamente in ordine crescente o decrescente. |
| `{EXPAND_SCHEMA}` | Valore booleano che determina se lo schema di output completo viene restituito come parte della risposta. |

**Richiesta**

La richiesta seguente recupererà gli ultimi due set di mappature all’interno dell’organizzazione IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/mappingSets?limit=2&start=0 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```json
{
    "data": [
        {
            "id": "428beb15b4864daaaa9dc3f005448005",
            "version": 1,
            "createdDate": 1582250953000,
            "modifiedDate": 1582251156000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_ui_platform",
            "supportVersion": "1.1",
            "inputSchema": {
                "id": "e660142cab8e438382abc5691b364b30",
                "version": 0,
                "sampleId": "f9e83882e3e34c1f8b873a3b8113c01e"
            },
            "outputSchema": {
                "id": "1956affc28be468aa452e5e47c680c6b",
                "version": 0,
                "schemaRef": {
                    "id": "https://ns.adobe.com/xdm/context/profile__union",
                    "contentType": "1.0"
                }
            },
            "mappings": [
                {
                    "id": "af809223484341009ce0db13d4b32a3a",
                    "version": 0,
                    "createdDate": 1582250953000,
                    "modifiedDate": 1582250953000,
                    "createdBy": "acp_xql_gateway",
                    "modifiedBy": "acp_xql_gateway",
                    "sourceType": "text/x.schema-path",
                    "source": "id",
                    "destination": "person.name.firstName",
                    "identity": false,
                    "primaryIdentity": false,
                    "matchScore": 0.0,
                    "functionVersion": 1,
                    "sourceAttribute": "id",
                    "destinationXdmPath": "person.name.firstName"
                }
            ],
            "status": "PUBLISHED",
            "strictMapping": false,
            "allowNullValues": false,
            "xdmVersion": "1.0",
            "schemaRef": {
                "id": "https://ns.adobe.com/xdm/context/profile__union",
                "contentType": "1.0"
            },
            "xdmSchema": "https://ns.adobe.com/xdm/context/profile__union"
        },
        {
            "id": "8afb1351833a4a4692ea61074b60813b",
            "version": 0,
            "createdDate": 1582250893000,
            "modifiedDate": 1582250893000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "supportVersion": "1.1",
            "inputSchema": {
                "id": "97fe2ecf4faa400bb66dd6be88a53fe4",
                "version": 0,
                "sampleId": "0248bfb352214f908bdd6cf9c19447e1"
            },
            "outputSchema": {
                "id": "e9c3696715d94905bb4e9bfc2c508e66",
                "version": 0,
                "schemaRef": {
                    "id": "https://ns.adobe.com/xdm/context/profile__union",
                    "contentType": "1.0"
                }
            },
            "mappings": [
                {
                    "id": "74647d8bf3b742f289534bee2fdeb732",
                    "version": 0,
                    "createdDate": 1582250893000,
                    "modifiedDate": 1582250893000,
                    "createdBy": "acp_xql_gateway",
                    "modifiedBy": "acp_xql_gateway",
                    "sourceType": "text/x.schema-path",
                    "source": "last_name",
                    "destination": "person.name.lastName",
                    "identity": false,
                    "primaryIdentity": false,
                    "matchScore": 0.0,
                    "functionVersion": 1,
                    "sourceAttribute": "last_name",
                    "destinationXdmPath": "person.name.lastName"
                }
            ],
            "status": "DRAFT",
            "strictMapping": false,
            "allowNullValues": false,
            "xdmVersion": "1.0",
            "schemaRef": {
                "id": "https://ns.adobe.com/xdm/context/profile__union",
                "contentType": "1.0"
            },
            "xdmSchema": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "_page": {
        "count": 0,
        "limit": 2
    }
}
```

## Creare un set di mappatura

Puoi creare un nuovo set di mappature effettuando una richiesta di POST al `/mappingSets` punto finale.

**Formato API**

```http
POST /mappingSets
```

**Richiesta**

La richiesta seguente crea un nuovo set di mappature, configurato dai parametri forniti nel payload.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/mappingSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "id",
            "destination": "_id",
            "name": "id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "firstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "lastName",
            "destination": "person.name.lastName"
        }
    ]
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `outputSchema.schemaRef.id` | ID dello schema XDM a cui si fa riferimento. |
| `outputSchema.schemaRef.contentType` | Determina il formato di risposta dello schema a cui si fa riferimento. Ulteriori informazioni su questo campo sono disponibili nella sezione [Guida per gli sviluppatori del Registro di sistema dello schema](../../xdm/api/schemas.md#lookup). |
| `mappings.sourceType` | Il tipo di origine descrive come il valore verrà estratto dall&#39;origine alla destinazione. |
| `mappings.source` | La posizione da cui desideri mappare i dati. |
| `mappings.destination` | Posizione in cui si desidera mappare i dati. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con le informazioni sul set di mappatura appena creato.

```json
{
    "id": "e7c80e4c0d8f4a98a7d400b4e178b635",
    "version": 0,
    "createdDate": 1614901254724,
    "modifiedDate": 1614901254724,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Convalida mappature

Puoi verificare che le mappature funzionino correttamente effettuando una richiesta POST al `/mappingSets/validate` punto finale.

**Formato API**

```http
POST /mappingSets/validate
```

**Richiesta**

La seguente richiesta convalida le mappature fornite nel payload.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/mappingSets/validate \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "id",
            "destination": "_id",
            "name": "id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "firstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "lastName",
            "destination": "person.name.lastName"
        }
    ]
}
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con le informazioni di convalida per la mappatura proposta.

```json
{
    "validationResponse": [
        {
            "status": "SUCCESS",
            "errors": null
        },
        {
            "status": "SUCCESS",
            "errors": null
        },
        {
            "status": "SUCCESS",
            "errors": null
        }
    ]
}
```

## Anteprima dei dati per le mappature

Puoi visualizzare in anteprima a cosa saranno mappati i tuoi dati effettuando una richiesta di POST al `/mappingSets/preview` punto finale.

**Formato API**

```http
POST /mappingSets/preview
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/mappingSets/preview \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
{
    "data": [
        {
            "id": 1234,
            "firstName": "Jim",
            "lastName": "Seltzer"
        }
    ],
    "mappingSet": {
        "outputSchema": {
            "schemaRef": {
                "id": "https://ns.adobe.com/stardust/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "mappings": [
            {
                "sourceType": "ATTRIBUTE",
                "source": "id",
                "destination": "_id",
                "name": "id",
                "description": "Identifier field"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "firstName",
                "destination": "person.name.firstName"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "lastName",
                "destination": "person.name.lastName"
            }
        ]
    }
}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con un&#39;anteprima dei dati mappati.

```json
[
    {
        "data": {
            "person": {
                "name": {
                    "firstName": "Jim",
                    "lastName": "Seltzer"
                }
            },
            "_id": "1234"
        },
        "errors": null
    }
]
```

## Cercare un set di mappature

Puoi recuperare un set di mappatura specifico fornendo il relativo ID nel percorso di una richiesta GET al `/mappingSets` punto finale. Questo endpoint supporta anche diversi parametri di query per consentire il recupero dei dettagli sulla versione del set di mappature specificata.

**Formato API**

```http
GET /mappingSets/{MAPPING_SET_ID}
GET /mappingSets/{MAPPING_SET_ID}?expandSchema={EXPAND_SCHEMA}
GET /mappingSets/{MAPPING_SET_ID}?version={VERSION}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{MAPPING_SET_ID}` | (**Obbligatorio**) L&#39;ID del set di mappature che desideri recuperare. |
| `{EXPAND_SCHEMA}` | Parametro di query booleano che determina se restituire lo schema di output come parte della risposta. |
| `{VERSION}` | Parametro di query integer che determina la versione del set di mappatura da recuperare. |

**Richiesta**

La richiesta seguente recupera informazioni dettagliate su un set di mappature specificato.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/mappingSets/e7c80e4c0d8f4a98a7d400b4e178b635 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sul set di mappatura che si desidera recuperare.

>[!NOTE]
>
>La risposta seguente è stata troncata per lo spazio.

```json
{
    "id": "e7c80e4c0d8f4a98a7d400b4e178b635",
    "version": 0,
    "createdDate": 1614901255000,
    "modifiedDate": 1614901255000,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "supportVersion": "1.1",
    "outputSchema": {
        "id": "cf0a57df22354cfdb5f32a747b63a456",
        "version": 0,
        "jsonSchema": {
            "title": "A sample schema",
            "description": "My sample schema",
            "type": "object",
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "description": "A unique identifier for the record.",
                    "type": "string"
                },
                "_repo": {
                    "type": "object",
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time"
                        }
                    }
                },
                "createdByBatchID": {
                    "type": "string",
                    "format": "uri-reference"
                },
                "modifiedByBatchID": {
                    "type": "string",
                    "format": "uri-reference"
                },
                "person": {
                    "type": "object",
                    "properties": {
                        "birthDate": {
                            "type": "string",
                            "format": "date"
                        },
                        "birthDayAndMonth": {
                            "type": "string",
                            "pattern": "[0-1][0-9]-[0-9][0-9]"
                        },
                        "birthYear": {
                            "type": "integer",
                            "minimum": 1,
                            "maximum": 32767
                        },
                        "gender": {
                            "type": "string",
                            "default": "not_specified",
                            "enum": [
                                "non_specific",
                                "not_specified",
                                "female",
                                "male"
                            ]
                        },
                        "name": {
                            "title": "Full name",
                            "description": "The person's full name.",
                            "type": "object",
                            "properties": {
                                "firstName": {
                                    "title": "First name",
                                    "type": "string"
                                },
                                "fullName": {
                                    "title": "Full name",
                                    "type": "string"
                                },
                                "lastName": {
                                    "title": "Last name",
                                    "type": "string"
                                },
                                "middleName": {
                                    "title": "Middle name",
                                    "type": "string"
                                }
                            }
                        }
                    }
                },
                "personID": {
                    "title": "Person ID",
                    "type": "string"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string"
                }
            },
            "version": "1.0",
            "imsOrg": "{ORG_ID}",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305"
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "id": "a11f44b0214d4fdcb79cbb5e1d93e638",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "id",
            "destination": "_id",
            "name": "id",
            "description": "Identifier field"
        },
        {
            "id": "b9bf7873451f4b7ba767ca3ba9327750",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "firstName",
            "destination": "person.name.firstName",
        },
        {
            "id": "bab961fc18f54789b9268ec04c6f6f9b",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "lastName",
            "destination": "person.name.lastName",
        }
    ],
    "status": "DRAFT",
    "strictMapping": false,
    "allowNullValues": false,
    "xdmVersion": "application/vnd.adobe.xed-full+json;version=1",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
    },
    "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305"
}
```

## Aggiornare un set di mappature

Puoi aggiornare un set di mappatura fornendo il relativo ID nel percorso di un `PUT` richiesta al `mappingSets` punto finale.

**Formato API**

```http
PUT /mappingSets/{MAPPING_SET_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{MAPPING_SET_ID}` | ID del set di mappature che desideri aggiornare. |

**Richiesta**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/conversion/mappingSets/e7c80e4c0d8f4a98a7d400b4e178b635 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "id",
            "destination": "_id",
            "name": "id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "firstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "lastName",
            "destination": "person.name.lastName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "nationality",
            "destination": "person.nationality"           
        }
    ]
}
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sul set di mappature appena aggiornato.

>[!NOTE]
>
>La risposta seguente è stata troncata per lo spazio.

```json
{
    "id": "e7c80e4c0d8f4a98a7d400b4e178b635",
    "version": 1,
    "createdDate": 1614901255000,
    "modifiedDate": 1614909614227,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "supportVersion": "1.1",
    "outputSchema": {
        "id": "cf0a57df22354cfdb5f32a747b63a456",
        "version": 0,
        "jsonSchema": {
            "title": "A sample schema",
            "description": "My sample schema",
            "type": "object",
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "description": "A unique identifier for the record.",
                    "type": "string",
                },
                "_repo": {
                    "type": "object",
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time"
                        }
                    }
                },
                "createdByBatchID": {
                    "type": "string",
                    "format": "uri-reference"
                },
                "modifiedByBatchID": {
                    "type": "string",
                    "format": "uri-reference"
                },
                "person": {
                    "type": "object",
                    "properties": {
                        "birthDate": {
                            "type": "string",
                            "format": "date"
                        },
                        "birthDayAndMonth": {
                            "type": "string",
                            "pattern": "[0-1][0-9]-[0-9][0-9]"
                        },
                        "birthYear": {
                            "type": "integer",
                            "minimum": 1,
                            "maximum": 32767
                        },
                        "gender": {
                            "type": "string",
                            "default": "not_specified",
                            "enum": [
                                "non_specific",
                                "not_specified",
                                "female",
                                "male"
                            ]
                        },
                        "name": {
                            "title": "Full name",
                            "description": "The person's full name.",
                            "type": "object",
                            "properties": {
                                "firstName": {
                                    "title": "First name",
                                    "type": "string"
                                },
                                "fullName": {
                                    "title": "Full name",
                                    "type": "string"
                                },
                                "lastName": {
                                    "title": "Last name",
                                    "type": "string"
                                },
                                "middleName": {
                                    "title": "Middle name",
                                    "type": "string"
                                },
                                "suffix": {
                                    "title": "Suffix",
                                    "type": "string"
                                }
                            }
                        }
                },
                "personID": {
                    "title": "Person ID",
                    "type": "string"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string"
                }
            },
            "version": "1.0",
            "imsOrg": "6A29340459CA8D350A49413A@AdobeOrg",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305"
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "id": "1bb13ec5929f4847a8ea0f1d9e60d3e6",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "id",
            "destination": "_id",
            "name": "id"
        },
        {
            "id": "394bec970d54410b98e1d4c55a3843ca",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "firstName",
            "destination": "person.name.firstName"
        },
        {
            "id": "a78729629b22418998b528755b3e0fb1",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "lastName",
            "destination": "person.name.lastName"
        },
        {
            "id": "c5211e1e295f48018c125c24a04e925a",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "nationality",
            "destination": "person.nationality"
        }
    ],
    "strictMapping": false,
    "allowNullValues": false,
    "xdmVersion": "application/vnd.adobe.xed-full+json;version=1",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
    },
    "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305"
}
```

## Elencare le mappature per un set di mappature

Puoi visualizzare tutte le mappature che appartengono a un set di mappatura specifico fornendo il relativo ID nel percorso di una richiesta di GET al seguente endpoint.

**Formato API**

```http
GET /mappingSets/{MAPPING_SET_ID}/mappings
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{MAPPING_SET_ID}` | ID del set di mappature per il quale desideri recuperare le mappature. |

**Richiesta**

La richiesta seguente restituisce tutte le mappature nel set di mappature specificato.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/mappingSets/e7c80e4c0d8f4a98a7d400b4e178b635/mappings \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```json
[
    {
        "id": "1bb13ec5929f4847a8ea0f1d9e60d3e6",
        "version": 0,
        "createdDate": 1614909614000,
        "modifiedDate": 1614909614000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceType": "text/x.schema-path",
        "source": "id",
        "destination": "_id",
        "name": "id",
        "description": "Identifier field",
        "identity": false,
        "primaryIdentity": false,
        "matchScore": 0.0,
        "functionVersion": 1,
        "sourceAttribute": "id",
        "destinationXdmPath": "_id"
    },
    {
        "id": "394bec970d54410b98e1d4c55a3843ca",
        "version": 0,
        "createdDate": 1614909614000,
        "modifiedDate": 1614909614000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceType": "text/x.schema-path",
        "source": "firstName",
        "destination": "person.name.firstName",
        "identity": false,
        "primaryIdentity": false,
        "matchScore": 0.0,
        "functionVersion": 1,
        "sourceAttribute": "firstName",
        "destinationXdmPath": "person.name.firstName"
    },
    {
        "id": "a78729629b22418998b528755b3e0fb1",
        "version": 0,
        "createdDate": 1614909614000,
        "modifiedDate": 1614909614000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceType": "text/x.schema-path",
        "source": "lastName",
        "destination": "person.name.lastName",
        "identity": false,
        "primaryIdentity": false,
        "matchScore": 0.0,
        "functionVersion": 1,
        "sourceAttribute": "lastName",
        "destinationXdmPath": "person.name.lastName"
    },
    {
        "id": "c5211e1e295f48018c125c24a04e925a",
        "version": 0,
        "createdDate": 1614909614000,
        "modifiedDate": 1614909614000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceType": "text/x.schema-path",
        "source": "nationality",
        "destination": "person.nationality",
        "identity": false,
        "primaryIdentity": false,
        "matchScore": 0.0,
        "functionVersion": 1,
        "sourceAttribute": "nationality",
        "destinationXdmPath": "person.nationality"
    }
]
```

## Cercare una mappatura all&#39;interno di un set di mappatura

Puoi recuperare una mappatura specifica per un set di mappatura fornendo i relativi ID nel percorso di una richiesta di GET all’endpoint seguente.

**Formato API**

```http
GET /mappingSets/{MAPPING_SET_ID}/mappings/{MAPPING_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{MAPPING_SET_ID}` | ID del set di mappatura di cui si desidera cercare le informazioni di mappatura. |
| `{MAPPING_ID}` | ID della mappatura da cercare. |

**Richiesta**

La richiesta seguente recupera informazioni su una mappatura specifica nel set di mappature specificato.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/mappingSets/e7c80e4c0d8f4a98a7d400b4e178b635/mappings/394bec970d54410b98e1d4c55a3843ca \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sulla mappatura specificata.

```json
{
    "id": "394bec970d54410b98e1d4c55a3843ca",
    "version": 0,
    "createdDate": 1614909614000,
    "modifiedDate": 1614909614000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceType": "text/x.schema-path",
    "source": "firstName",
    "destination": "person.name.firstName",
    "identity": false,
    "primaryIdentity": false,
    "matchScore": 0.0,
    "functionVersion": 1,
    "sourceAttribute": "firstName",
    "destinationXdmPath": "person.name.firstName"
}
```
