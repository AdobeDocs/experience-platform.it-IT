---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;Experience data model;Experience data model;Experience Data Model;modello dati;modello dati;modello dati;modello dati;registro schema;schema;schema;schema;schemi;creare;;home;popular topic;api;API;XDM;XDM system;experience data model;Experience data model;data model;data model;Data model;schema registry;schema Registry;schema;schema;schema;schemi;creare
solution: Experience Platform
title: Endpoint API per gli schemi
description: L’endpoint /schemas nell’API Schema Registry consente di gestire in modo programmatico gli schemi XDM all’interno dell’applicazione Experience.
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: 974faad835b5dc2a4d47249bb672573dfb4d54bd
workflow-type: tm+mt
source-wordcount: '2095'
ht-degree: 4%

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
| `{CONTAINER_ID}` | Contenitore che ospita gli schemi da recuperare: `global` per gli schemi creati da Adobe o `tenant` per gli schemi di proprietà dell&#39;organizzazione. |
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

Per cercare uno schema specifico, effettua una richiesta GET che include l’ID dello schema nel percorso.

**Formato API**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{CONTAINER_ID}` | Contenitore che ospita lo schema da recuperare: `global` per uno schema creato da Adobe o `tenant` per uno schema di proprietà dell&#39;organizzazione. |
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

Per istruzioni sulla creazione di uno schema senza classi o gruppi di campi, noto come schema basato su modello, vedere la sezione [Creare uno schema basato su modello](#create-model-based-schema).

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

L&#39;esecuzione di una richiesta GET per [elencare tutti gli schemi](#list) nel contenitore tenant includerebbe ora il nuovo schema. È possibile eseguire una [richiesta di ricerca (GET)](#lookup) utilizzando l&#39;URI `$id` codificato dall&#39;URL per visualizzare direttamente il nuovo schema.

Per aggiungere campi aggiuntivi a uno schema, è possibile eseguire un&#39;operazione [PATCH](#patch) per aggiungere gruppi di campi agli array `allOf` e `meta:extends` dello schema.

## Crea uno schema basato su modelli {#create-model-based-schema}

>[!AVAILABILITY]
>
>Data Mirror e gli schemi basati su modelli sono disponibili per i titolari di licenze di **Campagne orchestrate** Adobe Journey Optimizer. Sono disponibili anche come **versione limitata** per gli utenti di Customer Journey Analytics, a seconda della licenza e dell&#39;abilitazione della funzione. Contatta il tuo rappresentante Adobe per accedere.

Creare uno schema basato su modello effettuando una richiesta POST all&#39;endpoint `/schemas`. Gli schemi basati su modelli memorizzano dati strutturati in stile relazionale **senza** classi o gruppi di campi. Definisci i campi direttamente sullo schema e identifica lo schema come basato su modello utilizzando un tag di comportamento logico.

>[!IMPORTANT]
>
>Per creare uno schema basato su modello, impostare `meta:extends` su `"https://ns.adobe.com/xdm/data/adhoc-v2"`. Questo è un **identificatore di comportamento logico** (non un comportamento fisico o una classe). **non** fare riferimento a classi o gruppi di campi in `allOf` e **non** includere classi o gruppi di campi in `meta:extends`.

Creare prima lo schema con `POST /tenant/schemas`. Aggiungere quindi i descrittori richiesti con l&#39;API dei descrittori [(`POST /tenant/descriptors`)](../api/descriptors.md):

- [Descrittore chiave primaria](../api/descriptors.md#primary-key-descriptor): un campo chiave primaria deve essere al **livello radice** e **contrassegnato come obbligatorio**.
- [Descrittore versione](../api/descriptors.md#version-descriptor): **Obbligatorio** quando esiste una chiave primaria.
- [Descrittore di relazione](../api/descriptors.md#relationship-descriptor): facoltativo, definisce i join; cardinalità non applicata al momento dell&#39;acquisizione.
- [Descrittore marca temporale](../api/descriptors.md#timestamp-descriptor): per gli schemi di serie temporali, la chiave primaria deve essere una chiave **composita** che include il campo marca temporale.

>[!NOTE]
>
>Nell&#39;Editor schema dell&#39;interfaccia utente, i descrittori di versione e di marca temporale vengono visualizzati rispettivamente come &quot;[ !UICOTRNOL Identificatore versione]&quot; e &quot;[ !UICOTRNOL Identificatore marca temporale]&quot;.

<!-- >[!AVAILABILITY]
>
>Although `meta:behaviorType` technically accepts `time-series`, support is not currently available for model-based schemas. Set `meta:behaviorType` to `"record"`. -->

>[!CAUTION]
>
>Gli schemi basati su modelli sono **non compatibili con gli schemi di unione**. Non applicare il tag `union` a `meta:immutableTags` quando si utilizzano schemi basati su modelli. Questa configurazione è bloccata nell’interfaccia utente, ma non è attualmente bloccata dall’API. Per ulteriori informazioni sul comportamento dello schema di unione, consulta la [guida dell&#39;endpoint Unions](./unions.md).

**Formato API**

```http
POST /tenant/schemas
```

**Richiesta**

```shell
curl --request POST \
  --url https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
  "title": "marketing.customers",
  "type": "object",
  "description": "Schema of the Marketing Customers table.",
  "definitions": {
    "customFields": {
      "type": "object",
      "properties": {
        "customer_id": {
          "title": "Customer ID",
          "description": "Primary key of the customer table.",
          "type": "string",
          "minLength": 1
        },
        "name": {
          "title": "Name",
          "description": "Name of the customer.",
          "type": "string"
        },
        "email": {
          "title": "Email",
          "description": "Email of the customer.",
          "type": "string",
          "format": "email",
          "minLength": 1
        }
      },
      "required": ["customer_id"]
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
      "meta:xdmType": "object"
    }
  ],
  "meta:extends": ["https://ns.adobe.com/xdm/data/adhoc-v2"],
  "meta:behaviorType": "record"
}
'
```

### Proprietà corpo della richiesta

| Proprietà | Tipo | Descrizione |
| ------------------------------- | ------ | --------------------------------------------------------- |
| `title` | Stringa | Nome visualizzato dello schema. |
| `description` | Stringa | Breve spiegazione dello scopo dello schema. |
| `type` | Stringa | Deve essere `"object"` per gli schemi basati su modelli. |
| `definitions` | Oggetto | Contiene gli oggetti a livello di radice che definiscono i campi dello schema. |
| `definitions.<name>.properties` | Oggetto | Nomi di campi e tipi di dati. |
| `allOf` | Array | Fa riferimento alla definizione dell&#39;oggetto a livello di radice (ad esempio, `#/definitions/marketing_customers`). |
| `meta:extends` | Array | Deve includere `"https://ns.adobe.com/xdm/data/adhoc-v2"` per identificare lo schema come basato su modello. |
| `meta:behaviorType` | Stringa | Imposta su `"record"`. Usa `"time-series"` solo se abilitato e appropriato. |

>[!IMPORTANT]
>
>L’evoluzione dello schema per gli schemi basati su modelli segue le stesse regole aggiuntive degli schemi standard. Puoi aggiungere nuovi campi con una richiesta PATCH. Le modifiche, come la ridenominazione o la rimozione di campi, sono consentite solo se nel set di dati non sono stati acquisiti dati.

**Risposta**

In caso di esito positivo, la richiesta restituisce **HTTP 201 (creato)** e lo schema creato.

>[!NOTE]
>
>Gli schemi basati su modelli non ereditano i campi predefiniti (ad esempio, id, timestamp o eventType). Definisci tutti i campi obbligatori in modo esplicito nello schema.

**Risposta di esempio**

```json
{
  "$id": "https://ns.adobe.com/<TENANT_ID>/schemas/<SCHEMA_UUID>",
  "meta:altId": "_<SCHEMA_ALT_ID>",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "marketing.customers",
  "description": "Schema of the Marketing Customers table.",
  "type": "object",
  "definitions": {
    "marketing_customers": {
      "type": "object",
      "properties": {
        "customer_id": {
          "title": "Customer ID",
          "description": "Primary key of the customer table.",
          "type": "string",
          "minLength": 1
        },
        "name": {
          "title": "Name",
          "description": "Name of the customer.",
          "type": "string"
        },
        "email": {
          "title": "Email",
          "description": "Email of the customer.",
          "type": "string",
          "format": "email",
          "minLength": 1
        }
      },
      "required": ["customer_id"]
    }
  },
  "allOf": [
    { "$ref": "#/definitions/marketing_customers" }
  ],
  "meta:extends": ["https://ns.adobe.com/xdm/data/adhoc-v2"],
  "meta:behaviorType": "record",
  "meta:containerId": "tenant"
}
```

### Proprietà del corpo della risposta

| Proprietà | Tipo | Descrizione |
| ------------------- | ------ | -------------------------- |
| `$id` | Stringa | URL univoco dello schema creato. Da utilizzare nelle chiamate API successive. |
| `meta:altId` | Stringa | Identificatore alternativo dello schema. |
| `meta:resourceType` | Stringa | Tipo di risorsa (sempre `"schemas"`). |
| `version` | Stringa | Versione dello schema assegnata al momento della creazione. |
| `title` | Stringa | Nome visualizzato dello schema. |
| `description` | Stringa | Breve spiegazione dello scopo dello schema. |
| `type` | Stringa | Il tipo di schema. |
| `definitions` | Oggetto | Definisce gli oggetti o i gruppi di campi riutilizzabili utilizzati nello schema. Questo include in genere la struttura dati principale ed è indicato nell&#39;array `allOf` per definire la directory principale dello schema. |
| `allOf` | Array | Specifica l&#39;oggetto principale dello schema facendo riferimento a una o più definizioni (ad esempio, `#/definitions/marketing_customers`). |
| `meta:extends` | Array | Identifica lo schema come basato su modello (`adhoc-v2`). |
| `meta:behaviorType` | Stringa | Tipo di comportamento (`record` o `time-series`, se abilitato). |
| `meta:containerId` | Stringa | Contenitore in cui è memorizzato lo schema (ad esempio, `tenant`). |

Per aggiungere campi a uno schema basato su modello dopo la creazione, effettuare una [richiesta PATCH](#patch). Gli schemi basati su modelli non ereditano o evolvono automaticamente. Modifiche strutturali come la ridenominazione o l’eliminazione di campi sono consentite solo se nel set di dati non sono stati acquisiti dati. Una volta che i dati esistono, sono supportate solo **modifiche aggiuntive** (come l&#39;aggiunta di nuovi campi).

È possibile aggiungere nuovi campi a livello di radice (all&#39;interno della definizione radice o della radice `properties`), ma non è possibile rimuovere, rinominare o modificare il tipo di campi esistenti.

>[!CAUTION]
>
>L’evoluzione dello schema diventa limitata dopo che un set di dati è stato inizializzato utilizzando lo schema. Pianifica in anticipo i nomi e i tipi di campo: una volta acquisiti i dati, non è più possibile eliminare o modificare i campi.

## Aggiornare uno schema {#put}

Puoi sostituire un intero schema tramite un’operazione PUT, essenzialmente riscrivendo la risorsa. Quando si aggiorna uno schema tramite una richiesta PUT, il corpo deve includere tutti i campi necessari per [creare un nuovo schema](#create) in una richiesta POST.

>[!NOTE]
>
>Se si desidera aggiornare solo una parte di uno schema anziché sostituirla completamente, vedere la sezione relativa all&#39;aggiornamento di una parte di uno schema[.](#patch)

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
