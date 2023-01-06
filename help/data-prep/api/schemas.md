---
keywords: Experience Platform;home;argomenti popolari;preparazione dati;guida api;schemi;
solution: Experience Platform
title: Endpoint API per gli schemi
description: Puoi utilizzare l’endpoint `/schemas` nell’API Adobe Experience Platform per recuperare, creare e aggiornare programmaticamente gli schemi da utilizzare con Mapper in Platform.
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 5%

---



# Endpoint degli schemi

Gli schemi possono essere utilizzati con Mapper per garantire che i dati acquisiti in Adobe Experience Platform corrispondano a quanto si desidera acquisire. È possibile utilizzare `/schemas` per creare, elencare e ottenere schemi personalizzati da utilizzare con Mapper in Platform a livello di programmazione.

>[!NOTE]
>
>Gli schemi creati utilizzando questo endpoint vengono utilizzati esclusivamente con i set Mapper e di mappatura. Per creare schemi accessibili da altri servizi Platform, consulta la sezione [Guida per gli sviluppatori del Registro di sistema dello schema](../../xdm/api/schemas.md).

## Ottieni tutti gli schemi

Puoi recuperare un elenco di tutti gli schemi mappatore disponibili per la tua organizzazione IMS effettuando una richiesta di GET al `/schemas` punto finale.

**Formato API**

La `/schemas` l’endpoint supporta diversi parametri di query per facilitare il filtraggio dei risultati. Anche se la maggior parte di questi parametri sono opzionali, si consiglia vivamente di utilizzarli per ridurre i costi di overhead. Tuttavia, è necessario includere entrambi i `start` e `limit` come parte della richiesta. È possibile includere più parametri, separati da e commerciale (`&`).

```http
GET /schemas?limit={LIMIT}&start={START}
GET /schemas?limit={LIMIT}&start={START}&name={NAME}
GET /schemas?limit={LIMIT}&start={START}&orderBy={ORDER_BY}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{LIMIT}` | **Obbligatorio**. Specifica il numero di schemi restituiti. |
| `{START}` | **Obbligatorio**. Specifica l&#39;offset delle pagine dei risultati. Per ottenere la prima pagina di risultati, imposta il valore su `start=0`. |
| `{NAME}` | Filtra lo schema in base al nome. |
| `{ORDER_BY}` | Ordina l’ordine dei risultati. I campi supportati sono `modifiedDate` e `createdDate`. Puoi anteporre la proprietà a `+` o `-` per ordinarlo rispettivamente in ordine crescente o decrescente. |

**Richiesta**

La richiesta seguente recupera gli ultimi due schemi creati per la tua organizzazione IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas&start=0&limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta seguente restituisce lo stato HTTP 200 con un elenco degli schemi richiesti.

>[!NOTE]
>
>La risposta seguente è stata troncata per lo spazio.

```json
{
    "data": [
        {
            "id": "823ac494f35e4e84bcb2f061378fcca6",
            "version": 0,
            "jsonSchema": {
                "title": "Sample schema",
                "type": "object",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "description": "A unique identifier for the record.",
                        "type": "string",
                        "format": "uri-reference",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "city": {
                        "title": "City",
                        "description": "The name of the city.",
                        "type": "string",
                        "meta:xdmField": "xdm:city",
                        "meta:xdmType": "string"
                    }
                }
            },
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc",
                "contentType": "1.0"
            }
        },
        {
            "id": "0f868d3a1b804fb0abf738306290ae79",
            "version": 0,
            "jsonSchema": {
                "title": "Sample schema 2",
                "type": "object",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "description": "A unique identifier for the record.",
                        "type": "string",
                        "format": "uri-reference",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "city": {
                        "title": "City",
                        "description": "The name of the city.",
                        "type": "string",
                        "meta:xdmField": "xdm:city",
                        "meta:xdmType": "string"
                    }
                }
            },
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/0f868d3a1b804fb0abf738306290ae79",
                "contentType": "1.0"
            }
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

## Creare uno schema

È possibile creare uno schema su cui eseguire la convalida effettuando una richiesta di POST al `/schemas` punto finale. Esistono tre modi per creare uno schema: invio di un [Schema JSON](https://json-schema.org/), utilizzando dati di esempio o facendo riferimento a uno schema XDM esistente.

```http
POST /schemas
```

### Utilizzo di uno schema JSON

**Richiesta**

La seguente richiesta ti consente di creare uno schema inviando un [Schema JSON](https://json-schema.org/).

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con le informazioni sul nuovo schema creato.

```json
{
    "id": "6daffabf14b1425292add3719afc8fab",
    "version": 0,
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}
```

### Utilizzo di dati di esempio

**Richiesta**

La richiesta seguente ti consente di creare uno schema utilizzando dati di esempio precedentemente caricati.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "sampleId": "45439a93d48d47d098d26e0f0840cc02"  
 }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `sampleId` | ID dei dati di esempio di cui si basa lo schema. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con le informazioni sul nuovo schema creato.

```json
{
    "id": "b2ee78bd55ac45f781a93fb8b90d99b2",
    "version": 0,
    "jsonSchema": {
        "title": "SampleSchema:45439a93d48d47d098d26e0f0840cc02",
        "type": "object",
        "properties": {
            "gender": {
                "title": "gender",
                "type": "string"
            },
            "last_name": {
                "title": "last_name",
                "type": "string"
            },
            "id": {
                "title": "id",
                "type": "string"
            },
            "ip_address": {
                "title": "ip_address",
                "type": "string"
            },
            "first_name": {
                "title": "first_name",
                "type": "string"
            },
            "email": {
                "title": "email",
                "type": "string"
            }
        }
    },
    "sampleId": "45439a93d48d47d098d26e0f0840cc02"
}
```

### Fai riferimento a uno schema XDM

**Richiesta**

La richiesta seguente ti consente di creare uno schema facendo riferimento a uno schema XDM esistente.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "name": "outputSchema1",
     "schemaRef": {
         "id": "https://ns.adobe.com/{TENANT_ID}/schemas/0d555890502224d187b619f23c35c8d1",
         "contentType": "application/vnd.adobe.xed-full+json;version=1"
     }  
 }'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `name` | Nome dello schema che si desidera creare. |
| `schemaRef.id` | ID dello schema a cui si fa riferimento. |
| `schemaRef.contentType` | Determina il formato di risposta dello schema a cui si fa riferimento. Ulteriori informazioni su questo campo sono disponibili nella sezione [guida per gli sviluppatori del registro di sistema](../../xdm/api/schemas.md#lookup) |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con le informazioni sul nuovo schema creato.

>[!NOTE]
>
>La risposta seguente è stata troncata per lo spazio.

```json
{
    "id": "4b64daa51b774cb2ac21b61d80125ed0",
    "version": 0,
    "name": "schemaName",
    "jsonSchema": "{\"id\":null,\"schema\":null,\"_refId\":null,\"title\":\"SimpleUser\",...,\"imsOrg\":\"{ORG_ID}\",\"$id\":\"https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96\"}",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96",
        "contentType": "application/vnd.adobe.xed+json;version=1.0"
    }
}
```

## Creare uno schema utilizzando il caricamento di file

Puoi creare uno schema caricando un file JSON da cui convertire.

**Formato API**

```http
POST /schemas/upload
```

**Richiesta**

La seguente richiesta ti consente di creare uno schema da un file JSON caricato.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas/upload \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: multipart/form-data' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -F 'file=@{PATH_TO_FILE}.json'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con le informazioni sul nuovo schema creato.

```json
{
    "id": "292add3716daffabf14b14259afc8fab",
    "version": 0,
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}
```

## Recupera uno schema specifico

È possibile recuperare informazioni su uno schema specifico effettuando una richiesta di GET al `/schemas` e fornisce l’ID dello schema che desideri recuperare nel percorso della richiesta.

**Formato API**

```http
GET /schemas/{SCHEMA_ID}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{SCHEMA_ID}` | ID dello schema che stai cercando. |

**Richiesta**

La richiesta seguente recupera informazioni sullo schema specificato.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas/0f868d3a1b804fb0abf738306290ae79 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 con le informazioni sullo schema specificato.

```json
{
    "id": "0f868d3a1b804fb0abf738306290ae79",
    "version": 0,
    "jsonSchema": {
        "title": "Sample schema",
        "description": "Sample description",
        "type": "object",
        "properties": {
            "_id": {
                "title": "Identifier",
                "description": "A unique identifier for the record.",
                "type": "string",
                "format": "uri-reference",
                "meta:xdmField": "@id",
                "meta:xdmType": "string"
            },
            "personalEmail": {
                "title": "Personal Email",
                "description": "A personal email address.",
                "type": "object",
                "properties": {
                    "primary": {
                        "title": "Primary",
                        "description": "Primary email indicator.\n\nA Profile can have only one `primary` email address at a given point of time.\n",
                        "type": "boolean",
                        "meta:xdmField": "xdm:primary",
                        "meta:xdmType": "boolean"
                    },
                    "address": {
                        "title": "Address",
                        "description": "The technical address, e.g 'name@domain.com' as commonly defined in RFC2822 and subsequent standards.",
                        "type": "string",
                        "format": "email",
                        "meta:xdmField": "xdm:address",
                        "meta:xdmType": "string"
                    }
                },
                "meta:xdmField": "xdm:personalEmail",
                "meta:referencedFrom": "https://ns.adobe.com/xdm/context/emailaddress",
                "meta:xdmType": "object"
            }
        },
        "imsOrg": "6A29340459CA8D350A49413A@AdobeOrg",
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc"
    },
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc",
        "contentType": "1.0"
    }
}
```
