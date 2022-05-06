---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;modello dati;registro schema;gruppo di campi;gruppo di campi;gruppi di campi;creare
solution: Experience Platform
title: Endpoint API per gruppi di campi
description: L’endpoint /fieldgroups nell’API del Registro di sistema dello schema consente di gestire in modo programmatico i gruppi di campi dello schema XDM all’interno dell’applicazione di esperienza.
topic-legacy: developer guide
exl-id: d26257e4-c7d5-4bff-b555-7a2997c88c74
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 5%

---

# Endpoint dei gruppi di campi schema

I gruppi di campi schema sono componenti riutilizzabili che definiscono uno o più campi che rappresentano un concetto particolare, ad esempio una singola persona, un indirizzo postale o un ambiente browser Web. I gruppi di campi sono destinati a essere inclusi come parte di uno schema che implementa una classe compatibile, a seconda del comportamento dei dati che rappresentano (record o serie temporali). La `/fieldgroups` punto finale [!DNL Schema Registry] L’API ti consente di gestire in modo programmatico i gruppi di campi all’interno dell’applicazione di esperienza.

## Introduzione

L’endpoint utilizzato in questa guida fa parte dell’[[!DNL Schema Registry] API di ](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e importanti informazioni sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recupera un elenco di gruppi di campi {#list}

È possibile elencare tutti i gruppi di campi `global` o `tenant` effettuando una richiesta GET a `/global/fieldgroups` o `/tenant/fieldgroups`, rispettivamente.

>[!NOTE]
>
>Quando si elencano le risorse, il Registro di sistema dello schema limita i set di risultati a 300 elementi. Per restituire le risorse oltre questo limite, è necessario utilizzare i parametri di paging. Si consiglia inoltre di utilizzare parametri di query aggiuntivi per filtrare i risultati e ridurre il numero di risorse restituite. Vedi la sezione su [parametri di query](./appendix.md#query) nel documento di appendice per ulteriori informazioni.

**Formato API**

```http
GET /{CONTAINER_ID}/fieldgroups?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Il contenitore da cui si desidera recuperare i gruppi di campi: `global` per gruppi di campi creati da Adobi o `tenant` per i gruppi di campi di proprietà dell’organizzazione. |
| `{QUERY_PARAMS}` | Parametri di query opzionali per filtrare i risultati in base a. Consulta la sezione [documento appendice](./appendix.md#query) per un elenco dei parametri disponibili. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta seguente recupera un elenco di gruppi di campi dal `tenant` contenitore, utilizzando un `orderby` parametro di query per ordinare i gruppi di campi in base ai relativi `title` attributo.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dal `Accept` intestazione inviata nella richiesta. I seguenti `Accept` le intestazioni sono disponibili per elencare i gruppi di campi:

| `Accept` header | Descrizione |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Restituisce un breve riepilogo di ciascuna risorsa. Intestazione consigliata per l’elenco delle risorse. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Restituisce il gruppo di campi JSON completo per ogni risorsa, con l’originale `$ref` e `allOf` incluso. (Limite: 300) |

{style=&quot;table-layout:auto&quot;}

**Risposta**

La richiesta di cui sopra ha utilizzato il `application/vnd.adobe.xed-id+json` `Accept` , quindi la risposta include solo l’ `title`, `$id`, `meta:altId`e `version` attributi per ciascun gruppo di campi. Utilizzo dell&#39;altro `Accept` header (`application/vnd.adobe.xed+json`) restituisce tutti gli attributi di ciascun gruppo di campi. Selezionare il `Accept` a seconda delle informazioni richieste nella risposta.

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
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/fieldgroups"
    }
  }
}
```

## Cercare un gruppo di campi {#lookup}

Puoi cercare un gruppo di campi specifico includendo l’ID del gruppo di campi nel percorso di una richiesta GET.

**Formato API**

```http
GET /{CONTAINER_ID}/fieldgroups/{FIELD_GROUP_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Il contenitore che ospita il gruppo di campi da recuperare: `global` per un gruppo di campi creato da un Adobe o `tenant` per un gruppo di campi di proprietà dell&#39;organizzazione. |
| `{FIELD_GROUP_ID}` | La `meta:altId` o con codifica URL `$id` del gruppo di campi che si desidera cercare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta seguente recupera un gruppo di campi in base al relativo `meta:altId` nel percorso.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dal `Accept` intestazione inviata nella richiesta. Tutte le richieste di ricerca richiedono un `version` sono inclusi nella `Accept` intestazione. I seguenti `Accept` le intestazioni sono disponibili:

| `Accept` header | Descrizione |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Raw con `$ref` e `allOf`, include titoli e descrizioni. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` e `allOf` risolto, con titoli e descrizioni. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Raw con `$ref` e `allOf`, senza titoli o descrizioni. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` e `allOf` risolto, senza titoli o descrizioni. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` e `allOf` risolti, descrittori inclusi. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli del gruppo di campi. I campi restituiti dipendono dal `Accept` intestazione inviata nella richiesta. Esperimento con diversi `Accept` intestazioni per confrontare le risposte e determinare quale intestazione è migliore per il tuo caso d’uso.

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

## Creare un gruppo di campi {#create}

Puoi definire un gruppo di campi personalizzato nella sezione `tenant` effettuando una richiesta di POST.

**Formato API**

```http
POST /tenant/fieldgroups
```

**Richiesta**

Quando definisci un nuovo gruppo di campi, deve includere un `meta:intendedToExtend` attributo, elenco `$id` delle classi con cui il gruppo di campi è compatibile. In questo esempio, il gruppo di campi è compatibile con un `Property` classe definita in precedenza. I campi personalizzati devono essere nidificati in `_{TENANT_ID}` (come mostrato nell’esempio) per evitare conflitti con campi simili forniti da classi e altri gruppi di campi.

>[!NOTE]
>
>Per informazioni dettagliate su come definire diversi tipi di campi da includere nel gruppo di campi, consulta la guida in [definizione di campi personalizzati nell’API](../tutorials/custom-fields-api.md#define-fields).

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un payload contenente i dettagli del gruppo di campi appena creato, tra cui `$id`, `meta:altId`e `version`. Questi valori sono di sola lettura e sono assegnati dal [!DNL Schema Registry].

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

Esecuzione di una richiesta GET a [elenco di tutti i gruppi di campi](#list) nel contenitore tenant ora include il gruppo di campi Dettagli proprietà oppure è possibile [eseguire una richiesta di ricerca (GET)](#lookup) utilizzando l’URL-encoded `$id` URI per visualizzare direttamente il nuovo gruppo di campi.

## Aggiornare un gruppo di campi {#put}

È possibile sostituire un intero gruppo di campi con un’operazione PUT, essenzialmente riscrivendo la risorsa. Quando si aggiorna un gruppo di campi tramite una richiesta di PUT, il corpo deve includere tutti i campi necessari quando [creazione di un nuovo gruppo di campi](#create) in una richiesta POST.

>[!NOTE]
>
>Se si desidera aggiornare solo parte di un gruppo di campi invece di sostituirlo completamente, vedere la sezione in [aggiornamento di una parte di un gruppo di campi](#patch).

**Formato API**

```http
PUT /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{FIELD_GROUP_ID}` | La `meta:altId` o con codifica URL `$id` del gruppo di campi che si desidera riscrivere. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La seguente richiesta riscrive un gruppo di campi esistente, aggiungendo un nuovo `propertyCountry` campo .

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Una risposta corretta restituisce i dettagli del gruppo di campi aggiornato.

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

## Aggiornare una parte di un gruppo di campi {#patch}

È possibile aggiornare una parte di un gruppo di campi utilizzando una richiesta PATCH. La [!DNL Schema Registry] supporta tutte le operazioni standard di patch JSON, tra cui `add`, `remove`e `replace`. Per ulteriori informazioni sulla patch JSON, consulta la sezione [Guida di base sulle API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Per sostituire un’intera risorsa con nuovi valori anziché aggiornare singoli campi, consulta la sezione [sostituzione di un gruppo di campi con un’operazione PUT](#put).

**Formato API**

```http
PATCH /tenant/fieldgroups/{FIELD_GROUP_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{FIELD_GROUP_ID}` | L’URL è codificato `$id` URI o `meta:altId` del gruppo di campi che si desidera aggiornare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta di esempio riportata di seguito aggiorna la `description` di un gruppo di campi esistente e aggiunge un nuovo `propertyCity` campo .

Il corpo della richiesta assume la forma di una matrice, con ogni oggetto elencato che rappresenta una modifica specifica a un singolo campo. Ogni oggetto include l&#39;operazione da eseguire (`op`), su quale campo deve essere eseguita l&#39;operazione (`path`) e quali informazioni dovrebbero essere incluse in tale operazione (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

La risposta indica che entrambe le operazioni sono state eseguite correttamente. La `description` è stato aggiornato e `propertyCountry` è stato aggiunto in `definitions`.

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

## Eliminare un gruppo di campi {#delete}

Talvolta può essere necessario rimuovere un gruppo di campi dal Registro di sistema dello schema. A tal fine, esegui una richiesta DELETE con l’ID del gruppo di campi fornito nel percorso .

**Formato API**

```http
DELETE /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{FIELD_GROUP_ID}` | L’URL è codificato `$id` URI o `meta:altId` del gruppo di campi da eliminare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo vuoto.

Puoi confermare l&#39;eliminazione tentando un [richiesta di ricerca (GET)](#lookup) al gruppo di campi. Sarà necessario includere un `Accept` intestazione nella richiesta, ma deve ricevere uno stato HTTP 404 (Non trovato) perché il gruppo di campi è stato rimosso dal Registro di sistema dello schema.
