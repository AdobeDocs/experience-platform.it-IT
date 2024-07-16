---
title: Esporta endpoint API
description: L’endpoint /export nell’API Schema Registry consente di condividere risorse XDM tra sandbox.
exl-id: 1dcbfa59-af98-4db5-b6f4-f848e5bf5e81
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---

# Esporta endpoint

Tutte le risorse all&#39;interno di [!DNL Schema Library] sono contenute in una sandbox specifica in Adobe Experience Platform. In alcuni casi, potrebbe essere utile condividere risorse Experience Data Model (XDM) tra sandbox e organizzazioni. L&#39;endpoint `/rpc/export` nell&#39;API [!DNL Schema Registry] consente di generare un payload di esportazione per qualsiasi schema, gruppo di campi dello schema o tipo di dati in [!DNL Schema Library] e quindi di utilizzare tale payload per importare tale risorsa (e tutte le risorse dipendenti) in una sandbox di destinazione e in un&#39;organizzazione tramite l&#39;endpoint [`/rpc/import`](./import.md).

## Introduzione

L&#39;endpoint `/rpc/export` fa parte dell&#39;[[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e per le informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

L&#39;endpoint `/rpc/export` fa parte delle chiamate di procedura remota (RPC) supportate da [!DNL Schema Registry]. A differenza di altri endpoint nell&#39;API [!DNL Schema Registry], gli endpoint RPC non richiedono intestazioni aggiuntive come `Accept` o `Content-Type` e non utilizzano un `CONTAINER_ID`. Devono invece utilizzare lo spazio dei nomi `/rpc`, come dimostrato nelle chiamate API riportate di seguito.

## Generare un payload di esportazione per una risorsa {#export}

Per qualsiasi schema, gruppo di campi o tipo di dati esistente in [!DNL Schema Library], puoi generare un payload di esportazione effettuando una richiesta di GET all&#39;endpoint `/export`, fornendo l&#39;ID della risorsa nel percorso.

**Formato API**

```http
GET /rpc/export/{RESOURCE_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{RESOURCE_ID}` | `meta:altId` o `$id` con codifica URL della risorsa XDM da esportare. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente recupera un payload di esportazione per un gruppo di campi `Restaurant`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/export/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un array di oggetti, che rappresentano la risorsa XDM di destinazione e tutte le relative risorse dipendenti. In questo esempio, il primo oggetto nell&#39;array è un tipo di dati `Property` creato dal tenant e utilizzato dal gruppo di campi `Restaurant`, mentre il secondo oggetto è il gruppo di campi `Restaurant` stesso. Questo payload può quindi essere utilizzato per [importare la risorsa](#import) in una sandbox o organizzazione diversa.

Tutte le istanze dell&#39;ID tenant della risorsa vengono sostituite con `<XDM_TENANTID_PLACEHOLDER>`. Questo consente al registro dello schema di applicare automaticamente l’ID tenant corretto alle risorse in base alla posizione in cui vengono inviate nella chiamata di importazione successiva.

```json
[
    {
        "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.datatypes.fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:resourceType": "datatypes",
        "version": "1.0",
        "title": "Property",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "properties": {
                    "propertyId": {
                        "title": "Property ID",
                        "description": "ID for a company-owned property.",
                        "type": "string",
                        "isRequired": false,
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.propertyId",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    },
                    "jurisdiction": {
                        "title": "Jurisdiction",
                        "description": "",
                        "type": "string",
                        "isRequired": false,
                        "enum": [
                            "NA",
                            "UK",
                            "EU"
                        ],
                        "meta:enum": {
                            "NA": "North America",
                            "UK": "United Kingdom",
                            "EU": "European Union"
                        },
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.jurisdiction",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
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
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:xdmType": "object",
        "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "meta:sandboxType": "production"
    },
    {
        "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:resourceType": "mixins",
        "version": "1.0",
        "title": "Restaurant",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "type": "object",
                "properties": {
                    "_<XDM_TENANTID_PLACEHOLDER>": {
                        "type": "object",
                        "properties": {
                            "capacity": {
                                "title": "Capacity",
                                "description": "Restaurant capacity",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "kitchen": {
                                "title": "Kitchen Style",
                                "description": "Style of kitchen",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "rating": {
                                "title": "Rating",
                                "description": "",
                                "type": "integer",
                                "isRequired": false,
                                "meta:xdmType": "int"
                            },
                            "property": {
                                "title": "Property",
                                "description": "",
                                "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
                                "type": "object",
                                "meta:xdmType": "object"
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
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [],
        "meta:xdmType": "object",
        "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "meta:sandboxType": "production"
    }
]
```

## Importa la risorsa {#import}

Dopo aver generato il payload di esportazione dal file CSV, puoi inviare tale payload all&#39;endpoint `/rpc/import` per generare lo schema.

Per informazioni dettagliate su come generare schemi dai payload di esportazione, consulta la [guida dell&#39;endpoint &quot;import&quot;](./import.md).
