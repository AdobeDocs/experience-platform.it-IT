---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Aggiornare una risorsa
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 2%

---


# Aggiornare una risorsa

Puoi modificare o aggiornare le risorse nel contenitore tenant utilizzando una richiesta di PATCH. Supporta [!DNL Schema Registry] tutte le operazioni standard di patch JSON, incluse aggiunta, rimozione e sostituzione.

Per ulteriori informazioni sulla patch JSON, comprese le operazioni disponibili, consultate la documentazione [ufficiale relativa alla patch](http://jsonpatch.com/)JSON.

>[!NOTE]
>
>Se si desidera sostituire un&#39;intera risorsa con nuovi valori invece di aggiornare i singoli campi, consultare il documento sulla [sostituzione di una risorsa con un&#39;operazione](replace-resource.md)PUT.

## Aggiunta di mixaggi a uno schema

Una delle operazioni PATCH più comuni consiste nell&#39;aggiungere mixin definiti in precedenza a uno schema XDM, come illustrato nell&#39;esempio seguente.

**Formato API**

```http
PATCH /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{RESOURCE_TYPE}` | Il tipo di risorsa da aggiornare dal [!DNL Schema Library]. I tipi validi sono `datatypes`, `mixins`, `schemas`e `classes`. |
| `{RESOURCE_ID}` | URI con codifica URL `$id` o `meta:altId` della risorsa. |

**Richiesta**

Utilizzando un&#39;operazione PATCH, è possibile aggiornare uno schema per includere campi definiti in un mixin creato in precedenza. A tal fine, è necessario eseguire una richiesta di PATCH allo schema utilizzando l&#39;URI `meta:altId` o l&#39; `$id` URI con codifica URL.

Il corpo della richiesta include l&#39;operazione (`op`) che si desidera eseguire, dove (`path`) si desidera eseguire l&#39;operazione e quali informazioni (`value`) si desidera includere nell&#39;operazione. In questo esempio, il `$id` valore del mixin viene aggiunto sia ai campi `meta:extends` che `allOf` ai campi dello schema di destinazione.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "add", "path": "/meta:extends/-", "value":  "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"},
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"}}
      ]'
```

**Risposta**

La risposta indica che entrambe le operazioni sono state eseguite correttamente. Il mixin `$id` è stato aggiunto all&#39; `meta:extends` array e un riferimento (`$ref`) al mixin `$id` viene ora visualizzato nell&#39; `allOf` array.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Aggiornamento di singoli campi per una risorsa

È inoltre possibile inviare richieste PATCH che apportano più modifiche ai singoli campi all&#39;interno di una risorsa del Registro di sistema dello schema.

**Formato API**

```SHELL
PATCH /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{RESOURCE_TYPE}` | Il tipo di risorsa da aggiornare dal [!DNL Schema Library]. I tipi validi sono `datatypes`, `mixins`, `schemas`e `classes`. |
| `{RESOURCE_ID}` | URI con codifica URL `$id` o `meta:altId` della risorsa. |

**Richiesta**

Il corpo della richiesta include l&#39;operazione (`op`), la posizione (`path`) e le informazioni (`value`) necessarie per aggiornare il mixin. Questa richiesta aggiorna il mixin Dettagli proprietà per rimuovere il campo &quot;propertyCity&quot; e aggiungere un nuovo campo &quot;propertyAddress&quot; che fa riferimento a un tipo di dati standard contenente le informazioni sull&#39;indirizzo. Inoltre, aggiunge un nuovo campo &quot;emailAddress&quot; che fa riferimento a un tipo di dati standard con informazioni e-mail.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.e49cbb2eec33618f686b8344b4597ecf \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
          { "op": "remove", "path": "/definitions/vehicles/properties/_{TENANT_ID}/properties/propertyCity"},
          { "op": "add", "path": "/definitions/property/properties/_{TENANT_ID}/properties/propertyAddress", "value":
            {
              "title": "Property Address",
              "description": "Address of the Property",
              "$ref": "https://ns.adobe.com/xdm/common/address"
            } 
          },
          { "op": "add", "path": "/definitions/property/properties/_{TENANT_ID}/properties/emailAddress", "value":
            {
              "title": "Property Email Address",
              "description": "Email address of the Property",
              "$ref": "https://ns.adobe.com/xdm/context/emailaddress"
            } 
          },
      ]'
```

**Risposta**

Una risposta corretta indica che le operazioni sono state completate correttamente perché i nuovi campi sono presenti e il campo &quot;propertyCity&quot; è stato rimosso.

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
                        },
                        "propertyAddress": {
                            "title": "Property Address",
                            "description": "Address of the Property",
                            "$ref": "https://ns.adobe.com/xdm/common/address"
                        },
                        "emailAddress": {
                            "title": "Property Email Address",
                            "description": "Email address of the Property",
                            "$ref": "https://ns.adobe.com/xdm/context/emailaddress"
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
    "version": "1.1",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1552088205144,
        "repo:lastModifiedDate": 1552089776535,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```
