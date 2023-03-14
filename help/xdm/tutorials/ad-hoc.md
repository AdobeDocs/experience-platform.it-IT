---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;Experience data model;Experience data model;Experience Data Model;modello dati;modello dati;modello dati;modello dati;modello dati;registro schema;registro schema;ad hoc;ad hoc;ad hoc;ad hoc;ad hoc;adhoc;tutorial;creare;creare;schema;schema
solution: Experience Platform
title: Creare uno schema ad hoc
description: In circostanze specifiche, potrebbe essere necessario creare uno schema Experience Data Model (XDM) con campi a cui viene assegnato un namespace per l’utilizzo solo da un singolo set di dati. Questo viene definito schema "ad hoc". Gli schemi ad hoc vengono utilizzati in vari flussi di lavoro di acquisizione dati, ad Experience Platform, l’acquisizione di file CSV e la creazione di alcuni tipi di connessioni sorgente.
type: Tutorial
exl-id: bef01000-909a-4594-8cf4-b9dbe0b358d5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 3%

---

# Creare uno schema ad hoc

In circostanze specifiche, può essere necessario creare un [!DNL Experience Data Model] (XDM) con campi a cui viene assegnato un namespace per l’utilizzo solo da un singolo set di dati. Questo viene definito schema &quot;ad hoc&quot;. Gli schemi ad hoc vengono utilizzati in vari flussi di lavoro di acquisizione dati per [!DNL Experience Platform], inclusa l’acquisizione di file CSV e la creazione di alcuni tipi di connessioni sorgente.

Questo documento descrive i passaggi generali per la creazione di uno schema ad hoc tramite [API del registro dello schema](https://www.adobe.io/experience-platform-apis/references/schema-registry/). È destinato ad essere utilizzato in combinazione con altri [!DNL Experience Platform] esercitazioni che richiedono la creazione di uno schema ad hoc come parte del flusso di lavoro. Ciascuno di questi documenti fornisce informazioni dettagliate su come configurare correttamente uno schema ad hoc per il relativo caso d’uso specifico.

## Introduzione

Questo tutorial richiede una buona conoscenza di [!DNL Experience Data Model] (XDM). Prima di iniziare questo tutorial, consulta la seguente documentazione XDM:

- [Panoramica del sistema XDM](../home.md): panoramica di alto livello di XDM e della relativa implementazione in [!DNL Experience Platform].
- [Nozioni di base sulla composizione dello schema](../schema/composition.md): panoramica dei componenti di base degli schemi XDM.

Prima di iniziare questo tutorial, controlla [guida per sviluppatori](../api/getting-started.md) per informazioni importanti che è necessario conoscere per effettuare correttamente chiamate al [!DNL Schema Registry] API. Ciò include `{TENANT_ID}`, il concetto di &quot;contenitori&quot; e le intestazioni necessarie per effettuare le richieste (con particolare attenzione all’intestazione Accept e ai suoi possibili valori).

## Creare una classe ad hoc

Il comportamento dei dati di uno schema XDM è determinato dalla relativa classe sottostante. Il primo passaggio nella creazione di uno schema ad hoc consiste nel creare una classe basata su `adhoc` comportamento. A tale scopo, invia una richiesta POST al `/tenant/classes` endpoint.

**Formato API**

```http
POST /tenant/classes
```

**Richiesta**

La richiesta seguente crea una nuova classe XDM, configurata dagli attributi forniti nel payload. Fornendo un `$ref` proprietà impostata su `https://ns.adobe.com/xdm/data/adhoc` nel `allOf` questa classe eredita il `adhoc` comportamento. La richiesta definisce anche `_adhoc` oggetto, che contiene i campi personalizzati per la classe.

>[!NOTE]
>
>I campi personalizzati definiti in `_adhoc` varia a seconda del caso di utilizzo dello schema ad hoc. Fai riferimento al flusso di lavoro specifico nell’esercitazione appropriata per i campi personalizzati richiesti in base al caso d’uso.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New ad-hoc class",
        "description": "New ad-hoc class description",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/xdm/data/adhoc"
          },
          {
            "properties": {
              "_adhoc": {
                "type":"object",
                "properties": {
                  "field1": {
                    "type":"string"
                  },
                  "field2": {
                    "type":"string"
                  }
                }
              }
            }
          }
        ]
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `$ref` | Comportamento dei dati per la nuova classe. Per le classi ad hoc, questo valore deve essere impostato su `https://ns.adobe.com/xdm/data/adhoc`. |
| `properties._adhoc` | Oggetto che contiene i campi personalizzati per la classe, espressi come coppie chiave-valore di nomi di campo e tipi di dati. |

{style="table-layout:auto"}

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della nuova classe, sostituendo `properties._adhoc` il nome dell&#39;oggetto con un GUID che è un identificatore univoco di sola lettura generato dal sistema per la classe. Il `meta:datasetNamespace` viene generato automaticamente e incluso nella risposta.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:altId": "_{TENANT_ID}.classes.6395cbd58812a6d64c4e5344f7b9120f",
    "meta:resourceType": "classes",
    "version": "1.0",
    "title": "New Class",
    "description": "New class description",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/data/adhoc"
        },
        {
            "properties": {
                "_6395cbd58812a6d64c4e5344f7b9120f": {
                    "type": "object",
                    "properties": {
                        "field1": {
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "field2": {
                            "type": "string",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:extends": [
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557527784822,
        "repo:lastModifiedDate": 1557527784822,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `$id` | URI che funge da identificatore univoco generato dal sistema di sola lettura per la nuova classe ad hoc. Questo valore viene utilizzato nel passaggio successivo della creazione di uno schema ad hoc. |

{style="table-layout:auto"}

## Creare uno schema ad hoc

Dopo aver creato una classe ad hoc, puoi creare un nuovo schema che implementa tale classe effettuando una richiesta POST al `/tenant/schemas` endpoint.

**Formato API**

```http
POST /tenant/schemas
```

**Richiesta**

La richiesta seguente crea un nuovo schema, fornendo un riferimento (`$ref`) al `$id` della classe ad hoc creata in precedenza nel relativo payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New Schema",
        "description": "New schema description.",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
          }
        ]
      }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli dello schema appena creato, incluso il relativo schema generato dal sistema e di sola lettura `$id`.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
        }
    ],
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

## Visualizzare lo schema ad hoc completo

>[!NOTE]
>
>Questo passaggio è facoltativo. Se non desideri esaminare la struttura dei campi dello schema ad hoc, puoi passare alla sezione [passaggi successivi](#next-steps) alla fine di questa esercitazione.

Una volta creato lo schema ad hoc, puoi effettuare una richiesta di ricerca (GET) per visualizzare lo schema nel relativo modulo espanso. A tale scopo, utilizza l’intestazione Accept appropriata nella richiesta GET, come dimostrato di seguito.

**Formato API**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | Codifica URL `$id` URI o `meta:altId` dello schema ad hoc a cui desideri accedere. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente utilizza l’intestazione Accept `application/vnd.adobe.xed-full+json; version=1`, che restituisce il modulo espanso dello schema. Tieni presente che quando recuperi una risorsa specifica da [!DNL Schema Registry], l’intestazione Accept della richiesta deve includere la versione principale della risorsa in questione.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli dello schema, inclusi tutti i campi nidificati in `properties`.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "properties": {
        "_6395cbd58812a6d64c4e5344f7b9120f": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "field1": {
                    "type": "string",
                    "meta:xdmType": "string"
                },
                "field2": {
                    "type": "string",
                    "meta:xdmType": "string"
                }
            }
        }
    },
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "bTogM1ON2LO/F7rlcc1iOWmNVy0="
    }
}
```

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai creato un nuovo schema ad hoc. Se hai visitato questo documento come parte di un&#39;altra esercitazione, ora puoi utilizzare `$id` dello schema ad hoc per completare il flusso di lavoro come indicato.

Per ulteriori informazioni sull&#39;utilizzo di [!DNL Schema Registry] API, fare riferimento al [guida per sviluppatori](../api/getting-started.md).
