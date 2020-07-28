---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un mixin
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---


# Creare un mixin

Le miscele sono un insieme di campi utilizzati per descrivere un concetto particolare, ad esempio &quot;indirizzo&quot; o &quot;preferenze di profilo&quot;. Sono disponibili numerosi mixin standard, oppure potete definirne uno personalizzato quando desiderate acquisire informazioni univoche per la vostra organizzazione. Ogni mixin contiene un `meta:intendedToExtend` campo in cui sono elencate le classi con cui è compatibile il mixin.

Potrebbe essere utile rivedere tutti i mixin disponibili per acquisire familiarità con i campi inclusi in ciascuno. Potete elencare (GET) tutti i mixin compatibili con una particolare classe eseguendo una richiesta per ciascuno dei contenitori &quot;global&quot; e &quot;tenant&quot;, restituendo solo i mixin cui il campo &quot;meta:subjectToExtend&quot; corrisponde alla classe in uso. Gli esempi seguenti restituiranno tutti i mixin utilizzabili con la [!DNL XDM Individual Profile] classe:

```http
GET /global/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
GET /tenant/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
```

La richiesta API di esempio seguente crea un nuovo mixin nel contenitore tenant.

**Formato API**

```http
POST /tenant/mixins
```

**Richiesta**

Durante la definizione di un nuovo mixin, deve includere un `meta:intendedToExtend` `$id` attributo, in cui sono elencate le classi con cui il mixin è compatibile. In questo esempio, il mixin è compatibile con la classe Property precedentemente definita. I campi personalizzati devono essere nidificati sotto `_{TENANT_ID}` (come mostrato nell&#39;esempio) per evitare eventuali conflitti con altri mixin o campi dagli schemi di classe. Il `propertyConstruction` campo è un riferimento al tipo di dati creato nella chiamata precedente.

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
    "title": "Property Details",
    "description": "Detailed information related to the properties owned and operated by the company.",
    "type": "object",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
    ],
    "definitions": {
        "property": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "propertyName": {
                            "type": "string",
                            "title": "Property Name",
                            "description": "Name of the property",
                            "meta:xdmType": "string"
                        },
                        "propertyCity": {
                            "title": "Property City",
                            "description": "City where the property is located.",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "phoneNumber": {
                            "title": "Phone Number",
                            "description": "Primary phone number for the property.",
                            "type": "string",
                            "meta:xdmType": "string"
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
                            },
                            "meta:xdmType": "string"
                        },
                        "propertyConstruction": {
                            "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/property"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.mixins.e49cbb2eec33618f686b8344b4597ecf",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf",
    "version": "1.0",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1552088205144,
        "repo:lastModifiedDate": 1552088205144,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

L&#39;esecuzione di una richiesta di GET per elencare tutti i mixin nel contenitore tenant ora include il mixin Dettagli veicolo, oppure potete eseguire una richiesta di ricerca (GET) utilizzando l&#39;URI con codifica URL per visualizzare direttamente il nuovo mixin. `$id` Ricordare di includere l&#39;oggetto `version` nell&#39;intestazione Accetto per tutte le richieste di ricerca.
