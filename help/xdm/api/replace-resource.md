---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Sostituire una risorsa
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 1%

---


# Sostituire una risorsa

Il Registro di sistema dello schema consente di sostituire un&#39;intera risorsa tramite un&#39;operazione PUT. Questa operazione riscrive sostanzialmente la risorsa, pertanto il corpo della richiesta deve includere tutti i campi che sarebbero necessari per creare una nuova risorsa utilizzando una richiesta POST.

Questo metodo è particolarmente utile se desiderate aggiornare molte informazioni contemporaneamente nella risorsa.

>[!NOTE]
>
>Se si desidera aggiornare solo parte di una risorsa invece di sostituirla completamente, consultare il documento sull&#39; [aggiornamento di una risorsa con un&#39;operazione](update-resource.md)PATCH.

**Formato API**

Una richiesta PUT può essere eseguita solo con risorse definite nel contenitore tenant.

```http
PUT /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{RESOURCE_TYPE}` | Il tipo di risorsa da aggiornare dalla Libreria schema. I tipi validi sono `datatypes`, `mixins`, `schemas`e `classes`. |
| `{RESOURCE_ID}` | URI con codifica URL `$id` o `meta:altId` della risorsa. |

**Richiesta**

Questa richiesta di esempio sostituisce il tipo di dati Property Construction creato in un esempio precedente. Il corpo della richiesta è simile alla richiesta POST utilizzata per creare il tipo di dati, ma ora contiene un set aggiornato di campi con nuovi valori che sostituiscono quelli precedentemente definiti.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Construction",
        "description":"Information related to the construction of the property.",
        "type":"object",
        "properties": {
          "dateOpened": {
            "type":"string",
            "format": "date",
            "title": "Date Opened",
            "description": "The date the property was first opened."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "standAlone",
              "highRise",
              "stripMall"
            ],
            "meta:enum": {
              "standAlone": "Stand-Alone Building",
              "highRise": "High Rise Building",
              "stripMall": "Strip Mall"
            }
          },
          "constructionCompany": {
            "type": "string",
            "title": "Construction Company",
            "description": "Name of the construction company that completed the construction of the property."
          },
          "totalSquareFootage": {
            "type": "integer",
            "title": "Total Square Footage",
            "description": "Total square footage of the property."
          }
        } 
      }'
```

**Risposta**

Una risposta corretta restituisce i dettagli del tipo di dati, mostrando i campi e i valori aggiornati come forniti nella richiesta.

```JSON
{
    "title": "Property Construction",
    "description": "Information related to the construction of the property.",
    "type": "object",
    "properties": {
        "dateOpened": {
            "type": "string",
            "format": "date",
            "title": "Date Opened",
            "description": "The date the property was first opened.",
            "meta:xdmType": "date"
        },
        "propertyType": {
            "type": "string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
                "standAlone",
                "highRise",
                "stripMall"
            ],
            "meta:enum": {
                "standAlone": "Stand-Alone Building",
                "highRise": "High Rise Building",
                "stripMall": "Strip Mall"
            },
            "meta:xdmType": "string"
        },
        "constructionCompany": {
            "type": "string",
            "title": "Construction Company",
            "description": "Name of the construction company that completed the construction of the property.",
            "meta:xdmType": "string"
        },
        "totalSquareFootage": {
            "type": "integer",
            "title": "Total Square Footage",
            "description": "Total square footage of the property.",
            "meta:xdmType": "int"
        }
    },
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102",
    "version": "1.2",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1552087079285,
        "repo:lastModifiedDate": 1552090569013,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```
