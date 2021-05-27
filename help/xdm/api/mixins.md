---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;modello dati;registro mixin;registro schema;mixin;mixin;mixin;mixins;creare
solution: Experience Platform
title: Endpoint API per mixins
description: L’endpoint /mixins nell’API del Registro di sistema dello schema ti consente di gestire programmaticamente i mixin XDM all’interno dell’applicazione di esperienza.
topic-legacy: developer guide
exl-id: 93ba2fe3-0277-4c06-acf6-f236cd33252e
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 2%

---


# Endpoint Mixins (obsoleto)

>[!IMPORTANT]
>
>I mixin sono stati rinominati in gruppi di campi di schema e pertanto l’endpoint `/mixins` è stato dichiarato obsoleto a favore dell’endpoint `/fieldgroups`.
>
>Anche se `/mixins` continuerà a essere mantenuto come endpoint legacy, si consiglia vivamente di utilizzare `/fieldgroups` per le nuove implementazioni dell’API del Registro di sistema dello schema nelle applicazioni di esperienza. Per ulteriori informazioni, consulta la [guida endpoint dei gruppi di campi](./field-groups.md) .

I mixin sono componenti riutilizzabili che definiscono uno o più campi che rappresentano un concetto particolare, ad esempio una persona singola, un indirizzo postale o un ambiente browser web. I mixin sono destinati a essere inclusi come parte di uno schema che implementa una classe compatibile, a seconda del comportamento dei dati che rappresentano (record o serie temporali). L’endpoint `/mixins` nell’ API [!DNL Schema Registry] consente di gestire i mixin modo programmatico all’interno dell’applicazione di esperienza.

## Introduzione

L&#39;endpoint utilizzato in questa guida fa parte dell&#39; [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla relativa documentazione, una guida per la lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare chiamate a qualsiasi API di Experience Platform.

## Recupera un elenco di mixin {#list}

È possibile elencare tutti i mixin sotto il contenitore `global` o `tenant` effettuando una richiesta di GET rispettivamente a `/global/mixins` o `/tenant/mixins`.

>[!NOTE]
>
>Quando si elencano le risorse, il Registro di sistema dello schema limita i set di risultati a 300 elementi. Per restituire le risorse oltre questo limite, è necessario utilizzare i parametri di paging. Si consiglia inoltre di utilizzare parametri di query aggiuntivi per filtrare i risultati e ridurre il numero di risorse restituite. Per ulteriori informazioni, consulta la sezione sui [parametri di query](./appendix.md#query) nel documento di appendice .

**Formato API**

```http
GET /{CONTAINER_ID}/mixins?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Il contenitore da cui si desidera recuperare i mixin da: `global` per i mixin creati da Adobi o `tenant` per i mixin di proprietà della tua organizzazione. |
| `{QUERY_PARAMS}` | Parametri di query opzionali per filtrare i risultati in base a. Per un elenco dei parametri disponibili, vedere il [documento dell&#39;appendice](./appendix.md#query). |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta seguente recupera un elenco di mixin dal contenitore `tenant` utilizzando un parametro di query `orderby` per ordinare i mixin base al relativo attributo `title`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dall’intestazione `Accept` inviata nella richiesta. Le seguenti intestazioni `Accept` sono disponibili per elencare i mixin:

| `Accept` header | Descrizione |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Restituisce un breve riepilogo di ciascuna risorsa. Intestazione consigliata per l’elenco delle risorse. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Restituisce il mixin JSON completo per ogni risorsa, con i valori originali `$ref` e `allOf` inclusi. (Limite: 300) |

{style=&quot;table-layout:auto&quot;}

**Risposta**

La richiesta precedente utilizzava l’intestazione `application/vnd.adobe.xed-id+json` `Accept`, pertanto la risposta include solo gli attributi `title`, `$id`, `meta:altId` e `version` per ogni mixin. Utilizzando l&#39;altra intestazione `Accept` (`application/vnd.adobe.xed+json`) vengono restituiti tutti gli attributi di ciascun mixin. Seleziona l’intestazione `Accept` appropriata a seconda delle informazioni richieste nella risposta.

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

## Cerca un mixin {#lookup}

Puoi cercare un mixin specifico includendo l&#39;ID del mixin nel percorso di una richiesta di GET.

**Formato API**

```http
GET /{CONTAINER_ID}/mixins/{MIXIN_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Il contenitore che ospita il mixin da recuperare: `global` per un mixin creato in Adobe o `tenant` per un mixin di proprietà della tua organizzazione. |
| `{MIXIN_ID}` | Il `meta:altId` o URL-encoded `$id` del mixin che desideri cercare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta seguente recupera un mixin dal relativo valore `meta:altId` fornito nel percorso.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dall’intestazione `Accept` inviata nella richiesta. Tutte le richieste di ricerca richiedono che un `version` sia incluso nell&#39;intestazione `Accept`. Sono disponibili le seguenti intestazioni `Accept`:

| `Accept` header | Descrizione |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Raw con `$ref` e `allOf`, ha titoli e descrizioni. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` e  `allOf` risolta, ha titoli e descrizioni. |
| `application/vnd.adobe.xed-notext+json; version=1` | Non elaborato con `$ref` e `allOf`, senza titoli o descrizioni. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` e  `allOf` risolti, senza titoli o descrizioni. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` e  `allOf` risolti, descrittori inclusi. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli del mixin. I campi restituiti dipendono dall’intestazione `Accept` inviata nella richiesta. Sperimenta con diverse intestazioni `Accept` per confrontare le risposte e determinare quale intestazione è migliore per il tuo caso d’uso.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "fieldgroups",
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

Puoi definire un mixin personalizzato sotto il contenitore `tenant` effettuando una richiesta POST.

**Formato API**

```http
POST /tenant/mixins
```

**Richiesta**

Quando definisci un nuovo mixin, deve includere un attributo `meta:intendedToExtend`, elencando la `$id` delle classi con cui il mixin è compatibile. In questo esempio, il mixin è compatibile con una classe `Property` definita in precedenza. I campi personalizzati devono essere nidificati sotto `_{TENANT_ID}` (come mostrato nell&#39;esempio) per evitare conflitti con campi simili forniti da classi e altri mixin.

>[!NOTE]
>
>Per informazioni dettagliate su come definire diversi tipi di campi da includere nel mixin, consulta la [guida ai vincoli di campo](../schema/field-constraints.md#define-fields).

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

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un payload contenente i dettagli del mixin appena creato, inclusi `$id`, `meta:altId` e `version`. Questi valori sono di sola lettura e sono assegnati da [!DNL Schema Registry].

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "fieldgroups",
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

L&#39;esecuzione di una richiesta di GET a [elenca tutti i mixin](#list) nel contenitore tenant ora include il mixin Dettagli proprietà oppure è possibile [eseguire una richiesta di ricerca (GET)](#lookup) utilizzando l&#39;URI con codifica URL `$id` per visualizzare direttamente il nuovo mixin.

## Aggiornare un mixin {#put}

È possibile sostituire un intero mixin tramite un’operazione PUT, essenzialmente riscrivendo la risorsa. Quando aggiorni un mixin tramite una richiesta PUT, il corpo deve includere tutti i campi che sarebbero necessari durante la [creazione di un nuovo mixin](#create) in una richiesta POST.

>[!NOTE]
>
>Se desideri solo aggiornare parte di un mixin invece di sostituirlo completamente, consulta la sezione su [aggiornamento di una parte di un mixin](#patch).

**Formato API**

```http
PUT /tenant/mixins/{MIXIN_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MIXIN_ID}` | Il `meta:altId` o l&#39;URL-encoded `$id` del mixin che desideri riscrivere. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La seguente richiesta riscrive un mixin esistente, aggiungendo un nuovo campo `propertyCountry` .

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
  "meta:resourceType": "fieldgroups",
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

È possibile aggiornare una parte di un mixin utilizzando una richiesta PATCH. Il [!DNL Schema Registry] supporta tutte le operazioni standard di patch JSON, tra cui `add`, `remove` e `replace`. Per ulteriori informazioni sulla patch JSON, consulta la guida [Principi di base API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Per sostituire un&#39;intera risorsa con nuovi valori anziché aggiornare singoli campi, consulta la sezione relativa alla [sostituzione di un mixin con un&#39;operazione PUT](#put).

**Formato API**

```http
PATCH /tenant/mixin/{MIXIN_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{MIXIN_ID}` | URI con codifica URL `$id` o `meta:altId` del mixin che si desidera aggiornare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta di esempio seguente aggiorna il `description` di un mixin esistente e aggiunge un nuovo campo `propertyCity` .

Il corpo della richiesta assume la forma di una matrice, con ogni oggetto elencato che rappresenta una modifica specifica a un singolo campo. Ogni oggetto include l&#39;operazione da eseguire (`op`), il campo sul quale deve essere eseguita l&#39;operazione (`path`) e le informazioni da includere in tale operazione (`value`).

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

La risposta indica che entrambe le operazioni sono state eseguite correttamente. Il `description` è stato aggiornato e `propertyCountry` è stato aggiunto in `definitions`.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "fieldgroups",
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

Talvolta può essere necessario rimuovere un mixin dal Registro dello schema. A tal fine, esegui una richiesta DELETE con l’ID mixin fornito nel percorso .

**Formato API**

```http
DELETE /tenant/mixins/{MIXIN_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{MIXIN_ID}` | URI con codifica URL `$id` o `meta:altId` del mixin che si desidera eliminare. |

{style=&quot;table-layout:auto&quot;}

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

Puoi confermare l&#39;eliminazione tentando una richiesta [lookup (GET)](#lookup) al mixin. Sarà necessario includere un&#39;intestazione `Accept` nella richiesta, ma dovrebbe ricevere uno stato HTTP 404 (Non trovato) perché il mixin è stato rimosso dal Registro di sistema dello schema.
