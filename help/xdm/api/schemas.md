---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;modello dati;registro schema;schema;schema;schemi;schemi;schemi;creare
solution: Experience Platform
title: Endpoint API per gli schemi
description: L’endpoint /schemas nell’API del Registro di sistema dello schema ti consente di gestire programmaticamente gli schemi XDM all’interno dell’applicazione di esperienza.
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 5%

---

# Endpoint degli schemi

Uno schema può essere considerato come il modello per i dati che desideri inserire in Adobe Experience Platform. Ogni schema è composto da una classe e da zero o più gruppi di campi dello schema. La `/schemas` punto finale [!DNL Schema Registry] L’API ti consente di gestire gli schemi a livello di programmazione all’interno dell’applicazione di esperienza.

## Introduzione

L’endpoint API utilizzato in questa guida fa parte del [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e importanti informazioni sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recupera un elenco di schemi {#list}

Puoi elencare tutti gli schemi sotto la sezione `global` o `tenant` effettuando una richiesta GET a `/global/schemas` o `/tenant/schemas`, rispettivamente.

>[!NOTE]
>
>Quando si elencano le risorse, il Registro di sistema dello schema limita i set di risultati a 300 elementi. Per restituire le risorse oltre questo limite, è necessario utilizzare i parametri di paging. Si consiglia inoltre di utilizzare parametri di query aggiuntivi per filtrare i risultati e ridurre il numero di risorse restituite. Vedi la sezione su [parametri di query](./appendix.md#query) nel documento di appendice per ulteriori informazioni.

**Formato API**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Il contenitore che ospita gli schemi da recuperare: `global` per schemi creati da Adobi o `tenant` per gli schemi di proprietà dell’organizzazione. |
| `{QUERY_PARAMS}` | Parametri di query opzionali per filtrare i risultati in base a. Consulta la sezione [documento appendice](./appendix.md#query) per un elenco dei parametri disponibili. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La seguente richiesta recupera un elenco di schemi dal `tenant` contenitore, utilizzando un `orderby` parametro di query per ordinare i risultati in base ai relativi `title` attributo.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dal `Accept` intestazione inviata nella richiesta. I seguenti `Accept` le intestazioni sono disponibili per elencare gli schemi:

| `Accept` header | Descrizione |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Restituisce un breve riepilogo di ciascuna risorsa. Intestazione consigliata per l’elenco delle risorse. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Restituisce lo schema JSON completo per ogni risorsa, con originale `$ref` e `allOf` incluso. (Limite: 300) |

{style=&quot;table-layout:auto&quot;}

**Risposta**

La richiesta di cui sopra ha utilizzato il `application/vnd.adobe.xed-id+json` `Accept` , quindi la risposta include solo l’ `title`, `$id`, `meta:altId`e `version` attributi per ogni schema. Utilizzo dell&#39;altro `Accept` header (`application/vnd.adobe.xed+json`) restituisce tutti gli attributi di ogni schema. Selezionare il `Accept` a seconda delle informazioni richieste nella risposta.

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

Puoi cercare uno schema specifico effettuando una richiesta di GET che includa l’ID dello schema nel percorso.

**Formato API**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Il contenitore che ospita lo schema da recuperare: `global` per uno schema creato da un Adobe o `tenant` per uno schema di proprietà dell&#39;organizzazione. |
| `{SCHEMA_ID}` | La `meta:altId` o con codifica URL `$id` dello schema da cercare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta seguente recupera uno schema specificato dai relativi `meta:altId` nel percorso.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dal `Accept` intestazione inviata nella richiesta. Tutte le richieste di ricerca richiedono un `version` sono inclusi nella `Accept` intestazione. I seguenti `Accept` le intestazioni sono disponibili:

| `Accept` header | Descrizione |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Raw con `$ref` e `allOf`, include titoli e descrizioni. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` e `allOf` risolto, con titoli e descrizioni. |
| `application/vnd.adobe.xed-notext+json; version=1` | Raw con `$ref` e `allOf`, senza titoli o descrizioni. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` e `allOf` risolto, senza titoli o descrizioni. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` e `allOf` risolti, descrittori inclusi. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` e `allOf` risolto, con titoli e descrizioni. I campi obsoleti sono indicati con un `meta:status` attributo `deprecated`. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce i dettagli dello schema. I campi restituiti dipendono dal `Accept` intestazione inviata nella richiesta. Esperimento con diversi `Accept` intestazioni per confrontare le risposte e determinare quale intestazione è migliore per il tuo caso d’uso.

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
  "imsOrg": "{ORG_ID}",
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

Il processo di composizione dello schema inizia con l&#39;assegnazione di una classe. La classe definisce gli aspetti comportamentali chiave dei dati (record o serie temporali), nonché i campi minimi necessari per descrivere i dati che verranno acquisiti.

>[!NOTE]
>
>La chiamata di esempio riportata di seguito è solo un esempio di base su come creare uno schema nell’API, con i requisiti di composizione minimi di una classe e nessun gruppo di campi. Per i passaggi completi su come creare uno schema nell’API, incluso come assegnare campi utilizzando gruppi di campi e tipi di dati, vedi [esercitazione sulla creazione dello schema](../tutorials/create-schema-api.md).

**Formato API**

```http
POST /tenant/schemas
```

**Richiesta**

La richiesta deve includere un `allOf` attributo che fa riferimento al `$id` di una classe. Questo attributo definisce la &quot;classe base&quot; che lo schema implementerà. In questo esempio, la classe base è una classe &quot;Informazioni proprietà&quot; creata in precedenza.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `allOf` | Matrice di oggetti, con ogni oggetto che fa riferimento a una classe o a un gruppo di campi i cui campi vengono implementati dallo schema. Ogni oggetto contiene una singola proprietà (`$ref`) il cui valore rappresenta `$id` della classe o del gruppo di campi che verrà implementato dal nuovo schema. È necessario specificare una classe con zero o più gruppi di campi aggiuntivi. Nell&#39;esempio precedente, il singolo oggetto nel `allOf` array è la classe dello schema. |

{style=&quot;table-layout:auto&quot;}

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un payload contenente i dettagli dello schema appena creato, tra cui `$id`, `meta:altId`e `version`. Questi valori sono di sola lettura e sono assegnati dal [!DNL Schema Registry].

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
    "imsOrg": "{ORG_ID}",
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

Esecuzione di una richiesta GET a [elencare tutti gli schemi](#list) nel contenitore tenant ora includerebbe il nuovo schema. È possibile eseguire un [richiesta di ricerca (GET)](#lookup) utilizzando l’URL-encoded `$id` URI per visualizzare direttamente il nuovo schema.

Per aggiungere campi aggiuntivi a uno schema, è possibile eseguire una [Funzionamento PATCH](#patch) per aggiungere gruppi di campi al `allOf` e `meta:extends` array.

## Aggiornare uno schema {#put}

È possibile sostituire un intero schema tramite un’operazione PUT, essenzialmente riscrivendo la risorsa. Quando si aggiorna uno schema tramite una richiesta di PUT, il corpo deve includere tutti i campi necessari quando [creazione di un nuovo schema](#create) in una richiesta POST.

>[!NOTE]
>
>Se si desidera aggiornare solo parte di uno schema invece di sostituirlo completamente, vedere la sezione in [aggiornamento di una parte di uno schema](#patch).

**Formato API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | La `meta:altId` o con codifica URL `$id` dello schema che si desidera riscrivere. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La seguente richiesta sostituisce uno schema esistente, modificandone il `title`, `description`e `allOf` attributi.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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

È possibile aggiornare una parte di uno schema utilizzando una richiesta di PATCH. La [!DNL Schema Registry] supporta tutte le operazioni standard di patch JSON, tra cui `add`, `remove`e `replace`. Per ulteriori informazioni sulla patch JSON, consulta la sezione [Guida di base sulle API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Per sostituire un’intera risorsa con nuovi valori anziché aggiornare singoli campi, consulta la sezione [sostituzione di uno schema con un’operazione PUT](#put).

Una delle operazioni più comuni di PATCH consiste nell’aggiungere a uno schema gruppi di campi definiti in precedenza, come illustrato nell’esempio seguente.

**Formato API**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | L’URL è codificato `$id` URI o `meta:altId` dello schema da aggiornare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

Nella richiesta di esempio seguente viene aggiunto un nuovo gruppo di campi a uno schema aggiungendo il gruppo di campi `$id` sia per `meta:extends` e `allOf` array.

Il corpo della richiesta assume la forma di una matrice, con ogni oggetto elencato che rappresenta una modifica specifica a un singolo campo. Ogni oggetto include l&#39;operazione da eseguire (`op`), su quale campo deve essere eseguita l&#39;operazione (`path`) e quali informazioni dovrebbero essere incluse in tale operazione (`value`).

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

La risposta indica che entrambe le operazioni sono state eseguite correttamente. Gruppo di campi `$id` è stato aggiunto al `meta:extends` array e un riferimento (`$ref`) al gruppo di campi `$id` ora viene visualizzato in `allOf` array.

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
    "imsOrg": "{ORG_ID}",
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

## Abilitare uno schema da utilizzare nel profilo cliente in tempo reale {#union}

Al fine di uno schema a cui partecipare [Profilo cliente in tempo reale](../../profile/home.md), devi aggiungere un `union` tag per lo schema `meta:immutableTags` array. Puoi eseguire questa operazione effettuando una richiesta PATCH per lo schema in questione.

>[!IMPORTANT]
>
>I tag immutabili sono tag destinati a essere impostati ma non mai rimossi.

**Formato API**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | L’URL è codificato `$id` URI o `meta:altId` dello schema che desideri abilitare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta di esempio seguente aggiunge un `meta:immutableTags` a uno schema esistente, fornendo all&#39;array un singolo valore di stringa di `union` per abilitarlo all’uso in Profilo.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Una risposta corretta restituisce i dettagli dello schema aggiornato, indicando che il `meta:immutableTags` è stato aggiunto l’array .

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
    "imsOrg": "{ORG_ID}",
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

È ora possibile visualizzare l&#39;unione per la classe di questo schema per verificare che i campi dello schema siano rappresentati. Consulta la sezione [guida all’endpoint sindacati](./unions.md) per ulteriori informazioni.

## Eliminare uno schema {#delete}

Talvolta può essere necessario rimuovere uno schema dal Registro di sistema dello schema. A tal fine, esegui una richiesta DELETE con l’ID schema fornito nel percorso .

**Formato API**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | L’URL è codificato `$id` URI o `meta:altId` dello schema da eliminare. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 204 (Nessun contenuto) e un corpo vuoto.

Puoi confermare l&#39;eliminazione tentando una richiesta di ricerca (GET) allo schema. Sarà necessario includere un `Accept` intestazione nella richiesta, ma deve ricevere uno stato HTTP 404 (Non trovato) perché lo schema è stato rimosso dal Registro di sistema dello schema.
