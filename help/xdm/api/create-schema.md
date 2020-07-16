---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare uno schema
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 1%

---


# Creare uno schema

Uno schema può essere considerato come il modello per i dati in cui si desidera eseguire il caricamento [!DNL Experience Platform]. Ogni schema è composto da una classe e da zero o più mixin. In altre parole, non è necessario aggiungere un mixin per definire uno schema, ma nella maggior parte dei casi verrà utilizzato almeno un mixin.

Il processo di composizione dello schema inizia assegnando una classe. La classe definisce gli aspetti comportamentali chiave dei dati (record o serie temporali), nonché i campi minimi richiesti per descrivere i dati che saranno acquisiti.

**Formato API**

```http
POST /tenant/schemas
```

**Richiesta**

La richiesta deve includere un `allOf` attributo che fa riferimento alla classe `$id` di un oggetto. Questo attributo definisce la &quot;classe base&quot; che lo schema implementerà. In questo esempio, la classe base è una classe &quot;Informazioni sulle proprietà&quot; creata in precedenza.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Information",
        "description": "Property-related information.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590" 
          } 
        ]
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `allOf > $ref` | Il `$id` valore della classe che verrà implementato dal nuovo schema. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un payload contenente i dettagli dello schema appena creato, inclusi `$id`, `meta:altId`e `version`. Questi valori sono di sola lettura e vengono assegnati dal [!DNL Schema Registry].

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088461236,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

L&#39;esecuzione di una richiesta GET per elencare tutti gli schemi nel contenitore tenant ora includerebbe lo schema Informazioni proprietà, oppure potreste eseguire una richiesta di ricerca (GET) utilizzando l&#39; `$id` URI con codifica URL per visualizzare direttamente il nuovo schema. Ricordare di includere l&#39;oggetto `version` nell&#39;intestazione Accetto per tutte le richieste di ricerca.
