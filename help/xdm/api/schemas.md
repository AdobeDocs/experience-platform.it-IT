---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema;Schema;schemas;Schemas;create
solution: Experience Platform
title: Creare uno schema
description: L'endpoint /schemas nell'API del Registro di sistema dello schema consente di gestire gli schemi XDM a livello di programmazione all'interno dell'applicazione dell'esperienza.
topic: developer guide
translation-type: tm+mt
source-git-commit: 0b55f18eabcf1d7c5c233234c59eb074b2670b93
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 2%

---


# Endpoint schema

Uno schema può essere considerato come il modello per i dati da inserire in Adobe Experience Platform. Ogni schema è composto da una classe e da zero o più mixin. L&#39; `/schemas` endpoint nell&#39; [!DNL Schema Registry] API consente di gestire gli schemi a livello di programmazione all&#39;interno dell&#39;applicazione dell&#39;esperienza.

## Introduzione

L&#39;endpoint API utilizzato in questa guida è parte dell&#39; [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Prima di continuare, consultate la guida [](./getting-started.md) introduttiva per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente chiamate a qualsiasi API  Experience Platform.

## Recupero di un elenco di schemi {#list}

Potete elencare tutti gli schemi sotto il `global` contenitore o `tenant` il contenitore effettuando una richiesta di GET a `/global/schemas` o, `/tenant/schemas`rispettivamente.

>[!NOTE]
>
>Quando si elencano le risorse, il Registro di sistema dello schema limita i set di risultati a 300 elementi. Per restituire risorse oltre questo limite, è necessario utilizzare i parametri di paging. È inoltre consigliabile utilizzare parametri di query aggiuntivi per filtrare i risultati e ridurre il numero di risorse restituite. Per ulteriori informazioni, consulta la sezione sui parametri [di](./appendix.md#query) query nel documento allegato.

**Formato API**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Contenitore che contiene gli schemi da recuperare: `global` per  schemi creati dal Adobe o `tenant` per schemi di proprietà dell’organizzazione. |
| `{QUERY_PARAMS}` | Parametri di query facoltativi per filtrare i risultati per. Per un elenco dei parametri disponibili, consultare il documento [](./appendix.md#query) appendice. |

**Richiesta**

La richiesta seguente recupera un elenco di schemi dal `tenant` contenitore, utilizzando un parametro di `orderby` query per ordinare i risultati in base al relativo `title` attributo.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dall’ `Accept` intestazione inviata nella richiesta. Le seguenti `Accept` intestazioni sono disponibili per elencare gli schemi:

| `Accept` header | Descrizione |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Restituisce un breve riepilogo di ciascuna risorsa. Intestazione consigliata per elencare le risorse. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Restituisce lo schema JSON completo per ciascuna risorsa, con originale `$ref` e `allOf` incluso. (Limite: 300) |

**Risposta**

La richiesta precedente utilizzava l&#39; `application/vnd.adobe.xed-id+json` intestazione, pertanto la risposta includeva solo gli `Accept` , `title`, `$id`e `meta:altId``version` gli attributi per ogni schema. Utilizzando l&#39;altra `Accept` intestazione (`application/vnd.adobe.xed+json`) vengono restituiti tutti gli attributi di ogni schema. Selezionate l’ `Accept` intestazione appropriata in base alle informazioni richieste nella risposta.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0238be93d3e7a06aec5e0655955901ec",
      "meta:altId": "_{TENANT_ID}.schemas.0238be93d3e7a06aec5e0655955901ec",
      "version": "1.4",
      "title": "Hotels"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0ef4ce0d390f0809fad490802f53d30b",
      "meta:altId": "_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b",
      "version": "1.0",
      "title": "Loyalty Members"
    }
  ],
  "_page": {
        "orderby": "title",
        "next": null,
        "count": 2
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

## Cercare uno schema {#lookup}

È possibile ricercare uno schema specifico effettuando una richiesta di GET che includa l&#39;ID dello schema nel percorso.

**Formato API**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Contenitore che contiene lo schema da recuperare: `global` per uno schema  creato dal Adobe o `tenant` per uno schema di proprietà dell&#39;organizzazione. |
| `{SCHEMA_ID}` | La codifica `meta:altId` o URL `$id` dello schema da ricercare. |

**Richiesta**

La richiesta seguente recupera nel percorso uno schema specificato dal relativo `meta:altId` valore.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dall’ `Accept` intestazione inviata nella richiesta. Tutte le richieste di ricerca richiedono che `version` sia inclusa nell’ `Accept` intestazione. The following `Accept` headers are available:

| `Accept` header | Descrizione |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Raw con `$ref` e `allOf`, ha titoli e descrizioni. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` e `allOf` risolto, con titoli e descrizioni. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Raw con `$ref` e `allOf`, senza titoli o descrizioni. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` e `allOf` risolto, nessun titolo o descrizione. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` e `allOf` risolto, descrittori inclusi. |

**Risposta**

Una risposta corretta restituisce i dettagli dello schema. I campi restituiti dipendono dall’ `Accept` intestazione inviata nella richiesta. Provate con `Accept` intestazioni diverse per confrontare le risposte e determinare quale intestazione è più adatta al caso d’uso.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:altId": "_{TENANT_ID}.schemas.20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:resourceType": "schemas",
  "version": "1.1",
  "title": "Example schema",
  "type": "object",
  "description": "An example schema created within the tenant container.",
  "allOf": [
      {
          "$ref": "https://ns.adobe.com/xdm/context/profile",
          "type": "object",
          "meta:xdmType": "object"
      },
      {
          "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
          "type": "object",
          "meta:xdmType": "object"
      }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
      "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
      "repo:createdDate": 1602872911226,
      "repo:lastModifiedDate": 1603381419889,
      "xdm:createdClientId": "{CLIENT_ID}",
      "xdm:lastModifiedClientId": "{CLIENT_ID}",
      "xdm:createdUserId": "{USER_ID}",
      "xdm:lastModifiedUserId": "{USER_ID}",
      "eTag": "84b4da79b7445a4bf1c59269e718065effddb983c492f48e223d49c049c6d589",
      "meta:globalLibVersion": "1.15.4"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Creare uno schema {#create}

Il processo di composizione dello schema inizia assegnando una classe. La classe definisce gli aspetti comportamentali chiave dei dati (record o serie temporali), nonché i campi minimi richiesti per descrivere i dati che saranno acquisiti.

>[!NOTE]
>
>La chiamata di esempio riportata di seguito è solo un esempio di base di come creare uno schema nell&#39;API, con i requisiti minimi di composizione di una classe e nessun mixin. Per i passaggi completi su come creare uno schema nell&#39;API, inclusa la modalità di assegnazione dei campi tramite mixin e tipi di dati, vedere l&#39;esercitazione [sulla creazione](../tutorials/create-schema-api.md)dello schema.

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
| `allOf` | Un array di oggetti, con ogni oggetto che fa riferimento a una classe o a un mixin i cui campi viene implementato dallo schema. Ciascun oggetto contiene una singola proprietà (`$ref`) il cui valore rappresenta la classe o il `$id` mixin implementato dal nuovo schema. È necessario specificare una classe con zero o più mixine aggiuntive. Nell&#39;esempio precedente, il singolo oggetto nell&#39; `allOf` array è la classe dello schema. |

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

L&#39;esecuzione di una richiesta di GET per [elencare tutti gli schemi](#list) nel contenitore tenant ora includerebbe il nuovo schema. Potete eseguire una richiesta [di](#lookup) `$id` ricerca (GET) utilizzando l’URI con codifica URL per visualizzare direttamente il nuovo schema.

Per aggiungere altri campi a uno schema, è possibile eseguire un&#39;operazione [](#patch) PATCH per aggiungere mixin agli `allOf` array e agli `meta:extends` array dello schema.

## Aggiornare uno schema {#put}

È possibile sostituire un intero schema tramite un&#39;operazione PUT, in sostanza riscrivendo la risorsa. Quando si aggiorna uno schema tramite una richiesta di PUT, il corpo deve includere tutti i campi che sarebbero necessari per [creare un nuovo schema](#create) in una richiesta di POST.

>[!NOTE]
>
>Se si desidera aggiornare solo parte di uno schema invece di sostituirlo completamente, vedere la sezione sull&#39; [aggiornamento di una parte di uno schema](#patch).

**Formato API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | La codifica `meta:altId` o URL `$id` dello schema da riscrivere. |

**Richiesta**

La richiesta seguente sostituisce uno schema esistente, modificandone `title`, `description`e `allOf` gli attributi.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Commercial Property Information",
        "description": "Information related to commercial properties.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7" 
          } 
        ]
      }'
```

**Risposta**

Una risposta corretta restituisce i dettagli dello schema aggiornato.

```JSON
{
    "title":"Commercial Property Information",
    "description": "Information related to commercial properties.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
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
        "repo:lastModifiedDate": 1552088470592,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Aggiornare una parte di uno schema {#patch}

È possibile aggiornare una parte di uno schema utilizzando una richiesta di PATCH. Supporta [!DNL Schema Registry] tutte le operazioni standard di patch JSON, inclusi `add`, `remove`e `replace`. Per ulteriori informazioni sulla patch JSON, consultate la guida [ai fondamentali](../../landing/api-fundamentals.md#json-patch)API.

>[!NOTE]
>
>Se si desidera sostituire un&#39;intera risorsa con nuovi valori anziché aggiornare i singoli campi, consultare la sezione relativa alla [sostituzione di uno schema con un&#39;operazione](#put)PUT.

Una delle operazioni PATCH più comuni consiste nell&#39;aggiungere mixin definiti in precedenza a uno schema, come illustrato nell&#39;esempio seguente.

**Formato API**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | L’ `$id` URI con codifica URL o `meta:altId` dello schema da aggiornare. |

**Richiesta**

La richiesta di esempio seguente aggiunge un nuovo mixin a uno schema aggiungendo il `$id` valore del mixin sia agli `meta:extends` array che agli `allOf` array.

Il corpo della richiesta assume la forma di una matrice, con ogni oggetto elencato che rappresenta una specifica modifica a un singolo campo. Ogni oggetto include l&#39;operazione da eseguire (`op`), il campo sul quale deve essere eseguita l&#39;operazione (`path`) e quali informazioni devono essere incluse nell&#39;operazione (`value`).

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/meta:extends/-",
          "value":  "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        },
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
          }
        }
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

## Abilita uno schema da utilizzare nel profilo cliente in tempo reale {#union}

Affinché uno schema possa partecipare al profilo [cliente in tempo](../../profile/home.md)reale, è necessario aggiungere un `union` tag all&#39; `meta:immutableTags` array dello schema. È possibile eseguire questa operazione eseguendo una richiesta PATCH per lo schema in questione.

>[!IMPORTANT]
>
>I tag immutabili sono tag destinati a essere impostati ma non rimossi.

**Formato API**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | L’ `$id` URI con codifica URL o `meta:altId` dello schema da attivare. |

**Richiesta**

La richiesta di esempio riportata di seguito aggiunge un `meta:immutableTags` array a uno schema esistente, assegnando alla matrice un singolo valore di stringa di `union` per consentirne l&#39;utilizzo in Profile.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/meta:immutableTags",
          "value": ["union"]
        }
      ]'
```

**Risposta**

Una risposta corretta restituisce i dettagli dello schema aggiornato, indicando che l&#39; `meta:immutableTags` array è stato aggiunto.

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
    },
    "meta:immutableTags": [
      "union"
    ]
}
```

È ora possibile visualizzare l&#39;unione per la classe dello schema per confermare che i campi dello schema siano rappresentati. Per ulteriori informazioni, consulta la guida [all’endpoint](./unions.md) unioni.

## Eliminare uno schema {#delete}

Può essere talvolta necessario rimuovere uno schema dal Registro di sistema dello schema. A questo scopo, è necessario eseguire una richiesta di DELETE con l&#39;ID dello schema fornito nel percorso.

**Formato API**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | L’ `$id` URI con codifica URL o `meta:altId` dello schema da eliminare. |

**Richiesta**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo vuoto.

È possibile confermare l&#39;eliminazione provando una richiesta di ricerca (GET) allo schema. Sarà necessario includere un&#39; `Accept` intestazione nella richiesta, ma dovrebbe ricevere uno stato HTTP 404 (Non trovato) perché lo schema è stato rimosso dal Registro di sistema dello schema.