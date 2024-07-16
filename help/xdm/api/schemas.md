---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;modello dati;modello dati;modello dati;modello dati;registro schema;schema;schema;schemi;schemi;creare
solution: Experience Platform
title: Endpoint API per gli schemi
description: L’endpoint /schemas nell’API Schema Registry consente di gestire in modo programmatico gli schemi XDM all’interno dell’applicazione Experience.
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1443'
ht-degree: 3%

---

# Endpoint &quot;schema&quot;

Uno schema può essere considerato come la blueprint per i dati che desideri acquisire in Adobe Experience Platform. Ogni schema è composto da una classe e da zero o più gruppi di campi dello schema. L&#39;endpoint `/schemas` nell&#39;API [!DNL Schema Registry] consente di gestire in modo programmatico gli schemi all&#39;interno dell&#39;applicazione Experience.

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte dell&#39;[[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e per le informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Recuperare un elenco di schemi {#list}

È possibile elencare tutti gli schemi nel contenitore `global` o `tenant` effettuando una richiesta GET rispettivamente a `/global/schemas` o `/tenant/schemas`.

>[!NOTE]
>
>Quando si elencano le risorse, il registro dello schema limita il set di risultati a 300 elementi. Per restituire risorse oltre questo limite, è necessario utilizzare i parametri di paging. È inoltre consigliabile utilizzare parametri di query aggiuntivi per filtrare i risultati e ridurre il numero di risorse restituite. Per ulteriori informazioni, vedere la sezione relativa ai [parametri di query](./appendix.md#query) nel documento dell&#39;appendice.

**Formato API**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Contenitore che ospita gli schemi da recuperare: `global` per gli schemi creati dall&#39;Adobe o `tenant` per gli schemi di proprietà dell&#39;organizzazione. |
| `{QUERY_PARAMS}` | Parametri di query facoltativi in base ai quali filtrare i risultati. Per un elenco dei parametri disponibili, vedere il [documento di appendice](./appendix.md#query). |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente recupera un elenco di schemi dal contenitore `tenant`, utilizzando un parametro di query `orderby` per ordinare i risultati in base al relativo attributo `title`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dall&#39;intestazione `Accept` inviata nella richiesta. Le seguenti intestazioni `Accept` sono disponibili per gli schemi di elenco:

| Intestazione `Accept` | Descrizione |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Restituisce un breve riepilogo di ciascuna risorsa. Questa è l’intestazione consigliata per l’elenco delle risorse. (Limite: 300) |
| `application/vnd.adobe.xed+json` | Restituisce lo schema JSON completo per ogni risorsa, con `$ref` e `allOf` originali inclusi. (Limite: 300) |

{style="table-layout:auto"}

**Risposta**

La richiesta precedente ha utilizzato l&#39;intestazione `application/vnd.adobe.xed-id+json` `Accept`, pertanto la risposta include solo gli attributi `title`, `$id`, `meta:altId` e `version` per ogni schema. L&#39;utilizzo dell&#39;altra intestazione `Accept` (`application/vnd.adobe.xed+json`) restituisce tutti gli attributi di ogni schema. Selezionare l&#39;intestazione `Accept` appropriata in base alle informazioni richieste nella risposta.

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

Per cercare uno schema specifico, devi eseguire una richiesta di GET che includa l’ID dello schema nel percorso.

**Formato API**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Contenitore che ospita lo schema da recuperare: `global` per uno schema creato da un Adobe o `tenant` per uno schema di proprietà dell&#39;organizzazione. |
| `{SCHEMA_ID}` | `meta:altId` o `$id` con codifica URL dello schema che si desidera cercare. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente recupera uno schema specificato dal relativo valore `meta:altId` nel percorso.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Il formato della risposta dipende dall&#39;intestazione `Accept` inviata nella richiesta. Tutte le richieste di ricerca richiedono l&#39;inclusione di `version` nell&#39;intestazione `Accept`. Sono disponibili le seguenti `Accept` intestazioni:

| Intestazione `Accept` | Descrizione |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Raw con `$ref` e `allOf`, con titoli e descrizioni. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` e `allOf` risolti, con titoli e descrizioni. |
| `application/vnd.adobe.xed-notext+json; version=1` | Raw con `$ref` e `allOf`, nessun titolo o descrizione. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` e `allOf` risolti, nessun titolo o descrizione. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` e `allOf` risolti, descrittori inclusi. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` e `allOf` risolti, con titoli e descrizioni. I campi obsoleti sono indicati con un attributo `meta:status` di `deprecated`. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli dello schema. I campi restituiti dipendono dall&#39;intestazione `Accept` inviata nella richiesta. Prova a confrontare le risposte con intestazioni `Accept` diverse e a determinare quale sia il migliore per il tuo caso d&#39;uso.

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

## Crea uno schema {#create}

Il processo di composizione dello schema inizia assegnando una classe. La classe definisce gli aspetti comportamentali chiave dei dati (record o serie temporali), nonché i campi minimi necessari per descrivere i dati che verranno acquisiti.

>[!NOTE]
>
>La chiamata di esempio seguente è solo un esempio di base di come creare uno schema nell’API, con i requisiti minimi di composizione di una classe e nessun gruppo di campi. Per i passaggi completi su come creare uno schema nell&#39;API, incluso come assegnare campi utilizzando gruppi di campi e tipi di dati, consulta l&#39;[esercitazione per la creazione di schemi](../tutorials/create-schema-api.md).

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
| `allOf` | Array di oggetti, con ogni oggetto che fa riferimento a una classe o a un gruppo di campi di cui lo schema implementa i campi. Ogni oggetto contiene una singola proprietà (`$ref`) il cui valore rappresenta `$id` della classe o del gruppo di campi che il nuovo schema implementerà. È necessario specificare una classe, con zero o più gruppi di campi aggiuntivi. Nell&#39;esempio precedente, il singolo oggetto nell&#39;array `allOf` è la classe dello schema. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 (Creato) e un payload contenente i dettagli dello schema appena creato, inclusi `$id`, `meta:altId` e `version`. Questi valori sono di sola lettura e sono assegnati da [!DNL Schema Registry].

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

L&#39;esecuzione di una richiesta di GET per [elencare tutti gli schemi](#list) nel contenitore tenant includerebbe ora il nuovo schema. È possibile eseguire una [richiesta di ricerca (GET)](#lookup) utilizzando l&#39;URI `$id` con codifica URL per visualizzare direttamente il nuovo schema.

Per aggiungere campi aggiuntivi a uno schema, è possibile eseguire un&#39;operazione [PATCH](#patch) per aggiungere gruppi di campi agli array `allOf` e `meta:extends` dello schema.

## Aggiornare uno schema {#put}

Puoi sostituire un intero schema tramite un’operazione PUT, essenzialmente riscrivendo la risorsa. Quando si aggiorna uno schema tramite una richiesta PUT, il corpo deve includere tutti i campi necessari per [la creazione di un nuovo schema](#create) in una richiesta POST.

>[!NOTE]
>
>Se si desidera aggiornare solo una parte di uno schema anziché sostituirla completamente, vedere la sezione relativa all&#39;aggiornamento di una parte di uno schema](#patch).[

**Formato API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | `meta:altId` o `$id` con codifica URL dello schema che si desidera riscrivere. |

{style="table-layout:auto"}

**Richiesta**

La seguente richiesta sostituisce uno schema esistente, modificandone gli attributi `title`, `description` e `allOf`.

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

In caso di esito positivo, la risposta restituisce i dettagli dello schema aggiornato.

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

È possibile aggiornare una parte di uno schema utilizzando una richiesta PATCH. [!DNL Schema Registry] supporta tutte le operazioni Patch JSON standard, inclusi `add`, `remove` e `replace`. Per ulteriori informazioni sulla patch JSON, consulta la [guida delle API fondamentali](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Se desideri sostituire un&#39;intera risorsa con nuovi valori invece di aggiornare singoli campi, consulta la sezione sulla [sostituzione di uno schema tramite un&#39;operazione PUT](#put).

Una delle operazioni più comuni di PATCH consiste nell’aggiungere a uno schema gruppi di campi definiti in precedenza, come illustrato nell’esempio seguente.

**Formato API**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | URI `$id` con codifica URL o `meta:altId` dello schema che si desidera aggiornare. |

{style="table-layout:auto"}

**Richiesta**

La richiesta di esempio seguente aggiunge un nuovo gruppo di campi a uno schema aggiungendo il valore `$id` del gruppo di campi sia all&#39;array `meta:extends` che all&#39;array `allOf`.

Il corpo della richiesta è un array e ogni oggetto elencato rappresenta una modifica specifica di un singolo campo. Ogni oggetto include l&#39;operazione da eseguire (`op`), il campo in cui deve essere eseguita l&#39;operazione (`path`) e le informazioni da includere nell&#39;operazione (`value`).

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

La risposta mostra che entrambe le operazioni sono state eseguite correttamente. Il gruppo di campi `$id` è stato aggiunto all&#39;array `meta:extends` e un riferimento (`$ref`) al gruppo di campi `$id` ora viene visualizzato nell&#39;array `allOf`.

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

## Abilitare uno schema per l’utilizzo in Real-Time Customer Profile {#union}

Per consentire a uno schema di partecipare a [Real-Time Customer Profile](../../profile/home.md), è necessario aggiungere un tag `union` all&#39;array `meta:immutableTags` dello schema. Per farlo, devi effettuare una richiesta PATCH per lo schema in questione.

>[!IMPORTANT]
>
>I tag immutabili sono tag destinati a essere impostati, ma non rimossi.

**Formato API**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | URI `$id` o `meta:altId` con codifica URL dello schema che si desidera abilitare. |

{style="table-layout:auto"}

**Richiesta**

La richiesta di esempio seguente aggiunge un array `meta:immutableTags` a uno schema esistente, assegnando all&#39;array un singolo valore stringa di `union` per abilitarlo per l&#39;utilizzo nel profilo.

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

In caso di esito positivo, la risposta restituisce i dettagli dello schema aggiornato, mostrando che l&#39;array `meta:immutableTags` è stato aggiunto.

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

Ora puoi visualizzare l’unione per la classe di questo schema per confermare che i campi dello schema sono rappresentati. Per ulteriori informazioni, consulta la [guida dell&#39;endpoint Unions](./unions.md).

## Eliminare uno schema {#delete}

Talvolta può essere necessario rimuovere uno schema dal registro degli schemi. Questa operazione viene eseguita eseguendo una richiesta DELETE con l’ID schema fornito nel percorso.

**Formato API**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | URI `$id` con codifica URL o `meta:altId` dello schema che si desidera eliminare. |

{style="table-layout:auto"}

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

In caso di esito positivo, la risposta restituisce lo stato HTTP 204 (nessun contenuto) e un corpo vuoto.

Puoi confermare l’eliminazione tentando una richiesta di ricerca (GET) nello schema. È necessario includere un&#39;intestazione `Accept` nella richiesta, ma dovrebbe ricevere lo stato HTTP 404 (Non trovato) perché lo schema è stato rimosso dal registro degli schemi.
