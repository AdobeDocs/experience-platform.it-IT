---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;modello dati;registro del tipo di dati;registro schema;tipo di dati;tipo di dati;tipi di dati;creare
solution: Experience Platform
title: Endpoint API per i tipi di dati
description: L’endpoint /datatypes nell’API del Registro di sistema dello schema consente di gestire programmaticamente i tipi di dati XDM all’interno dell’applicazione di esperienza.
exl-id: 2a58d641-c681-40cf-acc8-7ad842cd6243
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 5%

---

# Endpoint per tipi di dati

I tipi di dati vengono utilizzati come campi di tipo riferimento nelle classi o nei gruppi di campi dello schema allo stesso modo dei campi letterali di base, con la differenza chiave che i tipi di dati possono definire più campi secondari. Sebbene siano simili ai gruppi di campi in quanto consentono un uso coerente di una struttura a più campi, i tipi di dati sono più flessibili perché possono essere inclusi in qualsiasi punto della struttura dello schema, mentre i gruppi di campi possono essere aggiunti solo a livello principale. La `/datatypes` punto finale [!DNL Schema Registry] L’API ti consente di gestire i tipi di dati in modo programmatico all’interno dell’applicazione di esperienza.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’[[!DNL Schema Registry] API di ](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e importanti informazioni sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recupera un elenco di tipi di dati {#list}

È possibile elencare tutti i tipi di dati in `global` o `tenant` effettuando una richiesta GET a `/global/datatypes` o `/tenant/datatypes`, rispettivamente.

>[!NOTE]
>
>Quando si elencano le risorse, il Registro di sistema dello schema limita i set di risultati a 300 elementi. Per restituire le risorse oltre questo limite, è necessario utilizzare i parametri di paging. Si consiglia inoltre di utilizzare parametri di query aggiuntivi per filtrare i risultati e ridurre il numero di risorse restituite. Vedi la sezione su [parametri di query](./appendix.md#query) nel documento di appendice per ulteriori informazioni.

**Formato API**

```http
GET /{CONTAINER_ID}/datatypes?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Il contenitore da cui si desidera recuperare i tipi di dati da: `global` per tipi di dati creati da Adobe o `tenant` per i tipi di dati di proprietà dell’organizzazione. |
| `{QUERY_PARAMS}` | Parametri di query opzionali per filtrare i risultati in base a. Consulta la sezione [documento appendice](./appendix.md#query) per un elenco dei parametri disponibili. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta seguente recupera un elenco di tipi di dati dal `tenant` contenitore, utilizzando un `orderby` parametro di query per ordinare i tipi di dati in base ai rispettivi `title` attributo.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dal `Accept` intestazione inviata nella richiesta. I seguenti `Accept` le intestazioni sono disponibili per elencare i tipi di dati:

| `Accept` header | Descrizione |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Restituisce un breve riepilogo di ciascuna risorsa. Intestazione consigliata per l’elenco delle risorse. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Restituisce il tipo di dati JSON completo per ogni risorsa, con l’originale `$ref` e `allOf` incluso. (Limite: 300) |

{style=&quot;table-layout:auto&quot;}

**Risposta**

La richiesta di cui sopra ha utilizzato il `application/vnd.adobe.xed-id+json` `Accept` , quindi la risposta include solo l’ `title`, `$id`, `meta:altId`e `version` attributi per ciascun tipo di dati. Utilizzo dell&#39;altro `Accept` header (`application/vnd.adobe.xed+json`) restituisce tutti gli attributi di ciascun tipo di dati. Selezionare il `Accept` a seconda delle informazioni richieste nella risposta.

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

Puoi cercare un tipo di dati specifico includendo l’ID del tipo di dati nel percorso di una richiesta GET.

**Formato API**

```http
GET /{CONTAINER_ID}/datatypes/{DATA_TYPE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Il contenitore che contiene il tipo di dati da recuperare: `global` per un tipo di dati creato da un Adobe o `tenant` per un tipo di dati di proprietà dell’organizzazione. |
| `{DATA_TYPE_ID}` | La `meta:altId` o con codifica URL `$id` del tipo di dati che si desidera cercare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta seguente recupera un tipo di dati in base al relativo `meta:altId` nel percorso.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dal `Accept` intestazione inviata nella richiesta. Tutte le richieste di ricerca richiedono un `version` sono inclusi nella `Accept` intestazione. I seguenti `Accept` le intestazioni sono disponibili:

| `Accept` header | Descrizione |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Raw con `$ref` e `allOf`, include titoli e descrizioni. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` e `allOf` risolto, con titoli e descrizioni. |
| `application/vnd.adobe.xed-notext+json; version=1` | Raw con `$ref` e `allOf`, senza titoli o descrizioni. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` e `allOf` risolto, senza titoli o descrizioni. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` e `allOf` risolti, descrittori inclusi. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli del tipo di dati. I campi restituiti dipendono dal `Accept` intestazione inviata nella richiesta. Esperimento con diversi `Accept` intestazioni per confrontare le risposte e determinare quale intestazione è migliore per il tuo caso d’uso.

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

Puoi definire un tipo di dati personalizzato nella sezione `tenant` effettuando una richiesta di POST.

**Formato API**

```http
POST /tenant/datatypes
```

**Richiesta**

La definizione di un tipo di dati non richiede `meta:extends` o `meta:intendedToExtend` né i campi devono essere nidificati per evitare conflitti.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Construction",
        "description":"Information related to the property construction",
        "type":"object",
        "properties": {
          "yearBuilt": {
            "type":"integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type":"string",
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
          }
        } 
      }'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un payload contenente i dettagli del tipo di dati appena creato, tra cui `$id`, `meta:altId`e `version`. Questi tre valori sono di sola lettura e sono assegnati dal [!DNL Schema Registry].

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

Esecuzione di una richiesta GET a [elenco di tutti i tipi di dati](#list) nel contenitore tenant ora include il tipo di dati Dettagli proprietà oppure è possibile [eseguire una richiesta di ricerca (GET)](#lookup) utilizzando l’URL-encoded `$id` URI per visualizzare direttamente il nuovo tipo di dati.

## Aggiornare un tipo di dati {#put}

È possibile sostituire un intero tipo di dati tramite un’operazione PUT, essenzialmente riscrivendo la risorsa. Quando si aggiorna un tipo di dati tramite una richiesta PUT, il corpo deve includere tutti i campi che sarebbero necessari quando [creazione di un nuovo tipo di dati](#create) in una richiesta POST.

>[!NOTE]
>
>Se desideri aggiornare solo parte di un tipo di dati invece di sostituirlo completamente, consulta la sezione [aggiornamento di una parte di un tipo di dati](#patch).

**Formato API**

```http
PUT /tenant/datatypes/{DATA_TYPE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DATA_TYPE_ID}` | La `meta:altId` o con codifica URL `$id` del tipo di dati che si desidera riscrivere. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta seguente riscrive un tipo di dati esistente, aggiungendo un nuovo `floorSize` campo .

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
            "type":"integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type":"string",
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

Una risposta corretta restituisce i dettagli del tipo di dati aggiornato.

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

È possibile aggiornare una parte di un tipo di dati utilizzando una richiesta PATCH. La [!DNL Schema Registry] supporta tutte le operazioni standard di patch JSON, tra cui `add`, `remove`e `replace`. Per ulteriori informazioni sulla patch JSON, consulta la sezione [Guida di base sulle API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Per sostituire un’intera risorsa con nuovi valori anziché aggiornare singoli campi, consulta la sezione [sostituzione di un tipo di dati con un’operazione PUT](#put).

**Formato API**

```http
PATCH /tenant/data type/{DATA_TYPE_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{DATA_TYPE_ID}` | L’URL è codificato `$id` URI o `meta:altId` del tipo di dati da aggiornare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta di esempio riportata di seguito aggiorna la `description` di un tipo di dati esistente e aggiunge un nuovo `floorSize` campo .

Il corpo della richiesta assume la forma di una matrice, con ogni oggetto elencato che rappresenta una modifica specifica a un singolo campo. Ogni oggetto include l&#39;operazione da eseguire (`op`), su quale campo deve essere eseguita l&#39;operazione (`path`) e quali informazioni dovrebbero essere incluse in tale operazione (`value`).

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

La risposta indica che entrambe le operazioni sono state eseguite correttamente. La `description` è stato aggiornato e `floorSize` è stato aggiunto in `definitions`.

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
        "type":"object",
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

Talvolta può essere necessario rimuovere un tipo di dati dal Registro di sistema dello schema. A tal fine, esegui una richiesta DELETE con l’ID del tipo di dati fornito nel percorso.

**Formato API**

```http
DELETE /tenant/datatypes/{DATA_TYPE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DATA_TYPE_ID}` | L’URL è codificato `$id` URI o `meta:altId` del tipo di dati da eliminare. |

{style=&quot;table-layout:auto&quot;}

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

Una risposta corretta restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo vuoto.

Puoi confermare l&#39;eliminazione tentando un [richiesta di ricerca (GET)](#lookup) al tipo di dati. Sarà necessario includere un `Accept` intestazione nella richiesta, ma deve ricevere uno stato HTTP 404 (Non trovato) perché il tipo di dati è stato rimosso dal Registro di sistema dello schema.
