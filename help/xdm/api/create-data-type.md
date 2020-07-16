---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creazione di un tipo di dati
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 1%

---


# Creazione di un tipo di dati

Se esistono strutture dati comuni che l&#39;organizzazione desidera utilizzare in più modi, è possibile definire un tipo di dati. I tipi di dati consentono l&#39;uso coerente di strutture con più campi, con maggiore flessibilità rispetto ai mixin quanto possono essere inclusi ovunque in uno schema aggiungendo tali strutture come `type` di un campo.

In altre parole, i tipi di dati consentono di definire una gerarchia di oggetti una volta e di farvi riferimento in un campo come qualsiasi altro tipo scalare.

**Formato API**

```http
POST /tenant/datatypes
```

**Richiesta**

La definizione di un tipo di dati non richiede `meta:extends` né `meta:intendedToExtend` campi, né i campi devono essere nidificati per evitare conflitti.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
              "shoppingCentre": "Shopping Center"
            }
          }
        } 
      }'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un payload contenente i dettagli del tipo di dati appena creato, inclusi `$id`, `meta:altId`e `version`. Questi tre valori sono di sola lettura e vengono assegnati dal [!DNL Schema Registry].

```JSON
{
    "title": "Property Construction",
    "description": "Information related to the property construction",
    "type": "object",
    "properties": {
        "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed.",
            "meta:xdmType": "int"
        },
        "constructionType": {
            "type": "string",
            "title": "Construction Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
                "freeStanding",
                "mall",
                "shoppingCenter"
            ],
            "meta:enum": {
                "freeStanding": "Free Standing Building",
                "mall": "Mall Space",
                "shoppingCentre": "Shopping Center"
            },
            "meta:xdmType": "string"
        }
    },
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102",
    "version": "1.0",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1552087079285,
        "repo:lastModifiedDate": 1552087079285,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

L&#39;esecuzione di una richiesta GET per elencare tutti i tipi di dati nel contenitore tenant ora include il tipo di dati Costruzione proprietà. È inoltre possibile eseguire una richiesta di ricerca (GET) utilizzando l&#39; `$id` URI con codifica URL per visualizzare direttamente il nuovo tipo di dati. Accertatevi di includere nell’ `version` intestazione Accetto la richiesta di ricerca.
