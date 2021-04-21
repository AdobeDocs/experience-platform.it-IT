---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;modello dati;registro schema;registro schema;ad hoc;ad hoc;ad hoc;Ad hoc;Ad hoc;tutorial;tutorial;creare;creare;schema;schema
solution: Experience Platform
title: Creare uno schema ad hoc
description: In circostanze specifiche, potrebbe essere necessario creare uno schema Experience Data Model (XDM) con campi che vengono spazi dei nomi per l’utilizzo solo da un singolo set di dati. Questo è denominato schema "ad hoc". Gli schemi ad hoc vengono utilizzati in vari flussi di lavoro di acquisizione dei dati, ad Experience Platform per l’acquisizione di file CSV e la creazione di determinati tipi di connessioni sorgente.
topic-legacy: tutorial
type: Tutorial
exl-id: bef01000-909a-4594-8cf4-b9dbe0b358d5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 2%

---

# Creare uno schema ad hoc

In circostanze specifiche, potrebbe essere necessario creare uno schema [!DNL Experience Data Model] (XDM) con campi che vengono spazi dei nomi per l’utilizzo solo da un singolo set di dati. Questo è denominato schema &quot;ad hoc&quot;. Gli schemi ad hoc vengono utilizzati in vari flussi di lavoro di inserimento dati per [!DNL Experience Platform], inclusi l’acquisizione di file CSV e la creazione di determinati tipi di connessioni sorgente.

Questo documento fornisce passaggi generali per la creazione di uno schema ad hoc utilizzando l&#39; [API del Registro di sistema dello schema](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). È progettato per essere utilizzato insieme ad altre esercitazioni [!DNL Experience Platform] che richiedono la creazione di uno schema ad-hoc come parte del loro flusso di lavoro. Ognuno di questi documenti fornisce informazioni dettagliate su come configurare correttamente uno schema ad hoc per il relativo caso d’uso specifico.

## Introduzione

Questa esercitazione richiede una buona comprensione del sistema [!DNL Experience Data Model] (XDM). Prima di avviare questa esercitazione, consulta la seguente documentazione XDM:

- [Panoramica](../home.md) del sistema XDM: Panoramica di alto livello di XDM e della sua implementazione in  [!DNL Experience Platform].
- [Nozioni di base sulla composizione](../schema/composition.md) dello schema: Panoramica dei componenti di base degli schemi XDM.

Prima di avviare questa esercitazione, controlla la [guida per gli sviluppatori](../api/getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente le chiamate all’ API [!DNL Schema Registry]. Questo include il tuo `{TENANT_ID}`, il concetto di &quot;contenitori&quot; e le intestazioni richieste per fare richieste (con particolare attenzione all&#39;intestazione Accept e ai suoi possibili valori).

## Creare una classe ad hoc

Il comportamento dei dati di uno schema XDM è determinato dalla classe sottostante. Il primo passaggio nella creazione di uno schema ad-hoc consiste nel creare una classe basata sul comportamento `adhoc` . A questo scopo, invia una richiesta POST all’endpoint `/tenant/classes` .

**Formato API**

```http
POST /tenant/classes
```

**Richiesta**

La richiesta seguente crea una nuova classe XDM, configurata dagli attributi forniti nel payload. Fornendo una proprietà `$ref` impostata su `https://ns.adobe.com/xdm/data/adhoc` nella matrice `allOf`, questa classe eredita il comportamento `adhoc`. La richiesta definisce anche un oggetto `_adhoc` , che contiene i campi personalizzati per la classe .

>[!NOTE]
>
>I campi personalizzati definiti in `_adhoc` variano a seconda del caso d’uso dello schema ad-hoc. Fai riferimento al flusso di lavoro specifico nell’esercitazione appropriata per i campi personalizzati richiesti in base al caso d’uso.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `$ref` | Il comportamento dei dati per la nuova classe. Per le classi ad-hoc, questo valore deve essere impostato su `https://ns.adobe.com/xdm/data/adhoc`. |
| `properties._adhoc` | Oggetto che contiene i campi personalizzati per la classe, espressi come coppie chiave-valore di nomi di campo e tipi di dati. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova classe, sostituendo il nome dell&#39;oggetto `properties._adhoc` con un GUID che è un identificatore univoco di sola lettura generato dal sistema per la classe. Anche l’attributo `meta:datasetNamespace` viene generato automaticamente e incluso nella risposta.

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
    "imsOrg": "{IMS_ORG}",
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
| `$id` | URI che funge da identificatore univoco generato dal sistema di sola lettura per la nuova classe ad-hoc. Questo valore viene utilizzato nel passaggio successivo della creazione di uno schema ad hoc. |

## Creare uno schema ad hoc

Dopo aver creato una classe ad-hoc, puoi creare un nuovo schema che implementa tale classe effettuando una richiesta POST all&#39;endpoint `/tenant/schemas`.

**Formato API**

```http
POST /tenant/schemas
```

**Richiesta**

La richiesta seguente crea un nuovo schema, fornendo un riferimento (`$ref`) al `$id` della classe ad-hoc creata in precedenza nel relativo payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Una risposta corretta restituisce i dettagli dello schema appena creato, incluso il relativo `$id` di sola lettura generato dal sistema.

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
    "imsOrg": "{IMS_ORG}",
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

## Visualizza lo schema ad-hoc completo

>[!NOTE]
>
>Questo passaggio è facoltativo. Se non desideri esaminare la struttura del campo dello schema ad-hoc, puoi passare alla sezione [passi successivi](#next-steps) alla fine di questa esercitazione.

Una volta creato lo schema ad-hoc, puoi effettuare una richiesta di ricerca (GET) per visualizzare lo schema nel relativo modulo espanso. Questa operazione viene eseguita utilizzando l’intestazione Accept appropriata nella richiesta GET, come illustrato di seguito.

**Formato API**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{SCHEMA_ID}` | URI con codifica URL `$id` o `meta:altId` dello schema ad-hoc a cui si desidera accedere. |

**Richiesta**

La richiesta seguente utilizza l&#39;intestazione Accept `application/vnd.adobe.xed-full+json; version=1`, che restituisce il modulo espanso dello schema. Tieni presente che quando recuperi una risorsa specifica da [!DNL Schema Registry], l’intestazione Accept della richiesta deve includere la versione principale della risorsa in questione.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

Una risposta corretta restituisce i dettagli dello schema, inclusi tutti i campi nidificati in `properties`.

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
    "imsOrg": "{IMS_ORG}",
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

Seguendo questa esercitazione, hai creato correttamente un nuovo schema ad-hoc. Se sei stato portato in questo documento come parte di un’altra esercitazione, ora puoi utilizzare il `$id` dello schema ad-hoc per completare il flusso di lavoro come indicato.

Per ulteriori informazioni sulle operazioni con l&#39;API [!DNL Schema Registry], consulta la [guida per gli sviluppatori](../api/getting-started.md).
