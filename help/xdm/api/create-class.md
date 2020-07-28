---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creazione di una classe
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


# Creazione di una classe

Il blocco predefinito principale di uno schema è una classe. La classe contiene il set minimo di campi che è necessario definire per acquisire i dati di base di uno schema. Ad esempio, se si stava progettando uno schema per auto e camion, molto probabilmente utilizzerebbero una classe chiamata Veicolo che descriveva le proprietà comuni di base di tutti i veicoli.

Esistono diverse classi standard fornite dal Adobe  e da altri [!DNL Experience Platform] partner, ma potete anche definire le vostre classi e salvarle nel [!DNL Schema Registry]. È quindi possibile comporre uno schema che implementa la classe creata e definire mixin compatibili con la classe appena definita.

>[!NOTE]
>
>Quando si compone uno schema basato su una classe definita dall&#39;utente, non sarà possibile utilizzare i mixin standard. Ciascun mixin definisce le classi con cui è compatibile nel relativo `meta:intendedToExtend` attributo. Una volta iniziata la definizione di mixin compatibili con la nuova classe (utilizzando la `$id` nuova classe nel `meta:intendedToExtend` campo del mixin), sarà possibile riutilizzare tali mixin ogni volta che si definisce uno schema che implementa la classe definita. Per ulteriori informazioni, consulta le sezioni sulla [creazione di mixin](create-mixin.md) e sulla [creazione di schemi](create-schema.md) .

**Formato API**

```http
POST /tenant/classes
```

**Richiesta**

La richiesta di creare (POST) una classe deve includere un `allOf` attributo contenente un `$ref` massimo di due valori: `https://ns.adobe.com/xdm/data/record` o `https://ns.adobe.com/xdm/data/time-series`. Questi valori rappresentano il comportamento su cui si basa la classe (record o serie temporali, rispettivamente). Per ulteriori informazioni sulle differenze tra i dati dei record e i dati delle serie temporali, vedere la sezione sui tipi di comportamento all&#39;interno delle [nozioni di base della composizione](../schema/composition.md)dello schema.

Quando si definisce una classe, è possibile includere anche mixin o campi personalizzati nella definizione della classe. In questo modo i mixin e i campi aggiunti verranno inclusi in tutti gli schemi che implementano la classe. La seguente richiesta di esempio definisce una classe denominata &quot;Property&quot;, che acquisisce informazioni relative a diverse proprietà possedute e gestite da una società. Include un `propertyId` campo da includere ogni volta che la classe viene utilizzata.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property",
        "description":"Properties owned and operated by the company.",
        "type":"object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property Identification Number",
                        "type": "string",
                        "description": "Unique Property identification number"
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `_{TENANT_ID}` | Lo `TENANT_ID` spazio dei nomi per l&#39;organizzazione. Tutte le risorse create dall&#39;organizzazione devono includere questa proprietà per evitare conflitti con altre risorse nel [!DNL Schema Registry]. |
| `allOf` | Elenco di risorse le cui proprietà devono essere ereditate dalla nuova classe. Uno degli `$ref` oggetti all&#39;interno della matrice definisce il comportamento della classe. In questo esempio, la classe eredita il comportamento &quot;record&quot;. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un payload contenente i dettagli della nuova classe creata, inclusi `$id`, `meta:altId`e `version`. Questi tre valori sono di sola lettura e vengono assegnati dal [!DNL Schema Registry].

```JSON
{
    "title": "Property",
    "description": "Properties owned and operated by the company.",
    "type": "object",
    "definitions": {
        "property": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "property": {
                            "title": "Property Information",
                            "type": "object",
                            "description": "Information about different owned and operated properties.",
                            "properties": {
                                "propertyId": {
                                    "title": "Property Identification Number",
                                    "type": "string",
                                    "description": "Unique Property identification number",
                                    "meta:xdmType": "string"
                                }
                            },
                            "meta:xdmType": "object"
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
            "$ref": "https://ns.adobe.com/xdm/data/record"
        },
        {
            "$ref": "#/definitions/property"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:extends": [
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "version": "1.0",
    "meta:resourceType": "classes",
    "meta:registryMetadata": {
        "repo:createDate": 1552086405448,
        "repo:lastModifiedDate": 1552086405448,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

L&#39;esecuzione di una richiesta di GET per elencare tutte le classi nel contenitore tenant ora include la classe Property. Potete anche eseguire una richiesta di ricerca (GET) utilizzando l&#39; `$id` URI con codifica URL per visualizzare direttamente la nuova classe. Accertatevi di includere l&#39;oggetto `version` nell&#39;intestazione Accetto durante l&#39;esecuzione di una richiesta di ricerca.
