---
keywords: Experience Platform ;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Come configurare un campo attributo calcolato
topic: guida
type: Documentazione
description: Gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento in attributi a livello di profilo. Per configurare un attributo calcolato, è innanzitutto necessario identificare il campo che includerà il valore dell'attributo calcolato. Questo campo può essere creato utilizzando l'API del Registro di sistema dello schema per definire uno schema e un mixin personalizzato che contenga il campo dell'attributo calcolato.
translation-type: tm+mt
source-git-commit: 2a4fb8af8cd29254c499bfa6bfb8b316a4834526
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 2%

---


# (Alfa) Configurare un campo attributo calcolato utilizzando l&#39;API del Registro di sistema dello schema

>[!IMPORTANT]
>
>La funzionalità dell&#39;attributo calcolato è attualmente in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Per configurare un attributo calcolato, è innanzitutto necessario identificare il campo che includerà il valore dell&#39;attributo calcolato. Questo campo può essere creato utilizzando l&#39;API del Registro di sistema dello schema per definire uno schema e un mixin personalizzato che contenga il campo dell&#39;attributo calcolato. È consigliabile creare uno schema e un mixin separati di &quot;Attributi calcolati&quot;, in cui l&#39;organizzazione può aggiungere qualsiasi attributo da utilizzare come attributi calcolati. In questo modo l&#39;organizzazione può separare in modo pulito lo schema di attributi calcolato da altri schemi utilizzati per l&#39;assimilazione dei dati.

Il flusso di lavoro in questo documento descrive come utilizzare l&#39;API del Registro di sistema dello schema per creare uno schema &quot;Attributo calcolato&quot; abilitato per il profilo che fa riferimento a un mixin personalizzato. Questo documento contiene un esempio di codice specifico per gli attributi calcolati, tuttavia, per informazioni dettagliate sulla definizione di mixin e schemi tramite l&#39;API, fare riferimento alla [Guida API del Registro di sistema dello schema](../../xdm/api/overview.md).

## Creare un mixin di attributi calcolati

Per creare un mixin utilizzando l&#39;API del Registro di sistema dello schema, iniziate effettuando una richiesta di POST all&#39;endpoint `/tenant/mixins` e fornendo i dettagli del mixin nel corpo della richiesta. Per informazioni dettagliate sull&#39;utilizzo dei mixin tramite l&#39;API del Registro di sistema dello schema, fare riferimento alla guida [agli endpoint API dei mixins](../../xdm/api/mixins.md).

**Formato API**

```http
POST /tenant/mixins
```

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "title":"Computed Attributes Mixin",
        "description":"Description of the mixin.",
        "type":"object",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "definitions": {
          "computedAttributesMixin": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "meta:xdmType": "object",
                "properties": {
                  "birthdayCurrentMonth": {
                    "type": "boolean",
                    "meta:xdmType": "boolean"
                  }
                }
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/computedAttributesMixin"
          }
        ]
      }'
```

| Proprietà | Descrizione |
|---|---|
| `title` | Nome del mixin che si sta creando. |
| `meta:intendedToExtend` | La classe XDM con cui è possibile utilizzare il mixin. |

**Risposta**

Una richiesta eseguita correttamente restituisce lo stato di risposta HTTP 201 (Creato) con un corpo di risposta contenente i dettagli del mixin appena creato, inclusi `$id`, `meta:altIt` e `version`. Questi valori sono di sola lettura e sono assegnati dal Registro di sistema dello schema.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.mixins.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Computed Attributes Mixin",
  "type": "object",
  "description": "Description of the mixin.",
  "definitions": {
    "computedAttributesMixin": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "birthdayCurrentMonth": {
              "type": "boolean",
              "meta:xdmType": "boolean"
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/computedAttributesMixin",
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
    "repo:createdDate": 1612861108205,
    "repo:lastModifiedDate": 1612861108205,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "627faa3346d3004aef2010e9bd2b7e721b19ae7857b276f3ef733e6e732d495f",
    "meta:globalLibVersion": "1.19.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Aggiorna mixin con altri attributi calcolati

Poiché sono necessari più attributi calcolati, potete aggiornare il mixin di attributi calcolati con attributi aggiuntivi effettuando una richiesta di PUT all&#39;endpoint `/tenant/mixins`. Per questa richiesta è necessario includere l’ID univoco del mixin creato nel percorso e tutti i nuovi campi che si desidera aggiungere nel corpo.

Per ulteriori informazioni sull&#39;aggiornamento di un mixin utilizzando l&#39;API del Registro di sistema dello schema, fare riferimento alla guida [agli endpoint API mixins](../../xdm/api/mixins.md).

**Formato API**

```http
PUT /tenant/mixins/{MIXIN_ID}
```

**Richiesta**

Questa richiesta aggiunge nuovi campi relativi alle informazioni `purchaseSummary`.

>[!NOTE]
>
>Quando aggiornate un mixin tramite una richiesta di PUT, il corpo deve includere tutti i campi che sarebbero necessari per creare un nuovo mixin in una richiesta di POST.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "type": "object",
        "title": "Computed Attributes Mixin",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "description": "Description of mixin.",
        "definitions": {
          "computedAttributesMixin": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "meta:xdmType": "object",
                "properties": {
                  "birthdayCurrentMonth": {
                    "type": "boolean",
                    "meta:xdmType": "boolean"
                  },
                  "purchaseSummary": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                      "totalSpend": {
                        "type": "number",
                        "meta:xdmType": "number"
                      },
                      "countPurchases": {
                        "meta:xdmType": "int",
                        "type": "integer",
                        "minimum": -2147483648,
                        "maximum": 2147483647
                      },
                      "averageSpend": {
                        "type": "number",
                        "meta:xdmType": "number"
                      }
                    }
                  }
                }
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/computedAttributesMixin"
          }
        ]
      }'
```

**Risposta**

Una risposta corretta restituisce i dettagli del mixin aggiornato.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.mixins.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Computed Attributes Mixin",
  "type": "object",
  "description": "Description of mixin.",
  "definitions": {
    "computedAttributesMixin": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "birthdayCurrentMonth": {
              "type": "boolean",
              "meta:xdmType": "boolean"
            },
            "purchaseSummary": {
              "type": "object",
              "meta:xdmType": "object",
              "properties": {
                "totalSpend": {
                  "type": "number",
                  "meta:xdmType": "number"
                },
                "countPurchases": {
                  "meta:xdmType": "int",
                  "type": "integer",
                  "minimum": -2147483648,
                  "maximum": 2147483647
                },
                "averageSpend": {
                  "type": "number",
                  "meta:xdmType": "number"
                }
              }
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/computedAttributesMixin",
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
    "repo:createdDate": 1612861108205,
    "repo:lastModifiedDate": 1612861108205,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "627faa3346d3004aef2010e9bd2b7e721b19ae7857b276f3ef733e6e732d495f",
    "meta:globalLibVersion": "1.19.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Creare uno schema abilitato per il profilo

Per creare uno schema utilizzando l&#39;API del Registro di sistema dello schema, iniziare effettuando una richiesta di POST all&#39;endpoint `/tenant/schemas` e fornendo i dettagli dello schema nel corpo della richiesta. Lo schema deve essere abilitato anche per [!DNL Profile] e deve essere visualizzato come parte dello schema unione per la classe dello schema.

Per ulteriori informazioni sugli schemi [!DNL Profile] e gli schemi di unione abilitati, consultare la [[!DNL Schema Registry] Guida API](../../xdm/api/overview.md) e la [documentazione di base sulla composizione dello schema](../../xdm/schema/composition.md).

**Formato API**

```http
POST /tenants/schemas
```

**Richiesta**

La richiesta seguente crea un nuovo schema che fa riferimento alla `computedAttributesMixin` creata in precedenza in questo documento (utilizzando il relativo ID univoco) ed è abilitata per lo schema di unione dei profili (utilizzando l&#39;array `meta:immutableTags`). Per istruzioni dettagliate su come creare uno schema utilizzando l&#39;API del Registro di sistema dello schema, fare riferimento alla [guida dell&#39;endpoint API di schema](../../xdm/api/schemas.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "type": "object",
        "title": "Computed Attributes Schema",
        "meta:extensible": false,
        "meta:abstract": false,
        "meta:immutableTags": [
          "union"
        ],
        "meta:extends": [
          "https://ns.adobe.com/xdm/context/profile",
          "https://ns.adobe.com/xdm/context/identitymap",
          "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
        ],
        "description": "Description of schema.",
        "definitions": {
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
          },
          {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
          },
          {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
          }
        ],
        "meta:class": "https://ns.adobe.com/xdm/context/profile"
      }' 
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un payload contenente i dettagli dello schema appena creato, inclusi `$id`, `meta:altId` e `version`. Questi valori sono di sola lettura e sono assegnati dal Registro di sistema dello schema.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/699c1f16821c51086394fef8233d7fdb61e6f5b574b5a230",
  "meta:altId": "_{TENANT}.schemas.699c1f16821c51086394fef8233d7fdb61e6f5b574b5a230",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Computed Attributes Schema",
  "type": "object",
  "description": "Description of schema.",
  "definitions": {},
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/identitymap",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/xdm/context/identitymap",
    "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/xdm/context/identitymap",
    "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1612385766411,
    "repo:lastModifiedDate": 1612385766411,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "a9c6b5c25c109970ffa5eaeb3db2b47b59c696e1d9407fb39ccf7e48b74b558e",
    "meta:globalLibVersion": "1.18.4"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT}",
  "meta:immutableTags": [
    "union"
  ]
}
```

## Passaggi successivi

Ora che avete creato uno schema e un mixin in cui memorizzare gli attributi calcolati, potete creare l&#39;attributo calcolato utilizzando l&#39;endpoint `/computedattributes` API. Per la procedura dettagliata per la creazione di un attributo calcolato nell&#39;API, segui i passaggi forniti nella [guida dell&#39;endpoint API degli attributi calcolati](ca-api.md).