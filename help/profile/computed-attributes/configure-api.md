---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Come configurare un campo attributo calcolato
type: Documentation
description: Gli attributi calcolati sono funzioni utilizzate per aggregare dati a livello di evento in attributi a livello di profilo. Per configurare un attributo calcolato, devi innanzitutto identificare il campo che conterrà il valore dell’attributo calcolato. Questo campo può essere creato utilizzando l’API del Registro di sistema dello schema per definire uno schema e un gruppo di campi personalizzati che conterrà il campo dell’attributo calcolato.
exl-id: 91c5d125-8ab5-4291-a974-48dd44c68a13
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 2%

---

# (Alpha) Configura un campo di attributi calcolato utilizzando l’API del Registro di sistema dello schema.

>[!IMPORTANT]
>
>La funzionalità dell&#39;attributo calcolato è attualmente in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Per configurare un attributo calcolato, devi innanzitutto identificare il campo che conterrà il valore dell’attributo calcolato. Questo campo può essere creato utilizzando l’API del Registro di sistema dello schema per definire uno schema e un gruppo di campi dello schema personalizzato che conterrà il campo dell’attributo calcolato. È consigliabile creare uno schema e un gruppo di campi &quot;Attributi calcolati&quot; separati in cui l’organizzazione può aggiungere qualsiasi attributo da utilizzare come attributi calcolati. Questo consente alla tua organizzazione di separare in modo pulito lo schema degli attributi calcolati da altri schemi utilizzati per l’inserimento dei dati.

Il flusso di lavoro in questo documento illustra come utilizzare l’API del Registro di sistema dello schema per creare uno schema &quot;Attributo calcolato&quot; abilitato per il profilo che fa riferimento a un gruppo di campi personalizzato. Questo documento contiene un codice di esempio specifico per gli attributi calcolati, tuttavia si prega di fare riferimento al [Guida all’API del registro dello schema](../../xdm/api/overview.md) per informazioni dettagliate sulla definizione di gruppi di campi e schemi tramite l’API.

## Creare un gruppo di campi attributi calcolati

Per creare un gruppo di campi utilizzando l’API del Registro di sistema dello schema, invia innanzitutto una richiesta di POST `/tenant/fieldgroups` e fornendo i dettagli del gruppo di campi nel corpo della richiesta. Per informazioni dettagliate sull’utilizzo dei gruppi di campi tramite l’API del Registro di sistema dello schema, consulta [guida all’endpoint API per i gruppi di campi](../../xdm/api/field-groups.md).

**Formato API**

```http
POST /tenant/fieldgroups
```

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "title":"Computed Attributes Field Group",
        "description":"Description of the field group.",
        "type":"object",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "definitions": {
          "computedAttributesFieldGroup": {
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
            "$ref": "#/definitions/computedAttributesFieldGroup"
          }
        ]
      }'
```

| Proprietà | Descrizione |
|---|---|
| `title` | Nome del gruppo di campi che si sta creando. |
| `meta:intendedToExtend` | Classe XDM con cui è possibile utilizzare il gruppo di campi. |

**Risposta**

Una richiesta corretta restituisce lo stato di risposta HTTP 201 (Creato) con un corpo di risposta contenente i dettagli del gruppo di campi appena creato, incluso il `$id`, `meta:altIt`e `version`. Questi valori sono di sola lettura e sono assegnati dal Registro di sistema dello schema.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.mixins.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Computed Attributes Field Group",
  "type": "object",
  "description": "Description of the field group.",
  "definitions": {
    "computedAttributesFieldGroup": {
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
      "$ref": "#/definitions/computedAttributesFieldGroup",
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

## Aggiorna gruppo di campi con attributi calcolati aggiuntivi

Poiché sono necessari più attributi calcolati, è possibile aggiornare il gruppo di campi attributi calcolati con attributi aggiuntivi effettuando una richiesta di PUT al gruppo di campi `/tenant/fieldgroups` punto finale. Questa richiesta richiede di includere l’ID univoco del gruppo di campi creato nel percorso e tutti i nuovi campi che si desidera aggiungere nel corpo.

Per ulteriori informazioni sull’aggiornamento di un gruppo di campi utilizzando l’API del Registro di sistema dello schema, consulta [guida all’endpoint API per i gruppi di campi](../../xdm/api/field-groups.md).

**Formato API**

```http
PUT /tenant/fieldgroups/{FIELD_GROUP_ID}
```

**Richiesta**

Questa richiesta aggiunge nuovi campi correlati a `purchaseSummary` informazioni.

>[!NOTE]
>
>Quando si aggiorna un gruppo di campi tramite una richiesta di PUT, il corpo deve includere tutti i campi che sarebbero necessari durante la creazione di un nuovo gruppo di campi in una richiesta di POST.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "type": "object",
        "title": "Computed Attributes Field Group",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "description": "Description of field group.",
        "definitions": {
          "computedAttributesFieldGroup": {
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
            "$ref": "#/definitions/computedAttributesFieldGroup"
          }
        ]
      }'
```

**Risposta**

Una risposta corretta restituisce i dettagli del gruppo di campi aggiornato.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.mixins.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Computed Attributes Field Group",
  "type": "object",
  "description": "Description of field group.",
  "definitions": {
    "computedAttributesFieldGroup": {
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
      "$ref": "#/definitions/computedAttributesFieldGroup",
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

Per creare uno schema utilizzando l&#39;API del Registro di sistema dello schema, inizia effettuando una richiesta di POST al `/tenant/schemas` e fornendo i dettagli dello schema nel corpo della richiesta. Lo schema deve essere abilitato anche per [!DNL Profile] e vengono visualizzati come parte dello schema di unione per la classe schema.

Per ulteriori informazioni su [!DNL Profile]schemi abilitati e schemi di unione, si prega di rivedere [[!DNL Schema Registry] Guida all’API](../../xdm/api/overview.md) e [documentazione di base sulla composizione dello schema](../../xdm/schema/composition.md).

**Formato API**

```http
POST /tenants/schemas
```

**Richiesta**

La richiesta seguente crea un nuovo schema che fa riferimento al `computedAttributesFieldGroup` creato in precedenza in questo documento (utilizzando il relativo ID univoco) ed è abilitato per lo schema di unione profili (utilizzando `meta:immutableTags` array). Per istruzioni dettagliate su come creare uno schema utilizzando l’API del Registro di sistema dello schema, consulta [Guida all’endpoint API per schemi](../../xdm/api/schemas.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un payload contenente i dettagli dello schema appena creato, tra cui `$id`, `meta:altId`e `version`. Questi valori sono di sola lettura e sono assegnati dal Registro di sistema dello schema.

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
  "imsOrg": "{ORG_ID}",
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

Ora che hai creato uno schema e un gruppo di campi in cui verranno memorizzati gli attributi calcolati, puoi creare l&#39;attributo calcolato utilizzando `/computedattributes` Endpoint API. Per passaggi dettagliati per la creazione di un attributo calcolato nell’API, segui i passaggi forniti nella [guida all’endpoint API degli attributi calcolati](ca-api.md).
