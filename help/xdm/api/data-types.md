---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;data model;data type registry;schema registry;data type;data type;data types;Data types;create
solution: Experience Platform
title: Endpoint API per tipi di dati
description: L’endpoint /datatypes nell’API Schema Registry consente di gestire in modo programmatico i tipi di dati XDM all’interno dell’applicazione Experience.
exl-id: 2a58d641-c681-40cf-acc8-7ad842cd6243
source-git-commit: 342da62b83d0d804b31744a580bcd3e38412ea51
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 4%

---

# Endpoint &quot;data types&quot;

I tipi di dati vengono utilizzati come campi del tipo di riferimento nelle classi o nei gruppi di campi dello schema allo stesso modo dei campi letterali di base, con la differenza fondamentale che i tipi di dati possono definire più sottocampi. Sebbene siano simili ai gruppi di campi in quanto consentono l’utilizzo coerente di una struttura a più campi, i tipi di dati sono più flessibili in quanto possono essere inclusi ovunque nella struttura dello schema, mentre i gruppi di campi possono essere aggiunti solo al livello principale. Il `/datatypes` endpoint nella [!DNL Schema Registry] API consente di gestire in modo programmatico i tipi di dati all’interno dell’applicazione Experience.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’[[!DNL Schema Registry] API di ](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Prima di continuare, controlla [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida per la lettura delle chiamate API di esempio di questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recuperare un elenco di tipi di dati {#list}

Puoi elencare tutti i tipi di dati in `global` o `tenant` mediante una richiesta GET a `/global/datatypes` o `/tenant/datatypes`, rispettivamente.

>[!NOTE]
>
>Quando si elencano le risorse, il registro dello schema limita il set di risultati a 300 elementi. Per restituire risorse oltre questo limite, è necessario utilizzare i parametri di paging. È inoltre consigliabile utilizzare parametri di query aggiuntivi per filtrare i risultati e ridurre il numero di risorse restituite. Consulta la sezione su [parametri di query](./appendix.md#query) nel documento dell’appendice per ulteriori informazioni.

**Formato API**

```http
GET /{CONTAINER_ID}/datatypes?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Il contenitore da cui desideri recuperare i tipi di dati: `global` per tipi di dati creati da Adobi o `tenant` per i tipi di dati di proprietà dell’organizzazione. |
| `{QUERY_PARAMS}` | Parametri di query facoltativi in base ai quali filtrare i risultati. Consulta la [documento dell&#39;appendice](./appendix.md#query) per un elenco dei parametri disponibili. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente recupera un elenco di tipi di dati da `tenant` contenitore, utilizzando un `orderby` parametro di query per ordinare i tipi di dati in base al relativo `title` attributo.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende da `Accept` intestazione inviata nella richiesta. I seguenti elementi `Accept` le intestazioni sono disponibili per elencare i tipi di dati:

| `Accept` intestazione | Descrizione |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Restituisce un breve riepilogo di ciascuna risorsa. Questa è l’intestazione consigliata per l’elenco delle risorse. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Restituisce il tipo di dati JSON completo per ogni risorsa, con originale `$ref` e `allOf` incluso. (Limite: 300) |

{style="table-layout:auto"}

**Risposta**

La richiesta precedente utilizzava `application/vnd.adobe.xed-id+json` `Accept` , pertanto la risposta include solo il `title`, `$id`, `meta:altId`, e `version` attributi per ciascun tipo di dati. Utilizzo dell&#39;altro `Accept` intestazione (`application/vnd.adobe.xed+json`) restituisce tutti gli attributi di ciascun tipo di dati. Seleziona la scheda appropriata `Accept` a seconda delle informazioni richieste nella risposta.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/78570e371092c032260714dd8bfd6d44",
      "meta:altId": "_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44",
      "version": "1.0",
      "title": "Loyalty"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/4b0329b5573cbb7cb757db667d7fdf66",
      "meta:altId": "_{TENANT_ID}.datatypes.4b0329b5573cbb7cb757db667d7fdf66",
      "version": "1.0",
      "title": "Property Details"
    }
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 2
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/datatypes?orderby=title"
    }
  }
}
```

## Cercare un tipo di dati {#lookup}

Per cercare un tipo di dati specifico, devi includere l’ID del tipo di dati nel percorso di una richiesta GET.

**Formato API**

```http
GET /{CONTAINER_ID}/datatypes/{DATA_TYPE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Contenitore che ospita il tipo di dati che desideri recuperare: `global` per un tipo di dati creato da un Adobe o `tenant` per un tipo di dati di proprietà dell’organizzazione. |
| `{DATA_TYPE_ID}` | Il `meta:altId` o con codifica URL `$id` del tipo di dati che si desidera cercare. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente recupera un tipo di dati in base al suo `meta:altId` valore fornito nel percorso.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende da `Accept` intestazione inviata nella richiesta. Tutte le richieste di ricerca richiedono un `version` essere inclusi nel `Accept` intestazione. I seguenti elementi `Accept` le intestazioni sono disponibili:

| `Accept` intestazione | Descrizione |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Raw con `$ref` e `allOf`, ha titoli e descrizioni. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` e `allOf` risolto, con titoli e descrizioni. |
| `application/vnd.adobe.xed-notext+json; version=1` | Raw con `$ref` e `allOf`, senza titoli o descrizioni. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` e `allOf` risolto, nessun titolo o descrizione. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` e `allOf` risolto, inclusi i descrittori. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del tipo di dati. I campi restituiti dipendono dal `Accept` intestazione inviata nella richiesta. Sperimenta con diversi `Accept` intestazioni per confrontare le risposte e determinare quale intestazione è più adatta al tuo caso d’uso.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/78570e371092c032260714dd8bfd6d44",
  "meta:altId": "_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Loyalty",
  "type": "object",
  "description": "Loyalty object containing loyalty-specific fields.",
  "definitions": {
    "customFields": {
      "properties": {
        "loyaltyId": {
          "title": "Loyalty ID",
          "description": "Unique loyalty program member ID. Should be in the format of an email address.",
          "type": "string",
          "meta:xdmType": "string"
        },
        "memberSince": {
          "title": "Member Since",
          "description": "Date person joined loyalty program.",
          "type": "string",
          "format": "date",
          "meta:xdmType": "date"
        },
        "points": {
          "title": "Points",
          "description": "Accumulated loyalty points",
          "type": "integer",
          "meta:xdmType": "int"
        },
        "loyaltyLevel": {
          "title": "Loyalty Level",
          "description": "The current loyalty program level to which the individual member belongs.",
          "type": "string",
          "enum": [
            "platinum",
            "gold",
            "silver",
            "bronze"
          ],
          "meta:enum": {
            "platinum": "Platinum",
            "gold": "Gold",
            "silver": "Silver",
            "bronze": "Bronze"
          },
          "meta:xdmType": "string"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields"
    }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1557529442681,
    "repo:lastModifiedDate": 1557529442681,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "50b8008b588e911314f9685240dd4c23a247f37179a6d9ff6ba3877dc11ca504",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Creare un tipo di dati {#create}

Puoi definire un tipo di dati personalizzato nella sezione `tenant` effettuando una richiesta POST.

**Formato API**

```http
POST /tenant/datatypes
```

**Richiesta**

A differenza dei gruppi di campi, la definizione di un tipo di dati non richiede `meta:extends` o `meta:intendedToExtend` e non è necessario nidificare i campi per evitare conflitti.

Quando si tratta di definire la struttura del campo del tipo di dati stesso, è possibile utilizzare tipi primitivi (come `string` o `object`) oppure puoi fare riferimento ad altri tipi di dati esistenti tramite `$ref` attributi. Consulta la guida su [definizione dei campi XDM personalizzati nell’API](../tutorials/custom-fields-api.md) per istruzioni dettagliate sul formato previsto per i diversi tipi di campi XDM.

La richiesta seguente crea un tipo di dati oggetto &quot;Property Construction&quot; con sottoproprietà `yearBuilt`, `propertyType`, e `location`:

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Construction",
        "description": "Information related to the property construction",
        "type": "object",
        "properties": {
          "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type": "string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCenter": "Shopping Center"
            }
          },
          "location": {
            "title": "Location",
            "description": "The physical location of the property.",
            "$ref": "https://ns.adobe.com/xdm/common/address"
          }
        }
      }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 (Creato) e un payload contenente i dettagli del nuovo tipo di dati creato, tra cui `$id`, `meta:altId`, e `version`. Questi tre valori sono di sola lettura e sono assegnati dal [!DNL Schema Registry].

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/669ffcc61cf5e94e8640dbe6a15f0f24eb3cd1ddbbfb6b36",
  "meta:altId": "_{TENANT_ID}.datatypes.669ffcc61cf5e94e8640dbe6a15f0f24eb3cd1ddbbfb6b36",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Property Construction",
  "type": "object",
  "description": "Information related to the property construction",
  "properties": {
    "yearBuilt": {
      "type": "integer",
      "title": "Year Built",
      "description": "The year the property was constructed.",
      "meta:xdmType": "int"
    },
    "propertyType": {
      "type": "string",
      "title": "Property Type",
      "description": "Type of building or structure in which the property exists.",
      "enum": [
        "freeStanding",
        "mall",
        "shoppingCenter"
      ],
      "meta:enum": {
        "freeStanding": "Free Standing Building",
        "mall": "Mall Space",
        "shoppingCenter": "Shopping Center"
      },
      "meta:xdmType": "string"
    },
    "location": {
      "title": "Location",
      "description": "The physical location of the property.",
      "$ref": "https://ns.adobe.com/xdm/common/address",
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "refs": [
    "https://ns.adobe.com/xdm/common/address"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1670885230789,
    "repo:lastModifiedDate": 1670885230789,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "d3cc803a1f8daa06b7c150d882bd337d88f4d5d5f08d36cfc4c2849dc0255f7e",
    "meta:globalLibVersion": "1.38.3.1"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

Esecuzione di una richiesta di GET a [elenca tutti i tipi di dati](#list) nel contenitore tenant ora includerebbe il tipo di dati Dettagli proprietà, oppure puoi [eseguire una richiesta di ricerca (GET)](#lookup) utilizzando la codifica URL `$id` URI per visualizzare direttamente il nuovo tipo di dati.

## Aggiornare un tipo di dati {#put}

Puoi sostituire un intero tipo di dati tramite un’operazione PUT, essenzialmente riscrivendo la risorsa. Quando si aggiorna un tipo di dati tramite una richiesta PUT, il corpo deve includere tutti i campi necessari quando [creazione di un nuovo tipo di dati](#create) in una richiesta POST.

>[!NOTE]
>
>Se si desidera aggiornare solo parte di un tipo di dati anziché sostituirlo completamente, vedere la sezione relativa a [aggiornamento di una parte di un tipo di dati](#patch).

**Formato API**

```http
PUT /tenant/datatypes/{DATA_TYPE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DATA_TYPE_ID}` | Il `meta:altId` o con codifica URL `$id` del tipo di dati che si desidera riscrivere. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente riscrive un tipo di dati esistente, aggiungendo un nuovo `floorSize` campo.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Construction",
        "description": "Information related to the property construction",
        "type": "object",
        "properties": {
          "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type": "string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCenter": "Shopping Center"
            }
          },
          "floorSize" {
            "type": "integer",
            "title": "Floor Size",
            "description": "The floor size of the property, in square feet."
          }
        } 
      }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli del tipo di dati aggiornato.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:altId": "_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Property Construction",
  "type": "object",
  "description": "Information related to the property construction",
  "properties": {
    "yearBuilt": {
      "type": "integer",
      "title": "Year Built",
      "description": "The year the property was constructed.",
      "meta:xdmType": "int"
    },
    "propertyType": {
      "type": "string",
      "title": "Property Type",
      "description": "Type of building or structure in which the property exists.",
      "enum": [
        "freeStanding",
        "mall",
        "shoppingCenter"
      ],
      "meta:enum": {
        "freeStanding": "Free Standing Building",
        "mall": "Mall Space",
        "shoppingCenter": "Shopping Center"
      },
      "meta:xdmType": "string"
    },
    "floorSize" {
      "type":  "integer",
      "title":  "Floor Size",
      "description":  "The floor size of the property, in square feet.",
      "meta:xdmType": "int"
    }
  },
  "refs": [],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1604524729435,
    "repo:lastModifiedDate": 1604524729435,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "1c838764342756868ca1297869f582a38d15f03ed0acfc97fda7532d22e942c7",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Aggiornare una parte di un tipo di dati {#patch}

È possibile aggiornare una parte di un tipo di dati utilizzando una richiesta PATCH. Il [!DNL Schema Registry] supporta tutte le operazioni Patch JSON standard, tra cui `add`, `remove`, e `replace`. Per ulteriori informazioni sulla patch JSON, vedi [Guida di base sulle API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Se desideri sostituire un’intera risorsa con nuovi valori invece di aggiornare singoli campi, consulta la sezione su [sostituzione di un tipo di dati tramite un’operazione PUT](#put).

**Formato API**

```http
PATCH /tenant/data type/{DATA_TYPE_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{DATA_TYPE_ID}` | Codifica URL `$id` URI o `meta:altId` del tipo di dati da aggiornare. |

{style="table-layout:auto"}

**Richiesta**

L’esempio di richiesta seguente aggiorna la `description` di un tipo di dati esistente e aggiunge un nuovo `floorSize` campo.

Il corpo della richiesta è un array e ogni oggetto elencato rappresenta una modifica specifica di un singolo campo. Ogni oggetto include l&#39;operazione da eseguire (`op`), campo in cui deve essere eseguita l&#39;operazione (`path`) e quali informazioni devono essere incluse in tale operazione (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/description",
          "value": "Construction-related information for a company-operated property."
        },
        { 
          "op": "add",
          "path": "/properties/floorSize",
          "value": {
            "type": "integer",
            "title": "Floor Size",
            "description": "The floor size of the property, in square feet."
          }
        }
      ]'
```

**Risposta**

La risposta mostra che entrambe le operazioni sono state eseguite correttamente. Il `description` è stato aggiornato, e `floorSize` è stato aggiunto in `definitions`.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "datatypes",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type": "object",
        "properties": {
            "propertyName": {
              "type": "string",
              "title": "Property Name",
              "description": "Name of the property"
            },
            "propertyCity": {
              "title": "Property City",
              "description": "City where the property is located.",
              "type": "string"
            },
            "propertyCountry": {
              "title": "Property Country",
              "description": "Country where the property is located.",
              "type": "string"
            },
            "phoneNumber": {
              "title": "Phone Number",
              "description": "Primary phone number for the property.",
              "type": "string"
            },
            "propertyType": {
              "type": "string",
              "title": "Property Type",
              "description": "Type and primary use of property.",
              "enum": [
                  "retail",
                  "yoga",
                  "fitness"
              ],
              "meta:enum": {
                  "retail": "Retail Store",
                  "yoga": "Yoga Studio",
                  "fitness": "Fitness Center"
              }
            },
            "propertyConstruction": {
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1594941263588,
    "repo:lastModifiedDate": 1594941538433,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "5e8a5e508eb2ed344c08cb23ed27cfb60c841bec59a2f7513deda0f7af903021",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Eliminare un tipo di dati {#delete}

Talvolta può essere necessario rimuovere un tipo di dati dal registro degli schemi. Questa operazione viene eseguita eseguendo una richiesta DELETE con l’ID del tipo di dati fornito nel percorso.

**Formato API**

```http
DELETE /tenant/datatypes/{DATA_TYPE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DATA_TYPE_ID}` | Codifica URL `$id` URI o `meta:altId` del tipo di dati che si desidera eliminare. |

{style="table-layout:auto"}

**Richiesta**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto) e un corpo vuoto.

È possibile confermare l’eliminazione tentando un [richiesta di ricerca (GET)](#lookup) al tipo di dati. Dovrai includere un `Accept` nella richiesta, ma dovrebbe ricevere lo stato HTTP 404 (Non trovato) perché il tipo di dati è stato rimosso dal registro degli schemi.
