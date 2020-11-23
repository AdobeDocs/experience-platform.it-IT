---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;mixin registry;Schema Registry;mixin;Mixin;mixins;Mixins;create
solution: Experience Platform
title: Creare un mixin
description: L'endpoint /mixins nell'API del Registro di sistema dello schema consente di gestire i mixin XDM a livello di programmazione all'interno dell'applicazione dell'esperienza.
topic: developer guide
translation-type: tm+mt
source-git-commit: 0b55f18eabcf1d7c5c233234c59eb074b2670b93
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 2%

---


# Endpoint Mixins

I mix sono componenti riutilizzabili che definiscono uno o più campi che rappresentano un concetto particolare, ad esempio una singola persona, un indirizzo postale o un ambiente browser Web. Le mixine devono essere incluse come parte di uno schema che implementa una classe compatibile, a seconda del comportamento dei dati che rappresentano (record o serie temporali). L&#39; `/mixins` endpoint nell&#39; [!DNL Schema Registry] API consente di gestire i mixin in modo programmatico all&#39;interno dell&#39;applicazione dell&#39;esperienza.

## Introduzione

L&#39;endpoint utilizzato in questa guida fa parte dell&#39; [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/mixin-registry.yaml). Prima di continuare, consultate la guida [](./getting-started.md) introduttiva per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente chiamate a qualsiasi API  Experience Platform.

## Recupera un elenco di mixin {#list}

È possibile elencare tutti i mixin sotto il `global` contenitore o `tenant` il contenitore effettuando una richiesta di GET a `/global/mixins` o `/tenant/mixins`, rispettivamente.

>[!NOTE]
>
>Quando si elencano le risorse, il Registro di sistema dello schema limita i set di risultati a 300 elementi. Per restituire risorse oltre questo limite, è necessario utilizzare i parametri di paging. È inoltre consigliabile utilizzare parametri di query aggiuntivi per filtrare i risultati e ridurre il numero di risorse restituite. Per ulteriori informazioni, consulta la sezione sui parametri [di](./appendix.md#query) query nel documento allegato.

**Formato API**

```http
GET /{CONTAINER_ID}/mixins?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Il contenitore da cui desiderate recuperare i mixin: `global` per  mixin creati dal Adobe o `tenant` per mixin di proprietà della vostra organizzazione. |
| `{QUERY_PARAMS}` | Parametri di query facoltativi per filtrare i risultati per. Per un elenco dei parametri disponibili, consultare il documento [](./appendix.md#query) appendice. |

**Richiesta**

La richiesta seguente recupera un elenco di mixin dal `tenant` contenitore, utilizzando un parametro di `orderby` query per ordinare i mixin in base al loro `title` attributo.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dall’ `Accept` intestazione inviata nella richiesta. Le seguenti `Accept` intestazioni sono disponibili per elencare i mixin:

| `Accept` header | Descrizione |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Restituisce un breve riepilogo di ciascuna risorsa. Intestazione consigliata per elencare le risorse. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Restituisce il mixin JSON completo per ogni risorsa, con l&#39;originale `$ref` e `allOf` incluso. (Limite: 300) |

**Risposta**

La richiesta precedente ha utilizzato l’ `application/vnd.adobe.xed-id+json` intestazione, pertanto la risposta include solo gli `Accept` , `title`, `$id`e `meta:altId``version` gli attributi per ciascun mixin. Utilizzando l’altra `Accept` intestazione (`application/vnd.adobe.xed+json`) vengono restituiti tutti gli attributi di ciascun mixin. Selezionate l’ `Accept` intestazione appropriata in base alle informazioni richieste nella risposta.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/6ece98e9842907c78c651f5b249d9f09",
      "meta:altId": "_{TENANT_ID}.mixins.6ece98e9842907c78c651f5b249d9f09",
      "version": "1.0",
      "title": "CRM Data"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/6386ee478a30914964c6e676ad55603c",
      "meta:altId": "_{TENANT_ID}.mixins.6386ee478a30914964c6e676ad55603c",
      "version": "1.9",
      "title": "Loyalty Member Details"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/67626b2830db3d3ea6c8f9d007aa5797",
      "meta:altId": "_{TENANT_ID}.mixins.67626b2830db3d3ea6c8f9d007aa5797",
      "version": "1.0",
      "title": "Restaurant"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/2583b25b613fec704da6ef70cf527688",
      "meta:altId": "_{TENANT_ID}.mixins.2583b25b613fec704da6ef70cf527688",
      "version": "1.1",
      "title": "Retail Customer Preferences"
    },
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 3
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/mixins"
    }
  }
}
```

## Cercare un mixin {#lookup}

Potete cercare un mixin specifico includendo l&#39;ID del mixin nel percorso di una richiesta di GET.

**Formato API**

```http
GET /{CONTAINER_ID}/mixins/{MIXIN_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Il contenitore che contiene il mixin da recuperare: `global` per un  mixin creato dal Adobe o `tenant` per un mixin di proprietà dell’organizzazione. |
| `{MIXIN_ID}` | Il `meta:altId` o l’URL codificato `$id` del mixin che si desidera cercare. |

**Richiesta**

La richiesta seguente recupera un mixin in base al `meta:altId` valore fornito nel percorso.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dall’ `Accept` intestazione inviata nella richiesta. Tutte le richieste di ricerca richiedono che `version` sia inclusa nell’ `Accept` intestazione. The following `Accept` headers are available:

| `Accept` header | Descrizione |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Raw con `$ref` e `allOf`, ha titoli e descrizioni. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` e `allOf` risolto, con titoli e descrizioni. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Raw con `$ref` e `allOf`, senza titoli o descrizioni. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` e `allOf` risolto, nessun titolo o descrizione. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` e `allOf` risolto, descrittori inclusi. |

**Risposta**

Una risposta corretta restituisce i dettagli del mixin. I campi restituiti dipendono dall’ `Accept` intestazione inviata nella richiesta. Provate con `Accept` intestazioni diverse per confrontare le risposte e determinare quale intestazione è più adatta al caso d’uso.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Favorite Hotel",
  "type": "object",
  "description": "",
  "definitions": {
    "customFields": {
      "type": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "favoriteHotel": {
              "title": "Favorite Hotel",
              "description": "Reference field for hotel schema.",
              "type": "string",
              "isRequired": false,
              "meta:xdmType": "string"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{IMS_ORG}",
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

## Creare un mixin {#create}

Potete definire un mixin personalizzato sotto il `tenant` contenitore effettuando una richiesta di POST.

**Formato API**

```http
POST /tenant/mixins
```

**Richiesta**

Durante la definizione di un nuovo mixin, deve includere un `meta:intendedToExtend` attributo, che elenca le classi con cui il mixin è compatibile `$id` del mixin. In questo esempio, il mixin è compatibile con una `Property` classe precedentemente definita. I campi personalizzati devono essere nidificati sotto `_{TENANT_ID}` (come mostrato nell&#39;esempio) per evitare conflitti con campi simili forniti da classi e altri mixin.

>[!NOTE]
>
>Per informazioni dettagliate su come definire diversi tipi di campo da includere nel mixin, consultate la guida [ai vincoli dei](../schema/field-constraints.md#define-fields)campi.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Details",
        "description":"Detailed information related to the properties owned and operated by the company.",
        "type":"object",
        "meta:intendedToExtend":["https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"],
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
                "$ref": "#/definitions/property"
            }
        ]
}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un payload contenente i dettagli del mixin appena creato, inclusi `$id`, `meta:altId`e `version`. Questi valori sono di sola lettura e vengono assegnati dal [!DNL Schema Registry].

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Detailed information related to the properties owned and operated by the company.",
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
  "imsOrg": "{IMS_ORG}",
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

L&#39;esecuzione di una richiesta di GET per [elencare tutti i mixin](#list) nel contenitore tenant ora include il mixin Dettagli proprietà, oppure potete [eseguire una richiesta](#lookup) `$id` di ricerca (GET) utilizzando l&#39;URI con codifica URL per visualizzare direttamente il nuovo mixin.

## Aggiornare un mixin {#put}

Potete sostituire un intero mixin tramite un’operazione PUT, essenzialmente riscrivendo la risorsa. Quando aggiornate un mixin tramite una richiesta di PUT, il corpo deve includere tutti i campi che sarebbero necessari per [creare un nuovo mixin](#create) in una richiesta di POST.

>[!NOTE]
>
>Se desiderate solo aggiornare parte di un mixin invece di sostituirla completamente, consultate la sezione sull&#39; [aggiornamento di una parte di un mixin](#patch).

**Formato API**

```http
PUT /tenant/mixins/{MIXIN_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MIXIN_ID}` | Il codice `meta:altId` o URL `$id` del mixin da riscrivere. |

**Richiesta**

La seguente richiesta riscrive un mixin esistente, aggiungendo un nuovo `propertyCountry` campo.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Details",
        "description": "Detailed information related to the properties owned and operated by the company.",
        "type": "object",
        "meta:intendedToExtend": ["https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"],
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
                "$ref": "#/definitions/property"
            }
        ]
      }'
```

**Risposta**

Una risposta corretta restituisce i dettagli del mixin aggiornato.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Detailed information related to the properties owned and operated by the company.",
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
  "imsOrg": "{IMS_ORG}",
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

## Aggiornare una parte di un mixin {#patch}

Potete aggiornare una parte di un mixin utilizzando una richiesta di PATCH. Supporta [!DNL Schema Registry] tutte le operazioni standard di patch JSON, inclusi `add`, `remove`e `replace`. Per ulteriori informazioni sulla patch JSON, consultate la guida [ai fondamentali](../../landing/api-fundamentals.md#json-patch)API.

>[!NOTE]
>
>Se desiderate sostituire un&#39;intera risorsa con nuovi valori invece di aggiornare i singoli campi, consultate la sezione relativa alla [sostituzione di un mixin con un&#39;operazione](#put)PUT.

**Formato API**

```http
PATCH /tenant/mixin/{MIXIN_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{MIXIN_ID}` | L’ `$id` URI con codifica URL o `meta:altId` del mixin da aggiornare. |

**Richiesta**

La richiesta di esempio riportata di seguito aggiorna il `description` livello di un mixin esistente e aggiunge un nuovo `propertyCity` campo.

Il corpo della richiesta assume la forma di una matrice, con ogni oggetto elencato che rappresenta una specifica modifica a un singolo campo. Ogni oggetto include l&#39;operazione da eseguire (`op`), il campo sul quale deve essere eseguita l&#39;operazione (`path`) e quali informazioni devono essere incluse nell&#39;operazione (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/description",
          "value": "Details relating to a property operated by the company."
        },
        { 
          "op": "add",
          "path": "/definitions/property/properties/_{TENANT_ID}/properties/propertyCity",
          "value": {
            "title": "Property City",
            "description": "City where the property is located.",
            "type": "string"
          }
        }
      ]'
```

**Risposta**

La risposta indica che entrambe le operazioni sono state eseguite correttamente. L’ `description` aggiornamento è stato `propertyCountry` aggiunto in `definitions`.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
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
  "imsOrg": "{IMS_ORG}",
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

## Eliminare un mixin {#delete}

Può essere talvolta necessario rimuovere un mixin dal Registro di sistema dello schema. Questa operazione viene eseguita eseguendo una richiesta DELETE con l&#39;ID mixin fornito nel percorso.

**Formato API**

```http
DELETE /tenant/mixins/{MIXIN_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MIXIN_ID}` | L’ `$id` URI con codifica URL o `meta:altId` del mixin da eliminare. |

**Richiesta**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo vuoto.

È possibile confermare l&#39;eliminazione provando una richiesta [di](#lookup) ricerca (GET) al mixin. Sarà necessario includere un&#39; `Accept` intestazione nella richiesta, ma dovrebbe ricevere uno stato HTTP 404 (Non trovato) perché il mixin è stato rimosso dal Registro di sistema dello schema.