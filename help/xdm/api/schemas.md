---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;modello dati;registro schema;schema;schema;schemi;schemi;schemi;creare
solution: Experience Platform
title: Endpoint API per gli schemi
description: L’endpoint /schemas nell’API del Registro di sistema dello schema ti consente di gestire programmaticamente gli schemi XDM all’interno dell’applicazione di esperienza.
topic: guida per sviluppatori
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
translation-type: tm+mt
source-git-commit: 610ce5c6dca5e7375b941e7d6f550382da10ca27
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 2%

---

# Endpoint degli schemi

Uno schema può essere considerato come il modello per i dati che desideri inserire in Adobe Experience Platform. Ogni schema è composto da una classe e da zero o più mixin. L’endpoint `/schemas` nell’ API [!DNL Schema Registry] consente di gestire gli schemi a livello di programmazione all’interno dell’applicazione di esperienza.

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39; [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Prima di continuare, controlla la [guida introduttiva](./getting-started.md) per i collegamenti alla relativa documentazione, una guida per la lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare chiamate a qualsiasi API di Experience Platform.

## Recupera un elenco di schemi {#list}

È possibile elencare tutti gli schemi sotto il contenitore `global` o `tenant` effettuando una richiesta di GET rispettivamente a `/global/schemas` o `/tenant/schemas`.

>[!NOTE]
>
>Quando si elencano le risorse, il Registro di sistema dello schema limita i set di risultati a 300 elementi. Per restituire le risorse oltre questo limite, è necessario utilizzare i parametri di paging. Si consiglia inoltre di utilizzare parametri di query aggiuntivi per filtrare i risultati e ridurre il numero di risorse restituite. Per ulteriori informazioni, consulta la sezione sui [parametri di query](./appendix.md#query) nel documento di appendice .

**Formato API**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Il contenitore che ospita gli schemi da recuperare: `global` per schemi creati da Adobi o `tenant` per schemi di proprietà della tua organizzazione. |
| `{QUERY_PARAMS}` | Parametri di query opzionali per filtrare i risultati in base a. Per un elenco dei parametri disponibili, vedere il [documento dell&#39;appendice](./appendix.md#query). |

**Richiesta**

La richiesta seguente recupera un elenco di schemi dal contenitore `tenant` utilizzando un parametro di query `orderby` per ordinare i risultati in base al relativo attributo `title`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dall’intestazione `Accept` inviata nella richiesta. Le seguenti intestazioni `Accept` sono disponibili per elencare gli schemi:

| `Accept` header | Descrizione |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Restituisce un breve riepilogo di ciascuna risorsa. Intestazione consigliata per l’elenco delle risorse. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Restituisce lo schema JSON completo per ogni risorsa, con i valori originali `$ref` e `allOf` inclusi. (Limite: 300) |

**Risposta**

La richiesta precedente utilizzava l’intestazione `application/vnd.adobe.xed-id+json` `Accept`, pertanto la risposta include solo gli attributi `title`, `$id`, `meta:altId` e `version` per ogni schema. Utilizzando l&#39;altra intestazione `Accept` (`application/vnd.adobe.xed+json`) vengono restituiti tutti gli attributi di ogni schema. Seleziona l’intestazione `Accept` appropriata a seconda delle informazioni richieste nella risposta.

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
| `{SCHEMA_ID}` | Il `meta:altId` o il codice URL `$id` dello schema da cercare. |

**Richiesta**

La richiesta seguente recupera uno schema specificato dal relativo valore `meta:altId` nel percorso.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dall’intestazione `Accept` inviata nella richiesta. Tutte le richieste di ricerca richiedono che un `version` sia incluso nell&#39;intestazione `Accept`. Sono disponibili le seguenti intestazioni `Accept`:

| `Accept` header | Descrizione |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Raw con `$ref` e `allOf`, ha titoli e descrizioni. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` e  `allOf` risolta, ha titoli e descrizioni. |
| `application/vnd.adobe.xed-notext+json; version=1` | Non elaborato con `$ref` e `allOf`, senza titoli o descrizioni. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` e  `allOf` risolti, senza titoli o descrizioni. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` e  `allOf` risolti, descrittori inclusi. |

**Risposta**

Una risposta corretta restituisce i dettagli dello schema. I campi restituiti dipendono dall’intestazione `Accept` inviata nella richiesta. Sperimenta con diverse intestazioni `Accept` per confrontare le risposte e determinare quale intestazione è migliore per il tuo caso d’uso.

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

Il processo di composizione dello schema inizia con l&#39;assegnazione di una classe. La classe definisce gli aspetti comportamentali chiave dei dati (record o serie temporali), nonché i campi minimi necessari per descrivere i dati che verranno acquisiti.

>[!NOTE]
>
>La chiamata di esempio riportata di seguito è solo un esempio di base su come creare uno schema nell’API, con i requisiti di composizione minimi di una classe e senza mixin. Per i passaggi completi su come creare uno schema nell&#39;API, incluso come assegnare campi utilizzando mixin e tipi di dati, consulta l&#39; [esercitazione sulla creazione dello schema](../tutorials/create-schema-api.md).

**Formato API**

```http
POST /tenant/schemas
```

**Richiesta**

La richiesta deve includere un attributo `allOf` che fa riferimento a `$id` di una classe. Questo attributo definisce la &quot;classe base&quot; che lo schema implementerà. In questo esempio, la classe base è una classe &quot;Informazioni proprietà&quot; creata in precedenza.

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
| `allOf` | Matrice di oggetti, con ogni oggetto che fa riferimento a una classe o a un mixin i cui campi viene implementato lo schema. Ogni oggetto contiene una singola proprietà (`$ref`) il cui valore rappresenta `$id` della classe o del mixin che verrà implementato il nuovo schema. È necessario fornire una classe con zero o più mixin aggiuntivi. Nell&#39;esempio precedente, l&#39;oggetto singolo nell&#39;array `allOf` è la classe dello schema. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un payload contenente i dettagli dello schema appena creato, inclusi `$id`, `meta:altId` e `version`. Questi valori sono di sola lettura e sono assegnati da [!DNL Schema Registry].

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

L’esecuzione di una richiesta di GET a [elenca tutti gli schemi](#list) nel contenitore tenant includerebbe ora il nuovo schema. Puoi eseguire una richiesta [di ricerca (GET)](#lookup) utilizzando l&#39;URI con codifica URL `$id` per visualizzare direttamente il nuovo schema.

Per aggiungere campi aggiuntivi a uno schema, è possibile eseguire un&#39;operazione [PATCH](#patch) per aggiungere mixin agli array `allOf` e `meta:extends` dello schema.

## Aggiornare uno schema {#put}

È possibile sostituire un intero schema tramite un’operazione PUT, essenzialmente riscrivendo la risorsa. Quando si aggiorna uno schema tramite una richiesta di PUT, il corpo deve includere tutti i campi necessari durante la [creazione di un nuovo schema](#create) in una richiesta di POST.

>[!NOTE]
>
>Se desideri aggiornare solo parte di uno schema invece di sostituirlo completamente, consulta la sezione su [aggiornamento di una parte di uno schema](#patch).

**Formato API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | La `meta:altId` o la codifica URL `$id` dello schema che si desidera riscrivere. |

**Richiesta**

La richiesta seguente sostituisce uno schema esistente, modificando i relativi attributi `title`, `description` e `allOf`.

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

È possibile aggiornare una parte di uno schema utilizzando una richiesta di PATCH. Il [!DNL Schema Registry] supporta tutte le operazioni standard di patch JSON, tra cui `add`, `remove` e `replace`. Per ulteriori informazioni sulla patch JSON, consulta la guida [Principi di base API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Per sostituire un&#39;intera risorsa con nuovi valori anziché aggiornare singoli campi, consulta la sezione relativa alla [sostituzione di uno schema con un&#39;operazione PUT](#put).

Una delle operazioni più comuni di PATCH consiste nell’aggiungere mixin definiti in precedenza a uno schema, come illustrato nell’esempio seguente.

**Formato API**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | URI con codifica URL `$id` o `meta:altId` dello schema da aggiornare. |

**Richiesta**

La richiesta di esempio seguente aggiunge un nuovo mixin a uno schema aggiungendo il valore `$id` di tale mixin sia agli array `meta:extends` che `allOf`.

Il corpo della richiesta assume la forma di una matrice, con ogni oggetto elencato che rappresenta una modifica specifica a un singolo campo. Ogni oggetto include l&#39;operazione da eseguire (`op`), il campo sul quale deve essere eseguita l&#39;operazione (`path`) e le informazioni da includere in tale operazione (`value`).

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

La risposta indica che entrambe le operazioni sono state eseguite correttamente. Il mixin `$id` è stato aggiunto all&#39;array `meta:extends` e un riferimento (`$ref`) al mixin `$id` viene ora visualizzato nell&#39;array `allOf`.

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

Affinché uno schema possa partecipare a [Profilo cliente in tempo reale](../../profile/home.md), è necessario aggiungere un tag `union` all&#39;array dello schema `meta:immutableTags`. Puoi eseguire questa operazione effettuando una richiesta PATCH per lo schema in questione.

>[!IMPORTANT]
>
>I tag immutabili sono tag destinati a essere impostati ma non mai rimossi.

**Formato API**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | URI con codifica URL `$id` o `meta:altId` dello schema da abilitare. |

**Richiesta**

La richiesta di esempio seguente aggiunge un array `meta:immutableTags` a uno schema esistente, assegnando all’array un valore di stringa singolo `union` per abilitarlo all’uso in Profilo.

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

Una risposta corretta restituisce i dettagli dello schema aggiornato, indicando che è stato aggiunto l’array `meta:immutableTags` .

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

È ora possibile visualizzare l&#39;unione per la classe di questo schema per verificare che i campi dello schema siano rappresentati. Per ulteriori informazioni, consulta la [guida all’endpoint delle unioni](./unions.md) .

## Eliminare uno schema {#delete}

Talvolta può essere necessario rimuovere uno schema dal Registro di sistema dello schema. A tal fine, esegui una richiesta DELETE con l’ID schema fornito nel percorso .

**Formato API**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | URI con codifica URL `$id` o `meta:altId` dello schema da eliminare. |

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

Puoi confermare l&#39;eliminazione tentando una richiesta di ricerca (GET) allo schema. Sarà necessario includere un&#39;intestazione `Accept` nella richiesta, ma deve ricevere uno stato HTTP 404 (Non trovato) perché lo schema è stato rimosso dal Registro di sistema dello schema.
